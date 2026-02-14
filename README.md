# 4-jenkins-shared-libraries

cosign generate-key-pair

password: 1234



```bash

docker build -t harishnshetty/cosign-demo:latest .

docker push harishnshetty/cosign-demo:latest

trivy image --ignore-unfixed --format cosign-vuln --output vuln.json harishnshetty/cosign-demo@sha256:a3d368a56d2a70311bf7b3971ca2345dbef6ba0a54251f33a8a7757966ec454f

# Attest

cosign attest --key cosign.key --type vuln --predicate vuln.json harishnshetty/cosign-demo@sha256:a3d368a56d2a70311bf7b3971ca2345dbef6ba0a54251f33a8a7757966ec454f


cosign sign --key cosign.key harishnshetty/cosign-demo@sha256:a3d368a56d2a70311bf7b3971ca2345dbef6ba0a54251f33a8a7757966ec454f

# Verify

cosign verify --key cosign.pub harishnshetty/cosign-demo@sha256:a3d368a56d2a70311bf7b3971ca2345dbef6ba0a54251f33a8a7757966ec454f


# Verify Attestation
cosign verify-attestation --key cosign.pub --type vuln harishnshetty/cosign-demo@sha256:a3d368a56d2a70311bf7b3971ca2345dbef6ba0a54251f33a8a7757966ec454f
```