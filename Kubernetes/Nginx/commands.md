command -1
    
    kubectl describe pod/nginx-pod -n nginx

command -2

    kubectl exec -it nginx-pod -n nginx -- bash
