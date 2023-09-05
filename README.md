# full-cycle-poc

This application have different types of pages (Server-Side Rendering, Client-Side Rendering, and Incremental Static Regeneration) in a Next.js application that fetches data from a GraphQL server using Apollo Client:

Also Dockerising all these application and spinup the same using kubernetes minqube

# Applications

- Next js app - (car-listing)
- node application for api - (api-server)
- graphql application for fetching api unging query - (graphql-server)


# Next.js GraphQL Data Fetching Example

This is a sample Next.js application that demonstrates different methods of fetching data from a GraphQL server using Apollo Client. The application includes the following types of pages:


- Server-Side Rendering (SSR) Page
- Client-Side Rendering (CSR) Page
- Incremental Static Regeneration (ISR) Page

# Getting Started to run application locally

1. **Clone the Repository:**

   Clone this repository to your local machine:

   git clone https://github.com/your-username/next-fullcycle-poc.git

2. **Install Dependencies:**

   Navigate to the project directory and install the required dependencies for each application:
    ```bash
    cd next-fullcycle-poc/car-listing
    npm install

    cd next-fullcycle-poc/server/api-server
    npm install

    cd next-fullcycle-poc/server/graphql-server
    npm install
    ```

3. **Set Up Apollo Client Configuration:**

   Open the 'lib/apolloClient.js' file and configure Apollo Client by setting the correct 'uri' option to your GraphQL server URL. Save the changes.

4. **Run the Next.js Application:**

   Start the Next.js development server:

   ```bash
   npm run dev
   ```

   Your application will be accessible at 'http://localhost:8080'.

## Pages

### Server-Side Rendering (SSR) Page

- Route: `/cars/list-ssr`
- Description: This page fetches data from the GraphQL server using Apollo Client during server-side rendering (SSR). Data is fetched on the server and sent as part of the initial HTML response.

### Client-Side Rendering (CSR) Page

- Route: `/cars/list-csr`
- Description: This page fetches data from the GraphQL server using Apollo Client on the client side. Data is fetched after the page loads in the user's browser.

### Incremental Static Regeneration (ISR) Page

- Route: `/cars/list-isr`
- Description: This page uses Incremental Static Regeneration (ISR) to fetch and statically generate data from the GraphQL server using Apollo Client. Data is fetched at build time and revalidated at a specified interval.



# Dockerize and run application through docker container

create docker image push to docker hub

docker image build -t <image_name>:<tag> <path>
docker push <user_name>/<tag>



Now deploy your Dockerized applications (Node.js API server, GraphQL server, and Next.js application) using Minikube:

```markdown
# Deploy and spinup Applications with Minikube

This guide explains how to deploy your Dockerized applications (Node.js API server, GraphQL server, and Next.js application) using Minikube, a tool for running a local Kubernetes cluster. Kubernetes allows you to manage and orchestrate containerized applications.

## Prerequisites

Before getting started, ensure you have the following installed on your machine:

- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)
- Docker (already configured to work with Minikube)

## Step 1: Start Minikube

Start Minikube to create and start a local Kubernetes cluster:

```bash
minikube start
```

## Step 2: Create Kubernetes Deployment and Service Files

For each of your Dockerized components (API server, GraphQL server, and Next.js application), create Kubernetes deployment and service YAML files. Adjust the image names and ports as needed.

Here's an example for the API server (`deployment.yaml`):

```yaml
# Example YAML content for api-server deployment.yaml

# ... (Deployment configuration)

---

# ... (Service configuration)
```

Create similar YAML files for your GraphQL server and Next.js application, replacing `api` with appropriate labels and image names.

## Step 3: Apply Kubernetes Configurations

Apply the Kubernetes configurations to your Minikube cluster using `kubectl`:

```bash
cd next-fullcycle-poc/server/api-server
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

cd next-fullcycle-poc/server/graphql-server
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

cd next-fullcycle-poc/server/car-listing
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

## Step 4: Expose Services (if needed)

Depending on your setup, you may need to expose services to access them outside the cluster. For example, to expose your Next.js application as a NodePort service:


kubectl expose deployment nextjs-deployment --type=NodePort --name=nextjs-service
```

## Step 5: Access Your Applications

Use `minikube service` to get the URL of a service and access your applications. For example:

cd next-fullcycle-poc/server/api-server
minikube service service


This will open a browser window or display the URL in your terminal, allowing you to access your Next.js application.

Repeat the process for your other services as needed.

## Customization

- Customize the Kubernetes configurations (YAML files) to match your specific setup, including image names, ports, and service types.

## Cleanup

When you're finished testing your applications, you can stop and delete the Minikube cluster:

```bash
minikube stop
minikube delete
```

## Dependencies

- Next.js
- Apollo Client
- GraphQL
- docker
- Minikube
- kubectl

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
```

Customize this README file to include specific details about your applications, image names, and ports. Users can follow these steps to deploy your Dockerized applications using Minikube.