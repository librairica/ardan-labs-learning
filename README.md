# ardan-labs-learning

## My Notes Day 2
- It's important to distinguish the line between devops and developer.
- A cluster defines the compute environment our services live in.
- Compute power in the form of nodes or machines.
- Kelsey Hightower said the whole point of k8s is to hide the machines (there's just compute power you can leverage)
- Docker represents the machine we're running on and the node itself.
- We're going to configure a cluster with one node that has 4 CPU and 6 Gigs of memory.
- Think of a pod as a compute environment where we can configure the service(s) or binary we want to run.
- A pod can have multiple services interacting with each other (e.g. over localhost).
- Pods can be replicated (i.e. a replica set), e.g. to have multiple instances of a service.
- If a pod goes down, k8s will restart it.
- Pods can have sidecars, e.g. a metrics sidecar that consumes metrics from the pod and decides where to send them.
- You can divide and quota the resources in the pod, e.g. assigning CPU at a pod level or service level.
- An App or CLI tool would exist outside the cluster but need access through raw tunnels to access the cluster.
- Telepresence is a tool that keeps the networking in the local dev environment similar to the deployed environment. It gives us a VPN into the cluster.
- "apply" is a request to k8s to asynchronously set our stuff up
- Deployment defines what the pod needs to look like
- Service defines the networking side of things, what's exposed or not, how things are named, etc.
- Disable CGO for testing so you can test things without the OS layer on your machine (where CGO is enabled by default)

Step 1.
Bring the cluster up