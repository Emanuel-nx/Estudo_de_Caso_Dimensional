# Estudo de Caso Dimensional

📌 
Este projeto é um estudo de caso sobre modelagem dimensional utilizando **Apache Spark**. Ele realiza a extração, transformação e carga (ETL) de um dataset armazenado no formato **Parquet**, criando tabelas dimensionais a partir de um conjunto de dados estruturado.

🚀 Tecnologias Utilizadas
- **Python** - Linguagem principal do projeto
- **Apache Spark** - Processamento distribuído de dados
- **PySpark** - API do Apache Spark para Python
- **Google Colab** - Ambiente de execução para rodar o projeto online
- **Parquet** - Formato de armazenamento eficiente para Big Data

✅ Estrutura do Projeto
- **dimensional_dataset.zip**: Arquivo compactado contendo os dados
- **Estudo_de_caso_Projeto_real.ipynb**: Notebook principal com código ETL

🔗 Como Clonar e Executar no Google Colab
1. Clone o repositório:
   ```bash
   git clone https://github.com/Emanuel-nx/Estudo_de_Caso_Dimensional.git
   ```
2. Acesse [Google Colab](https://colab.research.google.com/)
3. Envie o arquivo `Estudo_de_caso_Projeto_real.ipynb` para o Colab
4. Execute as células do notebook

📑 Explicação do Código
### Instalação de Dependências
```python
!pip install pyspark
```
Instala a biblioteca **PySpark** caso ainda não esteja instalada.

### Extração dos Dados
```python
!unzip dimensional_dataset.zip -d dimensional_dataset
```
Descompacta o dataset para uma pasta chamada `dimensional_dataset`.

### Inicialização do Spark
```python
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("dimensional").getOrCreate()
```
Cria uma **SparkSession**, necessária para utilizar as funcionalidades do Apache Spark.

### Leitura do Dataset
```python
df = spark.read.parquet('dimensional_dataset/content/dimensional_dataset')
df.show(5)
```
Carrega os dados do formato **Parquet** e exibe as primeiras linhas.

### Criação da Dimensão `People`
```python
people_cols = ['person_id', 'person_name', 'birth_date', 'email', 'phone_number', 'job']
people_df = df.select(*people_cols).distinct()
people_df.show(5)
```
Seleciona e remove duplicatas das colunas relacionadas a pessoas.

### Criação da Dimensão `Cities`
```python
from pyspark.sql import functions as F
cities_cols = ['city_name', 'zip_code', F.col('country_name').alias('country')]
cities_df = df.select(*cities_cols).distinct()
cities_df.show(5)
```
Seleciona e renomeia colunas para criar a dimensão de cidades.

## Contribuição
Sinta-se à vontade para criar **issues** ou **pull requests** no repositório!

## Autor
[Emanuel-nx](https://github.com/Emanuel-nx)

