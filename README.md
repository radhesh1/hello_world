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
3. Create a new source directory to place the hello world kernel module.
   ```
   mkdir kernel_modules
   ```

