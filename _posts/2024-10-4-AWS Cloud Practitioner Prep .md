---
title: "AWS Cloud Practitioner Prep"
categories: knowledge
permalink: /blogs/aws-prep
toc: true
toc_label: "Table of Contents"
toc_icon: stream # tasks #"torii-gate"
toc_sticky: true
#classes: wide
author_profile: false
---

> This is a resource on AWS Cloud Practitioner certification.

<td>
    <a href="https://www.credly.com/badges/9262eabb-7ebe-42bd-aa27-2cfcda52188b">
        <img src="/assets/c/aws-certified-cloud-practitioner-600-600.png" alt="AWS Cloud Practitioner" width="400"/>
    </a>
    <figcaption><a href="https://www.credly.com/badges/9262eabb-7ebe-42bd-aa27-2cfcda52188b">AWS Cloud Practitioner</a></figcaption>
    <p style="text-align: justify;">Update: I passed the AWS Cloud Practitioner exam on 31/12/2024.</p>
<td>

AWS Training 26/9/2024


# 📁 Module 1: IAM

- Cloud Terms/ Jargons
- Management Console

## cloud computing

traditional vs cloud computing: cloud is on-demand traditional vs cloud computing: cloud is on-demand traditional vs cloud computing: cloud is on-demand

traditional need upfront budget. (not on demand)

- maybe if dont have budget, only next year can implement

aws has bedrock (trained language model)

provision computing resources as needed (use when needed)

pay only what you use

## Breadth of services

foundation services: 

compute

networking

storage

security identity and compliance

AWS global infrastructure

example **aws services (hosted in a data centre, built throughout the world)**:

AWS EC2(cloud vm)

S3 (cloud storage)

AWS build region around the world

some country 2 region, like okyo, osaka

Malaysia, august we just got a region

Availability zone (AZ)

ALL AZ are connected with each other via high speed network (~100Gbps)

not too near, not too far, maybe 100km apart

- Min 3AZ in a Region. normally they dont disclose location of Data Centre for security zone

1st. choose region. (data residency stays there)

if US, data is in US, if MY, data in my

data sovereignity  (regulation of that country. if store in EU, need to follow that law like GDPR.)

AZ is hypermarket like Aeon, 

Local zone is like mini market (to be closer to a community, mini version)

maybe movie studio in an area, maybe build a local zone. lower latency cus meeting the needs to that community

wavelength zone: uses 5g infrastructure

## how many regions in the world?

https://aws.amazon.com/about-aws/global-infrastructure/

other cloud provider would say: more region around the world. but they might only have 1 AZ. 

AWS: 1 region: min 3 AZ

Region selection;

data compliance. subjected by law, regulation

latency: respond time.

pricing.

service availability.

## Edge location (600+ in the world)

- to support services around a region?
- data cache.

eg; netflix ori data from US, but if malaysia, get the data from edge

host services( AZ) vs distribute data(Edge location)

## AWS service management

- to use AWS, use a management console.
- if malaysia, ap-southeast-5
- service button v handy.

EC2: virtual servers in the cloud.

### machine learning services

ie want to build helpdesk . use amazon lex service.

want to use lifelike speech, use amazon polly

want to extract data, amazon textract

want to be minute writer, amazon transcribe.

more advanced users can use commandline

- AWS CLI

integrate with programming language

- SDKs

all the 3 will translate to API calls.

## Shared responsibility

customer: responsible for sec IN the cloud

AWS: responsible for sec OF the cloud

10:50 resume.

## IAM

individual account

aws account

(link to cc)

root user can delegate to IAM users (day to day ops)

- root user use for emergency only.
- can login as root or IAM user

Organisation

- multi-acc
- create root mgt group
    - Org unit
    - acct 1 , acct 2

login

https://aws.amazon.com/console/

IAM policy is in JSON

- have built in policies, no need to create ourselves

amazon web services.

IAM groups

policy precedence:

1. explicit DENY
2. explicit ALLOW
3. implicit DENY (if never say can, never say cannot = always cannot)

IAM roles

- virtual identity: assign policy to it
    - access card

instead of assigning permission by group, can give temporary role.

assume iam user is in iam role: like run as windows admin when run program

- each session

ie; EC2 instance (VM) that access RDS DB)

“assume” role.

Lab 1:

Task 2:

## AWS Account

Account ID

383481996289

Account Alias

Create

Sign-in URL for IAM users in this account

https://383481996289.signin.aws.amazon.com/console

# Module2: AWS Compute (EC2)

compute as a service on AWS

host ur app on VM instances 

- (EC2)

elastic compute cloud

elastic: flexible to meet demand..

host ur app on microservices (containers)

- ECS EKS(fargate(serverless too))

serverless = no need to think about server… just upload code. truly pay as u go

host ur app on serverless

- Lambda

## Amazon Machine Image (AMI)

vdisk 

- has OS
- storage mappings
- permission

auto scaling group (scale in out)

downtime if scale up or down but not horizontally (scale in/out) 

(scale down up takes minutes of downtime)

scale out : +

scale in: -

VM; virtualize hardware

- hypervisor

docker(container): virtualize process

containers: liteweight 

Container orchestrator:

ECS: elastic container service

- docker

EKS: elastic kubernetes service

- kubernetes

ECS is simple. cons: only in AWS

kubernetes (open source) 

container orchesrator: like a crane lifting containers(dockers)

container host

1. ec2 (cloud vm)
2. fargate (serverless hosting for contaier)

## Virtual Private Cloud (VPC)

1. create vpc (tied to a region)
- lab-vpc(10.0.0.0/16
1. subnet (tied to a zone)
2. create internet gateway
3. create a route in route table

# Module3: Networking

# Module4: AWS Storage

Block storage service

- elastic block store (EBS)

Elastic File system (EFS)

S3, simple storage system

# Module5: Database

# Module6: Loab balancing

# Module7: Course summary
Hope to ace the exam.