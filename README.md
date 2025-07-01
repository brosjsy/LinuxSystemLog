# LinuxSystemLog

Log monitoring plays a critical role in system administration, cybersecurity, and incident response. It involves continuously reviewing and analyzing system logs to detect unusual activity, track user behavior, troubleshoot errors, and maintain system health. During this lab, log monitoring was implemented to provide real-time visibility into the behavior of the Linux system, including authentication attempts, system boot activities, kernel-level messages, and scheduled tasks.

One of the most important benefits of log monitoring is security auditing. By analyzing logs such as /var/log/auth.log and /var/log/secure, I was able to identify failed login attempts, unauthorized access patterns, and sudo misuse. This is vital in detecting brute-force attacks or insider threats before they escalate.

Additionally, log monitoring supports performance troubleshooting. Logs like /var/log/syslog, /var/log/messages, and /var/log/dmesg provide insights into system errors, service failures, hardware issues, and boot problems. For example, I used tail -f and journalctl to track systemd service logs and quickly identify misconfigured or crashing services during runtime.

Furthermore, logs are essential for compliance and auditing in enterprise environments. Retaining and reviewing logs ensures that actions taken by users, cron jobs, and daemons are documented—providing accountability and traceability.

In this lab, I also utilized commands like grep, journalctl, and tail to filter and monitor log entries in real time. This demonstrated how Linux logs can be leveraged to maintain visibility over system operations and enforce security best practices.

Overall, log monitoring is not only useful but necessary for maintaining system integrity, optimizing performance, and ensuring a proactive approach to threat detection and system management.
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







