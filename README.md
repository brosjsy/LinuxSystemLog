# LinuxSystemLog
 Key Log Files in Linux are always located in /var/log)
 Here are the key locations to be watching when monitoring a linux log
 | Log File                       | Purpose                                    |
| ------------------------------ | ------------------------------------------ |
| `/var/log/syslog`              | General system activity (Debian/Ubuntu)    |
| `/var/log/messages`            | General system activity (RHEL/CentOS)      |
| `/var/log/auth.log`            | Authentication events (logins, sudo, etc.) |
| `/var/log/secure`              | Authentication logs (RHEL/CentOS)          |
| `/var/log/dmesg`               | Kernel ring buffer (boot & hardware logs)  |
| `/var/log/kern.log`            | Kernel logs                                |
| `/var/log/boot.log`            | Boot services and startup events           |
| `/var/log/cron`                | Cron job logs                              |
| `/var/log/httpd/` or `/nginx/` | Web server logs (access, error)            |
| `/var/log/faillog`             | Failed login attempts                      |

Here is a Basic Commands to Monitor linux Logs apparent to check the content or output of the lag 
````
cat /var/log/syslog
````

![image](https://github.com/user-attachments/assets/beb1005e-a231-4f1d-a6d3-a1c3e1bf9e8d)

````
less /var/log/auth.log
````
The First screenshot showcase me trying to login and purposely entering with wrong password to confirm if it will capture the authentication activity eg logins, sudo

![image](https://github.com/user-attachments/assets/891969a9-3292-4574-98ad-ddbca523d7f6)

As you can see from the screenshot below verifying the failed authentication 

"

Jul  1 05:09:16 localhost unix_chkpwd[4668]: password check failed for user (root)
Jul  1 05:09:16 localhost su: pam_unix(su:auth): authentication failure; logname=oraimo uid=1000 euid=0 tty=pts/3 ruser=oraimo rhost=  user=root

"


![image](https://github.com/user-attachments/assets/e5212c8d-d9f6-4481-86b1-6f4ed001f143)

For real time monitoring, it can be done using the following cmd line 
````
tail -f /var/log/messages
````

![image](https://github.com/user-attachments/assets/da01e59e-d222-44f3-b65f-97179021ee69)

````
tail -f /var/log/secure
````

![image](https://github.com/user-attachments/assets/35228f88-bfe9-4e24-8786-468cd5142416)

Other ways by which we can automate log monitoring is with the use of grep command 
````
grep "Failed" /var/log/secure
grep "authentication failure" /var/log/secure
````

![image](https://github.com/user-attachments/assets/d8f2fc43-5c5e-4c60-8753-7e8847500e09)

````
grep "agent" /var/log/messages
````

![image](https://github.com/user-attachments/assets/bfe9284a-36b8-4704-827d-a16a34547b9f)

Some notable command for monitoring the system can be used with the journalctl cmd 

![image](https://github.com/user-attachments/assets/7717f5b0-4531-4717-9f7e-45c13008f61e)

some other way of finding or looking for error or failed log with the use of journalctl is 
by directing the journalctl to a file for checking ie 
````
journalctl > journalct
````

![image](https://github.com/user-attachments/assets/cb821d81-ed57-41ec-b6ab-f8443b5eb9a0)

Confirm that the journalct file has been created 
````
ls -ltr 
````

![image](https://github.com/user-attachments/assets/dfa963d1-f095-4f66-8787-695f002a72f9)

now we check for the faied log from the jouranlct file with the use of grep 
````
grep "failed" journalct
````

![image](https://github.com/user-attachments/assets/d643be7e-950d-4ae8-8cc2-fde57fd0c411)

other useful journalctl command are 
````
journalctl                         # Show full system log
journalctl -xe                    # Show recent logs with errors
journalctl -u ssh                 # Logs for ssh service
journalctl -b                    # Show logs from current boot
journalctl --since "1 hour ago"  # Filter logs by time
````







