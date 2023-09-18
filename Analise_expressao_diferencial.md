## Análise de Expressão Diferencial

Nesta segunda parte, faremos uma análise de expressão gênica diferencial a partir
de um dataset obtido de tecido pulmonar de humanos sem e com crescimento
tumoral (non-small cell lung cancer adenocarcinoma). Esta análise busca identificar
quais são os genes que apresentam expressão diferencial entre os tecidos (neste
caso, normal/não doente e tumoral). O dataset que usaremos contém a contagem
de reads bruta para cada amostra por gene, e também já foi filtrado por parâmetros
de qualidade, cobertura durante o mapeamento, em etapas já vistas nas práticas
anteriores.


Faça download do dataset (“genes_TxN1.tsv”) com o comando:

```
curl https://raw.githubusercontent.com/rafaeliwama/STB_bioinformatics/main/genes_TxN.tsv > genes_TxN.tsv
```


Visualize o documento tabular por terminal (utilizando cat, head, tail, grep e sed) ou em uma planilha comum. Veja que são apresentadas ~15 mil linhas que representam os genes, e 12 colunas, indicando cada tecido (6 tumorais, iniciadas por t, e 6 normais, iniciadas por n). Este dataset será utilizado na tentativa de identificar genes potencialmente associados ao desenvolvimento de tumores em tecidos pulmonares.

```
head 
```

Para isso, utilizaremos o site IDEAMEX (Integrative Differential Expression Analysis for Multiple Experiments), o qual fará a análise de expressão gênica diferencial (DESeq2, Love et al. 2014). A abordagem comparativa mais comum para dados de RNASeq é testar a hipótese nula de que o logaritmo de fold change (LFC) entre controle e tratamento é zero, isto é, de que a expressão de determinado gene não é afetada pelo tecido. Ao final, essas análises realizam testes entre pares e atribuem um valor de significância aos valores encontrados, o p-value. Dada as múltiplas comparações, é preciso que os valores de p sejam corrigidos, e a forma como esse ajuste é feito pode variar conforme o software.  

Acesse o site do IDE AMEX. Insira seu e-mail e faça upload do arquivo .csv obtido acima. Selecione a opção “DESeq2”, como abaixo:
