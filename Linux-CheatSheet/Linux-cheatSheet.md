# Basic Linux Commands

-> [ File System Navigation ]


1. cd:
   
Purpose: Change directory.

Syntax: cd [directory]

Example:
cd /etc → go to /etc

Notes: With no argument, cd goes to home directory.


2. ls:
   
Purpose: List files and directories.

Syntax: ls [options] [path]

Example: ls -lah /var/log

Notes: Use ls --color=auto for colored output.


3. pwd:
   
Purpose: Print working directory.

Syntax: pwd

Example: If you are in /home/user/docs, it outputs /home/user/docs.

Notes: Useful to confirm your current location.



-> [ File & Directory Permissions ]



4. chmod:
   
Purpose: Change file/directory permissions.

Syntax: chmod [mode] file

Example:
chmod 755 script.sh → Owner: rwx, Group: r-x, Others: r-x
chmod u+x file.txt → Add execute for user.

Notes: Use octal numbers (644, 755) or symbolic (u+rwx).


5. chown:
   
Purpose: Change file ownership.

Syntax: chown [owner][:group] file

Example: sudo chown user:devgroup file.txt

Notes: Needs sudo if you’re not the file owner.



->  [ Package Management ]



6. apt:
   
Purpose: High-level package manager (Debian/Ubuntu).

Syntax: sudo apt [command] [package]

Common commands:
update (refresh package list)
upgrade (upgrade all packages)
install (install new package)
remove (uninstall)

Example: sudo apt update && sudo apt install nmap

Notes: Combines functions of apt-get and apt-cache.


7.dpkg:

Purpose: Low-level Debian package manager.

Syntax: sudo dpkg [options] file.deb

Common options: -i (install), -r (remove), -l (list installed).

Example:
sudo dpkg -i package.deb → install .deb
dpkg -l | grep apache → list apache packages.

Notes: Often used with apt (since apt handles dependencies).




->  [ Networking Commands ]



8. ifconfig:
    
Purpose: Display or configure network interfaces.

Syntax: ifconfig [interface] [options]

Example: ifconfig eth0 → show details of eth0.

Notes: Use ip addr show on modern systems.


9. ping:
    
Purpose: Test connectivity to a host.

Syntax: ping [host]

Example: ping -c 4 google.com

Notes: -c limits count (otherwise infinite until stopped).


10. netstat:
    
Purpose: Show network connections, ports, and routing tables.

Syntax: netstat [options]

Example: netstat -tuln | grep :80

Notes: Prefer ss -tuln in new systems.


11. traceroute:
    
Purpose: Show path packets take to a destination.

Syntax: traceroute [host]

Example: traceroute 8.8.8.8

Notes: Helps debug where connectivity is failing.
