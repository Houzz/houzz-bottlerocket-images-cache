

# example command to build gpu image

```bash
AWS_PROFILE=my-legacy-sso-stg ./snapshot.sh -r us-west-2 -a ami-06925b13649acba0a -i g5.xlarge nvcr.io/nvidia/k8s-device-plugin:v0.14.3,gcr.io/istio-release/proxyv2:1.17.5,477121734600.dkr.ecr.us-west-2.amazonaws.com/tritonserver:23.05-py3-aws-transformers,nvcr.io/nvidia/k8s/dcgm-exporter:3.3.8-3.6.0-ubuntu22.04
```

## use this to get ami id

https://docs.aws.amazon.com/eks/latest/userguide/retrieve-ami-id-bottlerocket.html

```bash
AWS_PROFILE=my-legacy-sso-ivy aws ssm get-parameter --name /aws/service/bottlerocket/aws-k8s-1.32/x86_64/latest/image_id \
    --region us-west-2 --output text
```

## memos for what we are building now.

### stg triton runtime

```bash
AWS_PROFILE=my-legacy-sso-stg ./snapshot.sh -r us-west-2 -a ami-06925b13649acba0a -i g5.xlarge quay.io/prometheus/node-exporter:v1.6.0,nvcr.io/nvidia/k8s-device-plugin:v0.14.3,gcr.io/istio-release/proxyv2:1.17.5,nvcr.io/nvidia/k8s/dcgm-exporter:3.3.8-3.6.0-ubuntu22.04,477121734600.dkr.ecr.us-west-2.amazonaws.com/triton@sha256:060f7185d72cae604e39c2d5a33da8403806aa3073f936fc3305a67230ef3233
```

snap-0ebb1854b9b9982c5

```bash
AWS_PROFILE=my-legacy-sso-stg ./snapshot.sh -r us-west-2 -a ami-06925b13649acba0a -i g5.xlarge quay.io/prometheus/node-exporter:v1.6.0,nvcr.io/nvidia/k8s-device-plugin:v0.14.3,gcr.io/istio-release/proxyv2:1.17.5,nvcr.io/nvidia/k8s/dcgm-exporter:3.3.8-3.6.0-ubuntu22.04,477121734600.dkr.ecr.us-west-2.amazonaws.com/triton@sha256:060f7185d72cae604e39c2d5a33da8403806aa3073f936fc3305a67230ef3233,754384638740.dkr.ecr.us-west-2.amazonaws.com/qpext:latest,754384638740.dkr.ecr.us-west-2.amazonaws.com/storage-initializer:v0.11.0
```

snap-043e1389b978fa8a0
somehow triton cannot recognize driver. need some wait time (sleep xxx)

### prod triton runtime

```bash
AWS_PROFILE=my-legacy-sso-prod ./snapshot.sh -r us-west-2 -sn subnet-9ed02ae8 -a ami-06925b13649acba0a -i g5.xlarge 602401143452.dkr.ecr.us-west-2.amazonaws.com/amazon-k8s-cni:v1.19.6-eksbuild.1,602401143452.dkr.ecr.us-west-2.amazonaws.com/amazon/aws-network-policy-agent:v1.2.2-eksbuild.1,602401143452.dkr.ecr.us-west-2.amazonaws.com/eks/aws-ebs-csi-driver:v1.45.0,602401143452.dkr.ecr.us-west-2.amazonaws.com/eks/csi-node-driver-registrar:v2.14.0-eksbuild.3,602401143452.dkr.ecr.us-west-2.amazonaws.com/eks/livenessprobe:v2.16.0-eksbuild.3,public.ecr.aws/eks-distro/kubernetes-csi/node-driver-registrar:v2.8.0-eks-1-27-3,public.ecr.aws/eks-distro/kubernetes-csi/livenessprobe:v2.10.0-eks-1-27-3,602401143452.dkr.ecr.us-west-2.amazonaws.com/eks/kube-proxy:v1.32.5-minimal-eksbuild.2,gcr.io/istio-release/proxyv2:1.17.5,688976015282.dkr.ecr.us-west-2.amazonaws.com/triton@sha256:b41202e88d846e77c11d93e2ae6c80f308f30cc01075563547a2ab3f3cb24476,quay.io/prometheus/node-exporter:v1.6.0,nvcr.io/nvidia/k8s-device-plugin:v0.14.3,nvcr.io/nvidia/k8s-device-plugin:v0.14.3
```

### ivy ghactions runtime



```bash
AWS_PROFILE=my-legacy-sso-ivy ./snapshot.sh -r us-west-2 -sn subnet-081eb4ab3886e6f73 -a ami-05f5efa6134aa9771 -i c6a.xlarge 754384638740.dkr.ecr.us-west-2.amazonaws.com/actions-runner:v1.49,754384638740.dkr.ecr.us-west-2.amazonaws.com/docker:dind,quay.io/prometheus/node-exporter:v1.3.1,registry.k8s.io/dns/k8s-dns-node-cache:1.23.1,754384638740.dkr.ecr.us-west-2.amazonaws.com/promtail:3.0.0

```

`snap-0dae37e1b9f80201f`

### ivy arc runtime - arm64

<!-- ami-0a7773157106f8334 -->

```bash
AWS_PROFILE=my-legacy-sso-ivy ./snapshot.sh -A arm64 -r us-west-2 -sn subnet-081eb4ab3886e6f73 -a ami-0a7773157106f8334 -i c8g.xlarge 754384638740.dkr.ecr.us-west-2.amazonaws.com/actions-runner:v1.49,754384638740.dkr.ecr.us-west-2.amazonaws.com/docker:dind,quay.io/prometheus/node-exporter:v1.3.1,registry.k8s.io/dns/k8s-dns-node-cache:1.23.1,754384638740.dkr.ecr.us-west-2.amazonaws.com/promtail:3.0.0

```

`snap-055843ebf47633c56`

### prod ollama runtime

```bash
AWS_PROFILE=my-legacy-sso-prod ./snapshot.sh -r us-west-2 -sn subnet-9ed02ae8 -a ami-06925b13649acba0a -i g5.xlarge gcr.io/istio-release/proxyv2:1.17.5,docker.io/ollama/ollama:0.12.3,quay.io/prometheus/node-exporter:v1.6.0,nvcr.io/nvidia/k8s-device-plugin:v0.14.3,nvcr.io/nvidia/k8s-device-plugin:v0.14.3
```

`snap-007f44dd23e7db95c`

### prod torch serve runtime

```bash
AWS_PROFILE=my-legacy-sso-prod ./snapshot.sh -r us-west-2 -sn subnet-9ed02ae8 -a ami-06925b13649acba0a -i g5.xlarge gcr.io/istio-release/proxyv2:1.17.5,index.docker.io/pytorch/torchserve-kfs@sha256:3c7e2c25399c4b7edfe5897b0d1b59c714f50c495a74c68efdffc51f2fd3092b,quay.io/prometheus/node-exporter:v1.6.0,nvcr.io/nvidia/k8s-device-plugin:v0.14.3,nvcr.io/nvidia/k8s-device-plugin:v0.14.3
```

`snap-0f3bc9fa8eed688a7`

### stg triton 25-09 py3 runtime

```bash
AWS_PROFILE=my-legacy-sso-stg ./snapshot.sh -r us-west-2 -a ami-06925b13649acba0a -i g5.xlarge quay.io/prometheus/node-exporter:v1.6.0,nvcr.io/nvidia/k8s-device-plugin:v0.17.1,gcr.io/istio-release/proxyv2:1.17.5,nvcr.io/nvidia/k8s/dcgm-exporter:3.3.8-3.6.0-ubuntu22.04,nvcr.io/nvidia/tritonserver:25.09-py3,754384638740.dkr.ecr.us-west-2.amazonaws.com/qpext:latest,754384638740.dkr.ecr.us-west-2.amazonaws.com/storage-initializer:v0.11.0
```

`snap-0dd1440e47ce0c8b3`

### prod triton 25-09 py3 runtime

```bash
AWS_PROFILE=my-legacy-sso-prod ./snapshot.sh -r us-west-2 -sn subnet-9ed02ae8 -a ami-06925b13649acba0a -i g5.xlarge gcr.io/istio-release/proxyv2:1.17.5,nvcr.io/nvidia/tritonserver:25.09-py3,quay.io/prometheus/node-exporter:v1.6.0,nvcr.io/nvidia/k8s-device-plugin:v0.17.1
```

`snap-09104410e26b37baa`
