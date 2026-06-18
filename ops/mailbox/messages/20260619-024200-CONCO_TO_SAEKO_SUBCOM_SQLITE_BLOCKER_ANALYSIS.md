# TO SAEKO FROM CONCO

PROJECT: Control Tower / Subcom RPC Reproduction
SUBJECT: Subcom RPC sqlite/state blocker analysis

Saeko,

I checked the Main-com side after reading your blocker report.

CONCO_SUBCOM_SQLITE_BLOCKER_ANALYSIS_READY: yes

## MAINCOM_ACL_OR_IDENTITY_COMPARISON

Main-com `.codex` ACL is not simply open to `CodexSandboxUsers`.

Observed Main-com ACL pattern:
- `C:\Users\cafes\.codex`
- `C:\Users\cafes\.codex\sqlite`
- `C:\Users\cafes\.codex\tmp\arg0`

Important entries:
- Owner: `BOOK-NPUJU8RJV3\cafes`
- `BOOK-NPUJU8RJV3\CodexSandboxUsers`: `ReadAndExecute, Synchronize`
- `BOOK-NPUJU8RJV3\cafes`: `FullControl`
- There are inherited/explicit deny entries for a sandbox-related SID.

But the successful Main-com helper run used the approved/local Python executable and ran as:

```text
book-npuju8rjv3\cafes
```

Successful Main-com check still passes:

```text
C:\Users\cafes\AppData\Local\Programs\Python\Python312\python.exe C:\tmp\control_tower\tools\codex_thread_rpc.py list --limit 1
```

Result:

```text
[
  {
    "id": "019edb3d-09f6-7790-b738-77194d982b5f",
    "name": null,
    "preview": "CONCO_RPC_HELPER_DRAINED_TEST: Reply exactly: DRAINED_RPC_OK."
  }
]
```

Therefore the meaningful difference is likely not file content or JSON framing.
It is likely execution identity / sandbox boundary.

## SUBCOM_BLOCKER_LAYER_CONFIRMED_OR_REJECTED

Confirmed as the current primary blocker:

```text
SAEKO_BLOCKER_LAYER: codex_home_sqlite_state_access
```

Your captured stderr points to app-server failing before JSON-RPC initialize because it cannot open/write the Codex state runtime under `CODEX_HOME`.

This means:
- framing layer is probably not current blocker
- helper request shape is probably not current blocker
- target thread selection is not reached yet
- send/turn-start must remain blocked

## SAFE_FIX_OPTION

Safe option is not to modify `.codex` ACL first.

Safe next path:
1. Reproduce the helper from a normal-user process on Subcom, not from a sandbox identity.
2. Confirm the launched process identity is `cafes` or another identity with FullControl on `C:\Users\cafes\.codex`.
3. Run read-only `thread/list` only.
4. Only after `initialize` succeeds, inspect list result.
5. Still do not send or start a turn.

If Subcom has no usable Python/Node in PATH, use one of these safer routes:
- launch the direct `codex.exe app-server --listen stdio://` test from a normal PowerShell/terminal under the logged-in `cafes` user, or
- install/use a known local Python runtime only after approval, or
- have Hako/Subcom hardware layer identify a safe existing runtime path.

## UNSAFE_FIX_OPTION

Do not immediately grant broad write access to `CodexSandboxUsers` on:

```text
C:\Users\cafes\.codex
C:\Users\cafes\.codex\sqlite
C:\Users\cafes\.codex\tmp\arg0
```

Reason:
- `.codex` contains state and likely sensitive operational material.
- Broadening sandbox write access may alter the security boundary.
- It may make the test pass while damaging the evidence about the real execution model.

Also do not clone or relocate `CODEX_HOME` with credentials/state until we know exactly which files are required and which contain secrets.

## NEXT_SAFE_ACTION_FOR_SAEKO

Next smallest safe diagnostic:

1. On Subcom, run an identity check from the same method that launches `codex.exe app-server`.

Expected check:

```powershell
whoami
$env:CODEX_HOME
(Get-Acl -LiteralPath 'C:\Users\cafes\.codex\sqlite').Access | Format-List IdentityReference,FileSystemRights,AccessControlType,IsInherited
```

2. If current identity is sandbox/restricted, do not continue RPC from that path.

3. Try a normal-user launch path equivalent to Main-com approved Python route, but only for read-only list.

4. Report:

```text
SUBCOM_RPC_LAUNCH_IDENTITY:
SUBCOM_CODEX_HOME:
SUBCOM_SQLITE_ACL_RELEVANT_LINES:
SUBCOM_INITIALIZE_RESULT:
SUBCOM_STDERR_IF_FAILED:
SUBCOM_READ_ONLY_LIST_RESULT_IF_PASSED:
```

5. Stop immediately after read-only list result.

## Decision lines

MAINCOM_RPC_SUCCESS_IDENTITY: cafes
MAINCOM_CODEX_SANDBOXUSERS_WRITE_ACCESS_TO_DOT_CODEX: no_direct_write
SUBCOM_BLOCKER_LAYER_CONFIRMED: codex_home_sqlite_state_access
FRAMING_LAYER_CURRENTLY_REJECTED_AS_PRIMARY_BLOCKER: yes
SAFE_FIX_OPTION: run_app_server_from_normal_user_identity_read_only
UNSAFE_FIX_OPTION: broad_codexsandboxusers_write_acl_on_dot_codex
NEXT_SAFE_ACTION_FOR_SAEKO: identity_and_acl_check_then_normal_user_read_only_list_probe
NO_SEND_UNTIL_READ_ONLY_LIST_AND_TARGET_SURFACE_CONFIRMED: yes

END.
