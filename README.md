
# 🐧 Hello World Linux Kernel Module

This is a simple **"Hello World" kernel module** written for Ubuntu/Linux systems.  
It demonstrates the basic structure of a Linux kernel module — how to build, load, and unload it using standard tools like `insmod`, `rmmod`, `lsmod`, and `dmesg`.

---

## 📁 Project Structure
hello-world-linux-kernel-module/
├── Makefile # Used to compile and clean the kernel module
└── hello.c # The source code for the kernel module

---

## ⚙️ Prerequisites

Before starting, make sure you have:
- Ubuntu or any Linux distribution with kernel headers installed  
- Basic knowledge of Linux terminal commands  
Pictures..........
![WhatsApp Image 2025-10-16 at 14 55 53_84427f85](https://github.com/user-attachments/assets/bf6ec186-6be7-4c50-8f93-9b6a4d9137a9)
![WhatsApp Image 2025-10-16 at 14 54 55_ba933480](https://github.com/user-attachments/assets/8c4012cb-f750-4240-9805-9509ee548eea)
![WhatsApp Image 2025-10-16 at 14 53 45_dc610e30](https://github.com/user-attachments/assets/8d23dd8e-a735-44a9-894a-95fa56371ba3)

Install required packages:
```bash
sudo apt update
sudo apt install build-essential linux-headers-$(uname -r)

🧠 Step 1: Create the Kernel Module

File: hello.c

#include <linux/module.h>
#include <linux/kernel.h>
#include <linux/init.h>

MODULE_LICENSE("GPL");
MODULE_AUTHOR("Your Name");
MODULE_DESCRIPTION("A simple Hello World Linux Kernel Module");

static int __init hello_init(void)
{
    printk(KERN_INFO "Hello, World! Kernel module loaded.\n");
    return 0;
}

static void __exit hello_exit(void)
{
    printk(KERN_INFO "Goodbye, World! Kernel module unloaded.\n");
}

module_init(hello_init);
module_exit(hello_exit);

🧩 Step 2: Create the Makefile

File: Makefile

obj-m += hello.o

all:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules

clean:
	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean


  🧰 Step 3: Build the Module

Run:

make


This will generate:

hello.ko   # The compiled kernel object module

🚀 Step 4: Load the Module

Insert the module into the kernel:

sudo insmod hello.ko


Check kernel messages:

dmesg | tail


You should see:

[xxxx.xxxxxx] Hello, World! Kernel module loaded.

🧹 Step 5: Verify the Module

List loaded modules:

lsmod | grep hello

🛑 Step 6: Remove the Module

Unload the module:

sudo rmmod hello


Check kernel logs again:

dmesg | tail


You should see:

[xxxx.xxxxxx] Goodbye, World! Kernel module unloaded.

🧼 Step 7: Clean Build Files

Run:

make clean

🧾 Output Example
$ sudo insmod hello.ko
$ dmesg | tail
[1234.567890] Hello, World! Kernel module loaded.

$ sudo rmmod hello
$ dmesg | tail
[1234.678901] Goodbye, World! Kernel module unloaded.

💡 Notes

printk() is used instead of printf() because it logs directly to the kernel log buffer.

dmesg displays these logs.

Always use sudo when loading or unloading kernel modules.

🧑‍💻 Author

Your Name
Created for educational purposes to understand Linux Kernel Module programming.

📜 License

This project is licensed under the GPL v2 License — free to use and modify.
---

Would you like me to include **GitHub badges** (for license, language, and stars/forks) and a **screensh
