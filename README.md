## Regex

São expressões utilizadas para buscas/substituições em padrões em strings. Devem ser colocados entre `//` e geralmente utilizados com os métodos `.replace()` e `split()`.

```
// Procura a
const regex = /a/

'Javascript'.replace(regex, 'x')
// retorna Jxvascript
```

### Literal

Utilizar um caractere literal irá realizar uma busca específica dele.

```
// Procura J seguido de a, v, e a
const regex = /Java/

'Javascript'.replace(regex, 'Type')
// retorna Typescript
```

### Flags

Modificam como a expressão é interpretada.

#### g

Significa global e retorna todos os resultados que estiverem dentro do padrão e não apenas o primeiro.

```
// Procura a
const regex = /a/

'Javascript'.replace(regex, 'x')
// retorna Jxvxscript
```

#### i 

Case insensitivity, ignora as diferenças entre maiúsculas e minúsculas. 

```
const regex = /Pe/gi

'Perdeu perdido'.replace(regex, 'Ba')
// retorna Bardeu Bardido
```

### Character class 

Ao colocarmos os caracteres entre colchetes, estamos definindo uma classe. `/[ab]/` irá procurar por a ou b. 

```
// Procura todo a, A, i, I
const regex = /[ai]/gi

'Javascript'.replace(regex, 'x')
// retorna Jxvxscrxpt
```

### Character class e Especiais

Podemos utilizar caracteres que não são alfanúmericos dentro da classe.

```
// Procura - ou .
const regex = /[-.]/g

'111.222-333-44'.replace(regex, '')
// retorna 11122233344
```

### Um ou Outro

Combina caracteres literais com uma classe para buscar variações: Ju[nl]ho busca Julho ou Junho.

```
// Procura B, seguido de r, a
// seguid de s ou z, seguido de i, l
const regex = /Bra[sz]il/g

'Brasil com z: Brazil'.replace(regex, 'Caneta')
// retorna Caneta com z: Caneta
```

### De A à Z

O traço - dentro de [] serve para definirmos um alcance de acordo com a [tabela unicode](unicode-table.com/pt/). `[A-Z]` irá buscar os caracteres de A à Z.


```
// Busca por itens de a à  z
const regex = /[a-z]/g

'JavaScript é uma linguagem'.replace(regex, '0')
// retorna J000S00000 é 0000000000
```

### Negar

Utilizando o acento circunflexo podemos negar caracteres.

```
// Busca por tudo que não estiver entre a e  z
const regex = /[ˆa-z]/g

'Brasil com z: Brazil'.replace(regex, '')
// retorna rasil com z  razil
```

### Ponto

O `.` seleciona qualquer caractere, exceto quebras de linha.

```
const regex = /./g

'Typescript'.replace(regex, 'n')
// retorna nnnnnnnnnnn
```

### Escapar Especiais

Caracteres especiais como o ponto `.` podem ser escapados utilizando a barra `\`, assim não terá sua função especial e será tratado como literal. Lista de caracteres especiais: `+*?ˆ$\.[]{}()|/`

```
const regex = /\./g

'999.222.222.222'.replace(regex, '-')
// 999-222-222-222
```

### Word

O `\w` irá selecionar qualquer caractere alfanumérico e o underline. É a mesma coisa que `[A-Za-z0-9_]`.

```
const regex = /\w/g

'Guarda-chuva R$ 23,00'.replace(regex, '-')
// ----------- -$ --,--
```

### Not Word

O `\W` irá selecionar tudo que não for caractere e o underline. É a mesma coisa que `[^A-Za-z0-9_]`.

```
const regex = /\W/g

'Guarda-chuva R$ 23,00'.replace(regex, '-')
// Guarda-chuva-R--23-00
```

### Digit

O `\d` irá selecionar qualquer dígito. É a mesma coisa que `[0-9]`.

### Not Digit

O `\n` irá selecionar tudo que não for dígito. É a mesma coisa que `[^0-9]`.

### Whitespace

O `\s` irá selecionar qualquer espaço em branco, incluindo espaços, tabs e quebra de linhas.

```
const regex = /\s/g

'+55 (21) 1111- 1111'.replace(regex, '')
// Retorna +55(21)1111-1111
```

### Not Whitespace

O `\S` irá selecionar qualquer não for espaço em branco.

```
const regex = /\S/g

'+55 (21) 1111- 1111'.replace(regex, 'X')
// Retorna XXX XXXX XXXXX XXXX
```

### Quantificador

É possível selecionar caracteres seguidos, como `/bbb/g` irá selecionar apenas `bbb`. Com as chaves podemos indicar a repetição `/b{3}/g`. Agora, ele está fazendo uma seleção completa e não caractere por caractere.

```
const regex = /a{4}/g

'Vaaaai ali por favor'.replace(regex, 'a')
// Retorna Vai ali por favor
```

### Quantificador Min e Max

Podemos informar o min e max do quantificador `/a{2, 4}/` vai selecionar quando aparecer `a` duas ou até quatro vezes. `/a{2,}` irá selecionar quando se repetir duas ou mais vezes.

### Mais +

O sinal de `+` significa que devemos selecionar quando existir pelo menos uma ou mais ocorrências.

```
// Procura dígitos em ocorrência de um ou mais
const regex = /\d+/g

'222.333.222.42'.replace(regex, 'X')
// Retorna X.X.X.X

// Começa com d, seguido por uma ou mais letras
const regexLetters = /d\w+/g

'Dígitos, dados, desenhos, Dito, d'.replace(regexLetters, 'X')
// Retorna Dígitos, X, X, Dito, d
```

### Asterisco *

O sinal `*` significa que devemos selecinar quando existor 0 ou mais ocorrências.

```
// Começa com d, seguido por zero ou mais letras
const regex = /d\w*/g

'Dígitos, dados, desenhos, Dito, d'.replace(regex, 'X')
// Retorna Dígitos, X, X, Dito, X
```

### Opcional ?

O sinal `?` significa que o caractere é opcional, pode ou não existir.

```
// Procura por regex com p opcional
const regex = /regexp?/g 

'Qual é o certo, regexp ou regex?'.replace(regex, 'Regular Expression')
// Qual é o certo, Regular Expression ou Regular Expression?
```

### Alternado |

O sinal `|` irá selecionar um ou outro.

```
// Procura por java ou php (case insensitive)
const regex = /java|php/gi 

'PHP e Java são linguagens diferentes'.replace(regex, 'x')
// x e x são linguagens diferentes
```

### Word Boundary \b

O sinal `\b` irá indicar que pretendemos fazer uma seleção que deve ter início e fim de não caracteres `\w`.

```
// Procura por java (case insensitive)
const regex = /java/gi 

'Java não é JavaScript'.replace(regex, 'x')
// x não é xScript

// Procura por java (case insensitive)
const regexBoundary  = /\bjava/gi 

'Java não é JavaScript'.replace(regexBoundary , 'x')
// x não é JavaScript

// Procura por dígitos em sequência que estejam isolados
const regexDigit = /\b\d+\b/gi 

'No Restaurante25 na rua 3, custa R$ 32,00'.replace(regexDigit, 'x')
// No Restaurante25 na rua x , custa R$ x,x
```

### Not Word Boundary \B

É o contrário do `\b`.

```
const regexDigit = /\B\d+\B/gi 

'11_22 33-44 55é66 77e88'.replace(regexDigit, 'x')
// 1x_x2 33-44 55é66 7xex8
```
