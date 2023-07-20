# container-in-go
This code demonstrates how containers are created in Linux.

Thanks to namespaces in Linux we could isolate containers from the Host system and also make us control what the container can see.\
with these lines of code and flags:\
`syscall.CLONE_NEWUTS`: This flag creates a new process namespace (UTS namespace) for the process, effectively isolating its hostname and domain name from the parent process and other processes in the system.

`syscall.CLONE_NEWPID`: This flag creates a new PID (Process ID) namespace for the process. The PID namespace isolates the process IDs, so the process sees only its own processes and not those from other namespaces.

`syscall.CLONE_NEWNS`: This flag creates a new mount namespace for the process. The mount namespace isolates the mount points and filesystem mounts, providing a separate filesystem view for the process.

```go
cmd.SysProcAttr = &syscall.SysProcAttr{
		Cloneflags: syscall.CLONE_NEWUTS | syscall.CLONE_NEWPID | syscall.CLONE_NEWNS,
		Unshareflags: syscall.CLONE_NEWNS,
	}
```
using `Control Group` helps us to control what container can use. TBD later

