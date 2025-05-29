# Module 11 - Deployment

### 5.1 Logs Before vs. After Exposure
- **Before**: Startup logs only:
  ```
  Started HTTP server on port 8080
  Started UDP server on port  8081
  ```
- **After**: Each HTTP request is logged:
  ```
  GET /
  GET /
  ```
  Every page reload generates a new `GET /` entry.

### 5.2 The `-n` Option and Namespaces
- `kubectl` without `-n` operates in the **default** namespace (your hello-node resources).
- System components (like Metrics Server, CoreDNS) live in **kube-system**, so you must run:
  ```bash
  kubectl get pods,services -n kube-system
  ```
- **Namespaces** logically partition cluster resources for isolation and organization.


## Reflection on Rolling Update & Kubernetes Manifest File

1. **Difference between RollingUpdate and Recreate strategies**  
   - **RollingUpdate**: Updates Pods incrementally. New Pods are created and become Ready before old Pods are terminated, enabling zero downtime.  
   - **Recreate**: Terminates all existing Pods before creating new ones. This leads to downtime between pod termination and startup of new Pods.

2. **Deploying with Recreate strategy**  
   I modified the Deployment manifest to use the Recreate strategy by adding:
   ```yaml
   strategy:
     type: Recreate
   ```
   After applying this manifest, when I updated the image, all existing Pods were terminated first, and only then the new Pods were created, resulting in a brief downtime for the service.

3. **Manifest for Recreate strategy (`deployment-recreate.yaml`)**  
  - Found within Repository

4. **Benefits of using Kubernetes manifest files**  
   - **Version Control**: Track changes over time and collaborate via Git.  
   - **Reproducibility**: Consistently recreate environments by applying the same manifests.  
   - **Automation**: Integrate with CI/CD pipelines to automatically deploy on commit.  
   - **Clarity**: Declarative configuration makes it clear what resources exist and how they’re configured.  

