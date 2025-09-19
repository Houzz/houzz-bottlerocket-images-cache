# example command to build gpu image

```bash
AWS_PROFILE=my-legacy-sso-stg ./snapshot.sh -r us-west-2 -a ami-06925b13649acba0a -i g5.xlarge nvcr.io/nvidia/k8s-device-plugin:v0.14.3,gcr.io/istio-release/proxyv2:1.17.5,477121734600.dkr.ecr.us-west-2.amazonaws.com/tritonserver:23.05-py3-aws-transformers,nvcr.io/nvidia/k8s/dcgm-exporter:3.3.8-3.6.0-ubuntu22.04
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
