# Setup Steps

> Edit this file so it matches exactly what you did. Delete any step you did not perform and fix any value that differs.

## 1. Create the VPC
- VPC console → Create VPC → name: `<name>`, IPv4 CIDR: `10.10.0.0/16`

## 2. Create four subnets
| Name | CIDR | AZ | Tier |
|---|---|---|---|
| `<subnet-1>` | `<CIDR>` | `<AZ>` | `<Public/Private>` |
| `<subnet-2>` | `<CIDR>` | `<AZ>` | `<Public/Private>` |
| `<subnet-3>` | `<CIDR>` | `<AZ>` | `<Public/Private>` |
| `<subnet-4>` | `<CIDR>` | `<AZ>` | `<Public/Private>` |

## 3. Internet Gateway and routing
- Create an Internet Gateway and attach it to the VPC
- Public route table: `0.0.0.0/0` → Internet Gateway; associate with the public subnets
- Private route table: no direct internet route (`<NAT Gateway if used>`); associate with the private subnets

## 4. Security groups
- Load balancer SG: allow `<HTTP 80 / HTTPS 443>` from `0.0.0.0/0`
- EC2 SG: allow `<port>` from the load balancer SG; `<SSH rule if any>`

## 5. Launch EC2 instances
- Launch EC2-A and EC2-B: AMI `<AMI>`, type `<type>`, subnet `<subnet>`
- User data / web server setup: `<what you installed, e.g. a simple web page that shows the instance name>`

## 6. Create the load balancer
- Type: `<ALB/NLB>`, internet-facing, in the public subnets
- Create a target group with EC2-A and EC2-B; health check `<path/port>`
- Listener: `<port>` → target group

## 7. IAM
- Role: `<name>` attached to the EC2 instances with policies `<policies>`

## 8. Monitoring and audit
- CloudWatch: `<metrics/alarms/logs>`
- CloudTrail: trail `<name>` enabled, logs to `<S3 bucket>`

## 9. Test
- Open the load balancer DNS name in a browser, refresh several times, and confirm responses alternate between EC2-A and EC2-B `<only if this is what you saw>`

## 10. Clean up
- Terminated EC2 instances, deleted the load balancer, NAT Gateway (if any), and VPC to avoid charges
