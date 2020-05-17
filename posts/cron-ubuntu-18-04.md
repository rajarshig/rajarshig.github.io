# Setup Cron job in Ubuntu 18.04
### Published at: 17/5/2020
---
Cron is a tool for time based job scheduling - found in most of Unix based operating systems. Although it was developed long time ago, its simplicity & effectiveness is remarkable.

## Use
Any script or command which is to be executed in some time interval, can be set with Cron.

## Points to remember
- Absolute paths for script or files need to be provided. For eg. I have a python file in a virtual environment which I want to set with Cron. In that case, I have to provide the command as below

```
/home/username/venv/bin/python  /home/username/venv/project/script.py
```
- It need to be planned if the output of the command (if any) need to be saved. It is also possible to setup email integration with a Cron job. 

## Steps
- Below command opens the crontab file for current user. At the bottom, we can add multiple cron entries
```
crontab -e
```
- A single cron entry follows `m h dom mon dow` format, which means `minute hour dayofmonth month dayofweek command`. Detail instruction & example are also included in the file itself
- To run a python script on 12PM daily, we would add below entry
```
0 12 * * * /home/username/venv/bin/python  /home/username/venv/project/script.py
```
- To ignore a field, use `*`. Then only the non `*` fields will be considered, as here I have ignored the dom, mon, dow fields, so the Cron will run daily
- As the minimum time field is minute, we can not use seconds for Cron
- After entering the entry, use `Ctrl+O` & `Ctrl+X` to save 
- Ensure there are no `\n` character in the entry line, else parsing error will be thown while saving

- The Cron `dameon` will check the entries in its own, so not need to restart it after entry
- The generated crontab file can be seen at `/var/spool/cron/crontabs/username`
- The log of the Cron job can be found in `syslog`. We can search Cron logs by username
```
cat /var/log/syslog | grep "CRON" | grep "username"
``` 

## Conclusion
- Although Cron has its limitation, it provides a very stable way to automate administrative tasks
- It provides many more features & options for various use cases

## References:
- [https://www.digitalocean.com/community/tutorials/how-to-use-cron-to-automate-tasks-ubuntu-1804](https://www.digitalocean.com/community/tutorials/how-to-use-cron-to-automate-tasks-ubuntu-1804)
- [https://www.cyberciti.biz/faq/how-do-i-add-jobs-to-cron-under-linux-or-unix-oses/](https://www.cyberciti.biz/faq/how-do-i-add-jobs-to-cron-under-linux-or-unix-oses/)

