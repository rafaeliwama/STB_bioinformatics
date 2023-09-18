## Análise de Expressão Diferencial

Nesta segunda parte, faremos uma análise de expressão gênica diferencial a partir
de um dataset obtido de tecido pulmonar de humanos sem e com crescimento
tumoral (non-small cell lung cancer adenocarcinoma). Esta análise busca identificar
quais são os genes que apresentam expressão diferencial entre os tecidos (neste
caso, normal/não doente e tumoral). O dataset que usaremos contém a contagem
de reads bruta para cada amostra por gene, e também já foi filtrado por parâmetros
de qualidade, cobertura durante o mapeamento, em etapas já vistas nas práticas
anteriores.

```
wget 
```

Visualize o documento tabular por terminal (utilizando cat, head, tail, grep e sed) ou em uma planilha comum. Veja que são apresentadas ~15 mil linhas que representam os genes, e 12 colunas, indicando cada tecido (6 tumorais, iniciadas por t, e 6 normais, iniciadas por n). Este dataset será utilizado na tentativa de identificar genes potencialmente associados ao desenvolvimento de tumores em tecidos pulmonares.

Exemplos de como inspecionar o arquivo:

Quantas colunas o documento possui?
```
head genes_TxN.tsv
```

Quantas linhas o documento possui?
```
wc -l genes_TxN.tsv
```

Este dataset será utilizado na tentativa de identificar genes potencialmente associados ao desenvolvimento de tumores em tecidos pulmonares. Para isso, utilizaremos o site IDEAMEX (Integrative Differential Expression Analysis for Multiple Experiments), o qual fará a análise de expressão gênica diferencial (DESeq2, Love et al. 2014). A abordagem comparativa mais comum para dados de RNASeq é testar a hipótese nula de que o logaritmo de fold change (LFC) entre controle e tratamento é zero, isto é, de que a expressão de determinado gene não é afetada pelo tecido. Ao final, essas análises realizam testes entre pares e atribuem um valor de significância aos valores encontrados, o p-value. Dada as múltiplas comparações, é preciso que os valores de p sejam corrigidos, e a forma como esse ajuste é feito pode variar conforme o software.  

Acesse o site do IDE AMEX (http://www.uusmb.unam.mx/ideamex/). Insira seu e-mail e faça upload do arquivo .tsv obtido acima. Selecione a opção “DESeq2”, como abaixo:
 
 <img width="416" alt="image" src="https://github.com/rafaeliwama/STB_bioinformatics/assets/46658489/63674c04-8409-4664-a514-1069e754c0a3">



Ignore a opção de atribuir batches. E deixe os nomes das amostras como estão.

<img width="343" alt="image" src="https://github.com/rafaeliwama/STB_bioinformatics/assets/46658489/26a53d6f-54af-4888-8514-cd34d2c920c4">


Selecione a comparação entre t (tumoral) e n (normal) na matriz apresentada abaixo. ***O valor de p-value deve ser 0.05 e o  LogFC = 0. Marque também a opção TOP.*** Continue para submeter os dados para análise (deve demorar 5 minutos).  

Faça download dos resultados por meio do **segundo link** fornecido.


**Questão 01.**

a. Com base na tabela TvsN_TOP.txt e no valor de cut-off escolhido (p < 0.05), quantos genes apresentaram índices comparativos     significativos?

b. Visualize o gráfico TvsN_plotPCA. Nele estão representados os resultados da análise de componentes principais (PCA) para o dataset. Brevemente, a PCA plota a dispersão da covariância dos dados em um gráfico bidimensional. Em outras palavras, quanto mais próximos os pontos, mais similares são suas atribuições (neste caso, perfil de expressão gênica) e, logo, quanto mais distantes, maior a diferença. Com base nestas informações e considerando a origem dos dados, levante hipóteses que expliquem a maior dispersão intragrupo das amostras tumorais. Em outras palavras, por que amostras da de tecidos tumorais apresentaram maiores diferenças entre si quando comparadas com o grupo das amostras de tecidos normais? 

c. Faça download dos resultados da mesma análise, porém com valor de significância p-value < 0.001.


Observe o gráfico TvsN_plotMA. Neste gráfico, estão representadas as contagens de cada gene (eixo x) versus o log de fold change (eixo y). O fold change, por sua vez, indica o valor (em escala logarítmica) de expressão de cada gene nas amostras Normal e Tumor (para identificar qual tecido está representado acima e abaixo da linha de corte de logFC, olhe os valores de FC na tabela TvsN.txt). Os pontos em azul indicam os genes que apresentaram diferença significativa nos valores de expressão. Observando os gráficos, há diferenças evidentes entre o número de genes diferencialmente expressos entre os dois tecidos? Qual a importância na escolha do valor de corte tanto no valor FC como de valor de significância?


