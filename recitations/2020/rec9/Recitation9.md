**Goal:** During this recitation, we will explore deploying Mayan EDMS
with Kubernetes and deploy an application using a typical microservice
architecture.

**Task:**

1.  Ensure you have Docker installed.

2.  In the Docker configuration, enable Kubernetes.

3.  Using your Docker Compose configuration you built during Recitation
    2, create a Kubernetes configuration for deploying Mayan-EDMS.

    a.  For this task, you should be creating 4 files:

        i.  *mayan-edms-service.yaml:*\
            This should be a LoadBalancer service that maps the correct
            ports for Mayan EDMS.

        ii. *mayan-edms-deployment.yaml:*\
            This file should provide the deployment information for
            mayan-edms, including how to setup the required environment
            variables, ports, and required image.\
            For this exercise, use the mayanedms/mayanedms:latest image.

        iii. *postgresql-service.yaml:*\
            This should be a LoadBalancer service that maps the correct
            ports for PostgreSQL.

        iv. *postgresql-deployment.yaml:*\
            This file should provide the deployment information for
            postgres, including how to setup the required environment
            variables, ports, and required image.\
            For this exercise, use the postgres:9.6 image.

4.  Try running your configuration with kubectl.

**Examples:**

Here's what a LoadBalancer service could look like:

> apiVersion: v1
>
> kind: Service
>
> metadata:
>
> name:
>
> labels:
>
> app:
>
> spec:
>
> type: LoadBalancer
>
> ports:
>
> \- port:
>
> selector:
>
> app:

Here's what a deployment could look like:

apiVersion: extensions/v1beta1

> kind: Deployment
>
> metadata:
>
> name:
>
> spec:
>
> replicas: 1
>
> template:
>
> metadata:
>
> labels:
>
> app:
>
> spec:
>
> containers:
>
> \- name:
>
> image:
>
> resources:
>
> requests:
>
> cpu: 100m
>
> memory: 100Mi
>
> env:
>
> \- name: SOME\_ENVIRONMENT\_KEY
>
> value: "VALUE"
>
> ports:
>
> \- containerPort:
