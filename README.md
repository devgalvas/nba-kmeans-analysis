# NBA Player Clustering Analysis

Este projeto visa agrupar jogadores da NBA da temporada 2024-2025 com base em suas estatísticas de desempenho, utilizando técnicas de aprendizado de máquina não supervisionado. O objetivo é identificar perfis de jogadores (como "Superstars", "Role Players", "Big Men", "Perimeter Specialists", etc.) de forma automática, sem depender apenas das posições tradicionais.

## 📋 Visão Geral

A análise utiliza um conjunto de dados com estatísticas detalhadas de jogadores e aplica os seguintes métodos:

1.  **Pré-processamento e Engenharia de Recursos:** Limpeza de dados, normalização e criação de novas métricas avançadas (e.g., eficiência de arremesso, impacto defensivo).
2.  **Redução de Dimensionalidade (PCA):** Utilização da Análise de Componentes Principais para visualizar os dados e reduzir a complexidade, mantendo a variância explicativa.
3.  **Clustering com K-Means:** Agrupamento dos jogadores em $K$ grupos distintos. O número ideal de clusters foi determinado usando o *Elbow Method* e o *Silhouette Score*.
4.  **Clustering com DBSCAN:** Aplicação de um algoritmo baseado em densidade para identificar clusters de formato arbitrário e detetar *outliers* (jogadores com estatísticas muito discrepantes da média).

## 📂 Estrutura do Projeto

- `notebook/` — notebooks Jupyter:
  - `1_PCA.ipynb`
  - `2kmeans_clustering_nba.ipynb`
  - `3_DBSCAN.ipynb`
- `data/`
  - `database_24_25.csv` — dados brutos
  - `features/` — arrays numpy usados nos notebooks
  - `processed_data/` — CSVs gerados pelo pipeline
- `images/` — figuras salvas pelos notebooks
- `requirements.txt` — dependências do projeto
- `README.md` — este arquivo


## 📊 Resultados Principais

### Análise de Componentes Principais (PCA)
A análise de PCA revelou que as duas primeiras componentes principais explicam uma parte significativa da variância dos dados:
* **PC1 (Volume Ofensivo):** Fortemente correlacionada com pontos (PTS), tentativas de arremesso (FGA) e minutos jogados (MP). Separa jogadores de alto volume (Superstars) dos jogadores de rotação.
* **PC2 (Estilo de Jogo - Interior vs. Perímetro):** Correlacionada positivamente com rebotes (TRB, ORB, DRB) e bloqueios (BLK), e negativamente com arremessos de 3 pontos (3PA). Distingue "Big Men" de jogadores de perímetro.

### K-Means Clustering
O algoritmo K-Means (com $K=4$, determinado via *Elbow Method*) identificou quatro grupos principais de jogadores:

1.  **Superstars / Alto Volume:** Jogadores de elite com alto uso ofensivo, muitos minutos e contribuição em múltiplas estatísticas (e.g., Giannis Antetokounmpo, Nikola Jokić).
2.  **All-Rounders / Versáteis:** Jogadores sólidos de rotação ou titulares que contribuem de forma equilibrada, mas com menor volume que as estrelas.
3.  **Especialistas em Perímetro:** Focados em arremessos de 3 pontos e criação de jogadas (Armadores/Alas).
4.  **Jogadores de Garrafão (Big Men):** Pivôs e alas-pivôs com foco em rebotes, bloqueios e eficiência no garrafão.


### DBSCAN
O DBSCAN foi utilizado para validar a estrutura dos dados e, principalmente, para identificar **outliers** — jogadores cujas estatísticas são tão únicas que não se encaixam perfeitamente em nenhum grupo padrão (muitas vezes as superestrelas extremas ou jogadores com perfis muito específicos).

## 🛠️ Como Executar

1.  **Clone o repositório:**
    ```bash
    git clone https://github.com/devgalvas/nba-kmeans-analysis.git
    cd nba-kmeans-analysis
    ```

2.  **Instale as dependências:**
    Certifique-se de ter o Python instalado.
    ```bash
    pip install -r requirements.txt
    ```

3.  **Execute os Notebooks:**
    Recomenda-se executar os notebooks na ordem numérica para garantir que os arquivos de dados intermediários sejam gerados corretamente:
    * `1_PCA.ipynb`
    * `2kmeans_clustering_nba.ipynb`
    * `3_DBSCAN.ipynb`

## 📦 Dependências

* numpy
* pandas
* matplotlib
* seaborn
* scikit-learn

## 🤝 Contribuição

Sinta-se à vontade para abrir *issues* ou enviar *pull requests* com melhorias para a análise ou novos métodos de clustering.

## 📄 Licença

Este projeto está sob a licença MIT.