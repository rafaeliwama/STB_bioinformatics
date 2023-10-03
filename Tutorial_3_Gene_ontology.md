# Parte III - Enriquecimento de vias metabólicas (Gene Ontology)
### Instrutores: Sónia C. S. Andrade, Rafael E. Iwama, Thainá Cortez.
Na última questão, você obteve gráficos e tabelas contendo informações sobre diferenças de expressão de vários genes. Entretanto, qual o significado biológico disso? Para responder essa questão, convém fazer uma análise de enriquecimento de termos GO (Gene Ontology). 

### O que é *gene ontology*?

*Gene ontology* ou simplesmente GO é um conjunto de termos com definições precisas e relações entre eles bem definidas. Estes termos nos ajudam a entender a função dos genes, através da associação entre um gene e um grupo de termos GO que representam um evento biológico ou uma estrutura. Um exemplo de termo GO é o GO:0015758, glucose transmenbrane transport (https://amigo.geneontology.org/amigo/term/GO:1904659). 

![Screenshot from 2023-09-25 13-44-50](https://github.com/rafaeliwama/STB_bioinformatics/assets/46658489/29b6deb8-f0f3-4267-8b25-0b8516ef3ffe)

Observe na figura que além do ID, há um nome, uma ontologia e uma definição. Neste caso, o termo descreve o processo de transporte de glucose através de um membrana. Desta forma, genes associados a este termo estão, possívelmente, associados a esta função.

Os termos GO estão organizados de forma hierárquica, em três grandes tipos ou domínios:
1. Processos biológicos (BP)
2. Funções moleculares (MF)
3. Componentes celulares (CC)

As relações entre os termos GO podem ser descritas de forma gráfica, como na figura abaixo:
![image](https://github.com/rafaeliwama/STB_bioinformatics/assets/46658489/15882f31-5c3a-4e78-ac04-0597fcf34e18)

Observe que o grau de generalidade dos termos muda, depéndendo do seu nível hierárquico. Termos pertencentes a níveis altos, são mais genéricos, enquanto termos de níveis mais baixos são mais específicos.

## Análise de enriquecimento de termos GO

Esse tipo de análise consiste em comparar a proporção de diferentes termos GO de um subconjunto de dados com uma referência. Isto é, se tivesse sorteado aleatoriamente genes desta referência, seria esperada a quantidade de qual termo GO? Dessa forma, podemos buscar se, no conjunto de genes diferencialmente expressos, existe algum termo GO mais frequente do que seria esperado se esse conjunto de genes viesse ao acaso.
Para fazer essa análise utilizaremos o site Gene Ontology e os resultados do IDEAMAX. Siga os passos abaixo:

Dentre os resultados que você obteve do IDEAMAX, existe um arquivo com a lista completa de genes (nvst.txt) e um com a lista apenas dos genes diferencialmente expressos (nvst_TOP.txt). Destes, separamos apenas a listas de genes total analisada e os genes super expressos para o tecido com com câncer. 

1. Acesse o site do Gene Ontology http://geneontology.org/ 

2. Cole, no espaço ao lado direito da tela, a lista de genes fornecidos no arquivo nvst_TOP.txt, selecione as opções *biological process* e *Homo sapiens*. Clique em Launch. Faça o mesmo para *molecular function*. 


<img width="1361" alt="image" src="https://github.com/rafaeliwama/STB_bioinformatics/assets/46658489/a61d1ec2-5aa4-4972-a2d8-a68cecfcfeb6">

3. Na aba dos resultados, clique em click here to display only significant results.

4. Observe os resultados, avalie a quantidade de vias enriquecidas e quais vias metabólicas estão envolvidas. Observe os resultados para biological process e molecular function. 

***Questão 1.***
**a.** Observe os resultados que são gerados ao selecionar as opções “GO biological process complete” e “GO molecular function complete”. Os termos GO apresentam uma relação hierárquica entre eles, onde o termo "parental" é composto por subontologias ou GOs child, que por sua vez, contém subontologias mais específicas. Se conseguimos identificar ontologias mais específicas, isso indica que temos mais genes enriquecidos nessas ontologias. Comparando os dois resultados ("biological process" e "molecular function"),você poderá notar uma diferença observada na profundidade hierárquica contida nas duas categorias. Por que será que isso ocorre?

Refaça a análise, porém troque a Reference list. Em vez de utilizar o banco de dados (*Homo sapiens*), utilize a lista com todos os genes analisados pelo IDEAMEX (nvst.txt) na aula anterior. **Para isso, ainda na página com os resultados exibidos, selecione, na opção** ***Reference List,*** **a opção “change” e então, selecione o arquivo nvst.txt (como na imagem abaixo)**. Corra a análise novamente clicando em Launch analysis. Isto poderá levar alguns minutos.

<img width="1015" alt="image" src="https://github.com/rafaeliwama/STB_bioinformatics/assets/46658489/d0aa49b9-5163-4caa-ae0c-a41b2057cd43">


Selecione a opção *biological process* e clique em Export > Table. 

Questão 2.
Houve diferença entre fazer essa análise fornecendo a lista reduzida de genes  (background) ou utilizando o banco de dados de *Homo sapiens*? Se sim, qual?

## Parte IV. Visualizando as vias enriquecidas
As plataformas para análise de vias enriquecidas podem fornecer imagens ilustrativas ou tabelas. Como o Gene Ontology utilizado fornece somente tabelas, utilizaremos o REVIGO (http://revigo.irb.hr/) para visualizar esses resultados. 

Com o resultado do Gene Ontology (utilizando a referência reduzida, isto é, os genes do arquivo nvst.txt), **abra a tabela (aqui chamada de analysis.txt) no terminal** e execute os seguintes comandos para extrair somente os termos GO e os valores de FDR:

**Obs: Caso você tenha problemas em gerar o arquivo table_st.txt, você pode utilizar o arquivo *table.txt* presente dentro do diretório do curso.**

1. Extraia o texto entre os dois parênteses, isto é, o código do termo GO, e remova as primeiras linhas de cabeçalho do arquivo:

```
grep -o -P '(?<=\().*(?=\))' analysis.txt |  sed -e '1,4d'  > GOs

```

2. Extraia somente a coluna do FDR e remova as primeiras linhas de cabeçalho do arquivo:

```
cut -f8 analysis.txt | sed -e '1,12d' > FDR

```

3. Junte os arquivos gerados em um único arquivo chamado *table.txt*, separando as colunas por um espaço:

```
paste GOs FDR -d " " > table_st.txt
```

Agora temos a lista de GOs e seus FDRs associados. Cole a lista do arquivo table.txt no REVIGO, selecione as opções *“Medium (0.7)”, “P-value”, “Yes”, “Homo sapiens”* e *“SimRel (default)”*. 

<img width="561" alt="image" src="https://github.com/rafaeliwama/STB_bioinformatics/assets/46658489/4272aa9c-e222-4d8b-b581-a3bd31142229">

**Questão 3.**

Observe os gráficos Scatterplot, Interactive Graph e o TreeMap. Qual você considera mais informativo?

