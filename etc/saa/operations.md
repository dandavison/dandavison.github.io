## Operation behavior by phase

The effect of an operation depends on the phase the Activity Execution is in:

| Operation | SCHEDULED (start delay) | dispatched (schedule-to-start) | STARTED (start-to-close + heartbeat) | SCHEDULED (retry backoff) | COMPLETED |
| --- | --- | --- | --- | --- | --- |
| pause | pausable | pausable | pause requestable | pausable | — |
| unpause (if paused) | dispatches at end of start delay | dispatches immediately | removes pause request | dispatches at end of retry backoff | — |
| update start_delay | updateable | not updateable | not updateable | not updateable | not updateable |
| cancel | cancellable | cancellable | cancel requestable | cancellable | — |
| reset | resettable | resettable | reset requestable | resettable | — |
| terminate | → Terminated | → Terminated | → Terminated | → Terminated | — |

An Activity Execution ends in one of these terminal states: Canceled, Completed, Failed, Terminated, TimedOut.
