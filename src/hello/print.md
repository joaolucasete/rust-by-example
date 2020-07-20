<!-- # Formatted print

Printing is handled by a series of [`macros`][macros] defined in [`std::fmt`][fmt]
some of which include:

* `format!`: write formatted text to [`String`][string]
* `print!`: same as `format!` but the text is printed to the console (io::stdout).
* `println!`: same as `print!` but a newline is appended.
* `eprint!`: same as `format!` but the text is printed to the standard error (io::stderr).
* `eprintln!`: same as `eprint!`but a newline is appended.

All parse text in the same fashion. As a plus, Rust checks formatting
correctness at compile time. -->

# Prints formatados

Print é feito por uma série de [`macros`][macros] definidos em [`std::fmt`][fmt]
alguns dos quais incluem:

* `format!`: escreva um texto formatados para [`String`][string]
* `print!`: igual a `format!` mas o texto é impresso no terminal (io::stdout).
* `println!`: igual a `print!` mas uma nova linha é anexada.
* `eprint!`: igual a `format!` mas o texto é impresso com o padrão de erros (io::stderr).
* `eprintln!`: igual a `eprint!` mas uma nova linha é anexada.

Todos analisam o texto da mesma maneira. Como um acréscimo, Rust verifica a correção de formatação em tempo de compilação.

<!-- 
```rust,editable,ignore,mdbook-runnable
fn main() {
    // In general, the `{}` will be automatically replaced with any
    // arguments. These will be stringified.
    println!("{} days", 31);

    // Without a suffix, 31 becomes an i32. You can change what type 31 is
    // by providing a suffix. The number 31i64 for example has the type i64.

    // There are various optional patterns this works with. Positional
    // arguments can be used.
    println!("{0}, this is {1}. {1}, this is {0}", "Alice", "Bob");

    // As can named arguments.
    println!("{subject} {verb} {object}",
             object="the lazy dog",
             subject="the quick brown fox",
             verb="jumps over");

    // Special formatting can be specified after a `:`.
    println!("{} of {:b} people know binary, the other half doesn't", 1, 2);

    // You can right-align text with a specified width. This will output
    // "     1". 5 white spaces and a "1".
    println!("{number:>width$}", number=1, width=6);

    // You can pad numbers with extra zeroes. This will output "000001".
    println!("{number:>0width$}", number=1, width=6);

    // Rust even checks to make sure the correct number of arguments are
    // used.
    println!("My name is {0}, {1} {0}", "Bond");
    // FIXME ^ Add the missing argument: "James"

    // Create a structure named `Structure` which contains an `i32`.
    #[allow(dead_code)]
    struct Structure(i32);

    // However, custom types such as this structure require more complicated
    // handling. This will not work.
    println!("This struct `{}` won't print...", Structure(3));
    // FIXME ^ Comment out this line.
}
``` -->

```rust, editável, ignore , mdbook executável
fn main() {
    // Em geral, o `{}`será automaticamente trocado com qualquer
    // argumento. Estes serão especificados.
    println!("{} dias", 31);

    // com um sufixo, 31 torna-se um i32. Você pode alterar o tipo de 31
    // fornecendo um sufixo. O número 31i64 por exemplo tem o tipo i64.

    // Existem vários padrões opcionais para trabalhar com isso.
    // Argumentos posicionais podem ser usados.
    println!("{0}, este é {1}. {1}, está é {0}", "Alice", "Bob");

    // Pode nomear argumentos.
    println!("{sujeito} {verbo} {objeto}",
             sujeito="o cachorro preguiçoso",
             objeto="a rápida raposa marrom",
             verbo="pula sobre");

    // Formatação especial pode ser especificada após um `:`.
    println!("{} de {:b} pessoas sabem binário, a outra metade não", 1, 2);

    // Você pode alinhar o texto à direita com uma largura especificada. Isso produzirá
    // "     1". 5 espaços em braco e "1".
    println!("{number:>width$}", number=1, width=6);

    // Você pode preencher números com zeros extras. Isso produzirá "000001".
    println!("{number:>0width$}", number=1, width=6);

    // Rust verifica até para garantir que o número corretos de argumentso seja usado
    println!("Meu nome é {0}, {1} {0}", "Bond");
    // FIXME ^ Add the missing argument: "James"

    // Crie uma estrutura chamada `Structure` que contém um `i32`.
    #[allow(dead_code)]
    struct Structure(i32);

    // Entretando, tipos personalizados como essa estrutura exigem procedimentos mais complicados.
    // Isso não vai funcionar.
    println!("Essa estrutura `{}` não imprime...", Structure(3));
    // FIXME ^ Comment out this line.
}
```
<!-- 
[`std::fmt`][fmt] contains many [`traits`][traits] which govern the display
of text. The base form of two important ones are listed below:

* `fmt::Debug`: Uses the `{:?}` marker. Format text for debugging purposes.
* `fmt::Display`: Uses the `{}` marker. Format text in a more elegant, user
friendly fashion.

Here, we used `fmt::Display` because the std library provides implementations
for these types. To print text for custom types, more steps are required.

Implementing the `fmt::Display` trait automatically implements the
[`ToString`] trait which allows us to [convert] the type to [`String`][string].
 -->


[`std::fmt`][fmt] contém algumas [`traits`][traits] que mandam na exibição de texto.
A forma básica de duas traits importantes estão abaixo.

* `fmt::Debug`: Usa o marcador `{:?}`. Formata o texto para propósitos de debug.
* `fmt::Display`: Usa o marcador `{}`. Formata em um texto mais elegante, um
modo mais amigável para o usuário.

Aqui, nós usamos `fmt::Display` porque o biblioteca std fornece implementações
para esses tipos. Para imprimir o texto para tipos personalizados, mais etapas são necessárias.

A Implementação da trait `fmt::Display` automaticamente implementa a trait [`ToString`]
que permite nós [convertemos][convert] o tipo para [`String`][string].

<!-- 
### Activities

 * Fix the two issues in the above code (see FIXME) so that it runs without
   error.
 * Add a `println!` macro that prints: `Pi is roughly 3.142` by controlling
   the number of decimal places shown. For the purposes of this exercise,
   use `let pi = 3.141592` as an estimate for pi. (Hint: you may need to
   check the [`std::fmt`][fmt] documentation for setting the number of
   decimals to display) -->
   
### Atividades

 * Resolva os dois problemas no código acima (veja FIXME) para que funcione sem erros.
 * Adicione uma macro `println!` que imprima: `Pi é aproximadamente 3.142` controlando
   o números de casas decimais mostradas. Para o propósito desse exercício,
   use `let pi = 3.141592` como um estimado para pi. (Sugestão: Você pode precisar
   checar a documentação de [`std::fmt`][fmt] para configurar a quantidade de
   decimais mostrados)

### See also:

[`std::fmt`][fmt], [`macros`][macros], [`struct`][structs],
and [`traits`][traits]

[fmt]: https://doc.rust-lang.org/std/fmt/
[macros]: ../macros.md
[string]: ../std/str.md
[structs]: ../custom_types/structs.md
[traits]: https://doc.rust-lang.org/std/fmt/#formatting-traits
[`ToString`]: https://doc.rust-lang.org/std/string/trait.ToString.html
[convert]: ../conversion/string.md
