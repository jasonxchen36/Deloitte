This process describes how to renew the Redis TLS Certificate, which is needed to enable TLS/SSL for authenticating the Redis server and Cribl Workers. Redis is used for caching files in order to drop a large volume of duplicate events in Cribl.

1. Renew the certificate in Venafi and make sure it is signed as a "TLS Web Server Authentication"
   `openssl x509 -in redis_dev_cert_2024.pem -noout -text` 
   `openssl x509 -in redis_prod_cert_2024.pem -noout -text`
2. Sudo to root
`sudo su`
3. Make a new cert pem file in /etc/redis
`vi /etc/redis/redis_<env>_cert_<YYYY>.pem`

   Example: `vi /etc/redis/redis_dev_cert_2024.pem`

4. Change the permissions of the new cert file to the redis service account:
`chown redis:root /etc/redis/redis_<env>_cert_<YYYY>.pem`

   Example: `chown redis:root /etc/redis/redis_dev_cert_2024.pem`

5. Update the redis.conf with the new file:
`vi /etc/redis.conf`
![image.png](/.attachments/image-dea2ae2b-55cb-4fbb-8273-f9561bc0b03d.png)

   ![image.png](/.attachments/image-603d1f37-c153-42d2-b637-9d497a6c7cf0.png)

6. Verify the update to redis.conf:
`cat /etc/redis.conf | grep .pem`

7. Restart Redis service
`systemctl restart redis`

8. Verify Redis is functioning properly
`systemctl status redis`
![image.png](/.attachments/image-c8257914-900c-4724-b9d4-91ba903c8a46.png)

   `tail -f /var/log/redis/redis.log`
   ![image.png](/.attachments/image-75df0381-6166-4664-a6cc-f81ea84fbc28.png)

    `ls -l /var/log/redis/`
    ![image.png](/.attachments/image-09f28eb4-e93e-48a6-8305-2ba8c440dde7.png)