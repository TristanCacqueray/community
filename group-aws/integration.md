# Integration Testing

There are very few integration tests for EC2. Those that
exist are in test/integration/targets

## Policy

Following the 2.4 release, all modules marked `stableinterface`
MUST have integration tests for new features. Upgrading to boto3
shall be considered a feature request.

Following the 2.5 release, all new modules MUST have integration
tests.

Modules marked `preview` SHOULD have integration tests for new
features.

Bug fixes for modules that currently have integration tests SHOULD
have tests added. Depending upon the urgency of the bug fix, we may
accept bug fixes without tests.

## Expected test criteria

* Resource creation
* Resource creation again
* Resource creation under check mode
* Resource modification
* Resource deletion

# Github PRs
There are some PRs with tests:

| Module               | PR                                                     |
|----------------------|--------------------------------------------------------|
| rds                  | [25646](https://github.com/ansible/ansible/pull/25646) |
| rds_param_group      | [25345](https://github.com/ansible/ansible/pull/25345) |

# State of the codebase (at 2018/06/22)

Existing test suites:

* `aws_api_gateway`
* `aws_caller_facts`
* `aws_config`
* `aws_ec2_inventory`
* `aws_eks`
* `aws_elasticbeanstalk_app`
* `aws_glue_connection`
* `aws_inspector`
* `aws_lambda`
* `aws_s3`
* `aws_ses_identity_policy`
* `aws_ses_identity`
* `aws_ssm_parameters`
* `aws_waf_web_acl`
* `cloudfront_distribution`
* `ec2_ami`
* `ec2_asg`
* `ec2_elb_lb`
* `ec2_group`
* `ec2_instance`
* `ec2_key`
* `ec2_vpc_egress_igw`
* `ec2_vpc_net`
* `ec2_vpc_route_table`
* `ec2_vpc_subnet`
* `ec2_vpc_vgw`
* `ec2_vpc_vpn_facts`
* `ecs_cluster`
* `ecs_ecr`
* `elb_application_lb`
* `elb_classic_lb`
* `elb_network_lb`
* `elb_target`
* `lambda_policy`

Note that the above list is not exhaustive because some targets contain test suites for
other modules (e.g. the `aws_waf_web_acl` test suite also contains tests for `aws_waf_condition`
 and `aws_waf_rule` modules)

List generated with:

```
echo {cloudf,ec2,aws,lambda,elb,ecs}*{/tasks/main.yml,/runme.sh} aws*/tasks/main.yaml  | xargs -n1 wc -l | awk '$1 > 2 {print $2}' | awk -F/ '{printf("* `%s`\n", $1)}' | sort
```

(the `$1 > 2` test avoids two test suites with a two line tasks/main.yml. The `echo | xargs -n1` avoids the `total` printed when `wc`ing multiple files.)
