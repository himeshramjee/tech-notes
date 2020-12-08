# Notes on building microservices at production scale - udemy course

## The Stack thus far

1. Visual Studio Code
1. Typescript
1. NodeJS
   1. express
   1. ts-node-dev
   1. typescript
   1. cors
   1. axios
   1. cookie-session
   1. express-validator
   1. express-async-errors
   1. jsonwebtoken
1. ExpressJS
1. ReactJS (react, react-dom, react-scripts)
1. Create-React-App|Scripts
1. Docker
1. Kubernetes
1. Skaffold for local dev
1. Next.JS
1. MongoDB
1. NATS Streaming Server / event bus
1. Redis
1. Tests
   1. jest
   1. ts-jest
   1. supertest
   1. mongodb-memory-server

## Best practices encountered

1. DRY by building central NPM modules to share code
1. Precisely define all events
1. Write everything in Typescript
   1. Makes it easier to deal with message contracts
1. Tests for all the things! Within reason.
   1. Really needs no explanation.
   1. Testing event flows can get really complex. Plan and write automated tests.
1. Run k8s cluster in the cloud and develop on it _almost as quickly_ as local
   1. Ok cloud costs may well block me here so let's see how this plays out.
1. Design and code for addressing concurrency issues

## High level steps for creating a service

1. Create package.json, install dependencies
   - e.g. `npm install @chaiwala/common express express-async-errors cookie-session express-validator jsonwebtoken mongoose typescript @types/cookie-session @types/express @types/jsonwebtoken @types/mongoose`
1. Write Dockerfile, commit to Git
1. Create index.ts to start main process (express app in this case)
1. Build image, push to docker hub/registry
1. Write k8s file for deployment and new service
1. Update skallfold.yml to do file sync between local dev and cluster
1. Write k8s for DB deployment (if the service requires is own persisted data/state)

## Useful commands

1. List k8s service for a given namespace
   - `kubectl get services -n ingress-nginx`
1. Reinstall ingress-nginx ([taken from here](https://kubernetes.github.io/ingress-nginx/deploy/))
   - Docker for Mac `kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.40.1/deploy/static/provider/cloud/deploy.yaml`
1. Generate a k8s stored secret
   - `kubectl create secret generic secrets-box --from-literal="teekeet-jwt-secret=asdf"`
1. Port forwarding from a k8s node
   - `kubectl port-forward nats-streaming-server-depl-7695c795bb-9v29n 4222:4222`
