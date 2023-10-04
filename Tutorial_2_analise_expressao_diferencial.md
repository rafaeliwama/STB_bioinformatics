# Parte II - Análise de Expressão Diferencial
### Instrutores: Sónia C. S. Andrade, Rafael E. Iwama, Thainá Cortez.

Nesta segunda parte, faremos uma análise de expressão gênica diferencial a partir
de um dataset obtido de tecido pulmonar de humanos sem e com crescimento
tumoral (non-small cell lung cancer adenocarcinoma). Esta análise busca identificar
quais são os genes que apresentam expressão diferencial entre os tecidos (neste
caso, normal/não doente e tumoral). O dataset que usaremos é proveniente de uma bibliteca de RNA-seq, que passou por processos de filtragem de qualidade, e mapeamento. Desta forma, ele contém a contagem *reads* brutos gerados pelo sequenciador para cada amostra por gene. Vamos tentar entender melhor os nossos dados:

Certifique-se que vc está no diretório STB_bioinformatics:

```
pwd STB_bioinformatics
```

Inspecione o conteúdo do diretório.
```
ls -lh
```

Note a presença de um documento tabular com formato ".tsv", chamado "genes_TxN.tsv".

Visualize o documento tabular por terminal (utilizando cat, head, tail, grep e sed) ou em uma planilha comum. Veja que são apresentadas ~15 mil linhas que representam os genes, e 12 colunas, indicando cada tecido (6 tumorais, iniciadas por t, e 6 normais, iniciadas por n). Este dataset será utilizado na tentativa de identificar genes potencialmente associados ao desenvolvimento de tumores em tecidos pulmonares.

Exemplos de como inspecionar o arquivo:

Quantas colunas o documento possui?

```
head genes_TxN.tsv
```

Observe a figura abaixo:
![Screenshot from 2023-09-25 12-12-43](https://github.com/rafaeliwama/STB_bioinformatics/assets/46658489/5b81e8e4-4d89-4037-8184-5745a5b41ec4)

Note que para cada gene, há uma contagem de *reads* para cada amostra/transcriptoma (t_1, t_2, n_1, n_2 e etc.). Esta é a contagem de reads que mapeiam para cada gene.

As contagens são diferentes para cada amostra, e nosso trabalho é tentar entender se as diferenças, para cada gene, entre tecidos (tumorais e normais) observadas nas contagens é estatisticamente significativo.

Quantas linhas o documento possui?
```
wc -l genes_TxN.tsv
```

Este dataset será utilizado na tentativa de identificar genes potencialmente associados ao desenvolvimento de tumores em tecidos pulmonares. Para isso, utilizaremos o site IDEAMEX (Integrative Differential Expression Analysis for Multiple Experiments), o qual fará a análise de expressão gênica diferencial (DESeq2, Love et al. 2014). A abordagem comparativa mais comum para dados de RNASeq é testar a hipótese nula de que o logaritmo de fold change (LFC) entre controle e tratamento é zero, isto é, de que a expressão de determinado gene não é afetada pelo tecido. Ao final, essas análises realizam testes entre pares e atribuem um valor de significância aos valores encontrados, o p-value. Dada as múltiplas comparações, é preciso que os valores de p sejam corrigidos, e a forma como esse ajuste é feito pode variar conforme o software.  

Acesse o site do IDE AMEX (http://www.uusmb.unam.mx/ideamex/). Insira seu e-mail e faça upload do arquivo .tsv obtido acima. Selecione a opção “DESeq2”, como abaixo:
 
 <img width="416" alt="image" src="https://github.com/rafaeliwama/STB_bioinformatics/assets/46658489/63674c04-8409-4664-a514-1069e754c0a3">



Ignore a opção de atribuir batches. E deixe os nomes das amostras como estão.

<img width="343" alt="image" src="https://github.com/rafaeliwama/STB_bioinformatics/assets/46658489/26a53d6f-54af-4888-8514-cd34d2c920c4">


Selecione a comparação entre t (tumoral) e n (normal) na matriz apresentada abaixo.

<img width="682" alt="Screen Shot 2023-10-03 at 11 02 35 PM" src="https://github.com/rafaeliwama/STB_bioinformatics/assets/46658489/45aaf632-a2dc-45e3-8f87-719507b0293f">

***O valor de p-value deve ser 0.05 e o  LogFC = 0. Marque também a opção TOP.*** Continue para submeter os dados para análise (deve demorar 5 minutos).  

Faça download dos resultados por meio do **segundo link** fornecido.

Você pode extrair os arquivos compactados com o comando abaixo:

```
tar xvfz DiffExpAllResults.tar.gz
```


**Questão 01.**

a. Com base na tabela TvsN_TOP.txt e no valor de cut-off escolhido (p < 0.05), quantos genes apresentaram índices comparativos     significativos?

b. Visualize o gráfico TvsN_plotPCA. Nele estão representados os resultados da análise de componentes principais (PCA) para o dataset. Brevemente, a PCA plota a dispersão da covariância dos dados em um gráfico bidimensional. Em outras palavras, quanto mais próximos os pontos, mais similares são suas atribuições (neste caso, perfil de expressão gênica) e, logo, quanto mais distantes, maior a diferença. Com base nestas informações e considerando a origem dos dados, levante hipóteses que expliquem a maior dispersão intragrupo das amostras tumorais. Em outras palavras, por que amostras da de tecidos tumorais apresentaram maiores diferenças entre si quando comparadas com o grupo das amostras de tecidos normais? 


