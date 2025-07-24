# Three Tier Application

This is an updated code from the original code: [AWS Three Tier Web Architecture Workshop](https://github.com/aws-samples/aws-three-tier-web-architecture-workshop/tree/main)


## Application code
This contains source codes for the `app-tier` and `web-tier`

## Getting Started
- On the web-tier instance, update `nginx.conf` with the internal loadbalancer dns.
``` 
 sudo -su ec2-user
 cd ~
 sudo vi /etc/nginx/nginx.conf
 sudo systemctl restart nginx
 ```

- On the app-tier instance, configure the database
```
 sudo -su ec2-user
 cd ~
 mysql -h CHANGE-TO-YOUR-RDS-ENDPOINT -u CHANGE-TO-USER-NAME -p # get the username and password from aws secret manager `db-cred`
 CREATE DATABASE webappdb;
 USE webappdb;
 CREATE TABLE IF NOT EXISTS transactions(id INT NOT NULL
     -> AUTO_INCREMENT, amount DECIMAL(10,2), description
     -> VARCHAR(100), PRIMARY KEY(id));
 INSERT INTO transactions (amount,description) VALUES ('400','groceries');

 # The output should look like this
 +----+--------+-------------+
 | id | amount | description |
 +----+--------+-------------+
 |  1 | 400.00 | groceries   |
 +----+--------+-------------+
 1 row in set (0.00 sec)
 
```