# Olá mundo

<!-- This is the source code of the traditional Hello World program. -->
Este é o código fonte do tradicional Olá mundo.

<!-- ```rust,editable
// This is a comment, and is ignored by the compiler
// You can test this code by clicking the "Run" button over there ->
// or if you prefer to use your keyboard, you can use the "Ctrl + Enter" shortcut

// This code is editable, feel free to hack it!
// You can always return to the original code by clicking the "Reset" button ->

// This is the main function
fn main() {
    // Statements here are executed when the compiled binary is called

    // Print text to the console
    println!("Hello World!");
}
``` -->
```rust, editável
// Isso é um comentário, e é ignorado pelo compilador
// Você pode testar esse código clicando no botão executar "Run", aqui ->
// ou se você preferir usar seu teclado, você pode usar o atalho "Ctrl + Enter"

// Este código é editável, sinta-se livre para muda-lo
// Você sempre pode retornar ao código original clicando no botão de resetar "Reset" ->

// Esta é a função principal
fn main() {
    // As declarações aqui são executadas quando o binário compilado é chamado

    // Escreva o texto para o console
    println!("Olá mundo!");
}
```
<!-- 
`println!` é um [*macro*][macros] that prints text to the
console.
 -->
`println!` é um [*macro*][macros] que escreve o texto no console.

<!-- A binary can be generated using the Rust compiler: `rustc`. -->
Um binário pode ser gerado usando o compilador do Rust: `rustc`.

```bash
$ rustc hello.rs
```

<!-- `rustc` will produce a `hello` binary that can be executed. -->
`rustc` produzirá um binário `hello` que pode ser executado.

<!-- ```bash
$ ./hello
Hello World!
``` -->

```bash
$ ./hello
Olá mundo!
```

<!-- ### Activity -->
### Atividade
<!-- 
Click 'Run' above to see the expected output. Next, add a new
line with a second `println!` macro so that the output
shows:

```text
Hello World!
I'm a Rustacean!
```
 -->
 
Clique no executar "Run" acima para ver a saída experada. Depois, adicione uma nova linha com um segundo macro `println!` para que a saída mostre:

```text
Olá mundo!
Eu sou um rustáceo!
```

[macros]: macros.md
