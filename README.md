# Miniprojeto_Caryane_T8
Análise Exploratória e Tratamento de Dados de Varejo  em Python (SCTI.SC - T8 / M1S07)
**Curso**: Análise de Dados com Python — Turma T8 (SCTI.SC)  
**Aluna**: Caryane Ferreira Ribeiro  
**Módulo**: Módulo 1 — Semana 07

# Mini-Projeto Avaliativo de Análise Exploratória de Dados — Varejo

## 1. Objetivo
Este projeto realiza a auditoria de qualidade, higienização, padronização e Análise Exploratória de Dados (AED) sobre o histórico de transações de uma rede de supermercados. O estudo identifica padrões de consumo, categorias dominantes e o perfil socioeconômico dos clientes.

## 2. Origem da Base de Dados
* **Fonte Original**: Base `Base Varejo.csv` (SCTI.SC / FATEC Rubens Lara).
* **Link de Download (Kaggle)**: [Kaggle - Base Varejo (namespaiva)](https://www.kaggle.com/datasets/namespaiva/base-varejo/code)
* **Período Analisado**: Transações registradas de **04/01/2019 a 08/12/2022**
* **Volume Bruto**: 830.000 linhas x 14 colunas.

## 3. Unidade da Análise
* **Definição**: Cada linha da base representa **1 item de produto individual adquirido** em uma determinada compra/nota fiscal (`CO_ID`) realizada por um cliente (`CL_ID`).
* **Nota de Negócio**: Contar linhas indica o volume de itens vendidos, **não** a quantidade de clientes únicos, notas fiscais emitidas ou faturamento monetário.

## 4. Colunas Utilizadas
* `DATA`: Data em que a compra foi realizada.
* `CO_ID`: Código identificador da compra (Nota Fiscal).
* `CL_ID`: Código identificador do cliente.
* `CL_GENERO`: Sexo biológico informado pelo cliente (M/F).
* `CL_EC` / `CL_EC_DESC`: Estado civil (1: Casado/União Estável, 2: Divorciado, 3: Separado, 4: Solteiro, 5: Viúvo).
* `CL_FHL`: Número de filhos do cliente.
* `CL_SEG`: Segmentação económica do cliente (Classes A, B e C).
* `PR_ID`: Código do produto (SKU).
* `PR_CAT`: Categoria do produto.
* `PR_NOME`: Nome descritivo do produto.

## 5. Diagnóstico de Qualidade (Sprint 1)
* **Colunas Residuais**: Identificadas e removidas 4 colunas nulas (`Unnamed: 10` a `13`) geradas por delimitadores sobressalentes ao final das linhas do CSV original.
* **Duplicatas Exatas**: Identificadas e contabilizadas 96.553 linhas 100% idênticas (11,63% da base bruta).
* **Inconsistências Categóricas**: Identificados 3.228 registros do produto SKU 107 com a categoria e nome preenchidos com o texto `#N/D`.

## 6. Decisões de Limpeza e Justificativas (Sprint 2)
1. **Remoção de Duplicatas Exatas**: Os 96.553 registros duplicados foram descartados para evitar contagem duplicada na venda de produtos.
2. **Tratamento do Texto `#N/D`**: As ocorrências do SKU 107 foram padronizadas para `"NÃO INFORMADO"`, preservando o registro das transações sem inventar dados.
3. **Conversão Temporal**: O campo `DATA` foi convertido para o tipo `datetime` em formato brasileiro (`DD/MM/YYYY`).

## 7. Funções Criadas (Sprint 3)
* `padronizar_texto(valor)`: Higieniza textos, remove espaços extras nas extremidades, trata nulos/inválidos e padroniza a caixa.
* `resumo_numerico(serie)`: Recebe uma Series numérica e retorna um dicionário contendo estatísticas completas (contagem válida, média, mediana, mínimo, máximo e desvio padrão).
  
## 8.Análises Realizadas  (Sprint 4)
1. **Perfil do Cesto de Compras (Filtro de Negócio)**: Aplicação da função `resumo_numerico` sobre a quantidade de itens por nota fiscal (`CO_ID`) e filtragem das compras de grande volume (> 50 itens).
2. **Agrupamento por Categoria (`groupby 1`)**: Avaliação do volume de itens vendidos, participação percentual e quantidade de SKUs distintos por categoria (`PR_CAT`).
3. **Agrupamento por Perfil do Consumidor (`groupby 2`)**: Cruzamento entre Classe Económica (`CL_SEG`) e Estado Civil (`CL_EC_DESC`).
4. **Análise Gráfica Exploratória**: Geração de histograma de itens por compra, boxplot de compras por classe econômica, gráfico de barras de categorias e gráfico de dispersão de perfil de clientes.
   
## 9. Conclusões Numéricas (Sprint 5)
1. **Volume Consolidado**: Após a limpeza, a base compreende **733.447 itens válidos**, distribuídos em **18.471 compras únicas** e **1.000 clientes**.
2. **Dominância de Alimentos**: A categoria `ALIMENTOS` concentra **52,38%** de todos os itens vendidos na rede (384.197 unidades).
3. **Tamanho Médio do Cesto**: Cada nota fiscal contém, em média, **39,71 itens** (mediana: 41 itens; mínimo: 1; máximo: 81).
4. **Frequência por Cliente**: Cada cliente realizou, em média, **18,47 compras** no período analisado.
5. **Concentração Socioeconômica**: A Classe B representa **63,88%** do volume total de itens adquiridos (468.505 itens).

## 10. Recomendação de Negócio
Focar ações promocionais e programas de fidelidade na categoria `ALIMENTOS` para clientes da Classe B, além de criar benefícios para compras de grande abastecimento (> 50 itens), como caixas rápidos dedicados.

## 11. Limitação da Análise
* **Ausência de Valores Monetários**: A base de dados **não possui preço unitário nem valor total das transações (R$)**. Desta forma, análises de "faturamento", "receita" ou "lucratividade" não podem ser calculadas.

## 13. Como Executar
1. Baixe o arquivo `Base Varejo.csv` pelo [Link do Kaggle](https://www.kaggle.com/datasets/namespaiva/base-varejo/code).
2. Coloque o arquivo `Base Varejo.csv` no mesmo diretório do notebook no Google Colab.
3. Execute o notebook `Miniprojeto_Caryane_T8.ipynb` do início ao fim para gerar o arquivo `varejo_limpo.csv`.

