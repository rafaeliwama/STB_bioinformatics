# Parte I - Introdução ao terminal
### Instrutores: Sónia C. S. Andrade, Rafael E. Iwama, Thainá Cortez.
## Se localizando no terminal

Ao entrar no terminal, você verá algo similar a isto:

```
usuario@DESKTOP-00RFJVC:~$ 
```

Em verde está indicado o nome do seu computador ou servidor. Em vermelho, o caminho (ou
endereço) no qual você se encontra. O símbolo “~” representa o caminho para seu diretório de
usuário (também reconhecido por /home). Para checar o diretório atual o qual você se encontra,
use o comando pwd.

```
usuario@DESKTOP-00RFJVC:~$ pwd
/home/user
```

Para checar os diretórios e arquivos contidos no diretório em que você se encontra, use o
comando ls (list). 

```
usuario@DESKTOP-00RFJVC:~$ ls
```

Visualize informações adicionais utilizando os argumentos -l (retorna os resultados em lista), -s
(tamanho dos arquivos), -h (tamanhos em formato mais compreensíveis) e -a (mostra arquivos
ocultos, isto é, cujo nome começa com “.”).

Dentro da pasta dados, liste as pastas existentes usando

```
usuario@DESKTOP-00RFJVC:~$ ls -l -h -a

total 17K
drwxr-x--- 11 deadg deadg 16 Mar 14 15:55 .
drwxr-xr-x 6 root root 6 Mar 14 15:29 ..
-rw------- 1 deadg deadg 7 Mar 14 15:35 .bash_history
-rw-r--r-- 1 deadg deadg 220 Mar 14 15:29 .bash_logout
-rw-r--r-- 1 deadg deadg 3.7K Mar 14 15:29 .bashrc
drwx------ 2 deadg deadg 3 Mar 14 15:34 .cache
drwxrwxr-x 3 deadg deadg 13 Jun 3 2020 FastQ-Screen-0.14.1
drwxrwxr-x 3 deadg deadg 3 Mar 14 15:49 .local
drwxrwxr-x 2 deadg deadg 2 Mar 14 15:55 pratica1
drwxrwxr-x 2 deadg deadg 2 Mar 14 15:34 pratica2
drwxrwxr-x 2 deadg deadg 2 Mar 14 15:35 pratica3
drwxrwxr-x 2 deadg deadg 2 Mar 14 15:35 pratica4
drwxrwxr-x 2 deadg deadg 2 Mar 14 15:35 pratica5
drwxrwxr-x 2 deadg deadg 2 Mar 14 15:35 pratica6
-rw-r--r-- 1 deadg deadg 807 Mar 14 15:29 .profile
-rw-rw-r-- 1 deadg deadg 209 Mar 14 15:55 .wget-hsts
     1     2   3    4      5      6        7

```

Essas colunas representam:
1. Permissões (explicado a seguir)
2. Links físicos para este arquivo   
3-4. Nome do grupo e do usuário   
5. Espaço utilizado pelo arquivo   
6. Momento em que foi feita a última edição       
7. Nome do arquivo.
Cada linha representa um arquivo ou diretório dentro do diretório “Documents/”.


Para criar um novo diretório, temos o comando mkdir (make directory). Para usá-lo, basta
adicionar o nome do diretório ***(não pode conter espaços!)*** depois do comando.

Crie um diretório com o nome pratica1.

```
usuario@DESKTOP-00RFJVC:~$ mkdir pratica1

```

![image](https://github.com/rafaeliwama/STB_bioinformatics/assets/46658489/2cadf6de-40e5-492b-aebf-b303ed877d68)

No Linux, não se recomenda o uso de espaço, acentos e cedilha em títulos de arquivos ou
diretórios. Caso realmente precise criar um diretório com espaço no título, use aspas (ex: “nome
do diretório”). Ainda assim, dê preferência ao underline (_) ou outro caractere.

Para entrar nesse diretório novo, use o comando cd (change directory), apenas o indicando
depois do cd.

```
usuario@DESKTOP-00RFJVC:~$ cd pratica1/
```

Para ir ao diretório superior (i.e. o diretório no qual o diretório atual está contido), basta indicar
“..”.

```
usuario@DESKTOP-00RFJVC:~/pratica1$ cd ..
```

Caso tenha alguma dúvida de como ou quais argumentos utilizar para determinado
comando, você pode utilizar o argumento --help. Experimente fazer isso com os comandos
indicados.

Agora, entre no seu diretório contido na pasta pratica1 para as próximas etapas desta
atividade.

Criando e editando arquivos de texto

Para criação de um novo arquivo, podem ser utilizados os comandos touch ou nano. O comando
nano abrirá o arquivo para edição, enquanto o comando touch somente criará o arquivo.
Execute:

```
usuario@DESKTOP-00RFJVC:~$ touch text.txt
```

Para editar o arquivo, execute o comando nano no terminal:

```
usuario@DESKTOP-00RFJVC:~$ nano text.txt
```

Será aberto um documento em branco. Digite o seguinte texto:

```
String1~
String2&gt;
string3
string 4
S t r i n g 6
String7String8String9
String*10
```

Para sair do documento pressione Ctrl + x e, em seguida, a tecla Y para salvar a edição e Enter
para sobrescrever o arquivo (caso deseje, no futuro, criar um novo arquivo a partir da edição
feita, aqui o nome do arquivo deve ser modificado). 

Para ver o arquivo de texto criado na tela do terminal, use o comando cat.

```
usuario@DESKTOP-00RFJVC:~$ cat text.txt

String1~
String2&gt;
string3
string 4
S t r i n g 6
String7String8String9
String*10
```

Para encontrar determinada sequência de caracteres alvo (também chamadas de strings), deve-
se utilizar o comando grep, o qual realizará um print das linhas que contenham os dados de
busca. Por exemplo, para encontrar apenas as linhas que contenham o texto “String” no arquivo
criado anteriormente (teste.txt), deve-se executar:

```
usuario@DESKTOP-00RFJVC:~$ grep &quot;String&quot; text.txt
String1~
String2&gt;
String7String8String9
String*10
```
![image](https://github.com/rafaeliwama/STB_bioinformatics/assets/46658489/77f2ec44-1c71-4c17-9ee6-a4a1713480cb)

Atenção: Observe que foram identificados somente os termos que iniciavam com letra
maiúscula (String). Isto ocorre porque o sistema diferencia, em suas buscas e linhas de
comando, caracteres maiúsculos e minúsculos.

Para substituir strings de um arquivo, utilizaremos o comando sed. O comando utiliza,
respectivamente, a string que deseja-se procurar e aquela que irá substituir o termo. 

Execute:

```
sed 's/ring/outra coisa/' text.txt
```

O resultado impresso na tela do terminal será: 

```
Stoutra coisa1~
Stoutra coisa2&gt;
stoutra coisa3
stoutra coisa 4
S t r i n g 6
Stoutra coisa7String8String9
Stoutra coisa*10
```

Para sobrescrever o arquivo com o resultado gerado, utilize o argumento ‘-i’:

```
sed -i 's/ring/outra coisa/' text.txt
```

Repare, contudo, que dois “ring” não foram substituídos. Isto ocorreu porque o comando sed, por padrão, substitui somente a primeira string de cada linha. Para que todos os termos ‘ring’ escritos sejam substituídos por ‘outra coisa’, basta inserir um ‘g’ ao fim do argumento com as aspas. 

```
sed -i 's/ring/outra coisa/g' text.txt
```

## Executando dois comandos simultaneamente

É possível aplicar dois comandos distintos em uma única execução. Por exemplo, para utilizar o comando grep a partir do resultado gerado pelo sed, basta adicionar ‘|’ entre os comandos:

usuario@DESKTOP-00RFJVC:~$ sed 's/ring/outra coisa/' text.txt | grep 'S'

Stoutra coisa1~
Stoutra coisa2>
S t r i n g 6
Stoutra coisa7String8String9
Stoutra coisa*10

Para salvar essa saída em um arquivo, use ‘>’ (“direcionar”) seguido do nome do novo arquivo.
usuario@DESKTOP-00RFJVC:~$ sed 's/ring/outra coisa/' text.txt |grep 'S' > nomequeeuquero.txt

Olhe o conteúdo do arquivo:

```
usuario@DESKTOP-00RFJVC:~$ cat nomequeeuquero.txt

Stoutra coisa1~
Stoutra coisa2>
S t r i n g 6
Stoutra coisa7String8String9
Stoutra coisa*10
```

Para realizar uma nova busca e adicionar o resultado ao final do arquivo anterior, utilize “>>” ao invés de “>”:


```
usuario@DESKTOP-00RFJVC:~$ sed 's/ring/outra coisa/' text.txt |grep '~' >> nomequeeuquero.txt

usuario@DESKTOP-00RFJVC:~$ cat nomequeeuquero.txt
Stoutra coisa1~
Stoutra coisa2>
S t r i n g 6
Stoutra coisa7String8String9
Stoutra coisa*10
Stoutra coisa1~
```

## Copiando, movendo e renomeando arquivos e pastas

Para copiar um arquivo, use o comando cp, indicando o nome do arquivo a ser copiado e o nome que a nova cópia terá.

```
usuario@DESKTOP-00RFJVC:~$ cp nomequeeuquero.txt  copia_nome.txt
```

Para copiar para outro diretório, adicione o caminho desse diretório antes do nome da cópia.

```
usuario@DESKTOP-00RFJVC:~$ mkdir new_dir
```

```
usuario@DESKTOP-00RFJVC:~$ cp nomequeeuquero.txt new_dir/copia2.txt
```

O comando mv pode também ser utilizado para renomear arquivos e pastas, movendo-os para o mesmo diretório com outro nome.

```
usuario@DESKTOP-00RFJVC:~$ mv copia_nome.txt new_dir/copia3
```

Para remover arquivos, use o comando rm seguido do nome do arquivo que deseja excluir.

```
usuario@DESKTOP-00RFJVC:~$ rm new_dir/copia3
```
![image](https://github.com/rafaeliwama/STB_bioinformatics/assets/46658489/77f2ec44-1c71-4c17-9ee6-a4a1713480cb)

**Lembre-se, o sistema Linux não alerta ou pede confirmação de exclusão de seus arquivos. Portanto, arquivos excluídos não vão para lixeira ou pastas temporárias e, logo, são perdidos definitivamente, sem possibilidade de recuperação. Sempre tenha um backup dos seus arquivos!**

## Organizando e filtrando arquivos

Nesta etapa, vamos utilizar uma tabela disponível online para explorar algumas formas de facilitar a visualização e edição de arquivos. Uma tabela contendo o mapa de inserção de transposons em Drosophila (fly base) pode ser encontrado no seguinte link: http://ftp.flybase.org/releases/FB2021_01/precomputed_files/insertions/insertion_mapping_fb_2021_01.tsv.gz

Para download do arquivo direto do terminal, use o comando wget:

```
usuario@DESKTOP-00RFJVC:~$ wget http://ftp.flybase.org/releases/FB2021_01/precomputed_files/insertions/insertion_mapping_fb_2021_01.tsv.gz
```

O arquivo está em uma forma compactada (.gz). Dentre as diversas ferramentas para descompactar arquivos, usaremos gunzip:

```
usuario@DESKTOP-00RFJVC:~$ gunzip insertion_mapping_fb_2021_01.tsv.gz
```

O comando cut pode ser usado para extrair da tabela apenas as colunas desejadas:

```
cut -fX FILE
```

Onde X é o número da coluna desejada e FILE é o arquivo em questão. Faça um teste extraindo a terceira coluna do arquivo e a salvando em um novo arquivo:

```
usuario@DESKTOP-00RFJVC:~$ cut -f3 insertion_mapping_fb_2021_01.tsv > col3
```

Para visualizar somente as primeiras 10 linhas do arquivo, execute o comando head.

```
usuario@DESKTOP-00RFJVC:~/ head col3

## FlyBase Insertion Mapping Table
## Generated: Tue Feb  2 21:30:51 2021
## Using datasource: dbi:Pg:dbname=fb_2021_01_reporting;

genomic_location
2L:19044446..19044446

2R:24123251..24123251
```

Remova as linhas em branco e, em seguida, o cabeçalho, com o comando sed (para melhor entendimento, leia o manual do comando):

```
usuario@DESKTOP-00RFJVC:~/ sed '/^$/d' col3 > col3a
usuario@DESKTOP-00RFJVC:~/ sed '/#/d' col3a > col3b
```

Para ordenar os resultados em ordem alfabética você pode usar sort. 

```
usuario@DESKTOP-00RFJVC:~/ sort col3b > sort_col3
```

Observação: caso tente ordenar o arquivo original com múltiplas colunas, não será possível usar o comando sort para ordenar a tabela inteira com base em uma única coluna que não seja a primeira.

Para remover linhas repetidas adjacentes, aplique o comando uniq (razão pela qual o comando sort é utilizado antes, garantindo que linhas idênticas estejam adjacentes na tabela):

```
usuario@DESKTOP-00RFJVC:~/ uniq sort_col3 > uniq_col3
```

Por fim, para comparar o número de linhas dos arquivos gerados, utilize o comando wc e o argumento -l (lines, ver help). 

```
usuario@DESKTOP-00RFJVC:~/ wc -l sort_col3 uniq_col3
70770 sort_col3
  63635 uniq_col3
 134405 total

```
