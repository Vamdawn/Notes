# Quartz Cron Expression

Cron表达式由7个子表达式组成，分别为:

1. Seconds: `0-59`
2. Minutes: `0-59`
3. Hours: `0-23`
4. Day-of-Month: `1-31`
5. Month: `0-11` or `JAN, FEB, MAR, APR, MAY, JUN, JUL, AUG, SEP, OCT, NOV, DEC`
6. Day-of-Week: `1-7` or `SUN, MON, TUE, WED, THU, FRI, SAT`
7. Year(Optional)

## sub-expression

- 每一个子表达式可以包含单个/范围/集合值 => e.g. `"JAN"` or `"JAN-APR"` or `"JAN,MAY,OCT"`
- 符号`*`表示当前表达式下的所有可能值 => e.g. `"0 0 0 1 * ?"` -- 每月1号00:00:00; `"0 0 0 ? * WED"` -- 每周三00:00:00
- 符号`/`表示起始值和递增值的集合, `${start}/${every}` 当前域范围内, 从`${start}`开始, 每次递增`${every}`的所有值 => e.g. `0 0/35 0 ? * *` -- 每天00:00:00和00:35:00
- 符号`?`只适用于Day-of-Month和Day-of-Week, 表示没有特定值
- `L` wip
- `W` wip
- `#` wip
