---
title: "Processes on Linux - an explanation."
seoTitle: "Process as used as Linux."
datePublished: Sun Mar 12 2023 18:56:20 GMT+0000 (Coordinated Universal Time)
cuid: clf5rb4si000409jqghy811xt
slug: processes-on-linux
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/WHWYBmtn3_0/upload/add2866bd8cf2f74125da23850e9168b.jpeg
tags: linux, devops, shell, process

---

In a Unix-like operating system-Linux and the others-a process is always running. This running process might not be visible or known by the user, but any app you open or command you execute start a process. In this computer age, many computers can run up to thousands and millions of processes at a time.

## What is a process?

***A process*** is an executing or running instance of a program. Any command you enter starts a process. Some processes run automatically as the system boots and stop until the system is shut down, such processes are called [System](https://en.wikipedia.org/wiki/Daemon_(computing)) daemons: they perform various system-related tasks and they always-with few exception-end with the letter d. An example is *httpd* which runs a web server, another is *init* which serves as an ancestor to all other processes. The maximum number of processes that can be run on a system is limited by the amount of physical memory(RAM) available.

Throughout this article, we will talk about processes, PID, types of processes, creating a background process, changing the priority of a process, and killing a process. before that let's talk about the benefits of the running process.

### Benefits of process

* Task scheduling to maximize CPU utilization: There are a certain number of tasks or processes a CPU can handle at a time. If there are more processes than CPU(and there usually are), the rest of the processes queue or wait(in order of their priority) before a CPU is free and they are run.
    
* Ability to perform different tasks simultaneously: By creating background processes, which are explained more clearly later. you can do any other task simultaneously while the other process is running on the same shell. this improves one efficiency and reduces the amount of time to perform some tasks.
    

### Process Identification Number (PID)

PID is an identification number that is automatically assigned to each process when it is created on a Unix-like machine. the default maximum value of PID is 32, 767. The PID is important to terminate the frozen or otherwise misbehaving program with the `kill` command. The `/proc` file on Linux always contains information about processes.

[Init](https://en.wikipedia.org/wiki/Init#:~:text=Init%20is%20a%20daemon%20process,is%20unable%20to%20start%20it.) is a daemon process, it is a direct or indirect ancestor of all other processes and automatically adopts an orphaned process. It has the same PID on any system and its value is always 1.

### How to get the PID of processes

There are various ways to get the PID of processes, they are:

1. [ps(process state)](https://www.geeksforgeeks.org/ps-command-in-linux-with-examples/) command: The `ps` command is used to list the currently running processes and their PID's along with some other information depending on different options or flags. If the command `ps` is typed without a flag, the output consists of four columns PID, TTY - terminal type, TIME - time the process has been running, and CWD - the command that launched the process.
    
2. `pidof`
    
    ```plaintext
    pidof [process name]
    ```
    
    It will output the PID of the process name.
    
3. [pgrep](https://linuxhint.com/pgrep-command-tutorial/#:~:text=The%20pgrep%20command%20allows%20a,matching%20text%20in%20the%20output.)
    
    The `pgrep` command is used to search for the PID of names. with flag `-l` it displays the process name along the process PID. e.g
    
    ```plaintext
    pgrep firefox
    ```
    
    Other commands to check for PID are `top`, `pstree` etc.
    

The **PID of the current shell** is stored in the special variable `$$`: it can be printed out this way:

```plaintext
echo $$
```

### Type of Processes

* Foreground processes: This type of process depends on the user for input. It is also referred to as an interactive process. It is the process of entering something on the shell and it waits for the process to finish; returns the output and returns the cursor to the Linux terminal.
    
* Background Processes: This type of process run independently of the user. It is an automatic and non-interactive process. We can create a background process and continue to work on another thing at a time, Thus, This gives us the flexibility to work on more than one thing at a time.
    

### Creating a Background process

Assuming you want to download a large file using `wget`, `wget` is a command line tool that makes it possible to download files and interact with REST APIS, assuming the time to download the file will take up to 15 minutes. This is too much time to wait, we can make it a background process and continue with another thing.

***To make a command run as a background process, You will add an ampersand(&) operator after the command***. This process will be forked and run in a separate sub-shell as a job. The shell immediately returns the status, 0 for true and continues as normal, either processing further commands in a script or returning the cursor to the Linux terminal. e.g.

```plaintext
wget https://wordprocess.org/latest.zip &
```

***A job*** is a process that the shell is managing and hasn't finished running.

***A forked process's job number*** stored the PID of the last background process. It is usually stored in the variable `&!` and can be printed out like this:

```plaintext
echo &!
```

### Traversing Background process

There are many commands used in working with background processes, they include:

* [jobs](https://www.ibm.com/docs/en/aix/7.1?topic=j-jobs-command): The command `job` displays the status of the jobs started in the shell environment.
    
* [fg](https://www.geeksforgeeks.org/fg-command-in-linux-with-examples/): The command brings the background process back to the foreground. It is very useful to return to a background process. it is used like this:
    
    ```plaintext
    fg [job number]
    ```
    
* [bg](https://www.geeksforgeeks.org/bg-command-in-linux-with-examples/): The command put the suspended process into the background i.e continues running the suspended process in the background. It is used like this:
    
    ```plaintext
    bg [job number]
    ```
    
* [nohup](https://www.digitalocean.com/community/tutorials/nohup-command-in-linux): Short for no hang-up. It keeps processes running even after exiting the shell or terminal. nohup is used to completely detach a process from the shell and continue after you log out e.g. You want to run a shell script name `todo.sh` in the background and to continue running after exiting the shell. It is used like this:
    
    ```plaintext
    nohup ./todo.sh &
    ```
    

***NB:*** Double ampersand (&&) represent `AND`. It is used to run a list of commands sequentially. You can escape the ampersand operator by using forward slash \\ e.g `\&`

### Niceness value of a process

Niceness value is the priority value given to a process prior to other processes. The value ranges from -20 through 19, where 0 is the default value.

You can change and reassign the nice value of a process by the command `nice` and `renice`: It is used like this

* [nice](https://www.geeksforgeeks.org/nice-and-renice-command-in-linux-with-examples/): assign value to a process by process name
    
    ```plaintext
    nice -n [value] [process name]
    ```
    
* [renice](https://www.geeksforgeeks.org/nice-and-renice-command-in-linux-with-examples/): Change the nice value of a process that is already running using PID
    
    ```plaintext
    renice [new value] -p 'PID'
    ```
    

### Killing a Process

To kill or stop a process there are majorly three commands which include:

* [kill](https://www.geeksforgeeks.org/kill-command-in-linux-with-examples/)
    
    ```plaintext
    kill PID
    ```
    
* [killall](https://www.google.com/amp/s/www.geeksforgeeks.org/killall-command-in-linux-with-examples/amp/)
    
* ```plaintext
        killall processname
    ```
    
* [pkill](https://linuxhint.com/the-pkill-command-in-linux/)
    
    ```plaintext
    pkill -SIGNAL processname
    ```
    

pkill is the most powerful of them all.

### Conclusion

***Linux Process*** is a very powerful feature in DevOps and Linux. The computer schedule task for maximum CPU utilization in order of the niceness of the process, the developer uses the background process utilization to work on more than one thing at a time, and its application is used in stopping a frozen process(program) or a misbehaving process.

This article has covered processes, PID, types of processes, creating a background process, changing the priority of a process, and killing a process.

Mastering the Linux Processes gives you the efficiency to work more than one thing at a time and understand the Linux kernel and the DevOps track better. Let's draw the veil here.

You can share your thoughts with me on Twitter [here](https://twitter.com/musoye1).

Happy Coding!