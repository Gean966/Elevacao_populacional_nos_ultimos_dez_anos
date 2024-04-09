import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Carregar os dados do arquivo CSV
file_path = "Caminho/para/seu/arquivo/elevaçao_populacional_nos_ultimos_dez_anos.csv"
data = pd.read_csv(file_path)

# Função para plotar histograma
def plot_histogram(data, column, color):
    plt.figure(figsize=(10, 6))
    sns.histplot(data[column], color=color, kde=True)
    plt.title(f'Distribuição de {column}')
    plt.xlabel(column)
    plt.ylabel('Frequência')
    plt.show()

# Função para plotar gráfico de dispersão
def plot_scatter(data, x_column, y_column, color):
    plt.figure(figsize=(10, 6))
    plt.scatter(data[x_column], data[y_column], color=color)
    plt.title(f'{y_column} em função de {x_column}')
    plt.xlabel(x_column)
    plt.ylabel(y_column)
    plt.show()

# Análise exploratória dos dados
print("Resumo estatístico dos dados:")
print(data.describe())

# Plotar histograma de vendas
plot_histogram(data, 'Vendas', 'blue')

# Análise de vendas ao longo dos anos
sales_by_year = data.groupby('Ano')['Vendas'].sum()
plt.figure(figsize=(10, 6))
sales_by_year.plot(kind='bar', color='blue')
plt.title('Vendas ao longo dos anos')
plt.xlabel('Ano')
plt.ylabel('Total de vendas')
plt.show()

# Análise de vendas por região
sales_by_region = data.groupby('Região')['Vendas'].sum()
plt.figure(figsize=(10, 6))
sales_by_region.plot(kind='bar', color='red')
plt.title('Vendas por região')
plt.xlabel('Região')
plt.ylabel('Total de vendas')
plt.show()

# Análise de vendas por mês
sales_by_month = data.groupby('Mês')['Vendas'].sum()
plt.figure(figsize=(10, 6))
sales_by_month.plot(kind='bar', color='green')
plt.title('Vendas por mês')
plt.xlabel('Mês')
plt.ylabel('Total de vendas')
plt.show()

# Plotar gráfico de dispersão de vendas em função do ano
plot_scatter(data, 'Ano', 'Vendas', 'purple')

# Análise de correlação entre variáveis
correlation_matrix = data.corr()
plt.figure(figsize=(10, 6))
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm')
plt.title('Matriz de Correlação')
plt.show()

# Outras análises podem ser realizadas aqui

# Salvar as visualizações
plt.savefig('analise_vendas.png')

print("Análise completa concluída.")
