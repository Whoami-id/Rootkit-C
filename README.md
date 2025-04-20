# Reboot Blocker Kernel Module

This project is a Linux kernel module that hooks and blocks the `reboot()` system call by modifying the system call table at runtime. It demonstrates advanced kernel-level techniques including:

- System call hooking
- Disabling write protection on the `CR0` register
- Dynamic lookup of kernel symbols using `kprobes`

## 🚨 Disclaimer

This project is intended **strictly for educational purposes**. Modifying kernel behavior can be dangerous and may cause system instability or data loss. Do **not** use on production machines.

## 🧠 How It Works

1. The module uses a `kprobe` to dynamically find the address of the `sys_call_table`.
2. It then disables the write protection bit in the CR0 control register.
3. The original `reboot()` syscall is saved.
4. A custom function `hackers_reboot()` is inserted to override the default behavior.
5. If `enable_reboot` is set to 0, the custom handler denies all reboot attempts by returning `EPERM`.

## 🛠️ Building & Running

```bash
make
sudo insmod reboot_blocker.ko

## 🛠️ Remove it
```bash
sudo rmmod reboot_blocker
