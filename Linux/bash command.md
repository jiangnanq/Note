## Bash command

- Crontab

To add or edit job in crontab
```
$crontab -e
```

Check job
```
$crontab -l
```

Schedule a cron every 5 minutes
```
*/10 * * * * /home/admin/ec2server/taxi.sh > /home/admin/output.txt 2>&1
```

Check history
```
$grep CRON /var/log/syslog
```

[Reference](https://tecadmin.net/crontab-in-linux-with-20-examples-of-cron-schedule/)

