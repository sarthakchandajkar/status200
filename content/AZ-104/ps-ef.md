This flag shows the names of all the running processes, their process identification numbers (PIDs), the PIDs of their parents (PPIDs), and when they began (STIME). It also shows what terminal, if any, they're attached to (TTY), how much CPU time they've racked up (TIME), and their full path names. Here's an abbreviated example:

```
UID         PID   PPID  C STIME TTY          TIME CMD
root          1      0  0 13:35 ?        00:00:03 /sbin/init
root          2      0  0 13:35 ?        00:00:00 [kthreadd]
root          3      2  0 13:35 ?        00:00:00 [rcu_gp]
root          4      2  0 13:35 ?        00:00:00 [rcu_par_gp]
root          5      2  0 13:35 ?        00:00:00 [kworker/0:0-cgr]
root          6      2  0 13:35 ?        00:00:00 [kworker/0:0H-kb]
root          8      2  0 13:35 ?        00:00:00 [mm_percpu_wq]
root          9      2  0 13:35 ?        00:00:01 [ksoftirqd/0]
root         10      2  0 13:35 ?        00:00:02 [rcu_sched]
```