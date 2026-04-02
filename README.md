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











    
   
