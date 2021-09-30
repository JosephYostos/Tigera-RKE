# Module 5: Securing RKE hosts

**Goal:** Secure RKE hosts ports with network policies.

Calico network policies not only can secure pod to pod communications but also can be applied to RKE hosts to protect host based services and ports. For more details refer to [Protect Kubernetes nodes](https://docs.tigera.io/security/kubernetes-nodes) documentaiton.

## Steps

1. Open a port of NodePort service for public access on RKE node.

    For the demo purpose we are going to expose the `default/frontend` service via the `NodePort` service type to open it for the public access.

    ```bash
    # expose the frontend service via the NodePort service type
    kubectl expose deployment frontend --type=NodePort --name=frontend-nodeport --overrides='{"apiVersion":"v1","spec":{"ports":[{"nodePort":30080,"port":80,"targetPort":8080}]}}'

    # test connection 
    nc -zv Node_IP 30080
    ```

    >It can take a moment for the node port to become accessible.

    If the SSH port was configured correctly, the `nc` command should show you that the port is open.

2. Enable `HostEndpoint` auto-creation for RKE cluster.

    When working with managed Kubernetes services, such as RKE, we recommend using `HostEndpoint` (HEP) auto-creation feature which allows you to automate the management of `HostEndpoint` resources for managed Kubernetes clusters whenever the cluster is scaled.

    >Before you enable HEP auto-creation feature, make sure there are no `HostEndpoint` resources manually defined for your cluster: `kubectl get hostendpoints`.

    ```bash
    # check whether auto-creation for HEPs is enabled. Default: Disabled
    kubectl get kubecontrollersconfiguration.p default -ojsonpath='{.status.runningConfig.controllers.node.hostEndpoint.autoCreate}'

    # enable HEP auto-creation
    kubectl patch kubecontrollersconfiguration.p default -p '{"spec": {"controllers": {"node": {"hostEndpoint": {"autoCreate": "Enabled"}}}}}'
    # verify that each node got a HostEndpoint resource created
    kubectl get hostendpoints
    ```

3. Implement a Calico policy to control access to the service of NodePort type.

    Deploy a policy that deny traffic to port 30080.

    ```bash
    # apply the policy
    kubectl apply -f demo/30-secure-hep/frontend-nodeport-access.yaml 
    
    # test access from Cloud9 shell
    nc -zv RKE_node_IP 30080
    ```

    Once the policy is implemented, you should not be able to access the node port `30080` 
    
    >Note that in order to control access to the NodePort service, you need to enable `preDNAT` and `applyOnForward` policy settings.

[Next -> Module 6](../modules/using-observability-tools.md)
