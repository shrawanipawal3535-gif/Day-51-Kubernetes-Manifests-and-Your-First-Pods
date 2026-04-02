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
Apply and verify:

kubectl apply -f busybox-pod.yaml
kubectl get pods
kubectl logs busybox-pod











    
   
