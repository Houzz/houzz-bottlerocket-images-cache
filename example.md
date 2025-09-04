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
