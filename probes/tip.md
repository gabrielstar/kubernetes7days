kubectl apply -f https://k8s.io/examples/pods/probe/http-liveness.yaml
kubectl apply -f https://k8s.io/examples/pods/probe/exec-liveness.yaml

kubectl describe pod liveness-http

Events:
  Type     Reason     Age               From               Message
  ----     ------     ----              ----               -------
  Normal   Scheduled  23s                                  Successfully assigned default/liveness-http to minikube
  Normal   Pulled     21s               kubelet, minikube  Successfully pulled image "k8s.gcr.io/liveness" in 1.577671921s
  Normal   Pulling    3s (x2 over 23s)  kubelet, minikube  Pulling image "k8s.gcr.io/liveness"
  Warning  Unhealthy  3s (x3 over 9s)   kubelet, minikube  Liveness probe failed: HTTP probe failed with statuscode: 500
  Normal   Killing    3s                kubelet, minikube  Container liveness failed liveness probe, will be restarted
  Normal   Created    2s (x2 over 21s)  kubelet, minikube  Created container liveness
  Normal   Started    2s (x2 over 21s)  kubelet, minikube  Started container liveness
  Normal   Pulled     2s                kubelet, minikube  Successfully pulled image "k8s.gcr.io/liveness" in 810.699566ms