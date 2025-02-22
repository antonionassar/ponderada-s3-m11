# Ponderada da Semana 3: Precificação de Arquitetura

## Racional dos Custos dos Serviços AWS

Conforme a arquitetura do projeto, escolhemos os serviços Amazon EC2 e Amazon S3 para garantir a eficiência e escalabilidade do processamento e armazenamento de dados. Abaixo está o racional por trás dos custos associados a cada serviço utilizado, evidenciando como se manteve a fidelidade ao escopo do pipeline, onde há a necessidade de ingestão, processamento e governança de dados em tempo real.

### 1. Amazon EC2

O Amazon EC2 é utilizado para fornecer capacidade computacional escalável na nuvem. No contexto deste projeto, as instâncias EC2 são configuradas para processar grandes volumes de dados, conforme descrito no escopo do projeto no documento TAPI.pdf. Os custos do EC2 são baseados no tipo de instância utilizada, no tempo de execução e na capacidade de armazenamento temporário necessário para o processamento dos dados.

- **Tipo de Instância**:  
  Foi escolhida a instância `t4g.nano`, que é econômica e eficiente para cargas de trabalho consistentes, como servidores de cliquehouse, rabbitmq, streamlit e fastapi.

  - Custo por hora: $0.0042
  - Custo mensal estimado (24/7): ~$3.07

- **Localização**:  
  As instâncias estão localizadas na região US East (N. Virginia), aproveitando o menor custo em hospedar nessa localização.

- **Configuração**:  
  Utiliza instâncias compartilhadas com sistema operacional Linux, otimizando custos e mantendo a flexibilidade necessária para o projeto.

#### Alinhamento com a Arquitetura de Dados

A escolha do Amazon EC2 para hospedar os componentes de processamento atende à necessidade de executar em tempo real o pipeline de dados, processando informações de diferentes pontos de inspeção do processo produtivo da Volkswagen. Isso garante a escalabilidade conforme o volume de dados aumenta ou diminui.

### 2. Amazon S3

O Amazon S3 é utilizado para armazenamento de dados brutos e processados. Ele oferece uma solução escalável e econômica para armazenar grandes volumes de dados, com alta durabilidade e disponibilidade. Os custos são baseados no volume de dados armazenados e nas operações realizadas (como upload e download de dados).

- **Armazenamento**:  
  Utilizamos o S3 Standard para armazenar dados de forma confiável e acessível.

  - Volume de armazenamento: 1 GB por mês
  - Custo por GB: $0.023
  - Custo mensal estimado: $0.023

- **Operações**:

  - PUT, COPY, POST, LIST: 256.000 solicitações por mês
    - Custo por 1.000 solicitações: $0.005
    - Custo mensal estimado: $1.28
  - GET e SELECT: 256.000 solicitações por mês
    - Custo por 1.000 solicitações: $0.0004
    - Custo mensal estimado: $0.1024

- **Segurança e Compliance**:  
  Implementamos políticas de segurança para garantir que os dados armazenados no S3 estejam protegidos e em conformidade com as regulamentações aplicáveis.

#### Alinhamento com a Arquitetura de Dados

O S3 é parte fundamental na arquitetura para armazenamento de dados históricos, possibilitando que novas análises e reprocessamentos sejam feitos de acordo com a evolução do projeto. Dessa forma, atende às demandas de governança e integridade que o pipeline requer.

## Custo Total Estimado

O custo total mensal estimado para a infraestrutura é de aproximadamente **$4.48**, considerando:

- EC2: $3.07
- S3 Armazenamento: $0.023
- S3 Operações: $1.38

### Observações

- Os custos foram calculados utilizando a [Calculadora de Preços da AWS](https://calculator.aws/) de forma a considerar **diferentes instâncias, regiões e cenários de uso**, demonstrando o uso eficiente da ferramenta de precificação.
- Os valores podem variar dependendo do uso real e da região escolhida.
- Não foram incluídos custos de transferência de dados entre serviços.
- Recomenda-se o uso do **AWS Cost Explorer** e, se necessário, de alertas de custo para monitoramento contínuo.
