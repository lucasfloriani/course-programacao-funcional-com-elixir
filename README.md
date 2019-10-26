# Programação Funcional com Elixir

## Princípios da Programação Funcional

* **First-Class Functions**
* **Pure Functions**
* **Immutable Variables**
* **Recursion**
* **Nonstrict evaluation**
* **Statements**
* **Pattern Matching**

### First-Class Functions

São funções que podem aceitar outra função como argumento ou mesmo retornar uma função, ou seja, é a capacidade de criar funções e devolvê-las ou passá-las para outras funções.

Auxilia na reutilização e abstração do código, exemplo:

```txt
func A(){...}
func B(){...} ou com lambda B = func{...}
func A(B){...}
```

Funções de primeira classe também são conhecidas como Higher-Order Functions (Funções de Ordem Superior) ou ainda First-Class Citizens (Cidadãos de Primeira Classe)

OBS: Lembre-se que quando falamos em **Lambda** _é possibilidade de criar uma função anônima_, já uma função de primeira classe é uma função que consegue receber funções anônimas como argumento/parâmetro, ou seja, receber lambdas

### Pure Functions

São funções que não tem efeitos colaterais

Efeitos colaterais são ações que uma função pode executar e que não estão contidas apenas na própria função.

Um exemplo de função impura é quando passamos uma variável global e a transformamos diretamente dentro dessa função.

Também são conhecidas por serem "indempotentes", ou seja, a mesma entrada sempre gera a mesma saída.

### Immutable Variables

Variáveis imutáveis, uma vez definidas, não podem ser alteradas.

Embora a imutabilidade pareça muito dificil de fazer, dado o fato de que o estado deve mudar dentro de uma aplicação em algum momento, veremos como tratar isso mais adiante.

```js
var minhaString = "abc"
substituir(minhaString, "a", "x") // xbc
console.log(minhaString) // abc
```

### Recursion

Em resumo, função recursiva é aquela que pode chamar a si mesma.

A **Recursão** permite escrever algoritmos menores e mais concisos e operar observando apenas as entradas para nossas funções.

Isso significa que a função estará preocupada apenas com a interação atual e se deve continuar.

### Nonstrict evaluation

**Avaliações não restritas** nos permitem ter variáveis que ainda não foram computadas.

Por outro lado, Strict Evaluation (Avaliações Rigorosas) atribuem uma variável assim que ela é definida, que é o que estamos acostumados.

Nonstrict significa que podemos ter uma variável que não seja atribuída (computada) até a primeira vez em que é referenciada.

OBS: Mesma idéia do lazy evaluation.

Nesse ponto podemos lembrar do Haskell que sempre levanta a bandeira do "Lazy Evaluation" (Avaliação Preguiçosa), "Delayed Evaluation" (Avaliação Tardia), ou ainda Call-by-name (Chame pelo nome) que a grosso modo são a mesma coisa.

Perceba que isso é inerente à linguagem de programação, não dependendo do programador.

### Statements

As **declarações** são pedaços de código "avaliáveis" que possuem um valor de retorno

Pense em instruções "if" que tenham algum valor de retorno

Cada linha de código deve ser considerada uma declaração.

```ruby
puts("O valor de retorno é #{x=1}) ## Um fmt.Println acaba retornando um valor
# O valor de retorno é 1
```

Ou seja, a programação funcional introduz a ideia de que cada linha de código deve retornar um valor.

Então, se estamos aptos a fazer mais uso de statements nós podemos reduzir o número de variáveis e se reduzimos a quantidade de variáveis, reduziremos também a necessidade de "mudá-las" e isso aumenta a habilidade de executar processos concorrentes e tornar-se mais funcional.

OBS: Ajuda na programação multithread, pois não é preciso gerenciar o valor das variáveis nos nucleos do processador utilizado.
OBS2: A programação funcional lhe tras a programação concorrente de uma forma mais simples.

### Pattern Matching

A "**correspondência de padrões**" não aparece realmente na matemática, mas ajuda a programação funcional a diminuir a necessidade de variáveis específicas.

Pattern matching nos permite procurar padrões simples em valores, estruturas de dados e até funções.

OBS: Pattern matching lembra muito regex, porem é utilizado em cima de valores, estruturas de dados e até funções conforme descrito acima.

No código, geralmente encapsulamos um grupo de variáveis juntas dentro de um objeto. A correspondência de padrões nos permite obter uma melhor verificação de tipos e extrair elementos de um objeto, criando instruções mais simples e concisas com menos necessidade de definições de variáveis.

Obs: **quanto menos variaveis é utilizado na programação funcional melhor**

## Paralelismo/Concorrência

A ideia de programação concorrente não é nova, e até algum tempo atrás os processadores possuíam apenas um núcleo, sendo assim, executar dois programas ao mesmo tempo, exigia que o processador executasse "um pouquinho" de cada, fazendo parecer que eles estavam funcionando ao mesmo tempo, quando na verdade eles estavam funcionando "**concorrentemente**".

Atualmente temos processadores que facilmente são multicore, ou seja, com vários núcleos (dual core, quad core, etc).

No entanto, muitos programas não tiram proveito disso, trabalhando ainda como "antigamente", sem aproveitar todo potencial que os processadores dispõe.

Se executarmos um programa e cada parte dele for executada por um núcleo processador, podemos dizer que ele está sendo executado em **paralelo**.

Ou ainda, se forem executados dois programas e cada um for executado em um core diferente, também teremos paralelismo, pois eles não disputam o mesmo core.

Sendo assim temos situações distintas de "**paralelismo**" e "**concorrência**" na execução de um sistema.

O paralelismo/concorrência, acaba se beneficiando quando usamos programação funcional, visto que muitos dos padrões aplicados (imutabilidade, funções puras, etc) facilitam a execução de programas em múltiplos cores.

Em relação ao Elixir, temos ainda uma vantagem, pois essa linguagem funciona em cima de uma máquina virtual (BEAM) que foi projetada para esse fim.

## Conhecendo o IEx, elixir e elixirc

### IEx

Prompt interativo onde podemos escrever código Elixir e obter o resultado no mesmo instante.

OBS: Para usa-lo é preciso digitar IEx no terminal.
OBS2: Carrega os arquivos beam que estão na pasta onde foi executado iex.

### Elixirc

Binário que permite a compilação de código Elixir

Compilando os arquivos para extensão **.beam**

OBS: Os arquivos devem possuir extensão **.ex**
OBS2: Precisa rodar _elixirc_ para transformar os arquivos
OBS3: A extensão **.ex** é para quando será compilado estes arquivos

### Elixir

Binário que permite executar um código elixir a partir de arquivos **.exs** (scripting)

OBS: Para executar individualmente é necessário rodar no terminal o comando **elixir nomeDoArquivo.exs**

## Funcionamento geral do Elixir

O Elixir é baseado em Módulos e Funções

### Módulos

É a forma usada para agrupar diversas funções como por exemplo:

* **String:** <https://hexdocs.pm/elixir/String.html>
* **IO:** <https://hexdocs.pm/elixir/IO.html>

### Funções

São as ações de fato:

* IO.puts("Hello!")
* IO.puts "Hello!" #Parênteses são opcionais*

Aridade das funções:

* Quantidade de argumentos de uma função
* **IO.puts/1**

### Tudo é uma expressão

* No elixir tudo é uma expressão.
* Expressão != Instrução
* Toda expressão possui retorno
  * IO.puts("Hello")
  * hello
  * :ok # Retorno da expressão

Esse é um princípio da programação funcional (**Statements**)
OBS: Expressão é uma instrução que traz um retorno

## Conhecendo um pouco mais do IEx

<https://hexdocs.pm/iex/IEx.html>

Existem diversos Helpers no IEx que podem ser acessados digitando-se o **h()**

1. Todos os helpers são mostrados com a sua respectiva aridade das funções
2. Podemos "pedir ajuda" sobre qualquer módulo ou função, bastando para isso invocar o **h(nome do módulo ou função)**. Ex: h(Enum) ou h(Enum.map)
3. Podemos "inspecionar quaolquer valor usando i(valor). Ex: i("olá")
4. Existem vários outros helpers como o **i/1** para inspecionar um elemento ou o **r/1**, que nesse caso permite recompilar um módulo informado.
5. Você pode "pedir ajuda" sobre os próprios helpers, bastando para isso invocar **h(helper) para conhecê-lo. Ex: h(v/0).
6. Use **CRTL + K** ou **clear/0** para limpar o terminal.

Podemos usar a tecla TAB para autocompletar o nome de módulos ou funções.

Para sair do IEx

1. Você pode pressionar **CRTL+C duas vezes**
2. Pressionar **CRTL+c e em seguida 'q'**
3. Ou ainda pode pressionar **CTRL+\\**

## Tipos básicos do elixir

| Valor     | Tipo        |
|-----------|-------------|
| 1         | integer     |
| 1.0       | float       |
| 0x1F      | integer     |
| true      | boolean     |
| :atom     | atom/symbol |
| "elixir"  | string      |
| [1, 2, 3] | list        |
| {1, 2, 3} | tuple       |

### Como saber o tipo de uma variável/termo

Funções do Módulo Kernel:
<https://hexdocs.pm/elixir/Kernel.html>

* is_boolean/1
* is_atom/1
* is_integer/1
* is_float/1
* is_number/1

### Integers e Floats

Funções para manipular de integers/floats

* div(10,3)   # Resultado sem casa decimal
* rem(10,3)   # Resto da divisão
* round(3.58) # Arredondar número Ex = round(3.5) == 4 && round(3.49) == 3
* trunc(3.58) # 'truncar' número

#### Curiosidade - Módulo Kernel

É um módulo que não precisa da utilização do seu prefixo para utilização
<https://hexdocs.pm/elixir/Kernel.html>

Obs: As funções acima listadas são do módulo Kernel

### Binário, Hexadecimal e Octal

O Elixir permite usar alguns atalhos quando queremos converter binário, hexadecimal e octal para inteiros através dos prefixos **0b**, **0x** e **0o**.

```txt
ob1010 # 10  (Binário)
0o755  # 493 (Octal)
0xFF   # 255 (Hexadecimal)
```

### Boolean

O Elixir aceita **true** e **false** como booleanos
OBS: Contem os operadores **NOT (!)**, **OR (||)** e **AND (&&)** na linguagem.

### Átomos

Átomos são constantes no qual o seu nome é o seu próprio valor. Eles são definidos colocando-se "dois pontos" na frente do nome do átomo
Ex :jackson

OBS:Em sua essência, **true** e **false** são átomos

```ruby
is_atom(false) # true
```

OBS2: É a mesma coisa que os symbols no Ruby
OBS3: Utilizado como auxiliar de chaves principalmente em listas e tuplas
OBS4: Mais rapido do que utilizar uma variável string

### Strings

Strings são delimitadas em aspas duplas e são codificadas por padrão em UTF-8

```ruby
"Elixir é legal!"
```

Você pode usar caracteres de escape como "\n" para nova linha. Pra vê-los em ação use...

```ruby
IO.puts("Elixir \né\n legal!")
```

Strings são representadas em binários, que são sequências de bytes

```ruby
is_binary("Elixir é legal!")
```

Para saber o número de bytes ocupados pela String, a função...

```ruby
byte_size("José")
```

Podemos interpolar código Elixir em uma String usando #{}

```ruby
abc = "Ihull!!"
IO.puts("Elixir é legal! #{abc}")
```

Para concatenar Strings use <>

```ruby
"Olá! " <> "Elixir é muito legal"
```

### Binários, Strings e Charlists

Strings são binários codificados em UTF-8, por isso a quantidade de bytes para representar uma string pode variar

```ruby
byte_size("Elixir é legal!")
String.length("Elixir é legal!")
```

Para saber qual o codepoint do caractere, use **?** antes do mesmo
OBS: Codepoints são caracteres Unicode que podem ser representados por **um ou mais bytes**

```ruby
?a # 97
?é # 233
```

Para conhecer a representação binária de uma String, concatene ela com <<0>>
OBS: Transforma em binário pois ao concatenar com um binário, a string acaba não sendo mais válida, tendo assim que virar uma variável do tipo binário.

```ruby
"Elixir é legal!" <> <<0>>
```

Para conhecer uma string a partir dos binários, basta atribuí-la a uma variável

```ruby
abc = <<69, 109, 105, 120, 105, 114, 32, 195, 169, 32, 108, 101, 103, 97, 108, 23>>
```

Codepoints são caracteres Unicode que podem ser representados por **um ou mais bytes**
OBS: Codepoints != Binário

```ruby
?é           # 233
"é" <> <<0>> # <<195, 169, 0>>
```

Internamento, o Elixir representa as Strings como uma sequência de Bytes ao invés de um array/vetor de caracteres, no entanto, caso seja necessário trabalhar com arrays de caracteres, podemos usar as **Charlists** bastando para isso usar aspas simples ao invés de duplas, veja:
OBS: Charlist == array de codepoints && String == binário

```ruby
'Elixir é legal!'              # É Charlist, pois foi declarado com aspas simples
"Elixir é legal!" <> <<0>>     # É String
to_charlist("Elixir é legal!") # Transformando String em Charlist
```

### Listas

As listas são delimitadas por colchetes e elas podem conter tipos diferentes

```ruby
[43, :yes, "hello", 67.32, true]
```

Listas podem ser concatenadas com "++" ou subtraídas com "--"

```ruby
[43, :yes, "hello"] ++ [67.32, true]
[43, :yes, "hello"] -- ["hello", true]
```

Listas no Elixir são **Listas Encadeadas** em sua essência, sendo assim os elementos não são indexados e não podemos acessar um elemento diretamente como em uma array/vetor

Em relação a listas, a biblioteca nos fornece duas funções especificas para pegar dados da lista, os quais são o **(head) hd/1** e **(tail) tl/1**
