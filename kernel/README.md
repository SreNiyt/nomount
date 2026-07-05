# NoMount Subsystem for Linux Kernel 4.19 (VFS Stealth Injection)
## Repository Structure
```text
kernel/
├── fs/
│   └── nomount.c      # Core VFS interception logic, Netlink socket handling, and RCU management
├── include/
│   └── linux/
│       └── nomount.h    # Data structures, Netlink family definitions, and function prototypes
└── patches/
    └── nomount_4.19_kernel_integration.patch # Monolithic patch to hook into core VFS infrastructure

```
## Kernel Integration Guide
To merge this subsystem into your existing target kernel tree (such as sashimi_kernel_xiaomi_blossom), execute the following steps exactly as described.
### 1. Stage the Source Components
Copy the standalone clean source components from this repository directly into their respective destinations inside your kernel directory.
```bash
# Execute these commands from the root of the nomount_k4.19 repository
cp kernel/include/linux/nomount.h /path/to/your/target_kernel/include/linux/
cp kernel/fs/nomount.c /path/to/your/target_kernel/fs/

```
### 2. Inject VFS Hooks and Netlink Integration
The provided patch in kernel/patches/ contains the necessary infrastructure modifications to connect the subsystem into the core VFS engine (specifically editing files like fs/open.c, fs/Makefile, and fs/Kconfig).
Navigate to your target kernel directory and apply the implementation patch:
```bash
cd /path/to/your/target_kernel/
git apply /path/to/nomount_k4.19/kernel/patches/nomount_4.19_kernel_integration.patch

```
*Note: Git will automatically scrub trailing whitespace variations and apply the code blocks cleanly across line numbers.*
### 3. Verify and Persist Integration State
Verify that the files have been modified correctly, ensure no reject files (.rej) were generated
