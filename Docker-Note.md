# Docker Notes

### Virtual machine vs Container

| Virtual machine | Container |
| ----------- | ----------- |
| An abstraction of a matchine (physical hardware) **Hypervisor** Vmware/Virtualbox | An Isolated environment for running an application |
| Runs a complete operating system including the kernel, thus requiring more system resources (CPU, memory, and storage) | Runs the user mode portion of an operating system, and can be tailored to contain just the needed services for your app, using fewer system resources. |
|Slows to start | Start quickly, lightweight |
|Need more hardware | Need less hardware |
|Use full blown OS | Use Os of the host |

### Docker Architecture

![image](https://github.com/user-attachments/assets/b5649fe7-44ad-425d-8394-0ef6c473dbea)

![image](https://github.com/user-attachments/assets/b21c10a0-c32c-49f7-b27d-c002c6791d5d)




### Install Docker

[Get started with Docker](https://www.docker.com/get-started/)


[Install wsl for windows](https://learn.microsoft.com/en-us/windows/wsl/install)

### Dev workflow

**What is image?**

- A cut-down OS
- A runtime environment
- Contains Application files
- Contains Third party libraries
- Contains Environment variables
