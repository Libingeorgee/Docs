##  SERVER SPACE EXAUSTED-ISSUE

- Open Terminal(Git-bash)

- Access root user server
```
cd /
```
-List files

```
ls -lrt
```
- Display disk usage in a human-readable format for the current directory

```
du -h -d1
```
- To find the large space occupied file and if it is a removable file(log_file and temp_file) please remove...

- find and delete files older than 7 days within the tomcat/logs/ directory (from logs)

```
find tomcat/logs/ -mtime +7 -print0 | xargs -r -0 rm -rf
```
- Truncate (empty) the contents of the file located at /var/log/syslog.1 (Delete data from syslog)

```
truncate -s 0 /var/log/syslog.1
```
Note:- Please ensure that *syslog* data are required for future reference, make sure files are needed or not

- And additionally;
  Display information about disk space usage

```
df -h
```
