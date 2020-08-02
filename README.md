# Moodle in AWS

This cloudformation stack is based on
[https://github.com/aws-samples/aws-refarch-moodle](https://github.com/aws-samples/aws-refarch-moodle)

It's the same architecture but with Aurora-MySQL and Nginx.

# Error during installation
  
During the installation, moodle will detect that it is not the same IP with which the installation was started, this is because it will detect the ALB's IP.  
To solve this, check the Nginx logs which is the ALB IP or check the network interfaces panel in the EC2 section. After that, connect to the database from the web instance. Verify the credentials in Secrets Manager, after that select the moodle database.

> sudo mysql -h writer-endpoint-db -u db-user -p

> show databases;

> use moodle-db;

> select lastip from mdl_user;

> update mdl_user set lastip='alb-ip' where username='admin';
