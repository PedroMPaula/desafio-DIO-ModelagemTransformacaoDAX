# 📊 Modelagem Star Schema no Power BI – Financial Sample

## 📌 Sobre o Projeto

Este projeto tem como objetivo transformar uma base de dados única (**Financial Sample**) em um modelo dimensional otimizado (**Star Schema**) utilizando o **Power BI**.

A proposta segue boas práticas de modelagem de dados, separando informações em **tabela fato** e **tabelas dimensão**, proporcionando melhor desempenho, organização e escalabilidade para análises.

---

## 🎯 Objetivo

* Aplicar conceitos de **modelagem dimensional**
* Criar um **modelo estrela (Star Schema)**
* Melhorar performance e organização dos dados
* Facilitar análises de vendas, lucro e desempenho

---

## 🧱 Estrutura do Modelo

### 🔵 Tabela Fato

**F_Vendas**

* SK_ID (chave substituta)
* ID_Produto
* Units Sold
* Sales
* Profit
* Discount
* Discount Band
* Segment
* Country
* Date

---

### 🟢 Tabelas Dimensão

**D_Produtos**

* ID_Produto
* Produto
* Média Units Sold
* Média Sales
* Mediana Sales
* Máximo Sales
* Mínimo Sales

---

**D_Produtos_Detalhes**

* ID_Produto
* Discount Band
* Sale Price
* Units Sold
* Manufacturing Price

---

**D_Descontos**

* ID_Produto
* Discount
* Discount Band

---

**D_Detalhes**

* Segment
* Country

---

**D_Calendário**

* Date
* Ano
* Mês
* Mês_Num
* AnoMes

---

## 🔗 Relacionamentos

O modelo segue o padrão:

* F_Vendas (N) → (1) D_Produtos
* F_Vendas (N) → (1) D_Produtos_Detalhes
* F_Vendas (N) → (1) D_Descontos
* F_Vendas (N) → (1) D_Calendário

Direção de filtro: **Single (Dimensão → Fato)**

---

## ⚙️ Etapas de Construção

1. Importação da base Financial Sample
2. Criação da tabela backup (**Financials_origem**)
3. Criação da tabela fato (**F_Vendas**)
4. Criação das tabelas dimensão via referência
5. Tratamento de dados:

   * Ajuste de tipos
   * Remoção de erros
   * Tratamento de valores nulos
6. Agrupamento de dados para métricas
7. Criação da tabela calendário com DAX
8. Definição dos relacionamentos
9. Criação de medidas analíticas

---

## 🧮 Funções e Recursos Utilizados

### 🔹 Power Query

* Referenciar tabelas
* Agrupar dados (Group By)
* Remover duplicatas
* Tratamento de erros
* Alteração de tipos

---

### 🔹 DAX

#### Tabela Calendário

```DAX
D_Calendario = 
ADDCOLUMNS(
    CALENDAR(MIN(F_Vendas[Date]), MAX(F_Vendas[Date])),
    "Ano", YEAR([Date]),
    "Mes", FORMAT([Date], "MMMM"),
    "Mes_Num", MONTH([Date]),
    "AnoMes", FORMAT([Date], "YYYY-MM")
)
```

---

#### Medidas

```DAX
Total Vendas = SUM(F_Vendas[Sales])

Total Lucro = SUM(F_Vendas[Profit])

Total Unidades = SUM(F_Vendas[Units Sold])

Ticket Médio = AVERAGE(F_Vendas[Sales])
```

---

## 📊 Análises Possíveis

* Vendas por produto
* Lucro por país
* Desempenho por segmento
* Evolução de vendas ao longo do tempo
* Impacto de descontos nas vendas

---

## 🖼️ Modelo Estrela (Exemplo)

<img width="1098" height="602" alt="image" src="https://github.com/user-attachments/assets/3d6f690a-c373-4b42-a186-1f8985990e32" />


---

## 📁 Estrutura do Repositório

```
📦 desafio-DIO-ModelagemTransformacaoDAX
 ┣ 📊 Financial Sample.xlsx
 ┣ 📈 ModelagemTransformacaoDAX.pbix
 ┗ 📄 README.md
```

---

## 🚀 Como Executar

1. Abra o **Power BI Desktop**
2. Importe o arquivo `Financial Sample.xlsx`
3. Aplique as transformações conforme descrito
4. Carregue o modelo
5. Explore os dashboards

---

## 🧠 Boas Práticas Aplicadas

* Separação entre fato e dimensão
* Redução de redundância
* Uso de chave substituta
* Modelo otimizado para performance
* Padronização de nomenclaturas

---

## 📌 Conclusão

Este projeto demonstra na prática como transformar uma base simples em um modelo analítico robusto, aplicando conceitos fundamentais de BI e modelagem de dados.

---


