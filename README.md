# Codeflix

### Codeflix, what is it? Features:

- It's a kind of a Netflix;
- It has customer subscription (we will have a specific microservice for this purpose);
- Video catalog for browsing;
- Video playback;
- Full text search in the catalog;
- Processing and encoding of videos (Made in Go);
- Administration of the video catalog;
- Administration of the subscription service;
- Authentication;

### Architectural decisions

- Architecture based on microservices;
- Technology suitable for each context (e.g. Go to process videos);
- Each microservice has its own CI/CD process;

### Scalability

- It will be a horizontal scale, made with k8s.
- The scaling process can be configured at the microservice level;
- All microservices will work stateless;
- When uploading any type of asset, it will be stored in Cloud Storage;
- The scaling process strategy will be increasing the number of K8s PODs;
- The autoscaling process will be through HPA (Horizontal pod autoscaler);

### Service Discover

- It will not be necessary to use Consul, K8s will do this instead;

### Eventual Consistency

- Each microservice will have its own database and communication will be asynchronous;
- Eventually the data may become inconsistent;
- The microservice will only duplicate the data necessary for its context;
- We will use Kafka Connect as a data replicator;

### Messaging

- Communication between microservices using RabbitMQ;
- There is no single truth about the choice made (as it could be Kafka, SNS, etc...);

### Resilience and Self healing

- To ensure resilience if one or more microservices go down, queues are essential;
- If a message is forwarded in the wrong pattern to a microservice, it can be forwarded to a dead-letter queue;
- If a container cannot handle certain traffic, we will have a circuit breaker in action and it will be recreated or restarted;

### Authentication

- Keycloak;
- OpenID Connect;
- Customization of the theme using react;
- Sharing of public key with services to verify the authenticity of tokens;
- Various types of ACL;
- Authentication flow for frontend and backend;

### Microservices:

- Backend Admin of the Video Catalog;
- Frontend Admin of the Video Catalog;
- Video Encoder;
- Video Catalog API backend;
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
- The CD process will: Generate the Docker image, Upload the image to a container registry, Execute the deployment on K8s;

### Kubernetes

- Managed cluster
- Deployment;
- Startup, Readiness and Liveness Probe for self healing;
- HPA to scale horizontally;

### Cloud providers

- IaC (Infra as code)
- Terraform, Ansible
- AWS, GCP and Azure;

### C4 Diagram
![Diagrama PlantUML]([link_para_a_imagem](https://cdn-0.plantuml.com/plantuml/dpng/lLV1RkCs4BtxAwR27XB0IIuzBL1WizwactQtwutJzYYCoOdCMY9LadBg5FsOe8T52_Gh_6CbPSPcHQlo0aLFbiZXcwStCvpnAsDHswOgHry8oSg64ooihStBYmkD3-U5i8jctXZIJ4bBqfupLLtK9Kf_vinONehvnUJBiwbV-lxzkuiAZINjblA9Eu52aZwlFVubvxTKtc5nag5PIvQDuKNfjcTsNH9y1M_GB8Y_SoidfwUZsTiFF-RJgzlPX-_owOVRkzlBcxkJqz782kkiiudYT5-ANrx2LAkVo2htktcoWYdW2YQDDWgkcxA4oPgLb8scv5Ra2V9AI66iHgvqpj1YgGerpYxZTO_WjZPFVWyumMhp5oTbid7sDMcIJ20eyxpwJsi2qw3n2rGeBT1afuTzep52ehHaKky6zhknqtYZzMlS8Qfm37Egm0L6UHCV74-BWh5jD4OidW6Ss-T7uEXFMRnNkiBiUGVYLQXH8rZIW8oCKO1x2HpwQBRsLFBNgf4SzVgaG4iFk1xlGvMTmgyZ081TNfpSwpQf-2uIUIlIEBiE6o-XrQQDQHoH7tOHkILarltEffVmSqDGf14QGvlPGZeKZ6C3pdppfoFYFw53ROviUOZPQxT-536No4M31LLGYfMcE8v9UltND7FkNkTeN93VXAT1lk_Niu_lVEnTi1z98d3aolJLGY3Y2hetY7qAtZXhZGNvX8MLGEVpxTtTT7RnZQlr2BVd_C0NT_0RWqvFv-9kCWtO7GLTI1GdFSwkjW-TWbVR72l5euzRQ-m22pow0DhAg6egpZYQHHgYnX6s-KfuOvT0xMjRda7fYgIDjTrwGRub47Zt8kOQ7uv2TNOndjTuz_4TZjVu24rTAkJ0LG00fkIAj1LSnL4R00lqF21N3x83wVPYhC7Wzq4tzI1moh8dFPtCHbKKqZ-29BRvepfZMk1EWLkSpuLz_n6kHOcmPNKkoUdymc9XN5CBhIuL2VhyJvjvAHYsbrbmVQz4glv1ty6AUCfWI5e8p7eL-3yfn298jLAn4YHNRGZQibEmJGaVySyFob0xsZUYz1vCEj0ROMebnLoqTmM2n1KLkFcq-Lq1WVAzTEq_FBqxuhwUNl5OYtXIcTuSttGILktbmcibf6rz9pmFiameKOd62cO8DLlaCS6euNIPEZ9NyRa3lIRgsRkMDmRc3a55rPoq0OfdgrGgP0lAbtY_H8VUli6t_iqtE3B6juNNMYr9nzu93EaL1HOh8KFUjpWUNXApYRDsDsVRtN7ct4J6spPKwA0h3-1kVUPSYSsdTarJNGeMsIGjDoeQZ6NkZy3H3RRp0V-6UELARc0W28vcGYwX4-Qax0uJ66pi4rK_imXz7S9PfNscqvmUHLD1EyaSxJREcOFQJRMoYgbIXKnAWG-D5VlP-r1LNkvsuxamJExnu6w07xuTKZzvhOmjD9ce1Zd1tfNn7nDiakBh-6bheZ61KYHUz5q7N0y8kFEUNBrBMhDIuTBLKNZgbCeD9sc5eqhHG8Q0ZNNhSGrPjSsFPlEaXJAT_pRH2BWV2Nh-5IRjO6Y2ZT0ZhPnn9DN0wUx1lIv77_DUZZitDC97A3FQImrKnI0fwGJkAFRfgS-xrdh2kS_ftYX4P7uRlN8Kcghy6m00)https://cdn-0.plantuml.com/plantuml/dpng/lLV1RkCs4BtxAwR27XB0IIuzBL1WizwactQtwutJzYYCoOdCMY9LadBg5FsOe8T52_Gh_6CbPSPcHQlo0aLFbiZXcwStCvpnAsDHswOgHry8oSg64ooihStBYmkD3-U5i8jctXZIJ4bBqfupLLtK9Kf_vinONehvnUJBiwbV-lxzkuiAZINjblA9Eu52aZwlFVubvxTKtc5nag5PIvQDuKNfjcTsNH9y1M_GB8Y_SoidfwUZsTiFF-RJgzlPX-_owOVRkzlBcxkJqz782kkiiudYT5-ANrx2LAkVo2htktcoWYdW2YQDDWgkcxA4oPgLb8scv5Ra2V9AI66iHgvqpj1YgGerpYxZTO_WjZPFVWyumMhp5oTbid7sDMcIJ20eyxpwJsi2qw3n2rGeBT1afuTzep52ehHaKky6zhknqtYZzMlS8Qfm37Egm0L6UHCV74-BWh5jD4OidW6Ss-T7uEXFMRnNkiBiUGVYLQXH8rZIW8oCKO1x2HpwQBRsLFBNgf4SzVgaG4iFk1xlGvMTmgyZ081TNfpSwpQf-2uIUIlIEBiE6o-XrQQDQHoH7tOHkILarltEffVmSqDGf14QGvlPGZeKZ6C3pdppfoFYFw53ROviUOZPQxT-536No4M31LLGYfMcE8v9UltND7FkNkTeN93VXAT1lk_Niu_lVEnTi1z98d3aolJLGY3Y2hetY7qAtZXhZGNvX8MLGEVpxTtTT7RnZQlr2BVd_C0NT_0RWqvFv-9kCWtO7GLTI1GdFSwkjW-TWbVR72l5euzRQ-m22pow0DhAg6egpZYQHHgYnX6s-KfuOvT0xMjRda7fYgIDjTrwGRub47Zt8kOQ7uv2TNOndjTuz_4TZjVu24rTAkJ0LG00fkIAj1LSnL4R00lqF21N3x83wVPYhC7Wzq4tzI1moh8dFPtCHbKKqZ-29BRvepfZMk1EWLkSpuLz_n6kHOcmPNKkoUdymc9XN5CBhIuL2VhyJvjvAHYsbrbmVQz4glv1ty6AUCfWI5e8p7eL-3yfn298jLAn4YHNRGZQibEmJGaVySyFob0xsZUYz1vCEj0ROMebnLoqTmM2n1KLkFcq-Lq1WVAzTEq_FBqxuhwUNl5OYtXIcTuSttGILktbmcibf6rz9pmFiameKOd62cO8DLlaCS6euNIPEZ9NyRa3lIRgsRkMDmRc3a55rPoq0OfdgrGgP0lAbtY_H8VUli6t_iqtE3B6juNNMYr9nzu93EaL1HOh8KFUjpWUNXApYRDsDsVRtN7ct4J6spPKwA0h3-1kVUPSYSsdTarJNGeMsIGjDoeQZ6NkZy3H3RRp0V-6UELARc0W28vcGYwX4-Qax0uJ66pi4rK_imXz7S9PfNscqvmUHLD1EyaSxJREcOFQJRMoYgbIXKnAWG-D5VlP-r1LNkvsuxamJExnu6w07xuTKZzvhOmjD9ce1Zd1tfNn7nDiakBh-6bheZ61KYHUz5q7N0y8kFEUNBrBMhDIuTBLKNZgbCeD9sc5eqhHG8Q0ZNNhSGrPjSsFPlEaXJAT_pRH2BWV2Nh-5IRjO6Y2ZT0ZhPnn9DN0wUx1lIv77_DUZZitDC97A3FQImrKnI0fwGJkAFRfgS-xrdh2kS_ftYX4P7uRlN8Kcghy6m00)
