# Action Model Rules (Locked)

Terminology
- Atomic unit = Action
- The word “event” is forbidden everywhere

Time
- time.value is source-faithful text
- time.value MUST NOT be normalized, parsed, or rewritten
- time.precision is the only machine-usable signal

Allowed precisions
- day
- month
- year
- century

Precision rules
- Minimum precision only
- Never infer missing precision
- Never upgrade precision
- Never downgrade precision
- Never convert centuries to years
- Never convert textual dates to ISO

Place
- Place names and countries are recorded as used at the time
- No modern renaming
- No geopolitical normalization

Schema behavior
- Schema validates structure only
- Schema must not validate or interpret time.value

Gold actions
- Human-created
- Stored separately
- Never auto-modified
