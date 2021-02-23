# Terraform notes/commands

terraform plan -target aws_db_subnet_group.mgmt-datasources-db-sng

## Target specific resource

terraform plan -target=aws_iam_server_certificate.senzing-alb-tls-cert

terraform state rm module.gost_crawl_cluster.module.eks_control_plane.aws_eks_cluster.cluster

## Using Templates

1. First generate cli input skeleton.

`aws ecs run-task --generate-cli-skeleton --profile int`

2. Remove unneeded configurations frmo cli-input file outout.  JSON Formatted terraform template file to be used as input to the aws cli (cli-input-vpc.tpl)

```json
{
    "capacityProviderStrategy": [
        {
            "capacityProvider": "",
            "weight": 0,
            "base": 0
        }
    ],
    "cluster": "",
    "count": 0,
    "enableECSManagedTags": true,
    "group": "",
    "launchType": "EC2",
    "networkConfiguration": {
        "awsvpcConfiguration": {
            "subnets": [
                ""
            ],
            "securityGroups": [
                ""
            ],
            "assignPublicIp": "DISABLED"
        }
    },
    "overrides": {
        "containerOverrides": [
            {
                "name": "",
                "command": [
                    ""
                ],
                "environment": [
                    {
                        "name": "",
                        "value": ""
                    }
                ],
                "cpu": 0,
                "memory": 0,
                "memoryReservation": 0,
                "resourceRequirements": [
                    {
                        "value": "",
                        "type": "GPU"
                    }
                ]
            }
        ],
        "cpu": "",
        "inferenceAcceleratorOverrides": [
            {
                "deviceName": "",
                "deviceType": ""
            }
        ],
        "executionRoleArn": "",
        "memory": "",
        "taskRoleArn": ""
    },
    "placementConstraints": [
        {
            "type": "distinctInstance",
            "expression": ""
        }
    ],
    "placementStrategy": [
        {
            "type": "binpack",
            "field": ""
        }
    ],
    "platformVersion": "",
    "propagateTags": "SERVICE",
    "referenceId": "",
    "startedBy": "",
    "tags": [
        {
            "key": "",
            "value": ""
        }
    ],
    "taskDefinition": ""
}
```

3. Terraform resource definitions

```hcl-terraform
data "template_file" "example" {
  template = "${file("cli-input-vpc.tpl")}"

  vars = {
    vpc-id = "vpc-061effee3ad7be455"
  }
}

# aws ec2 describe-vpcs --debug --cli-input-json ${replace(jsonencode(replace(data.template_file.example.rendered),"/\n/",""),"/\\n/"," ")} --profile int
# echo ${jsonencode(data.template_file.example.rendered)}
resource "null_resource" "run-command" {
  provisioner "local-exec" {
    command = <<EOF
aws ec2 describe-vpcs --debug --cli-input-json ${jsonencode(replace(data.template_file.example.rendered,"/\n/",""))} --profile int
EOF
  }
}
```


`aws ec2 describe-vpcs --cli-input-json file://cli-input-vpc.tpl --profile int`

## EFS Init resources

```yaml
version: 1
task_definition:
  task_execution_role: ecsTaskExecutionRole
  ecs_network_mode: awsvpc
  task_size:
    mem_limit: 1GB
    cpu_limit: 512
  efs_volumes:
    - name: senzing-efs-root
      filesystem_id: ${SENZING_AWS_EFS_FILESYSTEM_ID}
      root_directory: /
run_params:
  network_configuration:
    awsvpc_configuration:
      subnets:
        - ${SENZING_AWS_SUBNET_ID_1}
        - ${SENZING_AWS_SUBNET_ID_2}
      security_groups:
        - ${SENZING_AWS_EC2_SECURITY_GROUP}
      assign_public_ip: ENABLED
```

```yaml
version: '3'
services:
  efsinitcontainer:
    command:
      - mkdir
      - /efs/g2
      - "&&"
      - mkdir
      - -p
      - /efs/data/1.0.0
      - "&&"
      - mkdir
      - /efs/etc
      - "&&"
      - mkdir
      - /efs/var
    image: busybox
    logging:
      driver: awslogs
      options:
        awslogs-group: ${SENZING_AWS_LOGS_GROUP:-senzing-docker-compose-aws-ecscli-demo}
        awslogs-region: ${AWS_DEFAULT_REGION}
        awslogs-stream-prefix: efs-init
    user: ${SENZING_DOCKER_RUNAS_INIT_EFS}
    volumes:
      - senzing-efs-root:/efs
volumes:
  senzing-efs-root:
```

## Template File Reference

### Template File: Generating lists

Using templatefile function (starting in .12) allows the passing of lists, maps, etc.  Using template_file resource type only allows passing of simple variables (i.e. string), so combinations of split, join, format, and formatlist need to be used to replicate a list in a template config file.
e.g. to generate a template_file resource with a variable that is to be used as a comma separated list if VPC IDs the following could be done:

In template file named cli-input-vpc.tpl, we would have:
```json
{
    "VpcIds": [
     ${vpc-ids}
    ],
    "DryRun": false
}
```

A template_file resource would use join and formatlist to create a single string that is the list of VPC IDs to lookup.  The resulting template_file would be used in an aws cli command call using the cli-input-json parameter:

```hcl-terraform
variable "vpc_ids" {
  type    = list(string)
  default = ["vpc-061effee3ad7be455","vpc-032bea34fa239dcf8"]
}
data "template_file" "example" {
  template = "${file("cli-input-vpc.tpl")}"
  vars = {
    vpc-ids = "${join(",",formatlist("\"%s\"",var.vpc_ids))}"
  }
}
resource "null_resource" "run-command" {
  provisioner "local-exec" {
    command = <<EOF
aws ec2 describe-vpcs --cli-input-json ${jsonencode(replace(data.template_file.example.rendered,"/\n/",""))} --profile int
EOF
  }
}
```


%{ for addr in ip_addrs ~}
backend ${addr}:${port}
%{ endfor ~}

## Setting up VPC Flog Logs

terraform apply -target=aws_alb_target_group.senzing-alb-target-group -target=aws_alb_listener.senzing-alb-https-listener
