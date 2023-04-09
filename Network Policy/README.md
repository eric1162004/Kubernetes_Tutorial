## Network Policy Visualization
https://orca.tufin.io/netpol/

https://editor.networkpolicy.io/?id=P9BtsB0477XPOLRy


## Testing Network Policy
- create a pod and apply policy on it
`k run web --image=nginx -l app=web --port=80 --expose`
- test ingress 
`k run test --rm -it --restart=Never --image=alpine -- wget -qO- --timeout=2 [URL]`
- test egress
`k exec -it web -- sh`
