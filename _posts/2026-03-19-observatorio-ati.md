---
layout: post
title: "Por que criei o Observatório ATI e como foi o processo"
date: 2026-03-19 10:00:00 -0300
---

A criação do Observatório da Carreira ATI surgiu de uma necessidade prática: **entender, com dados concretos, a realidade da carreira de Analista em Tecnologia da Informação no Executivo Federal**.

Apesar de ser uma carreira estratégica para o Estado, as informações disponíveis estão dispersas, pouco estruturadas e de difícil análise. Perguntas simples — como distribuição por órgãos, ocupação de funções ou evolução da força de trabalho — exigiam esforço manual significativo ou simplesmente não tinham resposta clara.

Foi nesse contexto que nasceu o Observatório: **transformar dados públicos brutos em informação acessível, estruturada e útil para análise**.

## 🎯 Motivação

A principal motivação foi a ausência de transparência prática sobre a carreira. Embora os dados existam no Portal da Transparência, eles não estão organizados de forma que permita análises diretas.

O projeto busca responder perguntas como:

* Onde estão alocados os ATIs?
* Quantos ocupam funções comissionadas?
* Como está distribuída a carreira por nível e classe?
* Existe crescimento ou estagnação do quadro ao longo do tempo?

Além disso, há um objetivo mais amplo: **gerar evidência empírica para discussões sobre políticas públicas de tecnologia no Estado**.

## ⚙️ Arquitetura da Solução

O projeto foi estruturado com foco em desempenho, automação e escalabilidade, dividido em duas camadas principais:

### 1. Pipeline de ETL

O primeiro desafio foi lidar com o volume e a complexidade dos dados brutos.

O pipeline realiza:

* Extração de arquivos `.zip` do Portal da Transparência
* Leitura de datasets massivos (centenas de milhares de linhas)
* Filtragem específica da carreira ATI
* Cruzamento entre vínculos efetivos e funções comissionadas
* Tratamento de dados inconsistentes e nulos
* Geração de um dataset final leve e estruturado

Um ponto crítico foi a **reconstrução das funções comissionadas**, que exigiu lógica específica para interpretar siglas, níveis e descrições presentes nos dados.

Outro detalhe importante foi a identificação automática da data de referência a partir do nome do arquivo, permitindo versionamento temporal dos dados.

### 2. Camada de Visualização

Com os dados tratados, foi construída uma interface interativa utilizando Streamlit.

O dashboard permite:

* Aplicação de filtros dinâmicos (órgão, classe, ano, função)
* Visualização de KPIs em tempo real
* Análise gráfica da distribuição da carreira
* Exploração do histórico de ingressos
* Comparação entre ingressos e desligamentos

Para garantir performance, foi utilizado cache em memória, evitando recarregamento desnecessário dos dados.

## 🚀 Automação e Engenharia

Um dos pontos mais relevantes do projeto foi a automação completa do fluxo.

A solução utiliza:

* Pipeline de ETL desacoplado da visualização
* Versionamento de dados no próprio repositório
* Execução automatizada via GitHub Actions

Sempre que um novo arquivo é adicionado:

1. O ETL é executado automaticamente
2. Os dados são processados e otimizados
3. O arquivo bruto é descartado
4. O dataset final é atualizado

Isso garante que o Observatório esteja sempre atualizado sem necessidade de intervenção manual.

## ⚠️ Desafios Encontrados

Durante o desenvolvimento, alguns desafios técnicos se destacaram:

* **Qualidade dos dados:** presença de valores nulos, inconsistentes e codificações variadas
* **Estrutura não padronizada:** múltiplos vínculos por servidor exigindo agregação inteligente
* **Interpretação de funções:** ausência de padronização clara nas siglas e níveis
* **Performance:** necessidade de separar processamento pesado da camada de visualização

A solução adotada foi centralizar toda a complexidade no ETL, entregando ao dashboard apenas dados já prontos para consumo.

## 📊 Resultado

O resultado é um painel interativo que permite analisar a carreira ATI de forma clara, rápida e baseada em dados.

Mais do que um dashboard, o Observatório se torna uma ferramenta de apoio para:

* Tomada de decisão
* Discussões institucionais
* Estudos sobre governança digital
* Análise da evolução da força de trabalho em TI no governo

## 🔍 Considerações Finais

Este projeto demonstra como dados públicos, quando bem tratados, podem gerar valor real.

A proposta não é apenas visualizar informações, mas **traduzir dados em conhecimento útil**, especialmente em um contexto onde a tecnologia tem papel cada vez mais central na atuação do Estado.

O Observatório ainda pode evoluir com novas fontes de dados, análises preditivas e integração com indicadores mais amplos de transformação digital.

```bash
# Pipeline resumido
python etl_atis.py
streamlit run app.py
```