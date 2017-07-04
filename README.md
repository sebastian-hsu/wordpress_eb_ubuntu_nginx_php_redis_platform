# WordPress Environment with ALB based on my custom Elastic Beanstalk Platform (eb_ubuntu_nginx_php_redis_platform)
This project is for my own custom Elastic Beanstalk platform [eb_ubuntu_nginx_php_redis_platform](https://github.com/sebastian-hsu/eb_ubuntu_nginx_php_redis_platform) 

If you are new to Elastic Beanstalk, you can reference [my course](https://www.udemy.com/wordpress-on-aws/?couponCode=WP_AWS_EB) on Udemy.

## Create Elastic Beanstalk Environment
Create the environment by using EB CLI
```
eb create -p **CUSTOM-PLATFORM-ARN** -c **subdomain_name** -ip **profile_name** --elb-type application -i **instance_type** -k **key_name** --service-role **servicerole** --vpc.id **vpc_id** --vpc.ec2subnets **subnet1,subnet2** --vpc.elbsubnets **subnet1,subnet2** --vpc.securitygroups securitygroup1,securitygroup2 --vpc.elbpublic --vpc.publicip
```
- `eb create` options (Ref the detail official [documentation](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb3-create.html))

|Name|Description|
|:---:|---|
|-p|You should be able to get your **CUSTOM-PLATFORM-ARN** after platform is created. Or you can use `eb platform list` command under your platform project folder to get **CUSTOM-PLATFORM-ARN** .|
|-c|(Optional)Subdoamin name.|
|-ip|(Optional)Based on your environment, please make sure you have proper [instance role](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/concepts-roles.html#concepts-roles-instance) setup.|
|--elb-type|You must specify **application** in order to use ALB.|
|-i|(Optional)Instance type you need.|
|-k|(Optional)EC2 instance [key pair](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/using-features.managing.ec2.html).|
|--service-role|Default Elastic Beanstalk service role doesn't have ability to access [ALB]((#ALB)), you must specify your own [service role](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/concepts-roles.html#concepts-roles-service) properly.|
|--vpc.id|You have to specify a VPC ID in order to use ALB.|
|--vpc.ec2subnets|Specifies subnets for Amazon EC2 instances in a VPC.|
|--vpc.elbsubnets|Specifies subnets for the Elastic Load Balancing load balancer in a VPC.|
|--vpc.securitygroups|You need to set it properly if you want to [connect to your DB](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/AWSHowTo.RDS.html) outside this Elastic Beanstalk.|
|--vpc.elbpublic|(Optional)Check your VPC setting.|
|--vpc.publicip|(Optional)Check your VPC setting.|

There are some `.ebextensions` settings as below.  
### Cloudwatch Logs (remember to add IAM settings)
In this repo, I extend existing log streams and add nginx_logs, you can find in [nginx_logs.config](.ebextensions/nginx_logs.config)
> Be sure to have proper [CloudWatch Log IAM permission](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/AWSHowTo.cloudwatchlogs.html) in your **instance role**.
### <a name="ALB"></a>ALB (remember to add IAM settings)
I add ALB settings, you can modify base on your situation
> Be sure to have proper [ALB permission](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/environments-cfg-applicationloadbalancer.html) in your **service role**.
- [application-load-balancer.config](.ebextensions/application-load-balancer.config)
- [alb-default-process.config](.ebextensions/alb-default-process.config)

## This repo contains (install on 2017/05/25)
- [WordPress 4.8](https://wordpress.org/download/)
- [WooCommerce 3.0.7](https://wordpress.org/plugins/woocommerce/)
- [WordPress Importer 0.6.3](https://wordpress.org/plugins/wordpress-importer/)
- [Redis Object Cache 1.3.5](https://wordpress.org/plugins/redis-cache/)
- [Amazon Web Service 1.0.2](https://wordpress.org/plugins/amazon-web-services/)
- [WP Offload S3 Lite 1.1.6](https://wordpress.org/plugins/amazon-s3-and-cloudfront/)

## todo
- http2 alb
- http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/customize-environment-resources-elasticache.html

