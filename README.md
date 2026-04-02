# Day-51-Kubernetes-Manifests-and-Your-First-Pods

## Task
Yesterday you set up a cluster. Today you actually deploy something. You will learn the structure of a Kubernetes manifest file and use it to create Pods — the smallest deployable unit in Kubernetes. By the end of today, you should be able to write a Pod definition from scratch without looking at docs.

## Expected Output
  - At least 3 Pod manifests written by hand
  - A markdown file: day-51-pods.md
  - Screenshot of kubectl get pods showing your running pods

## The Anatomy of a Kubernetes Manifest

Every Kubernetes resource is defined using a YAML manifest with four required top-level fields:

<img width="617" height="256" alt="Image" src="https://github.com/user-attachments/assets/5591ee35-9451-453a-a622-e23f87f9ce8e" />

- apiVersion — tells Kubernetes which API group to use. For Pods, it is v1.
- kind — the resource type. Today it is Pod. Later you will use Deployment, Service, etc.
- metadata — the identity of your resource. name is required. labels are key-value pairs used for organization and selection.
- spec — the desired state. For a Pod, this means which containers to run, which images, which ports, etc.

## Challenge Tasks

## Task 1: Create Your First Pod (Nginx)

Create a file called nginx-pod.yaml

<img width="664" height="261" alt="Image" src="https://github.com/user-attachments/assets/f1b6a152-e618-49be-8033-fa0c0a0b8613" />

Apply it:

kubectl apply -f nginx-pod.yaml

<img width="588" height="36" alt="Image" src="https://github.com/user-attachments/assets/817b0dbf-7afd-4b33-84b1-aad121fb0eec" />

Verify:

kubectl get pods
kubectl get pods -o wide

<img width="977" height="136" alt="Image" src="https://github.com/user-attachments/assets/ce86673f-681f-4599-80d5-5765c8bd87c9" />

kubectl describe pod nginx-pod

<img width="584" height="197" alt="Image" src="https://github.com/user-attachments/assets/4512b65f-fad5-4e52-bc7b-c49b0d0edb52" />

kubectl logs nginx-pod

<img width="966" height="313" alt="Image" src="https://github.com/user-attachments/assets/aa49e5e6-ba61-4dc7-8686-bab435e02a39" />

kubectl exec -it nginx-pod -- /bin/bash
curl localhost:80
exit

<img width="719" height="527" alt="Image" src="https://github.com/user-attachments/assets/6f319920-3903-4314-b4a4-448a6bbd0f62" />

## Task 2: Create a Custom Pod (BusyBox)

Write a new manifest busybox-pod.yaml from scratch (do not copy-paste the nginx one):

<img width="723" height="269" alt="Image" src="https://github.com/user-attachments/assets/c61449a1-9f80-4aaf-b275-adab38a9f78e" />

Apply and verify:

kubectl apply -f busybox-pod.yaml

<img width="868" height="70" alt="Image" src="https://github.com/user-attachments/assets/ced894c5-6a86-4602-b5d3-9989182ce8cc" />

kubectl get pods

<img width="716" height="89" alt="Image" src="https://github.com/user-attachments/assets/756312c0-d3b5-4752-9e09-f90b043645e9" />

kubectl logs busybox-pod

<img width="699" height="41" alt="Image" src="https://github.com/user-attachments/assets/3560e377-b834-4b1d-9981-6e4b1a951252" />

## Task 3: Imperative vs Declarative

You have been using the declarative approach (writing YAML, then kubectl apply). Kubernetes also supports imperative commands:

kubectl run redis-pod --image=redis:latest

<img width="866" height="47" alt="Image" src="https://github.com/user-attachments/assets/e0f7ef6b-0258-4675-9efa-c9d52c65cbd2" />

kubectl get pods

<img width="763" height="117" alt="Image" src="https://github.com/user-attachments/assets/8d1ff29f-b7ba-42f6-b255-216420825cee" />

kubectl get pod redis-pod -o yaml

<img width="882" height="535" alt="Image" src="https://github.com/user-attachments/assets/8184d60e-85df-430c-b3d3-8c0fc4d44a50" />

kubectl run test-pod --image=nginx --dry-run=client -o yaml

<img width="939" height="355" alt="Image" src="https://github.com/user-attachments/assets/4d43bfcb-fb04-4e75-85b9-566f356cc6cd" />

## Task 4: Validate Before Applying

Before applying a manifest, you can validate it:

kubectl apply -f nginx-pod.yaml --dry-run=client

kubectl apply -f nginx-pod.yaml --dry-run=server

<img width="929" height="221" alt="Image" src="https://github.com/user-attachments/assets/082ed27b-076f-4ae0-ba80-f54afe6d4aa7" />

## Task 5: Pod Labels and Filtering

Labels are how Kubernetes organizes and selects resources. You added labels in your manifests — now use them:

kubectl get pods --show-labels

<img width="870" height="123" alt="Image" src="https://github.com/user-attachments/assets/b8e94e74-9823-433c-92b2-24e78a7e857b" />

kubectl get pods -l app=nginx
kubectl get pods -l environment=dev

<img width="775" height="122" alt="Image" src="https://github.com/user-attachments/assets/b9ccbf94-6624-4b1e-9357-82e10d1db8f4" />

kubectl label pod nginx-pod environment=production

<img width="893" height="43" alt="Image" src="https://github.com/user-attachments/assets/d76df07f-a405-449e-98f4-7317fc392a65" />

kubectl get pods --show-labels

<img width="898" height="135" alt="Image" src="https://github.com/user-attachments/assets/796222b5-4c63-4479-bb0f-4e391c24313f" />

kubectl label pod nginx-pod environment-

<img width="752" height="43" alt="Image" src="https://github.com/user-attachments/assets/dc5279a2-8529-46a4-bc55-f5c5e4b2b6de" />

## Task 6: Clean Up

Delete all the pods you created:

# Delete by name
kubectl delete pod nginx-pod
kubectl delete pod busybox-pod
kubectl delete pod redis-pod

# Or delete using the manifest file
kubectl delete -f nginx-pod.yaml

# Verify everything is gone
kubectl get pods








    
   
