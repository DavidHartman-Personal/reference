# Reference for using AWS Secrets Manager

{
    "executionRoleArn": "arn:aws:iam::aws_account_id:role/ecsTaskExecutionRole",
    "containerDefinitions": [
        {
            "entryPoint": [
                "sh",
                "-c"
            ],
            "portMappings": [
                {
                    "hostPort": 80,
                    "protocol": "tcp",
                    "containerPort": 80
                }
            ],
            "command": [
                "/bin/sh -c \"echo '<html> <head> <title>Amazon ECS Sample App</title> <style>body {margin-top: 40px; background-color: #333;} </style> </head><body> <div style=color:white;text-align:center> <h1>Amazon ECS Sample App</h1> <h2>Congratulations!</h2> <p>Your application is now running on a container in Amazon ECS.</p> </div></body></html>' >  /usr/local/apache2/htdocs/index.html && httpd-foreground\""
            ],
            "cpu": 10,
            "secrets": [
                {
                    "valueFrom": "arn:aws:secretsmanager:region:aws_account_id:secret:username_value-u9bH6K",
                    "name": "username_value"
                }
            ],
            "memory": 300,
            "image": "httpd:2.4",
            "essential": true,
            "name": "ecs-secrets-container"
        }
    ],
    "family": "ecs-secrets-tutorial"
}

      SENZING_DB_SECRET_VALUE: "${SENZING_RDS_SECRET_NAME}"
 "secrets": [
      {
        "valueFrom": "${SENZING_RDS_SECRETS_ARN}",
        "name": "SENZING_RDS_SECRET_VALUE"
      }