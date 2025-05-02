## ✅ Linux OS

**Q1: What operating systems are you familiar with and have worked on?**  
A: I have worked extensively with various Linux distributions such as Ubuntu, CentOS, Red Hat Enterprise Linux (RHEL), and Debian. I have also used Windows Server environments, especially in hybrid cloud and enterprise infrastructure scenarios.

**Q2: What is a kernel?**  
A: The kernel is the core component of an operating system that acts as a bridge between hardware and software. It manages system resources like CPU, memory, and I/O devices, and is responsible for process management, memory management, and hardware communication.

**Q3: Which Linux version did you use in your project?**  
A: In my most recent project, I used **Ubuntu 22.04 LTS** across all Kubernetes nodes in a multi-node cluster setup. I have also used CentOS 7 and RHEL 8 in earlier enterprise environments for web servers, Jenkins agents, and Docker hosts.

**Q4: Why do we use Linux OS rather than Windows or others?**  
A: Linux offers greater stability, security, flexibility, and performance for server and DevOps environments. It's open-source, cost-effective, and has strong community support. The ecosystem around containers (like Docker and Kubernetes) is also more mature and performant on Linux. Additionally, most cloud-native and DevOps tools are designed and tested primarily on Linux.

**Q5: Write a shell script to check the permissions of a specific directory for a special user.**  
```bash
#!/bin/bash

# Usage: ./check_permission.sh <username> <directory>
USER=$1
DIR=$2

if [[ -z "$USER" || -z "$DIR" ]]; then
    echo "Usage: $0 <username> <directory>"
    exit 1
fi

if id "$USER" &>/dev/null; then
    if [[ -d "$DIR" ]]; then
        sudo -u "$USER" test -r "$DIR" && echo "User $USER has read permission on $DIR" || echo "User $USER does NOT have read permission on $DIR"
        sudo -u "$USER" test -w "$DIR" && echo "User $USER has write permission on $DIR" || echo "User $USER does NOT have write permission on $DIR"
        sudo -u "$USER" test -x "$DIR" && echo "User $USER has execute permission on $DIR" || echo "User $USER does NOT have execute permission on $DIR"
    else
        echo "Directory $DIR does not exist."
    fi
else
    echo "User $USER does not exist."
fi

