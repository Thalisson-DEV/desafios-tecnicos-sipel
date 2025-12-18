# Desafio Técnico: Tratamento e Análise de Dados de Segurança (SST)

Seja bem-vindo(a) ao nosso desafio técnico de nivelamento! Este exercício foi pensado para entendermos o seu domínio atual sobre ferramentas de análise de dados, lógica de tratamento de bases e versionamento de projetos.

> **⚠️ Nota Importante:** Este desafio não tem como objetivo "aprovar" ou "reprovar", mas sim mapear seus conhecimentos atuais. Isso nos ajudará a entender até onde podemos cobrar tarefas complexas e como podemos ajudar na sua evolução técnica. Testes como este serão frequentes para acompanharmos o seu crescimento no setor!

---

## 👨‍💻 Cenário
Você recebeu três bases de dados brutas relacionadas a inspeções de segurança e desvios de campo. Atualmente, os dados estão "sujos", com valores faltantes e inconsistências que impedem uma análise real.

**Seu objetivo:** Limpar esses dados, relacioná-los e gerar os indicadores solicitados.

---

## 💾 Bases de Dados
No repositório, você encontrará os arquivos necessários:
1.  **Base Inspeções:** Registro de todas as visitas realizadas.
2.  **Base Desvios:** Registro de irregularidades encontradas nas inspeções.
3.  **Tabela Dimensão (Inspetores):** Tabela auxiliar que relaciona cada Inspetor ao seu respectivo **Setor** e **Base Operacional**.

---

## 📈 Desafio

### 1. Tratamento de Dados (ETL)
Você pode usar a ferramenta que preferir (**Python/Pandas, Power Query/Excel, SQL**, etc.).
* Remover registros duplicados.
* Tratar valores nulos ou vazios (decida se deve excluir ou preencher conforme a lógica).
* Padronizar formatos de data e nomes de inspetores.

### 2. Modelagem (MER)
Para que os dados façam sentido, você deve relacionar as tabelas seguindo a lógica de chaves (IDs). Note que um Desvio sempre pertence a uma Inspeção, e ambos possuem um Inspetor responsável.
```
      [ Dim_Inspetores ]           
      ------------------           
      - ID_Inspetor (PK) <--------------+
      - Nome_Inspetor                   |
      - Setor                           | (Relaciona por ID_Inspetor)
      - Base_Operacional                |
             ^                          |
             |                          v
      [ Fato_Inspeções ] ---------> [ Fato_Desvios ]
      ------------------    (1:N)   ----------------
      - ID_Inspeção (PK) <--------> - ID_Desvio
      - ID_Inspetor (FK)            - ID_Inspeção (FK)
      - Data_Inspeção               - ID_Inspetor (FK)
      - Status                      - Descrição_Desvio
```
### 3. Indicadores Solicitados
Você deve apresentar os seguintes resultados:
* **Total de Inspeções:** (Geral)
* **Média de Inspeções Mensais:** (Média de produtividade dos inspetores por mês)
* **Top 3 Inspetores:** (Quem mais realizou inspeções)
* **Top 3 Inspetores (Desvios):** (Quem mais encontrou desvios em campo)
* **Evolução Mensal Por Período:** Gráfico ou tabela com Total de Inspeções e Desvios por Mês.
* **Evolução Mensal Por Base e Setor:** Gráfico ou tabela com Total de Inspeções e Desvios por Setor e Base Operacional.
* **Cálculo do ICIT (Índice de Conformidade de Inspeção Técnica):**
    * $ICIT = \frac{\text{Total de Desvios (por inspetor/mês)}}{\text{Total de Inspeções (por inspetor/mês)}}$

---

## 🛠️ Guia de Versionamento (Git)
Se este é seu primeiro contato com Git, aqui estão os comandos essenciais para realizar o desafio:
Tudo descrito abaixo deve ser feito pelo terminal ou git bash já instalado na sua maquina, execute os comandos na ordem descrita.

1.  **Crie uma pasta nova no computador**
2.  **Clique com o botão direito dentro da pasta e vá em ```Abrir no terminal```
3.  **Clone o repositório:** ```git clone https://github.com/Thalisson-DEV/desafios-tecnicos-sipel```
4.  **Criar uma versão sua:** ```git checkout -b desafio-seunome```
    * Exemplo ```git checkout -b desafio-thalisson```
6.  **Salve o seu progresso:**
    * git add .
    * git commit -m "Explique o que você fez nesta etapa"
    * Exemplo ```git commit -m "modelei os dados e estes já estão prontos para serem utilizados no power bi"```
7.  **Enviar para o GitHub:** ```git push -u origin desafio-seunome```

---

## 💡 Exemplos para Consulta

### Exemplo em Python (Pandas)
```
import pandas as pd
df = pd.read_csv('inspecoes.csv')
df.drop_duplicates(inplace=True)
df['Data'] = pd.to_datetime(df['Data'])
```

### Exemplo em Power Query (M)
```
= Table.SelectRows(Tabela1, each ([Inspetor] <> null))
```
---

## 📤 Entrega
1.  **README Pessoal:** No seu repositório de entrega, edite o README explicando:
    * Qual ferramenta você usou (Python, Power BI, Excel?).
    * Quais foram os principais problemas que você encontrou nos dados.
    * Como você calculou o ICIT.
2.  **Resultado:** Pode ser um dashboard (PDF/Link), um script .py, um Jupyter Notebook ou uma planilha Excel tratada.

---
**Boa sorte! Use a criatividade e mostre como você organiza seu raciocínio lógico.**
