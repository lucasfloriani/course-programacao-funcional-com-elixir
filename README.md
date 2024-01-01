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
OBS3: É possivel utilizar a função **c/1** para compilar um arquivo com extensão **ex**

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

### Tuplas

As tuplas são delimitadas por chaves e elas podem conter tipos diferentes

```ruby
{43, :type, "hello", 67.32, true}
```

As tuplas são armazenadas continuamente na memória, ficando assim os dados um ao lado do outro nos registros da memória, resultando em dados bem próximos para acessar.
OBS: Mesmo esquema que os arrays e vetores de outras linguagens trabalham, ou seja, não é uma Lista encadeada

Assim como arrays em outras linguagens, podemos acessar um elemento específico em uma tupla

```ruby
elem({43, :yes, "hello", 67.32, true}, 2)
```

## Imutabilidade

A ideia por trás da imutabilidade é simplificar o trabalho de paralelismo

```ruby
list = [1, 2, 3, 4]
List.delete_at(list, -1)
# => 4
list ++ [1]
# => [1, 2, 3, 4, 1]
IO.inspect list
# => [1, 2, 3, 4]
```

Com base neste exemplo abaixo, o valor final em Elixir é **857** ou **365**?

```ruby
total = 857
total = 365
IO.puts total
```

Se você respondeu 857, **ERROU!**
O Elixir trabalha com "binding" de variáveis, ou seja, a variável **aponta para uma referência de memória que contém o valor**, sendo assim quando "re-atribuímos" (rebinding) a variável, **ela aponta para uma nova referência de memória**

O pulo do gato fica por conta de que o rebinding só ocorre quando o contexto for correto.
Para entendermos melhor, veja o exemplo a seguir:

```ruby
total = 876

defmodule Mutante do
  def mutar(valor) do
    valor = 1
    IO.puts "interno- #{valor}" # Aqui será exibido 1 ou 876?
    valor
  end
end

Mutante.mutar(total)
IO.puts "externo A- #{total}" # E aqui? 1 ou 876?

total = Mutante.mutar(total)
IO.puts "externo B- #{total}" # E agora, 1 ou 876?
```

Responsta do console

```txt
"interno- 1"
"externo A- 876"

"interno- 1"
"externo B- 1"
```

Como pudemos perceber, o valor pode ser alterado dependendo do contexto. Sendo assim:

"_Ser imutável não quer dizer que o valor nunca mudará, mas sim que ele está protegido de mudanças externas!_"

## Criando Módulos e Funções

O Elixir trabalha separando funções em módulos, inclusive já criamos nosso primeiro módulo e função aulas atrás

```ruby
defmodule Say do
  def hello do
    "Olá Mundo!!!"
  end
end
```

OBS: Nome do módulo em Pascal case e nome das funções em Snake case

Podemos usar namespaces para facilitar e evitar confusões em nossas aplicações. Para isso, podemos usar um ponto (.) para separar os namespaces em nossos módulos, veja:

```ruby
defmodule MyModule.SaySomething do
  def hello_world do
    "Olá Mundo!!!"
  end
end
```

OBS: Usado para prevenir a criação de um módulo com o mesmo nome que um existente na própria linguagem

## Funções Nomeadas vs Funções Anônimas

Até agora usamos "funções nomeadas" que basicamente são funções que possuem um nome
As funções anônimas são funções definidas sem um nome atrelado, mas que podem ser atribuídas (bind) a uma variável

```ruby
sum = fn (a, b) -> a + b end
# Para executar ela é necessário usar o ponto
sum.(2.3)
```

Para múltiplas instruções no corpo da função use ";" ou múltiplas linhas:

```ruby
printed_sum = fn (a, b) -> c = a + b;
IO.puts(">>#{c}<<") end

printed_sum = fn (a, b) ->
  c = a + b
  IO.puts(">>#{c}<<")
end
```

Podemos também remover os parênteses

```ruby
hello = fn name -> "Hello, #{name}!" end
hello.("Ana")
```

Podemos também criar funções anônimas sem parâmetros

```ruby
one_plus_one = fn -> 1 + 1 end
one_plus_one.()
```

## Capture Operator

O operador de captura (capture operator) "&" pode ser usado para basicamente duas coisas:

1 - Criar funções anônimas:

```ruby
sum = fn (a,b) -> a + b end

# Criando função anônima com Capture Operator
sm = &(&1 + &2)
# ou
sm = & &1 + &2
```

2 - Permitir que funções nomeadas possam ser usadas como função anônima:

```ruby
# Não possibilitar fazer desta maneira, uma das formas é utilizar Capture Operator
# upcase = String.upcase

upcase = fn string -> String.upcase(string) end
upcase.("hello, world!")

# Parecido com C, quando você usa "&" para pegar o endereço da memória
# Fazendo assim com que o upcase aponte para este endereço da memória (binding)
upcase = &String.upcase/1
upcase.("hello, world!")
```

## Pipe Operator

Para entender o Pipe Operator, vamos desconstruir esse exemplo

```ruby
IO.puts(String.length("Olá"))
```

A primeira coisa que podemos fazer para melhorar a legibilidade e entendimento é separá-la em dois passos:

```ruby
str_len = String.length("Olá")
IO.puts(str_len)
```

Um próximo refatoramento que podemos fazer é entender e usar o pipe operator **"|>"**

```ruby
String.length("Olá") |> IO.puts
```

"_O pipe operator permite que o resultado da expressão anterior seja o valor para o primeiro parâmetro da expressão seguinte._"

Sendo assim, podemos desconstruir ainda mais:

```ruby
"Olá!" |> String.length |> IO.puts
```

Por fim, podemos organizar de uma forma mais legível:

```ruby
"Olá!"
|> String.length
|> IO.puts
```

## First-Class Function

First-Class Functions ou First-Class Citizens, essa segunda "traduzida" ficaria algo como "Cidadãos de Primeira Classe"
A ideia por trás desse conceito é que em uma linguagem funcional uma função deve ser como qualquer outro valor, ou seja, no Elixir funções são valores do tipo **function**

Vejamos esse exemplo:

```ruby
taxa_basica = fn (preco) -> 5 end
taxa_promocional = fn (preco) -> preco * 0.12 end
preco_total = fn (preco, f_taxa) -> preco + f_taxa.(preco) end

preco_total.(1000, taxa_basica)
preco_total.(1000, taxa_promocional)
```

## First-Class Functions vs Higher-Order Functions

Uma higher-order function é uma função que **pode receber uma função** como argumento **ou retornar uma função**

As higher-order functions são um contraste com as **order-functions** que são funções que não podem receber funções como argumento ou retornar funções.

Veja esse exemplo de uma função retornando uma função:

```ruby
defmodule Salario do
  def calculo_do_bonus(porcentagem) do
    fn(salario) -> salario * porcentagem end
  end
end

# bonus_para_gerente = Salario.calculo_do_bonus(1.05)
# bonus_para_gerente.(1000)
# => 1050.0
```

Em resumo, quando você diz que uma linguagem suporta first-class functions, quer dizer que a linguagem trata as funções como valores e que você pode atribuir, por exemplo, elas a uma variável.
Por outro lado, as higher-order functions são funções que trabalham com outras funções, podendo também recebê-las ou retorná-las.

## Pattern matching

A primeira coisa que precisamos aprender sobre Pattern Matching é que o "=" não é um operador de atribuição no Elixir

```ruby
n1 = 1
# 1
1 = n1
# 1
2 = n1
# ** (MatchError) no match of right hand side value: 1
```

OBS: "=" é um matching operator
OBS2: Ele faz a verificação se no lado esquerdo tem uma variável, verificando assim se pode ser apontado o valor na direita a ele.
OBS3: Faz a comparação entre os endereços de memória caso o valor da esquerda não for uma variável.

O Match Operator só "atribui variáveis do lado esquerdo do operador match

Agora que ja entendemos o Match Operator, vamos brincar com o Pattern Matching, que tem o mesmo princípio mas pode ser aplicado a estruturas mais complexas

```ruby
{a, b, c} = {:jackson, "pires", 123}
# {:jackson, "pires", 123}

a
# :jackson

b
# "pires"

c
# 123
```

Perceba que no exemplo anterior, do lado esquerdo temos uma tupla constituída apenas de variáveis, e do lado direito uma tupla com alguns valores
O Elixir verifica se as estruturas podem ser correspondidas e em caso positivo faz as atribuições
Caso as estruturas não sejam equivalentes, um erro ocorrerá

```ruby
{a, b, c} = {:jackson, "pires"}
# ** (MatchError) no match of right hand side value: {:jackson, "pires"}

{a, b, c} = [:jackson, "pires", 123]
# ** (MatchError) no match of right hand side value: [:jackson, "pires", 123]
```

Outra coisa interessante que podemos usar com Pattern Matching é a estrutura de cabeça e causa para listas.

```ruby
[cabeca | cauda] = [1, 2, 3]
# [1, 2, 3]

cabeca
# 1

cauda
# [2, 3]
```

OBS: Pode ser chamada ao pé da letra de Correspondência de Padrões

### Underscore e Pin

Ainda sobre Pattern Matching, imagine que temos a seguinte situação

```ruby
{x, y} = {32, 25}
```

Até aí tudo bem, mas e se não quisermos o valor do y? Neste caso seremos obrigados a informar uma variável?

A resposta para isto é o **underscore** "_"

```ruby
{x, _} = {32, 35}
```

Sempre usaremos o underscore "_" quando não nos importamos com o valor.
Assim apenas o **x** vai apontar para o 32 enquanto o outro valor pra gente não importa
Em resumo o underscore age como uma variável que descarta o valor logo depois de "atribuída"

Agora vamos falar sobre o pin operator. Veja o exemplo:

```ruby
x = 21
# 21
x = 43
# 43
```

Notadamento o x começou apontando para 21 e em seguida foi reassociado (rebind) para o 43.
Mas, e se a gente não quisesse permitir essa reassociação?

É ai que entra o pin operator "^".
O uso do pin operator é justamente para impedir a reassociação de variáveis.

```ruby
x = 34
# 34
^x = 45
# ** (MatchError) no match of right hand side value: 45
```

Perceba que colocando o "^" antes da variável o Elixir levantou um erro informando que o 45 não "casa" com o valor atual do **x**, ou seja, o pin operator evitou o rebind.

O legal do pin operator é que podemos usá-lo em conjunto com o pattern matching, fazendo com que seja evitado novos rebinds que não desejamos. Veja:

```ruby
{x, y} = {76, 89}
# {76, 89}

x
# 76

y
# 89

{x, ^y} = {12, 67}
# ** (MatchError) no match of right hand side value: {12, 67}
```

OBS: Não faz rebind se o valor for o mesmo

### Fazendo matching de parte de uma string

```ruby
"Content-Type: " <> content_type = "Content-Type: text/html; charset=UTF-8"
# content_type = "text/html; charset=UTF-8"
# Variável tem que ficar no lado direito do <>
```

## Keyword Lists e Maps

### Keyword Lists

Para entender as Keyword Lists, vamos imaginar uma tupla (que é indexável) armazenado em uma lista em cada posição.

```ruby
{"hello", :world, 123} # tupla
["Elixir", :phoenix, true, 456] #lista
[{:a. 22}, {:b, 77}]
```

Uma keyword list sempre possuirá uma tupla em cada posição e essa tupla obrigatoriamente conterá uma chave e um valor, ou seja, um átomo e um valor; Sendo assim, podemos reescrever uma keyword list desta maneira

```ruby
[{:a, 22}, {:b, 77}] == [a:22, b:77]
```

Apesar das keyword lists também serem listas encadeadas em sua essência, é possível acessar qualquer elemento indicando sua chave, veja:

```ruby
minha_kwl = [a: 22, b: 77]
# [a: 22, b: 77]
minha_kwl[:a]
# 22
```

É interessante perceber que por não ser indexada a keyword list permite valores repetidos, mas nesses casos ele vai retornar apenas o primeiro valor e da chave encontrada, por isso, a ordem importa!

```ruby
x = [a: 22, b: 77, a: 99]
x[:a]
# 22
```

Em resumo:

* **Keyword Lists devem possuir átomos como chave**
* **Nas Keyword Lists a ordem das chaves importa**
* **Nas Keyword Lists podem existir chaves iguais**

### Maps

Os Maps são muito parecidas com as KeyWords Lists pois também são formados por pares de chave-valor.

A primeira diferença fica por conta que os Maps **são indexados** (ou seja, não é baseado em lista encadeada), a segunda é que **não são permitidas chaves iguais**, justamente por ela ser indexada, e a terceira é que **a chave pode ser determinada por qualquer tipo de dado**, não necessariamente um átomo.

```txt
m = %{:a => 1, 2 => :b}
n = %{"z" => 5, 8 => true}

m[2]
# :b

n["z"]
# 5
```

Outra característica interessante é que também é possível acessar as chaves do **tipo átomo** através da sintaxe do ponto.

```txt
m = %{:a => 1, :b => "xyz"}

m.a
# 1

m.b
"xyz"
```
