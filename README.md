# CVE-2020-8835
```
In the Linux kernel 5.5.0 and newer, the bpf verifier (kernel/bpf/verifier.c) 
does not properly restrict the register bounds for 32-bit operations,
leading to out-of-bounds reads and writes in kernel memory. 

This vulnerability also affects the Linux 5.4 stable series, starting with v5.4.7,
as the introducing commit was backported to that branch. 
This vulnerability was fixed in 5.6.1, 5.5.14, and 5.4.29.

Mitigation for this vulnerability is available by setting the 
'kernel.unprivileged_bpf_disabled' sysctl to '1'.
This disables unprivileged access to the bpf() syscall entirely.

This issue is also mitigated on systems that use secure
boot, because of the kernel lockdown feature which blocks
BPF program loading.
```

## Compile

```console
gcc -o exploit ./exploit.c
```

## Mitigation

##### Ubuntu
```console
$ sudo sysctl kernel.unprivileged_bpf_disabled=1

$ echo kernel.unprivileged_bpf_disabled=1 | \
  sudo tee /etc/sysctl.d/90-CVE-2020-8835.conf
```
##### Redhat
```console
$ sysctl -w kernel.unprivileged_bpf_disabled=1
```

