# Moodle in AWS

This cloudformation stack is based on
[https://github.com/aws-samples/aws-refarch-moodle](https://github.com/aws-samples/aws-refarch-moodle)

It's the same architecture but with Aurora-MySQL and Nginx.

# Before run the cloudformation stack
Plase download this files, upload to your bucket and change all templates URL in the **00-master.yaml** file

> TemplateURL: https://bucketurl/file.yaml

with your bucket URL.

After that, check the permissions in your bucket.

# Error during installation
  
During the installation, Moodle will detect that it's not the same IP with which the installation was started, this is because it will detect the ALB's IP.  
To solve this, check on the log files which the ALB IP is or check the network interfaces panel in the EC2 section. Then, connect to the database from the web instance, verify the credentials in Secrets Manager and select the moodle database.

> sudo mysql -h writer-endpoint-db -u db-user -p

> show databases;

> use moodle-db;

> select lastip from mdl_user;

> update mdl_user set lastip='alb-ip' where username='admin';

# Notes
This stack has no Redis cache but the application works better with Redis instead of Memcached
