# Compute services

## EC2 - Elastic Cloud Compute

VMs, standard AWS hosting service

## EC2 Container service

Manage docker containers

## Elastic Beanstalk

Automatically provisions services; allows developers to focus on their code. Auto scaling groups, load balancers, EC2 instances.

## Lambda

Upload code and control when it executes, don't have to worry about underlying machines. Functional.

## Lightsail

Virtual Private Service (VPS), static IP server to log into via SSH. Has a management console. (Watered down version of EC2, just deal with underlying OS)

## Batch

For batch cloud computing.

# Storage services

## S3 - Simple Storage Service

Object based storage, files go into buckets (that are in the cloud)

## EFS - Elastic File System

Can store files on a volume and mount it onto multiple virtual machines.

## Glacier

Data archival. Can store large amounts of data for cheap, but not easily accessible.

## Snowball

Migrate large amounts of data into the data centre (terabytes).

## Storage Gateway

Virtual machines to install locally that will be replicated in S3.

# Databases

## RDS - Relational Database Service

mySQL, pSQL, Microsoft SQL Server, Aurora (Amazon's sql), Oracle

## DynamoDB

Non relational DBs

## Elasticache

Cache commonly queried data from the DB

## Red Shift

Data warehousing and business intelligence. Complex queries can be completed a lot faster than in production.

# Migration

## AWS Migration Hub

Tracking service to track applications as they are migrated to AWS. Integrates with other migration services.

## Application Discovery Service

Automates detection of applications and keeps track of their dependencies.

## Database Migration Service

Migrate database from 'on premises' to AWS (can be tracked with AWS Migration Hub)

## Server Migration Service

Migrate virtual and physical servers from 'on premises' to AWS (can be tracked with AWS Migration Hub)

## Snowball

Migrate large amounts of data into the data centre (terabytes).
 
# Networking and Content Delivery

## VPC - Virtual Private Cloud

Virtual data centre; configure the firewalls, availability zones, network side address ranges, network ACLS, route tables.

## CloudFront

Amazon's Content Delivery Network: Media assets, video files, image files can be stored physically closer to the user for quicker access.

## Route 53

Amazon's DNS service. Look up for IPs.

## API Gateway

