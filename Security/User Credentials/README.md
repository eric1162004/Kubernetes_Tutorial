## Creating Users

- generate private key
`openssl genrsa -out mike.key 2048`

- generate CSR with the private key
`openssl req -new -key mike.key -out mike.csr -subj "/CN=mike/O=dev"`

- decode CSR
`openssl req -in mike.csr -noout -text`

- Convert CSR to base64
`cat mike.csr | base64 | tr -d "\n"`

Apply CSR object
```
cat <<EOF | kubectl apply -f -
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: mike
spec:  
  request: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURSBSRVFVRVNULS0tLS0NCk1JSUNZakNDQVVvQ0FRQXdIVEVOTUFzR0ExVUVBd3dFYldsclpURU1NQW9HQTFVRUNnd0RaR1YyTUlJQklqQU4NCkJna3Foa2lHOXcwQkFRRUZBQU9DQVE4QU1JSUJDZ0tDQVFFQTBmWGtYNCs0Nkh1azAxSVB6ZXV0WkhPd21vU1oNCkw1Z2tLVlptelhTQXoweUEydzNGSGFITzRncHpvYlh6L29tbXhVV21KeEhwY0dFSnlqVzRGYU1pMnh4YjVPdFcNCjJySEt2NkxiallPNlpETGJjTmphQ2pkZG9QalFsS1EySmd4Q1g4amZvNHpQUVdibFlLSEE1ZHhRd0tubXlpb0YNCnRZK3Rub3orN1p0TnY0MmRUNzJhY2UvVHVFQTh3RXN4Q2RIRlpBSVN5aXIwWktoT0ZkeG9HemdhSmhVcFdzYVgNClpxTmdhZG9LMms5Y21YWnlJMmNRU3F1RHc3SnVPbHJDbGFwZWlKV3d6R295amdXSE8rNERNeWh1Z0t1cUV4VW4NCmw4QkRkN0N6MUkzKyt3NUV1NHNmWjJJOERob1Y4SkZySlNGZVdNeDFvRjJIMXhSWUtoNG00ZWNqcXdJREFRQUINCm9BQXdEUVlKS29aSWh2Y05BUUVMQlFBRGdnRUJBQ1JzTmJMV2I4QkRCVGwzTHAzejY2V2FHaE9LQzRhSmNNNzMNCmgzRVU3VUlFZEc5SE8vaUxUTjVQaGF2NDRqYTJzdEovak5STFFDRWdaVXRYRHdSVFJuR1gzdWlmcEtUczJ3VVYNClRWY20xZlNxcjUyWTA3aW50TDdkQXE3VlBsd2R1dHJnVzROOFZybmFXd2VJVXRUTlNGTTlyK3VQeU9WMmpCMG4NCkd2MUczZDBhUFM2N2Z4c01iZWpxZkxCYjZqRTk5bGYrZVcwTEhSd0ZVdldhNnVZQ25BTWtMVUp1QmxFK2k4elANCkQxWlZNOWxCY0trVHhYTlZoeTlvUlhzV2pLWkR0MVJqR3N6d3lJRDRWMlk3b05BRTdJeTN3d2pnbmVrMHVSdDYNClFxTkhZSU1BdTBwc2xYSFl4WGg1Vm10WDRheW9kSVVRR09hVjh6M284azFSbnhad2lFYz0NCi0tLS0tRU5EIENFUlRJRklDQVRFIFJFUVVFU1QtLS0tLQ0K
  signerName: kubernetes.io/kube-apiserver-client
  expirationSeconds: 86400 # one day
  usages:
  - client auth
EOF
```

- get cst
`kubectl get csr`

- approve csr
`kubectl certificate approve mike`

- extract certificate
`kubectl get csr mike -o jsonpath='{.status.certificate}' | base64 -d > mike.crt`

## Update Kubeconfig with the user credentials
- Set credentials
`kubectl config set-credentials mike --client-key=mike.key --client-certificate=mike.crt --embed-certs=true`

- Set context
`kubectl config set-context mike --cluster=minikube --user=mike --namespace=default`

- Switch context
`kubectl config use-context mike`

