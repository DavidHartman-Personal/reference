- Migrate TF resources to shared TF repos and use PR process for deployments.
  - Backing components - RDS, EFS, ECS Cluster, ALB
  - Setup/Config services tasks - init EFS, Install Senzing filesystem objects, create/init DB schema
  - Senzing Services - Senzing API Server, Web App, Streamloader, Streamproducer, Xterm/ssh, SwaggerUI

- Route53 recs and TF code for internal senzing API Server
  - Internal A record created for senzing.mgmt.beta
  - Need to add additional paths/tg port/container mapping for Web App
  - Confirm scoring account access to senzing API using URL
    - Access works using private IPs/ports, but not with r53 defined names in dev scoring.  KR was investigating what may be causing the issue.  This would address Yahongs items 2 and 3 from above.

- AWS Keys removed everywhere and IAM roles used and secrets used instead
  - RDS Cluster In Progress - Includes using Secrets for DB creds
  - Web App Task needs to be updated
  - Streamloader, Streamproducer and Redoer also need updates to use Roles

- Streamloader additional tasks up and running - KR manually created/started working task.  DH will use the newly created task as a model for adjusting tf resources.  This would address Yahong's items 1 and 4 from above.

- Test loads to confirm license limit (and a baseline performance feel) - Will start when streamloader task fixes/adjustments are confirmed.
  - Used to confirm license limitations.
