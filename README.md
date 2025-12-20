# MVP-Engenharia-de-Dados
Projeto MVP da sprint Engenharia de Dados da Pós Graduação de Ciência de Dados &amp; Analytics na PUC Rio


## Sumário
- Objetivo do Projeto
- Coleta de Dados
- Modelagem dos Dados
- Catálogo de Dados
- Carga dos Dados
- Análise dos Dados
- Autoavaliação
- Referências
- Documentação Completa

## Objetivo do Projeto

Com base na análise de dados baixados da API do Tesouro Nacional durante o período de 2013 a 2024 dos entes federativos dos Estados brasileiros, responder as seguintes perguntas:

- O investimento público segue um padrão uniforme ao longo do tempo ou apresenta variações?

- A capacidade de investimento dos Estados está associada a uma maior receita ou a uma maior despesa?

- Estados com maiores gastos brutos são os que mais investem em termos percentuais?

- Estados priorizam despesas correntes em detrimento dos investimentos ao longo do tempo?

## Coleta de Dados

A coleta dos dados foi realizada a partir do dataset do SICONFI (Sistema de Informações Contábeis e Fiscais do Setor Público Brasileiro) que é uma plataforma do Tesouro Nacional que recebe, processa e divulga informações contábeis, financeiras e estatísticas de todos os entes federativos. É uma ferramenta essencial para a transparência e o acompanhamento da gestão fiscal do país.

Os dados foram carregados diretamente da API do Tesouro Nacional através de código python. Os principais passos foram:

- Importação de bibliotecas necessárias para baixar os dados no código Python.

- Cria uma tabela relacionando a sigla do Estado com o código do mesmo segundo a classificação do IBGE.

- Definir o intervalo de busca dos dados de 2013 a 2024.

- A URL base da API SICONFI: url_base = "https://apidatalake.tesouro.gov.br/ords/siconfi/tt/dca"

- Os dados são baixados e guardados em um único Dataframe pandas após processos anteriores, para logo em seguida converter para o Spark DataFrame.

- Cria uma tabele BRONZE e salva tudo.

## Modelagem dos Dados

A modelagem dos dados seguiu uma abordagem em camadas inspirada na arquitetura Data Lakehouse, amplamente utilizada em projetos de Engenharia de Dados, permitindo organização, escalabilidade e separação clara de responsabilidades ao longo do pipeline.

- **Camada Bronze:** Armazenamento dos dados brutos extraídos diretamente da API do SICONFI, preservando a estrutura original e garantindo rastreabilidade da fonte.

- **Camada Silver:** Etapa responsável pela limpeza, padronização e transformação dos dados, incluindo:
    * consolidação contábil de receitas, despesas e investimentos;
    * aplicação de regras de negócio;
    * cálculo de métricas intermediárias.

- **Camada Gold:** Camada analítica final do projeto, estruturada em um esquema flat, contendo uma única tabela com todas as métricas consolidadas e deflacionadas. Essa abordagem foi adotada para facilitar o consumo analítico, eliminar a necessidade de junções complexas e otimizar análises exploratórias e visualizações.

A granularidade da camada Gold é definida por **Unidade da Federação (UF)** e **Ano**.

## Catálogo de Dados

Esta seção apresenta o catálogo de dados da tabela analítica final do projeto, descrevendo sua estrutura, origem e significado das informações disponibilizadas.

**Tabela**: `workspace.mvp.gold_dca`

**Descrição:** Tabela analítica contendo métricas fiscais consolidadas e deflacionadas dos estados brasileiros, utilizada como base para todas as análises do projeto.

**Granularidade:**
 * Unidade da Federação (UF)
 * Ano

**Período de abrangência:** 2013 a 2024

**Fontes dos dados:**
 * Tesouro Nacional – SICONFI (Receitas, Despesas e Investimentos)
 * IPEA – IPCA (deflator)

## Carga dos Dados

A carga dos dados foi realizada utilizando o Databricks, com persistência das tabelas no formato Delta Lake, garantindo versionamento, confiabilidade e desempenho nas operações analíticas.

Cada camada do pipeline foi salva como uma tabela independente, respeitando a separação entre dados brutos, transformados e analíticos.

## Análise dos Dados

As análises realizadas tiveram como objetivo responder às perguntas propostas no escopo do projeto, utilizando métricas consolidadas e dados deflacionados, garantindo comparabilidade temporal e consistência econômica.

Os resultados incluem:

- análise temporal dos investimentos públicos;

- relação entre receita, despesa e capacidade de investimento;

- ranking percentual médio de investimento por estado;

- avaliação da priorização de despesas correntes ao longo do tempo.

## Autoavaliação

Durante o desenvolvimento do projeto tiveram vários desafios que foram superados através da persistência em encontrar soluções e aplicação dos conceitos de engenharia de dados.

O projeto atendeu aos objetivos propostos, aplicando conceitos fundamentais de Engenharia de Dados, como ingestão via API, modelagem em camadas, deflação econômica e construção de uma camada analítica estruturada em esquema flat.

Além disso, o uso de ferramentas como Databricks e Delta Lake permitiu a construção de um pipeline robusto, organizado e reprodutível.

## Referências

- Tesouro Nacional – SICONFI

- Instituto de Pesquisa Econômica Aplicada (IPEA) – IPCA

- Documentação oficial do Databricks

## Documentação Completa

A documentação completa do projeto, incluindo notebooks, análises e gráficos, encontra-se neste repositório
