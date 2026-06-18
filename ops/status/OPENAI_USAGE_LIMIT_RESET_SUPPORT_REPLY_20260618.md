# OPENAI_USAGE_LIMIT_RESET_SUPPORT_REPLY_20260618

FROM: CONCO
TO: SSONG
DATE_KST: 2026-06-18
SUBJECT: Support answer about ChatGPT Pro usage limit reset

## 1. Context

Ssong is on the $200/month ChatGPT Pro tier.

An in-app message offered a `usage limit reset`. Ssong clicked it because active Codex/ChatGPT work could not continue without the reset.

Ssong then asked OpenAI support four direct questions:

```text
I clicked “usage limit reset” on my $200 ChatGPT Pro account.

Was this free?
Did it create any charge?
Did it reduce or borrow from my future usage limit?
Which limit did it reset?
```

## 2. Support Answer Summary

The support reply stated:

```text
Was it free?
- Yes. Usage-limit resets are not billed as a separate purchase.

Did it create any charge?
- No. No separate charge is created by resetting a usage limit.

Did it reduce or borrow from future usage?
- No. Documented limits reset on their normal schedule; they do not borrow from future quota.

Which limit reset?
- It resets the specific model/tool limit shown in the message or model picker.
- The model picker can show reset timing for that model's personal limit.
```

## 3. Operational Conclusion

```text
USAGE_LIMIT_RESET_SEPARATE_CHARGE: no
USAGE_LIMIT_RESET_FREE: yes
USAGE_LIMIT_RESET_BORROWS_FROM_FUTURE_QUOTA: no
NORMAL_RESET_SCHEDULE_AFFECTED: no
RESET_SCOPE: specific_model_or_tool_limit_shown_in_ui
```

## 4. Use

This record should be used as billing/usage evidence if an ambiguous usage reset UI appears again or if future billing confusion arises.

Local copy:

```text
C:\tmp\control_tower\OPENAI_USAGE_LIMIT_RESET_SUPPORT_REPLY_20260618.md
```

END.
