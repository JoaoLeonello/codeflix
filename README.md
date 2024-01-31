# Codeflix
This project compiles my knowledge in development

### Escalabilidade

- Será uma escala horizontal, feito com k8s.
- O processo de escala poderá ser configurado a nível de microserviço;
- Todos os microserviços trabalharão de forma stateless;
- Quando utilizado upload de qualquer tipo de asset, será armazenado em Cloud Storage;
- O processo de escala será no aumento na quantidade de PODs do K8s;
- O processo de autoscalling será através de HPA (Horizontal pod autoscaler);

### Service Discover

- Não será necessário usar Consul, o K8s fará esse trabalho;

### Consistência Eventual

- Cada microserviço terá seu próprio banco de dados e a comunicação será assíncrona;
- Eventualmente os dados poderão ficar inconsistentes;
- O microsserviço duplicará apenas os dados necessários para o seu contexto;
- Usaremos Kafka Connect como replicador de dados;

### Mensageria

- Comunicação entre microservices usando RabbitMQ;
- Não há uma verdade única sobre a escoha realizada;

### Resiliência e Self healing

- Para garantir a resiliência caso um ou mais microserviços fiquem fora do ar, as filas são essenciais;
- Caso uma mensagem seja encaminhada no padrão errado para algum microserviço, esta pode ser encaminhada para um dead-letter queue;
- Caso um container não aguente determinado tráfego, teremos um circuit breaker em ação e ele será recriado ou reiniciado;

### Autenticação

- Keycloak;
- OpenID Connect;
- Customização do tema usando react;
- Compartilhamento de chave pública com os serviços para a verificação de autenticadade dos tokens;
- Diversos tipos de ACL;
- Flow de autenticação para frontend e backend;

### Microserviços:

- Backend Admin do Catálogo de Vídeos;
- Frontend Admin do Catálogo de Vídeos;
- Encoder de Vídeos;
- Backend API do Catálogo de Vídeos;
- Frontend do Catálogo de Vídeos;
- Assinatura do Codeflix pelo cliente;
- Autenticação entre Microserviços com Keycloak;
- Comunicação assíncrona entre os Microserviços com RabbitMQ;
- Replicação de dados utilizando Apache Kafka e Kafka Connect;

### Desenvolvimento e deploy

- Docker é o protagonista do ambiente de desenvolvimento;
- Para cada PR será gerado um processo de CI usando Github Actions;
- O processo de CI fará: Subir a aplicação docker, Executar os testes, Utilizar o sonarqube;
- No caso de acontecer o merge, o processo de CD acontece;
- Fará a geração da imagem Docker;
- Realizará o upload da imagem em um container registry;
- Executará o deploy no K8s;

### Kubernetes

- Cluster gerenciado
- Deploy;
- Startup, Readiness e Liveness Probe para self healing;
- HPA para escalar horizontalmente;

### Cloud providers

- IaC (Infra as code)
- Terraform, Ansible
- AWS, GCP e Azure;
