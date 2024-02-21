# ACK service controller for Amazon Elastic Container Service

This repository contains source code for the AWS Controllers for Kubernetes
(ACK) service controller for ECS. Most of the code in this repository is
generated, for any modifications or enhancements please refer to the
[contribution guide][contributing].

## Controller release phase

Current project stage: **RELEASED** \
Current maintenance phase: **PREVIEW**

## Available CRDs

The following CRDs are available for use with the ECS service controller:
- [Cluster](config/crd/bases/ecs.services.k8s.aws_clusters.yaml)
- [Service](config/crd/bases/ecs.services.k8s.aws_services.yaml)
- [TaskDefinition](config/crd/bases/ecs.services.k8s.aws_taskdefinitions.yaml)

## Quick install

EFS service controller can be installed in your cluster using the following command:

```shell
export SERVICE=efs
export RELEASE_VERSION=$(curl -sL https://api.github.com/repos/aws-controllers-k8s/${SERVICE}-controller/releases/latest | jq -r '.tag_name | ltrimstr("v")')
export AWS_REGION=us-west-2
export ACK_SYSTEM_NAMESPACE=ack-system

aws ecr-public get-login-password --region us-east-1 | helm registry login --username AWS --password-stdin public.ecr.aws

helm install ack-$SERVICE-controller \
  --create-namespace -n $ACK_SYSTEM_NAMESPACE ack-$SERVICE-controller \
  oci://public.ecr.aws/aws-controllers-k8s/$SERVICE-chart \
  --version=$RELEASE_VERSION --set=aws.region=$AWS_REGION
```

## Contributing

We welcome community contributions and pull requests.

See our [contribution guide](/CONTRIBUTING.md) for more information on how to
report issues, set up a development environment, and submit code.

We adhere to the [Amazon Open Source Code of Conduct][coc].

You can also learn more about our [Governance](/GOVERNANCE.md) structure.

[coc]: https://aws.github.io/code-of-conduct

## License

This project is [licensed](/LICENSE) under the Apache-2.0 License.

[contributing]: https://aws-controllers-k8s.github.io/community/docs/contributor-docs/overview/