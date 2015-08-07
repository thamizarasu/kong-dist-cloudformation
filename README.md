# [KONG][kong-url] :heavy_plus_sign: [AWS CloudFormation](https://aws.amazon.com/cloudformation/)

- Website: [getkong.org][kong-url]
- Documentation: [getkong.org/docs][kong-docs]
- Mailing List: [Google Groups][google-groups-url]

[![][kong-logo]][kong-url]

This CloudFormation template helps you model and set up Kong's resources in AWS easily.

## Summary

You have option to chose between two templates:

1. provision Kong resources along with a new [Cassandra cluster](http://cassandra.apache.org/), using The [Datastax Cassandra](http://docs.datastax.com/en/cassandra/2.2/cassandra/install/installAMI.html) ami.
2. 
2. provisions Kong resources with user provided Cassandra seed nodes. 

###  Kong with Cassandra DB

| Region            | HVM AMIs                                                                    | PV AMIs                                                                     |
| ----------------: | --------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| `us-east-1`       | [![Kong Stack launch][kong-stack-badge]][us-east-1-caas-hvm-stack-url]      | [![Kong Stack launch][kong-stack-badge]][us-east-1-caas-pv-stack-url]       |
| `us-west-1`       | [![Kong Stack launch][kong-stack-badge]][us-west-1-caas-hvm-stack-url]      | [![Kong Stack launch][kong-stack-badge]][us-west-1-caas-pv-stack-url]       |
| `us-west-2`       | [![Kong Stack launch][kong-stack-badge]][us-west-2-caas-hvm-stack-url]      | [![Kong Stack launch][kong-stack-badge]][us-west-2-caas-pv-stack-url]       |
| `eu-west-1`       | [![Kong Stack launch][kong-stack-badge]][eu-west-1-caas-hvm-stack-url]      | [![Kong Stack launch][kong-stack-badge]][eu-west-1-caas-pv-stack-url]       |
| `ap-northeast-1`  | [![Kong Stack launch][kong-stack-badge]][ap-northeast-1-caas-hvm-stack-url] | [![Kong Stack launch][kong-stack-badge]][ap-northeast-1-caas-pv-stack-url]  |
| `ap-southeast-1`  | [![Kong Stack launch][kong-stack-badge]][ap-southeast-1-caas-hvm-stack-url] | [![Kong Stack launch][kong-stack-badge]][ap-southeast-1-caas-pv-stack-url]  |
| `ap-southeast-2`  | [![Kong Stack launch][kong-stack-badge]][ap-southeast-2-caas-hvm-stack-url] | [![Kong Stack launch][kong-stack-badge]][ap-southeast-2-caas-pv-stack-url]  |
| `sa-east-1`       | [![Kong Stack launch][kong-stack-badge]][sa-east-1-caas-hvm-stack-url]      | [![Kong Stack launch][kong-stack-badge]][sa-east-1-caas-pv-stack-url]       |

###  Kong without Cassandra DB (you need to bring yours)


| Region            | HVM AMIs                                                                | PV AMIs                                                               |
| ----------------: | ----------------------------------------------------------------------- | --------------------------------------------------------------------- |
| `us-east-1`       | [![Kong Stack launch][kong-stack-badge]][us-east-1-hvm-stack-url]       | [![Kong Stack launch][kong-stack-badge]][us-east-1-pv-stack-url]      |
| `us-west-1`       | [![Kong Stack launch][kong-stack-badge]][us-west-1-hvm-stack-url]       | [![Kong Stack launch][kong-stack-badge]][us-west-1-pv-stack-url]      |
| `us-west-2`       | [![Kong Stack launch][kong-stack-badge]][us-west-2-hvm-stack-url]       | [![Kong Stack launch][kong-stack-badge]][us-west-2-pv-stack-url]      |
| `eu-west-1`       | [![Kong Stack launch][kong-stack-badge]][eu-west-1-hvm-stack-url]       | [![Kong Stack launch][kong-stack-badge]][eu-west-1-pv-stack-url]      |
| `ap-northeast-1`  | [![Kong Stack launch][kong-stack-badge]][ap-northeast-1-hvm-stack-url]  | [![Kong Stack launch][kong-stack-badge]][ap-northeast-1-pv-stack-url] |
| `ap-southeast-1`  | [![Kong Stack launch][kong-stack-badge]][ap-southeast-1-hvm-stack-url]  | [![Kong Stack launch][kong-stack-badge]][ap-southeast-1-pv-stack-url] |
| `ap-southeast-2`  | [![Kong Stack launch][kong-stack-badge]][ap-southeast-2-hvm-stack-url]  | [![Kong Stack launch][kong-stack-badge]][ap-southeast-2-pv-stack-url] |
| `sa-east-1`       | [![Kong Stack launch][kong-stack-badge]][sa-east-1-hvm-stack-url]       | [![Kong Stack launch][kong-stack-badge]][sa-east-1-pv-stack-url]      |
 
 
### Cloudformation parameters
 
| Parameter                   | Default      | Description                                                                          |
| --------------------------: | ------------ | ------------------------------------------------------------------------------------ |
| `SSHLocation`               | `0.0.0.0/0`  | The IP address range that can be used to SSH to the Kong and Cassandra EC2 instances |
| `KongProxyAccess`           | `0.0.0.0/0`  | The IP address range that can be used to access the Kong admin server                |
| `KongAdminAccess`           | `0.0.0.0/0`  | The IP address range that can be used to access the Kong proxy server                |
| `KongKeyName`               | `-`          | Existing EC2 KeyPair to enable SSH access to the Kong instances                      |
| `KongFleetMaxSize`          | `2`          | Max Number of Kong instances *(Min: `1`, Max: `10`)*                                 |
| `KongFleetDesiredSize`      | `2`          | Desired Number of Kong instances *(Min: `1`, Max: `10`)*                             |
| `KongInstanceType`          | `c3.8xlarge` | EC2 instance type for Kong                                                           |
| `KongVersion`               | `0.4.1`      | Kong version                                                                         |
| `CassandraKeyName`          | `-`          | Existing EC2 KeyPair to enable SSH access to the instances for Cassandra             |
| `CassandraFleetSize`        | `1`          | Number of nodes in cluster. *(Min: `1`, Max: `10`)*                                  |
| `CassandraAvailabilityZone` | `-`          | Availablity zone in which cassandra cluster would be created, *for multi regions and zones cluster please refer to [Datastax documentation](http://docs.datastax.com/en/cassandra/2.2/cassandra/planning/planPlanningEC2.html?scroll=planPlanningEC2__multi-region-deploy).* |
| `CassandraInstanceType`     | `c3.2xlarge` | EC2 instance type for Cassandra                                                      |
| `CassandraClusterName`      | `-`          | Cassandra cluster name                                                               |
| `CassandraClusterVersion`   | `2.2.0`      | Cassandra cluster version                                                            |
| `CassandraVersion`          | `Community`  | Cassandra version                                                                    |
| `CassandraOpsCenterAccess`  | `0.0.0.0/0`  | The IP address range that can access OpsCenter for Cassandra cluster management      |


### Steps to launch a Kong stack on AWS cloud

1. Create a key pair to access Cassandra instance. Move to next step if you want to use any existing key pair.
2. Create a key pair to access Kong instances. Move to next step if you want to use any existing key pair.
3. Select the region, the virtualization type and then click launch stack. You should see AWS cloudformation "Select Template" page.
4. You can change the stack name. Click next to move to "Specify parameter" page.
5. Fill in all the parameters details. If you chose to launch Kong with Cassandra you would be asked to fill in extra parameters to create a Cassandra cluster. Read description of field and enter the value for each field. 
6. Click next to move to "Option page". Add Tags and other fields according to your requirements otherwise click next.Note: Template is configured to add a "Name" tag to each relevant resource. 
7. Review the information for the stack. When you're satisfied with the settings, click Create
8. AWS CloudFormation begins creating the resources that are specified in the template. To monitor the progress go to AWS CloudFormation console, select the stack in the list. In the stack details pane, click the Events tab to see the progress. 
9. It will take several minutes(~20 minutes) to create the stack. Once the stack has a status of CREATE_COMPLETE, click on output tab to get the proxy and Admin URL, it may take 60 seconds more for links to become active 
 
#### Important note

1. The security configuration on the templates opens up all externally accessible ports to incoming traffic from any IP address if defualt is chosen(0.0.0.0/0). The risk of data loss is high. If you desire a more secure configuration, please update access fields with appropiate IP address range.
2. Template installs many resources on AWS. You will be billed just for the AWS resources used.
3. Some of the instance types may not be supported in all the AWS Regions, so chose next best available option.

## Enterprise Support

Support, Demo, Training, API Certifications and Consulting available at http://getkong.org/enterprise.

[kong-url]: https://getkong.org/
[kong-docs]: https://getkong.org/docs/
[kong-logo]: http://i.imgur.com/4jyQQAZ.png
[kong-benefits]: http://cl.ly/image/1B3J3b3h1H1c/Image%202015-07-07%20at%206.57.25%20PM.png
[mashape-url]: https://www.mashape.com
[license-url]: https://github.com/Mashape/kong/blob/master/LICENSE
[license-badge]: https://img.shields.io/github/license/mashape/kong.svg
[gitter-url]: https://gitter.im/Mashape/kong
[gitter-badge]: https://img.shields.io/badge/Gitter-Join%20Chat-blue.svg
[google-groups-url]: https://groups.google.com/forum/#!forum/konglayer

[us-east-1-caas-hvm-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=kong-elb-cassandra-hvm&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-cassandra-hvm.template
[us-west-1-caas-hvm-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=us-west-1#/stacks/new?stackName=kong-elb-cassandra-hvm&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-cassandra-hvm.template
[us-west-2-caas-hvm-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?stackName=kong-elb-cassandra-hvm&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-cassandra-hvm.template
[eu-west-1-caas-hvm-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/new?stackName=kong-elb-cassandra-hvm&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-cassandra-hvm.template
[ap-northeast-1-caas-hvm-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=kong-elb-cassandra-hvm&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-cassandra-hvm.template
[ap-southeast-1-caas-hvm-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/new?stackName=kong-elb-cassandra-hvm&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-cassandra-hvm.template
[ap-southeast-2-caas-hvm-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/new?stackName=kong-elb-cassandra-hvm&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-cassandra-hvm.template
[sa-east-1-caas-hvm-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=sa-east-1#/stacks/new?stackName=kong-elb-cassandra-hvm&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-cassandra-hvm.template
[us-east-1-caas-pv-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=kong-elb-cassandra-pv&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-cassandra-pv.template
[us-west-1-caas-pv-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=us-west-1#/stacks/new?stackName=kong-elb-cassandra-pv&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-cassandra-pv.template
[us-west-2-caas-pv-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?stackName=kong-elb-cassandra-pv&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-cassandra-pv.template
[eu-west-1-caas-pv-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/new?stackName=kong-elb-cassandra-pv&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-cassandra-pv.template
[ap-northeast-1-caas-pv-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=kong-elb-cassandra-pv&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-cassandra-pv.template
[ap-southeast-1-caas-pv-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/new?stackName=kong-elb-cassandra-pv&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-cassandra-pv.template
[ap-southeast-2-caas-pv-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/new?stackName=kong-elb-cassandra-pv&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-cassandra-pv.template
[sa-east-1-caas-pv-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=sa-east-1#/stacks/new?stackName=kong-elb-cassandra-pv&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-cassandra-pv.template
[us-east-1-hvm-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=kong-elb-hvm&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-hvm.template
[us-west-1-hvm-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=us-west-1#/stacks/new?stackName=kong-elb-hvm&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-hvm.template
[us-west-2-hvm-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?stackName=kong-elb-hvm&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-hvm.template
[eu-west-1-hvm-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/new?stackName=kong-elb-hvm&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-hvm.template
[ap-northeast-1-hvm-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=kong-elb-hvm&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-hvm.template
[ap-southeast-1-hvm-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/new?stackName=kong-elb-hvm&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-hvm.template
[ap-southeast-2-hvm-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/new?stackName=kong-elb-hvm&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-hvm.template
[sa-east-1-hvm-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=sa-east-1#/stacks/new?stackName=kong-elb-pv&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-hvm.template
[us-east-1-pv-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?stackName=kong-elb-pv&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-pv.template
[us-west-1-pv-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=us-west-1#/stacks/new?stackName=kong-elb-pv&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-pv.template
[us-west-2-pv-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?stackName=kong-elb-pv&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-pv.template
[eu-west-1-pv-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/new?stackName=kong-elb-pv&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-pv.template
[ap-northeast-1-pv-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new?stackName=kong-elb-pv&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-pv.template
[ap-southeast-1-pv-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-1#/stacks/new?stackName=kong-elb-pv&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-pv.template
[ap-southeast-2-pv-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=ap-southeast-2#/stacks/new?stackName=kong-elb-pv&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-pv.template
[sa-east-1-pv-stack-url]: https://console.aws.amazon.com/cloudformation/home?region=sa-east-1#/stacks/new?stackName=kong-elb-pv&templateURL=https:%2F%2Fs3.amazonaws.com%2Fkong-cf-templates%2Fv1.0%2Fkong-elb-pv.template
[kong-stack-badge]: https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png
