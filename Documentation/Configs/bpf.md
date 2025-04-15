# BPF CONFIG
#
#
```sh
Kernel hacking  --->
	[*] Tracers  --->
		[*]   Kernel Function Tracer
		[*]   Enable uprobes-based dynamic events

	Compile-time checks and compiler options  --->	
		Debug information (Generate DWARF Version 5 debuginfo)  --->
			(X) Generate DWARF Version 5 debuginfo
		[*] Generate BTF type information

General setup  --->
	BPF subsystem  --->
		[*] Enable bpf() system call
		[*] Enable BPF Just In Time compiler
		[*]   Permanently enable BPF JIT and remove BPF interpreter
		[*] Disable unprivileged BPF by default 
		[*] Enable BPF LSM Instrumentation

	-*- Control Group support  --->
		[*]   Support for eBPF programs attached to cgroups

Security options  --->
	(...,bpf) Ordered list of enabled LSMs
```

```sh
sudo apt install --no-install-suggests --no-install-recommends libbpf1
```