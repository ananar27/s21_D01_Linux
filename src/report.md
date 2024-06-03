
# Linux D01 report by ananar27

## Part 1. Installation of the OS

![Part 1.](pictures/task1.png)  *OS installed*

- Ubuntu version checked via `cat /etc/issue` command.

## Part 2. Creating a user

- Add new user via `sudo useradd (name)` command.

![Part 2.1](pictures/task2_1.png)  *new user*

- Add new user to `adm` group via `sudo usermod -a -G adm (name)`

![Part 2.2](pictures/task2_2.png)  *new user added to adm group*

- Check if user is present via `cat /etc/passwd`

![Part 2.3](pictures/task2_3.png)  *new user present*

## Part 3. Setting up the OS network

- Machine name can be set via `hostnamectl set-hostname 'new-hostname'` command, where 'new-hostname' is the desired name.
- Another option is to change `/etc/hostname` file.

![Part 3.1](pictures/task3_1.png)  *new hostname*

- Timezone can be changed via `sudo timedatectl set-timezone Europe/Moscow` command, where `Europe/Moscow` can be changed to desired timezone.

![Part 3.2](pictures/task3_2.png)  *new timezone*

- Output the names of the network interfaces can be obtained via looking to catalog */sys/class/net* or by using command `ip -br a show`.
- The `lo` or 'loopback device' is a special, virtual network interface that computer uses to communicate with itself. It is used mainly for diagnostics and troubleshooting, and to connect to servers running on the local machine.

![Part 3.3](pictures/task3_3.png)  *new network interfaces*

- To get the ip address of the device we are working on from the DHCP server, we need to use `sudo dhclient -v enpOs3`, where `enpOs3` was discovered earlier.

- DHCP - Dynamic Host Configuration Protocol.ip route | grep default

![Part 3.4](pictures/task3_4.png)  *DHCP*

- Return your external IP via `curl ifconfig.me`.
- You can also use `wget -qO- eth0.me`.

![Part 3.5](pictures/task3_5.png)  *external IP*

- Get information about default IP with `ip route | grep default`.

![Part 3.6](pictures/task3_6.png)  *default IP*

- To change  ip, gw, dns settings we need to change file */etc/netplan/00-installer-config.yaml*. Set `dhcp4` to `false`. Add addresses.

![Part 3.7](pictures/task3_7.png)  *new network settings*

- Reboot with `sudo reboot` and then ping 1.1.1.1 and ya.ru remote hosts. Look on the 0% packet loss.

![Part 3.8](pictures/task3_8.png)  *ping results*

## Part 4. OS Update

- Update the OS via `sudo apt-get update` command.

- Then use `sudo apt-get upgrade` command. Confirm changing the disk space.

![Part 4.1](pictures/task4_1.png)  *update*

## Part 5. Using the sudo command

- command `sudo` stands for "Substitute User and do". It enables users to run programs with the security privileges of another user, by default the superuser.

- Change password for `useruser` user.

![Part 5.1](pictures/task5_1.png)  *password change*

- Give sudo rights to `useruser` user by using `sudo usermod -a -G sudo useruser`

![Part 5.2](pictures/task5_2.png)  *sudo rights*

- Change the user via `su useruser` and use `sudo hostnamectl set-hostname newhost`

![Part 5.3](pictures/task5_3.png)  *change user*

## Part 6. Installing and configuring the time service

- Output the current time.

![Part 6.1](pictures/task6_1.png)  *current time*

- Install ntp for time sync with `sudo apt-get install ntpdate`.

![Part 6.2](pictures/task6_2.png)  *ntp installed*

- Output the current time once again.

![Part 6.3](pictures/task6_3.png)  *current time again*

## Part 7. Installing and using text editors

- Installation of VIM, NANO, MCEDIT.

![Part 7.1](pictures/task7_1.png)  *VIM, NANO, MCEDIT*

![Part 7.2](pictures/task7_2.png)  *VIM, NANO, MCEDIT*

![Part 7.3](pictures/task7_3.png)  *VIM, NANO, MCEDIT*

- Screenshot of VIM. To exit with save you need to quit insert mode by pressing `ESC`, then you need to type `:wq`.

![Part 7.4](pictures/task7_4.png)  *VIM redacted*

- Screenshot of NANO. To exit with save you need to press `CTRL+X`, then press `Y` to confirm.

![Part 7.5](pictures/task7_5.png)  *NANO redacted*

- Screenshot of MCEDIT. To exit with save you need to press `F2`, confirm with `Enter`, press `F10`.

![Part 7.6](pictures/task7_6.png)  *MCEDIT redacted*

- Screenshot of VIM with edited content. To quit without saving press `ESC` and then type `:q!`.

![Part 7.7](pictures/task7_7.png)  *VIM redacted*

- Screenshot of NANO with edited content. To quit without saving you need to press `CTRL+X`, then press `n` to confirm.

![Part 7.8](pictures/task7_8.png)  *NANO redacted*

- Screenshot of MCEDIT. To exit without save you need to press `F10` and `n` to confirm.

![Part 7.9](pictures/task7_9.png)  *MCEDIT redacted*

- VIM can search and replace with a single command `:s/<search_term>/<replace_term>`

![Part 7.10](pictures/task7_10.png)  *VIM rserach/replace*

- For NANO you need to press `CTRL`+`\`. Type search string, press `ENTER`. Then type substitute string, press `ENTER` again. Press `a` to change all occurances.

![Part 7.11](pictures/task7_11.png)  *NANO rserach/replace*


- For MCEDIT you need to press `F4`, type search word, press `TAB`, type substitute word, press `ENTER` and then press `ENTER` again.

![Part 7.12](pictures/task7_12.png)  *MCEDIT rserach/replace*

## Part 8. Installing and basic setup of the SSHD service

- Install OpenSSH-server via `sudo apt install openssh-server`.

![Part 8.1](pictures/task8_1.png)  *OpenSSH-server installed*

- Start SSH automatically on boot by using `sudo systemctl enable ssh`.
![Part 8.2](pictures/enable-ssh)  *OpenSSH-server started*


- To reset to port 2022 we nned to edit file */etc/ssh/sshd_config*: uncomment port 22 in file and change 22 to 2022.

![Part 8.2](pictures/task8_2.png)  *OpenSSH-server started*


- Use `ps` command to see ssh process. We need to use `-C` to print only the process IDs of SSHd.

![Part 8.3](pictures/task8_3.png)  *openssh-server ps*

- Rebbot system via `sudo reboot`. Install netstat via `sudo apt install net-tools`. Call `netstat -tan` and examine if `tcp 0 0.0.0.0:2022 0.0.0.0:* LISTEN` is present.

![Part 8.4](pictures/task8_4.png)  *install nettools*
![Part 8.5](pictures/task8_5.png)  *OpenSSH-server netstat*

- Netstat is a command line utility that can be used to list out all the network (socket) connections on a system.

- Key `-a`: (all) Displays all options, not displays listen associated by default

- Key `-t` (tcp) only shows TCP-related options

- Key `-n` refuses to display an alias, which can display all of the numbers into numbers.

- Column `Proto`: the protocol (tcp, udp, raw) used by the socket.

- Column `Recv-Q`: the count of bytes not copied by the user program connected to this socket.

- Column `Send-Q`: the count of bytes not acknowledged by the remote host.

- Column `Local Address`: address and port number of the local end of the socket.

- Column `Foreign Address`: address and port number of the remote end of the socket.

- Column `State`: the state of the socket.

- 0.0.0.0 can be used as own source address in IP.

## Part 9. Installing and using the top, htop utilities

- Install top and htop utilities. They were already installed on my system.

![Part 9.1](pictures/task9_1.png)  *top and htop installed*

- top utility output. You can see needed values at the picture below.

![Part 9.2](pictures/task9_2.png)  *top output*

1. Uptime: 14 min 05 sec;

2. Number of authorised users: 1;

3. Total system load: 0.13%;

4. Total number of processes: 94;

5. Cpu load: 100.0 (id)

6. Memory load: 153.3 used, 473.3 cache.

7. Pid of the process with the highest memory usage: 642 (use `SHIFT`+`M`)

8. Pid of the process taking the most CPU time: 2013

- To sort in htop, you need to press `F6` and choose process.

![Part 9.3](pictures/task9_3.png)  *htop output*

![Part 9.4](pictures/task9_4.png)  *htop output*

![Part 9.5](pictures/task9_5.png)  *htop output*

![Part 9.6](pictures/task9_6.png)  *htop output*

- filtered for SSHd process. Press `F4` and type needed process.

![Part 9.7](pictures/task9_7.png)  *htop output*

- htop with the syslog process. You need to press `F3` and type needed process.

![Part 9.8](pictures/task9_8.png)  *htop output*

- To add output, enter setup mode by pressing `F2`, choose and add needed outputs to right column.

![Part 9.9](pictures/task9_9.png)  *htop output*
![Part 9.10](pictures/task9_10.png)  *htop output*
![Part 9.11](pictures/task9_11.png)  *htop output*
![Part 9.12](pictures/task9_12.png)  *htop output*
![Part 9.13](pictures/task9_13.png)  *htop output*
![Part 9.14](pictures/task9_14.png)  *htop output*

## Part 10. Using the fdisk utility

- Run `fdisk -l` command.

![Part 10.](pictures/task10.png)  *fdisk output*

- name: /dev/sda;
- disk size: 10GiB;
- sector quantity : 20971520;
- swap size : 0.

## Part 11. Using the df utility

- Run `df` command

![Part 11.1](pictures/task11_1.png)  *df output*

- Partition size: 8408452.
- Space used: 4141876.
- Space free: 3817860.
- Percentage used: 53.
- Measurement unit: kylobytes.

![Part 11.2](pictures/task11_2.png)  *df -Th output*

- Partition size: 8.1G.
- Space used: 4.0G.
- Space free: 3.7G.
- Percentage used: 53.
- Filesystem: `ext4`.

## Part 12. Using the du utility

- Output the size of /home, /var, /var/log folders. Use `du -lhs`+name command.

![Part 12.1](pictures/task12_1.png)  *du output*

- Output the size of all contents in /var/log.

![Part 12.2](pictures/task12_2.png)  *du output*

## Part 13. Installing and using the ncdu utility

- Install ncdu via `sudo apt install ncdu`.

![Part 13.1](pictures/task13_1.png)  *ncdu installed*
![Part 13.2](pictures/task13_2.png)  *ncdu installed*
![Part 13.3](pictures/task13_3.png)  *ncdu installed*

## Part 14. Working with system logs

- Open */var/log/dmesg* via `cat /var/log/dmesg`

![Part 14.1](pictures/task14_1.png)  *cat /var/log/dmesg*

- Open */var/log/syslog* via `cat /var/log/syslog`

![Part 14.2](pictures/task14_2.png)  *cat /var/log/syslog*

- Open */var/log/auth.log* via `cat /var/log/auth.log`

![Part 14.3](pictures/task14_3.png)  *cat /var/log/auth.log*

- Check login via `lastlog`. Here my user is specified via `lastlog -u vova`.

![Part 14.4](pictures/task14_4.png)  *lastlog output*

- Restart SSHd via `sudo systemctl restart sshd`. Find last rows in */var/log/syslog*

![Part 14.5](pictures/task14_5.png)  *cat /var/log/syslog*

## Part 15 Using the CRON job scheduler

- To run `uptime` via CRON you need to type `crontab -e` and add `*/2 * * * * uptime` at the end.

![Part 15.1](pictures/task15_1.png)  *crontab -e*

- Current tasks can be checked via `crontab -l`.

![Part 15.2](pictures/task15_2.png)  *crontab -l*
