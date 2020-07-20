<!-- # Display

`fmt::Debug` hardly looks compact and clean, so it is often advantageous to
customize the output appearance. This is done by manually implementing
[`fmt::Display`][fmt], which uses the `{}` print marker. Implementing it
looks like this:

```rust
// Import (via `use`) the `fmt` module to make it available.
use std::fmt;

// Define a structure for which `fmt::Display` will be implemented. This is
// a tuple struct named `Structure` that contains an `i32`.
struct Structure(i32);

// To use the `{}` marker, the trait `fmt::Display` must be implemented
// manually for the type.
impl fmt::Display for Structure {
    // This trait requires `fmt` with this exact signature.
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Write strictly the first element into the supplied output
        // stream: `f`. Returns `fmt::Result` which indicates whether the
        // operation succeeded or failed. Note that `write!` uses syntax which
        // is very similar to `println!`.
        write!(f, "{}", self.0)
    }
}
``` -->

# Display

`fmt::Debug` dificilmente parece compacto e limpo, por isso é frequentemente vantajoso
personalizar a aparência da saída. Isso é feito implementando manualmente
[`fmt::Display`][fmt], que usa o marcador de impressão `{}`. Implementando-o
parecido com isso:

```rust
// Importe (via `use`) o módulo `fmt` para disponibilizá-lo.
use std::fmt;

// Defina uma estrutura para cada `fmt::Display` ser implementado. Isso é
// uma tupla chamada `Structure` que contém um `i32`.
struct Structure(i32);

// Para usar o marcador `{}`, a trait `fmt::Display` deve ser implementada
// manualmente para o tipo.
impl fmt::Display for Structure {
    // Essa trait precisa do `fmt` com essa assinatura exata.
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Escreva estritamente o primeiro elemento dentro da saída fornecida
        // stream: `f`. Retorna `fmt::Result` que indica se a
        // operação foi bem sucedida ou falhou. Observe que `write!` usa uma sintaxe
        // que é muito similar com `println!`.
        write!(f, "{}", self.0)
    }
}
```
<!-- 
`fmt::Display` may be cleaner than `fmt::Debug` but this presents
a problem for the `std` library. How should ambiguous types be displayed?
For example, if the `std` library implemented a single style for all
`Vec<T>`, what style should it be? Would it be either of these two?

* `Vec<path>`: `/:/etc:/home/username:/bin` (split on `:`)
* `Vec<number>`: `1,2,3` (split on `,`)

No, because there is no ideal style for all types and the `std` library
doesn't presume to dictate one. `fmt::Display` is not implemented for `Vec<T>`
or for any other generic containers. `fmt::Debug` must then be used for these
generic cases.

This is not a problem though because for any new *container* type which is
*not* generic,`fmt::Display` can be implemented.

```rust,editable
use std::fmt; // Import `fmt`

// A structure holding two numbers. `Debug` will be derived so the results can
// be contrasted with `Display`.
#[derive(Debug)]
struct MinMax(i64, i64);

// Implement `Display` for `MinMax`.
impl fmt::Display for MinMax {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Use `self.number` to refer to each positional data point.
        write!(f, "({}, {})", self.0, self.1)
    }
}
 -->


`fmt::Display` pode ser mais limpo que `fmt::Debug` mas isso apresenta
um problema para a biblioteca `std`. Como tipos ambíguos podem ser implementados?
Por exemplo, se a biblioteca `std` implementa um único estilo para todos
`Vec<T>`, que estilo será? Seria um desses dois?

* `Vec<path>`: `/:/etc:/home/username:/bin` (Divida em `:`)
* `Vec<number>`: `1,2,3` (Divida em `,`)

Não, porque não é um estilo ideal para todos os tipos e na biblioteca `std`
não presume-se ditar um. `fmt::Display` não é implementando para `Vec<T>`
ou para qualquer outro recipiente genérico. `fmt::Debug` deve ser usado para esses casos genéricos.

Isso não é um problema até porque para qualquer novo tipo *recipiente* que
*não* é genérico,`fmt::Display` pode ser implementado.

```rust, editável
use std::fmt; // Importe `fmt`

// A estrutura guarda dois números. `Debug` será derivado para que os resultados possam
// ser contrastados com `Display`.
#[derive(Debug)]
struct MinMax(i64, i64);

// Implemente `Display` para `MinMax`.
impl fmt::Display for MinMax {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Use `self.number` para se referir a cada ponto de dados posicional.
        write!(f, "({}, {})", self.0, self.1)
    }
}

<!-- 
// Define a structure where the fields are nameable for comparison.
#[derive(Debug)]
struct Point2D {
    x: f64,
    y: f64,
}

// Similarly, implement `Display` for `Point2D`
impl fmt::Display for Point2D {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Customize so only `x` and `y` are denoted.
        write!(f, "x: {}, y: {}", self.x, self.y)
    }
}

fn main() {
    let minmax = MinMax(0, 14);

    println!("Compare structures:");
    println!("Display: {}", minmax);
    println!("Debug: {:?}", minmax);

    let big_range =   MinMax(-300, 300);
    let small_range = MinMax(-3, 3);

    println!("The big range is {big} and the small is {small}",
             small = small_range,
             big = big_range);

    let point = Point2D { x: 3.3, y: 7.2 };

    println!("Compare points:");
    println!("Display: {}", point);
    println!("Debug: {:?}", point);

    // Error. Both `Debug` and `Display` were implemented, but `{:b}`
    // requires `fmt::Binary` to be implemented. This will not work.
    // println!("What does Point2D look like in binary: {:b}?", point);
}

So, `fmt::Display` has been implemented but `fmt::Binary` has not, and
therefore cannot be used. `std::fmt` has many such [`traits`][traits] and
each requires its own implementation. This is detailed further in
[`std::fmt`][fmt].
``` -->


// Definir uma estrutura em que os campos sejam nomeados para comparação.
#[derive(Debug)]
struct Point2D {
    x: f64,
    y: f64,
}

// Igualmente, implemente `Display` por `Point2D`
impl fmt::Display for Point2D {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Personalize para que apenas `x` e `y` sejam denotados.
        write!(f, "x: {}, y: {}", self.x, self.y)
    }
}

fn main() {
    let minmax = MinMax(0, 14);

    println!("Compare estruturas:");
    println!("Display: {}", minmax);
    println!("Debug: {:?}", minmax);

    let big_range =   MinMax(-300, 300);
    let small_range = MinMax(-3, 3);

    println!("A mairo faixa é {big} e a menor é {small}",
             small = small_range,
             big = big_range);

    let point = Point2D { x: 3.3, y: 7.2 };

    println!("Compare pontos:");
    println!("Display: {}", point);
    println!("Debug: {:?}", point);

    // Erro. Ambos `Debug` e `Display` foram implementados, mas `{:b}`
    // necessita implementar `fmt::Binary`. Isso não vai funcionar.
    // println!("Como o Point2D se parece em binário: {:b}?", point);
}
```
Então, `fmt::Display` foi implementando mas `fmt::Binary` não, e
portanto não pode ser usado. `std::fmt` tem muitas [`traits`][traits] e
cada uma necessita de sua própria implementação. Isso é detalhado mais adiante em
[`std::fmt`][fmt].

<!-- ### Activity

After checking the output of the above example, use the `Point2D` struct as a
guide to add a Complex struct to the example. When printed in the same
way, the output should be:

```txt
Display: 3.3 + 7.2i
Debug: Complex { real: 3.3, imag: 7.2 }
``` -->

### Atividade

Depois de checar a saída do exemplo acima, use a estrutura `Point2D` como um
guia para adicionar estruturas mais complexas ao exemplo. Quando impresso da mesma
maneira, a saída pode ser:

```txt
Display: 3.3 + 7.2i
Debug: Complex { real: 3.3, imag: 7.2 }
```


<!-- ### See also:

[`derive`][derive], [`std::fmt`][fmt], [macros], [`struct`][structs],
[`trait`][traits], and [use][use]

[derive]: ../../trait/derive.md
[fmt]: https://doc.rust-lang.org/std/fmt/
[macros]: ../../macros.md
[structs]: ../../custom_types/structs.md
[traits]: ../../trait.md
[use]: ../../mod/use.md
 -->

 ### Veja também:

[`derive`][derive], [`std::fmt`][fmt], [macros], [`struct`][structs],
[`trait`][traits], e [use][use]

[derive]: ../../trait/derive.md
[fmt]: https://doc.rust-lang.org/std/fmt/
[macros]: ../../macros.md
[structs]: ../../custom_types/structs.md
[traits]: ../../trait.md
[use]: ../../mod/use.md
