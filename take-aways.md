Here are my top 10 takeaways of AWS re:Invent 2018 (random order)
# 1. Product / feature launches
## 1. Firecracker & Lamdba Layers & Lambda runtimes
* AWS majorly invests in Lambda as it is a big succes.
* They now support Lamda layers giving structure to lamdba applications. This is very usefull as one of the risks of Lamda is it'll start like a simple pet store but ends up in spaghetti over time, running in all kinds of un-transparant (dead)loops. Very usefull extension!
* Lambda Layers are positioned to hold common logic/data/code in single functions so you don't have to include them each time you build a new lambda function.
* With other runtimes they now support adding your own favorite runtime. Amongst them is Cobol. Oh-my-god..!
* With Firecracker AWS kinda open-sourced Lambda. Although it will not be the exact copy of todays Lambda it's definitly interesting to have micro-vm-like services. It spins up in around 125 msec, which is definitly an improved compared to containers.

## 2. Amazon Outposts
* AWS's on prem stack. Very awesome.
* Athough it will not support all AWS services off course, it seems to support the most interesting ones: EC2, Lambda, Fargate, ECS, EKS. Not sure what it support on db part.
* Can be of great value for teams which understand AWS, but need to deploy some stuff on-prem as well for whatever reason (like latency).
* Nice competition to Azure Stack
* Has the benefit of partability.
* Gives the opportunity to limit the number of IaaS / PaaS platforms for ABN AMRO

## 3. AWS Step Functions extensions
* AWS now supports native coupling with Services like ECS, Batch, Fargate, DynamoDB, SNS and SQS to use in AWS Step Functions.
* This functionality overlaps with stuff we currently do in ESB: mediation, transformation, integrating and other EIP (Enterprise Integration Patterns)-functionality
* It is likely the need for mediation grows on AWS as our usage of AWS grows in itself. Ie the need to create a business meaningsfull API which combines data/functionality from multiple components. Step Functions might be usefull in this area. More analysis is needed

## 4. DynamoDB Transactions
* Gives transactionality for DynamoDB. Very powerfull for applications now running on mainframe requiring this type of transactions. Ie payments, investment systems. This is now one of most important reason to still use mainframe.
* As DynamoDB is distributed by design, records can still be altered by other nodes. But DynamoDB gives back an error in that case so transactionality seems safeguarded. Not clear what this will do with transaction latency though, but it's worth a while analyses the technical details of it.

## 5. AWS Control Tower
* Gives insights in security and compliance. Definitly interesing for large enterprise as ABN AMRO as it gives an instant view on compliance.

## 6. Tooling to assess on AWS Well-architected Framework
* Very powerfull tool based on Amazons Well-Architected Framework.
* Helps teams in automatically assessing how they're doing and if they comply to best practice designs / architectures.
* Very powerfull for the stage in which ABN AMRO is. Helps in giving teams a mirror without having to hire 100 sr. AWS-consultants.

## 7. Tranfer for sFTP & AWS DataSync
* Ok, not the most skyrocketing technology, but very usefull in ABN AMROs journey to cloud.
* Directly moves files from on-prem NFS to S3

## 8. Amazon Managed Streaming for Kafka
* In preview only. Covers a fully managed Kafka solution. First impression by experts it that it doesn't add much, and is an older version. But for ABN AMRO this can be a very nice (DIAL?) building block. To be furter analysed

## 9. Amazon Blockchain
* Fully managed Blockchain solution supporting Hyperledger Fabric and Ethereum.
* As other participants in the chain also need to have AWS's version of Amazon Blockchain it seems to contradict to the idea of having a central ledger to support a certain community.

## 10. AWS Ground Station
* Groundstation-as-a-Service to connect to your/open satellites and process satellite data. Who doesn't own a satellite anno 2018?
* These Amazon flyboys have to much money :)

# 2 Other takeaways
## 2.1 Insights on AWS API-gateway & DevPortal
* AWS released a brand new devportal in october.
* AMongste others it supports: X-ray tracing and cloudwatch
* API-gateway support burstable throttling aka "Token Bucket Algoritm". This is very powerfull for traffic management and is not supported by Apigee (out of the box). As ABN Amro we really could use this
* Announced to support websockets from now on
* The AWS Marketplace can be an interesting Open Banking channel for our API-products. It has very wide audience. It is based on Usage Plans. Might be worth a detailed look. Off course AWS API-gateway is mandatory. Will not work with apigee.
* API-gateway can auto-generate SDKs

## 2.2 Microservices
* trace_id are considered very crucial. We've seen this challenge before with APIs and is very complex in large applicational chains.
* Financial times has good experience with OpenTracing supporting an e2e trace_id. Is supported by lots of big vendors.
* FT struggles: how to prevent technology explosion as a result of microservices?

## 2.3 Kubernetes
* Multiple (larger) parties conclude in practice they are complex and hard to manage. Benefits are big though. Complex areas: DNS, auto failovers, resends etc. Also config/maintenance of CNI = Container Network interface in EKS is hard.
* 51% of worldwide kubernetes containers run on aws
* Q: EKS is managed service so AWS has access to data? How to secure this?

## 2.4 RedHat OpenShift
* OCP = Openshift Container Platform
* OCP = RHEL + Kubernetes + CI/CD + selfservices + Grafana + Prometheus
* OCP will be offered as service on AWS (wizard style) as a result of the partnership between AWS and RH. Interesting as competes with part of aws products
* Openshift seems quite handy to support multicloud. AWS EKS -even with fargate- is only for AWS offers cluster-wide event streams
* No announcements on EKS on Fraget (booooh)

## 2.5 . Continous deployment advanced best practices
* AWS CodePipeline for pipeline design. AWS CodeDeploy for actual deployments. Seems pretty nice if you are all-in on AWS
* automated deployment tests can be created based on cloudwatch. ie latency tests etc. Nice.
* Nice examples for more complex rollouts: Pseudecode example:

      if($deployCanary()) {
        if($deployAZ1()) {
          for($i=1; $i=8; $i++) {
            deployAZ($i);    
          }
        }
      }

* We should be able to connect quite easily to SNOW, enforcing change approvals.
