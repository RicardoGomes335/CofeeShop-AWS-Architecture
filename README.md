
# CoffeeShop Serverless Architecture

Este projeto implementa uma arquitetura serverless para uma loja online chamada **CoffeeShop** usando serviços da AWS como Lambda, API Gateway e DynamoDB. Esta arquitetura é econômica, escalável e fácil de gerenciar.

<img src="/assets/img/CofeeShopAWS.png">

## Architecture Overview

1. **User Access**: Os clientes acessam o site ou aplicativo móvel do CoffeeShop.
2. **Amazon Route 53**: Encaminha o tráfego para a API hospedada no Amazon API Gateway.
3. **Amazon API Gateway**: Encaminha solicitações HTTP de entrada para funções do AWS Lambda.
4. **AWS Lambda**: Executa a lógica de negócios para exibição de catálogo de produtos, processamento de pedidos e pagamento.
5. **Amazon S3**: Armazena ativos estáticos (HTML, CSS, imagens de produtos).
6. **Amazon DynamoDB**: Usa um banco de dados NoSQL para armazenar dados de produtos e pedidos.
7. **Amazon RDS (Opcional)**: Para necessidades de banco de dados relacional (por exemplo, transações, contas de usuário).
8. **AWS CloudWatch**: Monitora a integridade do aplicativo, métricas de desempenho e gera alarmes.
9. **Amazon Cognito**: Gerencia a autenticação do usuário.
10. **Amazon CloudFront**: Distribui conteúdo estático globalmente para acesso mais rápido.

## Etapas para implementação

### 1. Configuração de domínio com Route 53
- Crie uma zona hospedada no Route 53 e mapeie seu domínio para o API Gateway.
- Adicione as tags: `Environment: Production` e `Service: Route53`.

### 2. API Gateway
- Configure endpoints RESTful no **Amazon API Gateway**.
- Habilite o cache para reduzir custos.
- Adicione as tags: `Service: APIGateway`, `Environment: Production`.

### 3. Funções Lambda (Lambda Functions)
- Desenvolva funções para adicionar produtos ao carrinho, processar pedidos, etc.
- Adicione as tags: `Function: AddToCart`, `Owner: DevTeam`, `Environment: Production`.

### 4. DynamoDB
- Use o DynamoDB para armazenar catálogos de produtos, pedidos e dados de clientes.
- Adicione as tags: `Service: DynamoDB`, `CostCenter: Orders`, `Environment: Production`.

### 5. S3 para conteúdo estático
- Armazene imagens de produtos e ativos da web no **Amazon S3**.
- Adicione as tags: `Service: S3`, `Type: ProductImages`, `Environment: Production`.

### 6. CloudFront para distribuição global
- Use o **Amazon CloudFront** para distribuir ativos estáticos globalmente.
- Adicione as tags: `Service: CloudFront`, `Environment: Production`.

### 7. Monitoramento com CloudWatch
- Monitore o desempenho do Lambda, as métricas de solicitação de API e o uso do DynamoDB com o **AWS CloudWatch**.
- Defina alarmes para métricas críticas.
- Adicione as tags: `Service: CloudWatch`, `Environment: Production`.

### 8. Autenticação com Cognito
- Integre o **Amazon Cognito** para autenticação de usuários.
- Adicione as tags: `Service: Cognito`, `CostCenter: Auth`, `Environment: Production`.

## Gestão de Custos com Tags
Para rastrear custos de forma eficaz, as seguintes tags são aplicadas a todos os recursos:
- `Environment`: `Production`, `Development`, `Test`.
- `Service`: e.g., `Lambda`, `API Gateway`, `DynamoDB`, `CloudFront`.
- `CostCenter`: e.g., `Orders`, `Products`, `UserAccounts`.
- `Owner`: `DevTeam`, `OpsTeam`.

## Monitoramento
- Configure o **AWS CloudWatch** para rastrear latência, taxas de erro e contagens de solicitações.
- Habilite **CloudWatch Logs** para funções do Lambda para capturar todos os dados de execução.

## Diagrama
Um diagrama para esta arquitetura está disponível no arquivo `diagram.drawio`.

## License
This project is open-sourced under the MIT License.
