# Aula de Associações - Exemplos

## Elemento classe

```mermaid
classDiagram
    class Retangulo {
        - largura: double
        - algura: double
        + Retangulo(a: double, l: double)
        + getArea() double
        + getPerimetro() double
    }
```

## Associação entre classes

### Definição

```mermaid
classDiagram
    direction TB    
    Aluno -- Curso
    Carro -- Motor
```

### Multiplicidade

```mermaid
%%{init: {'flowchart': {'nodeSpacing': 100, 'rankSpacing': 100}}}%%
classDiagram
    direction LR
    class Carro {
        - marca : String
        - propulsor : Motor
        - rodas : Roda[]
        + Carro()
        + acelerar(v: int) void
    }
    
    class Motor {
        - cavalos: int
        - cilindros: int
        - giroAtual: int
        + Motor()
        + acelerar(v: int) void
    }
    
    class Roda {
        - diametro: double
        - materal: String
        - calibragem: double
        + Roda()
    }
    
    Roda "3..4" -- "1" Carro
    Carro "1" -- "1" Motor
```

```mermaid
%%{init: {'flowchart': {'nodeSpacing': 100, 'rankSpacing': 100}}}%%
classDiagram
    direction LR
    class Ponto {
        - x : double
        - y : double
        + Ponto(x : int, y : int)
        + getDistance(Ponto outro)
    }
    
    class Triangulo {
        - vertices : Set~Ponto~
        + Triangulo()
        + getArea() double
        + getPerimetro() double
    }

    class Retangulo {
        - vertices : Set~Ponto~
        + Retangulo()
        + getArea() double
        + getPerimetro() double
    }
    
    Triangulo "0..*" -- "3" Ponto
    Ponto "4" -- "0..*" Retangulo
```

### Navegabilidade
```mermaid
%%{init: {'flowchart': {'nodeSpacing': 100, 'rankSpacing': 100}}}%%
classDiagram
    class Carro {
        - marca : String
        - propulsor : Motor
        + Carro()
        + acelerar(v: int) void
    }
    
    class Motor {
        - giroAtual: int
        + Motor()
        + acelerar(v: int) void
    }
    
    class Aluno {
        - nome : String
        - matricula : String
        - curso : Curso
        + Aluno()
    }
    
    class Curso {
        - nome : String
        - cargaHoraria : int
        - alunos : Set~Aluno~
        + Curso()
    }
    
    Carro "1" --> "1" Motor : possui
    Aluno "*" <--> "0..1" Curso
```

### Agregação

```mermaid
%%{init: {'flowchart': {'nodeSpacing': 100, 'rankSpacing': 100}}}%%
classDiagram
    direction TB
    class Carro {
        - marca : String
        - propulsor : Motor
        - rodas : Roda[]
        + Carro()
        + acelerar(v: int) void
        + calibrado() boolean
    }
    
    class Roda {
        - diametro: double
        - materal: String
        - calibragem: double
        + Roda()
    }
    
    note for Carro "public boolean calibrado ( ) {
    ⠀⠀for ( Roda r : this.rodas) {
    ⠀⠀⠀⠀if ( r.calibragem <= 34 ) {
    ⠀⠀⠀⠀⠀return false;
    ⠀⠀⠀⠀}
    ⠀⠀}
    ⠀⠀return true;
    }"
    
    Roda "3..4" --o "1" Carro
```

### Composição

```mermaid
%%{init: {'flowchart': {'nodeSpacing': 100, 'rankSpacing': 100}}}%%
classDiagram
    direction TB
    class Livro {
        - titulo : String
        - autor : Pessoa
        - capitulos : List~Capitulo~
        + Livro(t : String, a : Pessoa)
        + adicionaCapitulo(t : String, n : int) void
        + imprimir() void
    }
    
    class Capitulo {
        - titulo : String
        - numeroPaginas : int
        + Capitulo(t : String, n : int)
    }
    
    note for Livro "public void adicionaCapitulo(String t, int n) {
    ⠀⠀this.capitulos.add(new Capitulo(t, n);
    }"
    
    Capitulo "1..*" --* "1" Livro
```

### Dependência

```mermaid
%%{init: {'flowchart': {'nodeSpacing': 100, 'rankSpacing': 100}}}%%
classDiagram
    direction TB
    class Jogador {
        - nome : String
        + Jogador(n : String)
        + jogar(d : Dado) void
    }
    
    class Dado {
        - numeroDeLados : int
        + Dado(l : int)
        + rolar() int
    }
    
    note for Jogador "public void jogar(Dado d){
    ⠀⠀int res = d.rolar()
    ⠀⠀// ...
    }"
    
    Dado <.. Jogador : jogar
```

## Exemplo

```mermaid
%%{init: {'flowchart': {'nodeSpacing': 100, 'rankSpacing': 100}}}%%
classDiagram
    direction TB
    class App {
        -gerenciador: Gerenciador
        +executa() void
    }

    class Gerenciador {
        -pedidos: Queue~Pedido~
        +registrarPedido() void
        +listarPedidos() List~Pedido~
    }

    class Pedido {
        -numero: int
        -data: LocalDate
        -itens: List~Item~
        +adicionarItem(Item) void
        +valorTotal() void
    }

    class Item {
        -nome: String
        -descricao: String
        -categoria: String 
        -preco: double
        -restricoes: Set~String~
        -categoria: String
    }

    class Cardapio {
        -itens: Set~Item~
        +getItem(nome : String) Item
        +listarItens() List~Item~
        +listarItens(categoria : String) List~Item~
    }

    App "1" --> "1"  Gerenciador
    Gerenciador "1" *-- "*" Pedido
    Gerenciador ..> Cardapio : registrarPedido
    Cardapio "1" *-- "*" Item
    Item "*" --o "*" Pedido
```



























