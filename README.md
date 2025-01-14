# ardan-labs-learning

## RJ's Favorite Bill Quotes
- "Keep things simple until you can't"
- "Determine the purpose of the logs"
- "Always return concrete types"
- "Prototype driven development, data oriented design"
- "If you don't understand the data you don't understand the problem"
- "Comments are code - treat them as such"
- "We don't make things easy TO DO, we make things easy TO UNDERSTAND"

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
- The go runtime is not kubernetes aware (why it doesn't realize cores limitations) -> use the uber pkg maxprocs
- Make 4 CPUs the main benchmark, then see if it works with less (explains why at ~45:00 in Day 2 Hour 2).
- The garbage collector takes 25% of your CPU.
- A mux (or router) is a piece of code that registers handler functions to a specific URL and matches routes to handlers.
- pprof source code: https://cs.opensource.google/go/go/+/master:src/net/http/pprof/pprof.go
- Don't use the default server mux; it can expose your server publicly.
- Parent go routines shouldn't terminate until child go routines have terminated (orphan go routines).
- A parent go routine can assign ownership to a "foster parent" (probably their parent).
- http://localhost:4000/debug/pprof/
- http://localhost:4000/debug/vars is a metrics endpoint
- A Go routine is an application-level thread.
- Concurrency means out of order execution.
- Helm creates the ambassador namespace.
- Pull telepresence image: `docker pull docker.io/datawire/tel2:2.10.4`


Step 1.
Bring the cluster up

Step 2.
Do configuration

Bill's rules for configuration:
1. Read in configuration in main.go
2. All configuration should have default values for dev environment (except personal key)
3. The service should allow for --help to show how configuration can be overridden