# Vacation

1 automation(s) in this category.

| Automation | Description |
|---|---|
| Vacation Water and Light Control | Controls the main water valve and four lights while vacation mode is active. Opens the water and turns the lights on when someone is genuinely home (deadbolt unlocked, and alarm disarmed unless the alarm check is bypassed). Closes the water and turns the lights off when the house is secured, and as a nightly backstop at 02:00.

A 10 minute heartbeat re-asserts the intended state so a missed event cannot leave the water in the wrong position. Push notifications are suppressed on heartbeat runs to avoid spamming, and are also suppressed for the nightly reset on the open branch.

input_boolean.vacation is the master gate; nothing here runs unless it is on. input_boolean.vacation_alarm_disable drops the Ring alarm state out of both decisions, for when the alarm is unavailable or not being armed.

TWO DEFECTS FIXED 2026-08-26.

FIRST: both choose branches carried enabled: false on their only condition. Home Assistant SKIPS a disabled condition rather than failing it, so each branch was left with no conditions at all and evaluated as unconditionally true. With mode: single the first branch always won, meaning that while vacation mode was on, every trigger including the 10 minute heartbeat and the 02:00 nightly reset opened the water valve and turned the lights on. The close branch was unreachable. Vacation mode therefore meant the water was permanently ON, the exact opposite of its purpose. Both conditions are now enabled.

SECOND: the close branch's else clause was missing its Jinja delimiters. The expression sat as bare text between {% else %} and {% endif %} instead of inside {{ }}, so it rendered as a literal string rather than a boolean. Home Assistant treats a non-truthy string as false, so even with the condition enabled the close branch could never fire whenever vacation_alarm_disable was off, and the water would still never shut off. The open branch was written correctly, which is why the bug was easy to miss on a visual comparison. Now wrapped correctly.

DESIGN DECISION 2026-08-26: the nightly_reset escape now applies in BOTH modes. Previously it only existed in the else path, so with vacation_alarm_disable ON the 02:00 reset could not close the valve and only the deadbolt being locked could. That asymmetry is a poor failure mode for a water valve, where the safe direction is closed. Scott did not recall the original intent and asked for a judgement call; revisit before the next trip if a different behaviour is wanted.

DISABLED 2026-08-26 at Scott's request. He wants no automated control of the main water valve at all unless he deliberately turns this back on for a trip. Turning on input_boolean.vacation alone will NOT arm it while the automation itself is off. Re-enable this automation AND set the vacation boolean before leaving.

ORIGINAL INTENT, recalled by Scott 2026-08-26. This exists for when a family member comes by to feed and water the dogs while Scott is away. That person can be forgetful about switching things off, so the automation does it for them. The front deadbolt is the presence proxy: unlocking it means the carer has arrived, so water and lights come on; locking it means they have left, so water and lights go off. The 10 minute heartbeat catches any missed lock or unlock event. input_boolean.vacation_alarm_disable exists because the carer will not be arming the Ring alarm, so the alarm state has to drop out of the decision.

That makes the alarm-disabled path the carer's normal path, which is exactly why the 02:00 nightly reset now applies there too. Under the old code, if the carer forgot to lock the deadbolt on their way out, the water stayed on all night with nobody in the house, and the nightly backstop could not close it in that mode. This is the single most likely real-world failure this automation is meant to prevent.

The disabled conditions were most likely a deliberate override during a four day trip, to force the water to stay on regardless of state, and were never re-enabled afterwards. |
