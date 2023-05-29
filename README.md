# hello_world Kernel Module
## Steps to build the module

1. Install build-essential and relevant linux headers packages. These are mandatory packages required for kernel module development. These can be installed on ubuntu by running the below command.
   ```
   sudo apt-get install build-essential linux-headers-`uname -r`
   ```
   
2. Make sure to login as root, to avoid any permission errors for the operations that we perform later.
   ```
   sudo -i
   ```
   
3. Create a new source directory to place the hello world kernel module.
   ```
   mkdir kernel_modules
   ```
   
4. Create a new source directory to place the hello world kernel module.
   ```
   mkdir kernel_modules
   ```
   
5.  Create your hello world kernel module named “hello_world_mod.c” inside the source directory.
    ```
    cd kernel_modules
    nano hello_world_mod.c
    ```
    The content of kernel module named “hello_world_mod.c” :
    ```
    #include<linux/module.h>
    #include<linux/kernel.h>
       
    MODULE_LICENSE("GPL");
    MODULE_AUTHOR("Radhesh Goel");
    MODULE_DESCRIPTION("A simple hello world module");
    MODULE_VERSION("0.01");
    
    static int __init hello_mod_init(void)
    {
            printk(KERN_ALERT "Hello world from kernel!! \n");
            return 0;
    }
    
    static void __exit hello_mod_exit(void)
    {
            printk(KERN_ALERT "Exiting hello world module from kernel !!!\n");
    }
   
    module_init(hello_mod_init);
    module_exit(hello_mod_exit);
    ```
   **You can observe that we have written a simple kernel module with 2 functions — module init and module exit that shall be called when the kernel module is loaded into(using insmod) and unloaded     from(rmmod) the kernel respectively**
   
   
6.  Create the make file inside the source directory. This is required to build the kernel module program which shall generate the required .ko file (kernel object).
    **Note: Make sure to append the correct .o name to the obj-m variable in the make file (should be similar to the file name used for the kernel module program). As hello_world_mod.c name is used for the kernel module program in this example, the respective object file name hello_world_mod.o needs to be appended to the obj-m variable in make file.**
    
    ```
    nano Makefile
    ```
    The Content of Makefile :
    ```
    obj-m += hello_world_mod.o
    
    all:
         make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules
    
    clean:
         make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean
    ```
