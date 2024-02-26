# Kuma Deployment on OpenShift
## An alternative approach from: 
- [Uptime Kuma Helm Chart](https://github.com/k3rnelpan1c-dev/uptime-kuma-helm)
  - [Leveraging the same repackaged version of Uptime-Kuma](https://quay.io/repository/k3rnel-pan1c/uptime-kuma?tab=info)

## Directory Structure

The project is structured as follows:

```plaintext
.
├── deployment
│   ├── deployment.yaml    # Deployment configuration for the Kuma application
│   ├── kuma-pvc.yaml      # Persistent Volume Claim for the Kuma application
│   ├── namespace.yaml     # Namespace definition for the Kuma application
│   ├── route.yaml         # Route configuration for external access
│   └── service.yaml       # Service configuration for the Kuma application
└── README.md              # This file
```

## Deployment Instructions

Follow these steps to deploy the Kuma application:

1. **Create a New Project (Namespace)**

   Run the following command to create a new project in OpenShift:

   ```
   oc new-project kuma
   ```

   This command creates a new namespace/project named `kuma`.

2. **Apply the Configuration**

   Navigate to the root of the project directory and apply the configurations in the `deployment` directory:

   ```
   oc apply -f deployment/
   ```

   This command deploys all the necessary components for the Kuma application as defined in the YAML files within the `deployment` directory.

3. **Verify the Deployment**

   After applying the configurations, ensure that all components are correctly deployed and running. You can check the status of the deployment using:

```bash
oc get all -n kuma
NAME                               READY   STATUS    RESTARTS   AGE
pod/uptime-kuma-589dc68974-t5l5n   1/1     Running   0          8m13s

NAME                          TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
service/uptime-kuma-service   ClusterIP   172.30.152.171   <none>        3001/TCP   37m

NAME                          READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/uptime-kuma   1/1     1            1           19m

NAME                                     DESIRED   CURRENT   READY   AGE
replicaset.apps/uptime-kuma-589dc68974   1         1         1       19m

NAME                            HOST/PORT                   PATH   SERVICES              PORT   TERMINATION   WILDCARD
route.route.openshift.io/kuma   kuma.apps.prox.turbra.lab          uptime-kuma-service   3001                 None

```
