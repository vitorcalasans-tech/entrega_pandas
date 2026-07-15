Aqui está o relatório do seu trabalho prático com um visual mais limpo, profissional e estruturado para facilitar a leitura.

---

# Relatório Prático: Análise Exploratória de Emendas Parlamentares (2014–2025)

Este documento apresenta a síntese do trabalho prático de **Análise Exploratória de Dados (EDA)** realizado com a biblioteca `pandas` em Python. O objetivo foi investigar a consistência, a estrutura e a qualidade dos dados referentes à execução financeira de emendas parlamentares individuais no Brasil.

---

## 🎯 1. Escopo e Objeto de Estudo

O conjunto de dados analisado engloba os recursos federais direcionados por deputados e senadores a estados e municípios brasileiros no período de **2014 a 2025**. As informações contidas no dataset estruturam-se em quatro pilares fundamentais:

* **Identificação e Autoria:** Nome dos autores das emendas, tipos de emenda e códigos de identificação.


* **Geolocalização:** Estados, municípios e regiões beneficiadas pelos repasses.


* **Classificação Orçamentária:** Áreas públicas de destino (como Saúde, Educação e Turismo), programas de governo e ações específicas.


* **Ciclo Financeiro:** Valores empenhados, liquidados, pagos, cancelados e restos a pagar.



---

## ⚙️ 2. Etapas do Desenvolvimento Técnico

O fluxo de análise exploratória seguiu um roteiro lógico e sistemático de inspeção de dados:

### 📥 Passo 1: Importação e Visualização Inicial

O dataset foi carregado diretamente de uma URL de nuvem utilizando o método `pd.read_csv()`. Com a aplicação de `Df.head(10)`, realizou-se a primeira inspeção visual, identificando que os registros do topo da tabela remontam ao ano de 2014 e correspondem a transferências com finalidades específicas.

### 📏 Passo 2: Verificação de Volume e Dimensão

Por meio do atributo `Df.shape`, constatou-se a robustez da base de dados, composta por:

* **88.596 linhas** (emendas cadastradas).


* **28 colunas** (variáveis/atributos).



### 🔍 Passo 3: Diagnóstico de Tipagem (Data Types)

A execução de `Df.info()` e `Df.dtypes` revelou uma inconsistência crítica para futuras análises matemáticas:

> ⚠️ **Inconsistência Identificada:** As variáveis de valores financeiros (como *Valor Empenhado* e *Valor Pago*) foram carregadas como o tipo genérico `object` (texto/string), e não como dados numéricos (`float64`).
> 
> 
> * **Impacto:** Isso impede a realização direta de operações matemáticas, como soma de repasses, cálculo de médias ou plotagem de gráficos financeiros.
> 
> 
> 
> 

### 🧹 Passo 4: Mapeamento de Valores Ausentes e Ruídos

O teste `Df.isnull().sum()` indicou, inicialmente, a ausência de valores estritamente nulos (`NaN` ou `None`). Contudo, a análise visual revelou que o dataset utiliza o recurso de preencher dados ausentes com strings textuais como `"Sem informação"` ou `"S/I"`, mascarando a ausência real de dados.

### 📅 Passo 5: Análise Temporal de Atualização

Ao ordenar o DataFrame de forma decrescente utilizando a coluna `Ano da Emenda` (`Df.sort_values(by='Ano da Emenda', ascending=False).head(8)`), confirmou-se o amplo espectro temporal coberto pelo arquivo, que se estende de forma consistente **até o ano de 2025**.

### 📊 Passo 6: Estatística Descritiva Inicial

A aplicação de `Df.describe()` confirmou a distribuição dos dados ao longo de 11 anos, situando a média e a mediana das emendas próximas ao ano de 2019. A análise também validou o erro de tipagem mapeado no Passo 3, uma vez que as colunas financeiras não foram contempladas no relatório estatístico descritivo automatizado.

### 🔚 Passo 7: Inspeção de Encerramento (Tail)

Com o comando `Df.tail(5)`, analisou-se o fim do arquivo. Concluiu-se que o dataset se encontra estruturalmente completo e sem quebras físicas de linha, embora registros mais antigos (próximos a 2014) apresentem maior incidência de dados não preenchidos (mascarados sob o rótulo `"Sem informação"`).

---

## 💡 Próximos Passos Recomendados para o Projeto

Com base nos diagnósticos da EDA, o trabalho exige as seguintes etapas de **limpeza e preparação de dados (Data Wrangling)** para viabilizar análises avançadas:

1. **Conversão de Tipos:** Tratar as strings financeiras (removendo caracteres como `R$`, pontos e espaços) e convertê-las para o tipo `float`.


2. **Tratamento de Strings Vazias:** Substituir as marcações `"Sem informação"` e `"S/I"` por valores nulos reais (`NaN`) para garantir a precisão de cálculos estatísticos futuros.
