# Codeflix

### Scalability

- It will be a horizontal scale, made with k8s.
- The scaling process can be configured at the microservice level;
- All microservices will work statelessly;
- When uploading any type of asset, it will be stored in Cloud Storage;
- The scaling process will not increase the number of K8s PODs;
- The autoscaling process will be through the HPA (Horizontal pod autoscaler);

### Service discovery

- It will not be necessary to use Consul, K8s will do this work;

### Eventual Consistency

- Each microservice will have its own database and communication will be asynchronous;
- eventually the data may become inconsistent;
- The microservice will only duplicate the data necessary for its context;
- We will use Kafka Connect as a data replicator;

### Messaging

- Communication between microservices using RabbitMQ;
- There is no single truth about the choice made;

### Resilience and Self-Healing

- To ensure resilience if one or more microservices go offline, queues are essential;
- If a message is forwarded in the wrong pattern to a microservice, it may be forwarded to a dead letter queue;
- If a container does not have specific traffic, we will have a circuit breaker in action and it will be recreated or restarted;

### Authentication

- Keychain;
- OpenID connection;
- Customization of the theme using react;
- Public key sharing with services for token authentication selection;
- Various types of ACL;
- Authentication flow for frontend and backend;

### Microservices:

- Backend Admin of the Video Catalog;
- Frontend Admin of the Video Catalog;
- Video Encoder;
- Video Catalog Backend API;
- Frontend of the Video Catalog;
- Subscription to Codeflix by the customer;
- Authentication between Microservices with Keycloak;
- Asynchronous communication between Microservices with RabbitMQ;
- Data replication using Apache Kafka and Kafka Connect;

### Development and deployment

- Docker is the protagonist of the development environment;
- For each PR a CI process will be generated using Github Actions;
- The CI process will: Upload the docker application, Run the tests, Use sonarqube;
- In case the merge happens, the CD process takes place;
- Will generate the Docker image;
- Will upload the image to a container registry;
- Will execute the deployment on K8s;

###Kubernetes

- Managed cluster
- Deploy;
- Startup, Readiness and Liveness Probe for self-healing;
- HPA to scale horizontally;

### Cloud providers

- IaC (Infra as code)
-Terraform, Ansible
- AWS, GCP and Azure;
