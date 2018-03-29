
# Notes for AWS EC2

1. After create EC2 instance
```
    $ chmod 400 /path/my_key_pair.pem
    $ ssh -i /path/my_key_pair.pem ec2-user@ec2-198-51-100-1.compute-1.amazonaws.com
```
2. Transfering file to instance
```
    $ scp -i /path/my_key_pair.pem /path/SampleFile.txt ec2-user@ec2-198-51-100.1.compute-1.amazonaws.com
```