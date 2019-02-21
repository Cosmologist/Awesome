# strace
[strace](https://strace.io/) is Linux utility to monitor and tamper with interactions between processes and the Linux kernel (system calls, signal deliveries, and changes of process state).

## Examples
```
# Monitoring file activity
strace -p process-pid

# Monitoring the network
strace -e trace=network

# Monitoring memory calls
strace -e trace=memory
```
## Links
- [The ultimate strace cheat sheet](https://linux-audit.com/the-ultimate-strace-cheat-sheet/)
