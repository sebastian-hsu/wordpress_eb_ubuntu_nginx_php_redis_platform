# This project is for my own custom Elastic Beanstalk platform [eb_nginx_php_redis_platform](https://github.com/sebastian-hsu/eb_nginx_php_redis_platform) 

## Create Elastic Beanstalk Environment
You have to create the environment by using EB CLI
```

```

There are some `.ebextensions` settings as below.  
### Cloudwatch Logs (remember to add IAM settings)
In this repo, I extend existing log streams and add nginx_logs, you can find in [nginx_logs.config](.ebextensions/nginx_logs.config)
> Be sure to have proper [CloudWatch Log IAM permission](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/AWSHowTo.cloudwatchlogs.html) in your instance role which you can find under [**Configuration**] > [**Instance**] > [**Server**] > [**Instance profile**]
### ALB (remember to add IAM settings)
I add ALB settings, you can modify base on your situation
> Be sure to have proper [ALB permission](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/environments-cfg-applicationloadbalancer.html) in your instance role which you can find under [**Configuration**] > [**Instance**] > [**Server**] > [**Instance profile**]
- [application-load-balancer.config](.ebextensions/application-load-balancer.config)
- [alb-default-process.config](.ebextensions/alb-default-process.config)

