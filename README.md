# Miniprojeto_Caryane_T8
Análise Exploratória e Tratamento de Dados de Varejo Supermercadista em Python (SCTI.SC - T8 / M1S07)

# Mini-Projeto de Análise Exploratória de Dados - Varejo Supermercadista

## 1. Objetivo
Este projeto tem como objetivo realizar a auditoria de qualidade, higienização, padronização e Análise Exploratória de Dados (AED) sobre o histórico de transações de uma rede de supermercados. A análise identifica padrões de consumo, categorias dominantes e perfil socioeconômico dos clientes.

## 2. Origem da Base de Dados
* **Fonte**: Base `Varejo.csv` (SCTI.SC / FATEC Rubens Lara).
* **Período**: Transações registradas de 04/01/2019 a 08/12/2022.
* **Volume Bruto**: 830.000 linhas x 14 colunas.

## 3. Unidade da Análise
* **Conceito**: Cada linha da base representa **1 item de produto individual adquirido** em uma determinada compra (nota fiscal `CO_ID`) realizada por um cliente (`CL_ID`).
* **Atenção**: Contar linhas indica volume de itens vendidos, **não** quantidade de clientes, notas fiscais ou faturamento monetário.

## 4. Colunas Utilizadas
* `DATA`: Data em que a compra foi realizada.
* `CO_ID`: Código identificador da compra (Nota Fiscal).
* `CL_ID`: Código identificador do cliente.
* `CL_GENERO`: Sexo biológico informado pelo cliente (M/F).
* `CL_EC` / `CL_EC_DESC`: Estado civil (1: Casado/União Estável, 2: Divorciado, 3: Separado, 4: Solteiro, 5: Viúvo).
* `CL_FHL`: Número de filhos do cliente.
* `CL_SEG`: Segmentação econômica do cliente (Classes A, B e C).
* `PR_ID`: Código do produto (SKU).
* `PR_CAT`: Categoria do produto.
* `PR_NOME`: Nome descritivo do produto.

## 5. Diagnóstico de Qualidade
* **Colunas Residuais**: Removidas 4 colunas nulas (`Unnamed: 10` a `13`) geradas por ponto-e-vírgula excedente ao final do arquivo CSV.
* **Duplicatas Exatas**: Identificadas e registradas 96.553 linhas idênticas (11,63% da base bruta).
* **Inconsistências**: Identificados 3.228 registros do produto SKU 107 com a categoria e nome preenchidos como `#N/D`.

## 6. Decisões de Limpeza e Justificativas
1. **Remoção de Duplicatas Exatas**: 96.553 registros 100% idênticos foram descartados para evitar distorção na contagem de produtos vendidos.
2. **Tratamento de Textos (`#N/D`)**: O código de produto 107 foi padronizado como categoria `"NÃO INFORMADO"`, mantendo os registros para não perder a contagem de itens de compras reais.
3. **Conversão de Tipos**: Campo `DATA` convertido para `datetime` permitindo filtragem temporal.

## 7. Funções Criadas
* `padronizar_texto(valor)`: Recebe valor textual, remove espaços excedentes, trata valores nulos/inválidos e padroniza a caixa do texto.
* `resumo_numerico(serie)`: Recebe uma Series numérica e retorna um dicionário contendo estatísticas (contagem, média, mediana, mínimo, máximo, desvio padrão).

## 8. Principais Conclusões
1. **Volume Consolidado**: Após a limpeza, a base compreende **733.447 itens válidos**, distribuídos em **18.471 compras únicas** efetuadas por **1.000 clientes**.
2. **Dominância de Alimentos**: A categoria `ALIMENTOS` representa **52,38%** de todos os itens vendidos (384.197 unidades), seguida por `HIGIENE` (18,78%) e `LIMPEZA` (17,54%).
3. **Tamanho Médio do Cesto**: Cada compra contém, em média, **39,71 itens** (mediana: 41 itens; mínimo: 1; máximo: 81).
4. **Frequência de Compras**: Cada cliente realizou, em média, **18,47 compras** durante o período analisado.
5. **Concentração por Classe**: A Classe B representa **63,88%** de todo o volume de itens adquiridos (468.505 itens).

## 9. Recomendação
Focar ações promocionais e programas de fidelidade no abastecimento da categoria `ALIMENTOS` para clientes da Classe B, além de criar combos de compras de grande volume (> 50 itens) oferecendo desconto no frete ou caixa rápido exclusivo.

## 10. Limitações da Análise
* **Ausência de Valor Monetário**: A base de dados **não contém preço unitário nem valor total das compras (R$)**. Portanto, análises de "faturamento", "receita" ou "lucratividade" não podem ser calculadas diretamente.

## 11. Como Executar
1. Clone este repositório ou baixe os arquivos.
2. Certifique-se de ter o Python 3.x com `pandas`, `matplotlib` e `seaborn` instalados.
3. Coloque o arquivo `Base Varejo.csv` na mesma pasta do script.
4. Execute o notebook `projeto_varejo_aed.py` do início ao fim para regenerar o arquivo `varejo_limpo.csv`.
