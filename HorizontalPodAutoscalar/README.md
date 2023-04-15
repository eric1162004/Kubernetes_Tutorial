# Create the HorizontalPodAutoscaler

`kubectl autoscale deployment php-apache --cpu-percent=50 --min=1 --max=10`

# You can use "hpa" or "horizontalpodautoscaler"; either name works OK.
`kubectl get hpa`

# Run this in a separate terminal
# so that the load generation continues and you can carry on with the rest of the steps
`kubectl run -i --tty load-generator --rm --image=busybox:1.28 --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://php-apache; done"`

