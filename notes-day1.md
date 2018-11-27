## 1. Accelerating Customer Workloads Through Containers
* Based on GoPro case. They migrated from monolithical Ruby app to MSA. Reasons:
  * Scale
  * Accelerate dev
  * Easier adoption
  * Automation

> *Questions / Actions*:
> * How to prevent technology explosion as a result of microservices?
> * Need a deepdive on OpenShift. Usefull for multicloud support?
> * EKS is managed service so AWS has access to data? How to secure this?

## 2. AWS Landing zone strategies
* Spend costs by teams is mentioned a lot. How do we handle this within AAB? Best practices:
  * Set costs alarms in aws
  * To enforce using corporate account: scan p2p declarations, than inform. Later on decline expense.
* “Team shared “ services are generic services. Seems like capabilities. When to user team shared in 1 account, and when to chose for a new account?
* Enforce umbrella account: scan p2p declarations 1 - inform, 2 - decline expense.
> Question: does AAB have account team?

## 3. Continous deployment advanced best practices
* AWS CodePipeline for pipeline design. AWS CodeDeploy for actual deployments.
* automated deployment test can be based on cloudwatch. ie latency
* Example: approval message to SNS, then lambda-, or manual function to give approval back to CodePipeline

      comments: {
        maxTime:2,
        metricsRequired: 120,
        namespace: lambda
      }

Nice example: first canary instance, if succeed then zone 1, if this also succeeds, then zone 2-8

    if($deployCanary()) {
        if($deployAZ1()) {
          for($i=1; $i=8; $i++) {
            deployAZ($i);    
          }
        }
    }

> Question: We should be able to connect easily to SNOW, enforcing change approvals.
> What the hell is this blastradius?

## 4. Deploying Microservices using Fargate
### Basics
* Management: ECS and EKS
* Hosting, where they run: EC2 and Fargate
* Fargate: runtime environment, seems CaaS-like
* Fargate is still based on ECS constructs, like tasks, cluster
* Reasons not to choose for Fargate: GPU, Windows native, priviliged Containers. But EC2 and Fargate can co-exist

### Networking
* Each task gets its own interface
* Advice: run in multiple AZ/subnets
* Route53 creates namespace, CNAME and SRV

### KPMG Example Case
* @Ariane Gadd
* CloudOps teams; 150+ prject in use; 250+ production workloads.
* Migration from EC2 -> Fargate;
* Why?
  * no logging on to servers anymore! Full automation
  * reliability & stability
* Using Twistlock for container security
* Why KPMG chose aws:
  * costs
  * Speed of delivery
  * Automation and DevOps

> Question: Since it is PaaS-alike, does AWS has access to container data?
