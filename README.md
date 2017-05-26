# WordPress based on my custom Elastic Beanstalk Platform (eb_ubuntu_nginx_php_redis_platform)
This project is for my own custom Elastic Beanstalk platform [eb_ubuntu_nginx_php_redis_platform](https://github.com/sebastian-hsu/eb_ubuntu_nginx_php_redis_platform) 

## Create Elastic Beanstalk Environment
Create the environment by using EB CLI
```
eb create -p **CUSTOM-PLATFORM-ARN** -c **subdomain_name** -ip **profile_name** --elb-type application -i **instance_type** -k **key_name** --service-role **servicerole** --vpc.id **vpc_id** --vpc.ec2subnets **subnet1,subnet2** --vpc.elbsubnets **subnet1,subnet2** --vpc.securitygroups securitygroup1,securitygroup2
```
- CUSTOM-PLATFORM-ARN: You should be able to get your **CUSTOM-PLATFORM-ARN** after platform is created. Or you can use `eb platform list` command under your platform project folder to get **CUSTOM-PLATFORM-ARN**
- subdomain_name: (optional)
- profile_name: (optional)
- instance_type: (optional)
- key_name: (optional)
- servicerole: (must)
- vpc_id: (must)
- subnet1,subnet2: (must)

There are some `.ebextensions` settings as below.  
### Cloudwatch Logs (remember to add IAM settings)
In this repo, I extend existing log streams and add nginx_logs, you can find in [nginx_logs.config](.ebextensions/nginx_logs.config)
> Be sure to have proper [CloudWatch Log IAM permission](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/AWSHowTo.cloudwatchlogs.html) in your instance role which you can find under [**Configuration**] > [**Instance**] > [**Server**] > [**Instance profile**]
### ALB (remember to add IAM settings)
I add ALB settings, you can modify base on your situation
> Be sure to have proper [ALB permission](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/environments-cfg-applicationloadbalancer.html) in your instance role which you can find under [**Configuration**] > [**Instance**] > [**Server**] > [**Instance profile**]
- [application-load-balancer.config](.ebextensions/application-load-balancer.config)
- [alb-default-process.config](.ebextensions/alb-default-process.config)

## This repo has following plugins (install on 2017/05/25)
- [WooCommerce](https://wordpress.org/plugins/woocommerce/)
- [WordPress Importer](https://wordpress.org/plugins/wordpress-importer/)
- [Redis Object Cache](https://wordpress.org/plugins/redis-cache/)
- [Amazon Web Service](https://wordpress.org/plugins/amazon-web-services/)
- [WP Offload S3 Lite](https://wordpress.org/plugins/amazon-s3-and-cloudfront/)

## todo
- http2 alb
- http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/customize-environment-resources-elasticache.html

