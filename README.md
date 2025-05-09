# WordPress Helm Package


# Pre-requisite (Connect to EKS Cluster)
aws eks update-kubeconfig --name shared-eks-cluster --region us-east-1
aws eks update-kubeconfig --name weishen_ce09-eks-cluster --region us-east-1

# Use to validate chart during the development
helm lint ./wordpress-chart

# Use this directly for customize Helm Chart
helm install wp-release ./wordpress-chart -n ws-wp-activity
helm upgrade --install wp-release ./wordpress-chart -n ws-wp-activity

# Create Helm Chart
helm create wordpress-chart

# Create namespace
kubectl create namespace <your-name>-wp-activity
kubectl create namespace ws-wp-activity

# Deploy the Helm Chart
helm install wp-release . -n <your-name>-wp-activity
helm install wp-release . -n ws-wp-activity

# Deploy the Helm Chart
helm upgrade wp-release . -n ws-wp-activity


Verify:
kubectl get all -n <your-name>-wp-activity
kubectl get all -n ws-wp-activity

# Get the external load balancer
kubectl get svc wordpress -n <your-name>-wp-activity
kubectl get svc wordpress -n ws-wp-activity

Example output:   
NAME        TYPE           CLUSTER-IP     EXTERNAL-IP        PORT(S)        AGE
wordpress   LoadBalancer   10.0.120.7     a1b2c3d4.elb.amazonaws.com   80:30968/TCP   2m
   
Take the EXTERNAL-IP or domain (e.g., a1b2c3d4.elb.amazonaws.com) and open it in your browser:   
http://a1b2c3d4.elb.amazonaws.com


# Mics:
kubectl describe pod wordpress-7595f479b-fv8m4 -n ws-wp-activity
helm uninstall wp-release -n ws-wp-activity
helm list -n ws-wp-activity -q | xargs -n1 -I{} helm uninstall {} -n ws-wp-activity

Results:
1. ![alt text](image.png)  
      
2. ![alt text](image-1.png)   
   
3. ![alt text](image-2.png)   
   
4. Service:   
![alt text](image-3.png)  
   
5. Browser:   
![alt text](image-4.png)       

6. Login:
![alt text](image-5.png)   

# After update with mysql secret varaible then
 helm upgrade --install wp-release ./wordpress-chart -n ws-wp-activity


Secret:         
 ![alt text](image-6.png)   
 ![alt text](image-7.png)   
 Disable Decode:   
 ![alt text](image-8.png)   