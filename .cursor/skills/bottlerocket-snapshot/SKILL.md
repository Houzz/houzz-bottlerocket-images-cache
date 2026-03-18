---
name: bottlerocket-snapshot
description: Build EBS snapshots for Bottlerocket data volumes with pre-pulled container images. Use when building Bottlerocket AMI cache, creating image snapshots, pre-warming container images for EKS nodes, or when the user mentions snapshot.sh, bottlerocket cache, or cached container images.
---

# Bottlerocket Image Snapshot

Build EBS snapshots for Bottlerocket data volumes with cached container images. The script launches an EC2 instance, pulls images, stops the instance, and creates an EBS snapshot.

## Quick Start

```bash
AWS_PROFILE=<profile> ./snapshot.sh -r <region> -a <ami-id> -i <instance-type> <comma-separated-images>
```

## Required

- **Images**: Comma-separated list of container images (no spaces). Last positional argument.
- **AWS_PROFILE**: Set for SSO/credential context (e.g. `my-legacy-sso-stg`, `my-legacy-sso-prod`, `my-legacy-sso-ivy`).

## Key Options

| Option | Short | Default | Description |
|--------|-------|---------|-------------|
| `--region` | `-r` | env/IMDS | AWS region |
| `--ami` | `-a` | SSM bottlerocket 1.27 | AMI ID or SSM path |
| `--instance-type` | `-i` | m5.large | EC2 instance type (use g5.xlarge for GPU, c6a/c7a for CPU) |
| `--subnet-id` | `-sn` | default VPC | Subnet (required for prod) |
| `--arch` | `-A` | amd64 | Architecture (e.g. `arm64` for Graviton) |

## Get Bottlerocket AMI ID

```bash
AWS_PROFILE=<profile> aws ssm get-parameter --name /aws/service/bottlerocket/aws-k8s-1.32/x86_64/latest/image_id \
  --region <region> --output text
```

For ARM64: use `arm64` in the path instead of `x86_64`.

## Common Presets

See [backlogs.md](../../backlogs.md) for presets (stg/prod triton, ivy GHActions, ollama, torchserve, elevation/texture workers, etc.).

**Example – stg triton runtime:**
```bash
AWS_PROFILE=my-legacy-sso-stg ./snapshot.sh -r us-west-2 -a ami-06925b13649acba0a -i g5.xlarge \
  quay.io/prometheus/node-exporter:v1.6.0,nvcr.io/nvidia/k8s-device-plugin:v0.17.1,gcr.io/istio-release/proxyv2:1.17.5,...
```

**Example – prod (subnet required):**
```bash
AWS_PROFILE=my-legacy-sso-prod ./snapshot.sh -r us-west-2 -sn subnet-9ed02ae8 -a ami-06925b13649acba0a -i g5.xlarge \
  <images>
```

**Example – ARM64 (ivy arc):**
```bash
AWS_PROFILE=my-legacy-sso-ivy ./snapshot.sh -A arm64 -r us-west-2 -sn subnet-081eb4ab3886e6f73 -a ami-0a7773157106f8334 -i c8g.xlarge \
  <images>
```

## Workflow

1. Deploy EC2 via CloudFormation
2. Wait for SSM
3. Stop kubelet
4. Clean existing images
5. Pull images (ECR auth handled automatically)
6. Stop instance
7. Create EBS snapshot
8. Delete stack

Output: snapshot ID (e.g. `snap-0ebb1854b9b9982c5`).

## Files

- `snapshot.sh` – main script
- `ebs-snapshot-instance.yaml` – CloudFormation template
- `backlogs.md` – presets and memo
