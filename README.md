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
