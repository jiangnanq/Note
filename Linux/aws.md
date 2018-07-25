---
title: AWS
date: 2018-2-1
tags: AWS 
---

- After create EC2 instance

```bash
$ chmod 400 /path/my_key_pair.pem
$ ssh -i /path/my_key_pair.pem ec2-user@ec2-198-51-100-1.compute-1.amazonaws.com
```

- Transfering file to instance

```bash
$ scp -i /path/my_key_pair.pem /path/SampleFile.txt ec2-user@ec2-198-51-100.1.compute-1.amazonaws.com
```
