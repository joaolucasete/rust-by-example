<!-- # Comments -->
# Comentários

<!-- Any program requires comments, and Rust supports
a few different varieties: -->
Qualquer programa precisa de comentários, e Rust suporta algumas variedades diferentes:
<!--  
* *Regular comments* which are ignored by the compiler:
   * `// Line comments which go to the end of the line.`
   * `/* Block comments which go to the closing delimiter. */`
* *Doc comments* which are parsed into HTML library
  [documentation][docs]:
   * `/// Generate library docs for the following item.`
   * `//! Generate library docs for the enclosing item.`
 -->

 
* *Comentários regulares* são ignorados pelo compilador:
   * `// Comentário de linha que vai até o final da linha.`
   * `/* Comentário de bloco que vai até o fechamento do delimitador. */`
* *Comentários de documentação* são analisados na biblioteca html
  [documentação][docs]:
   * `/// Gere documentos da biblioteca para o seguinte item.`
   * `//! Gere documentos da biblioteca para o item anexo.`


<!-- ```rust,editable
fn main() {
    // This is an example of a line comment
    // There are two slashes at the beginning of the line
    // And nothing written inside these will be read by the compiler

    // println!("Hello, world!");

    // Run it. See? Now try deleting the two slashes, and run it again.

    /* 
     * This is another type of comment, a block comment. In general,
     * line comments are the recommended comment style. But
     * block comments are extremely useful for temporarily disabling
     * chunks of code. /* Block comments can be /* nested, */ */
     * so it takes only a few keystrokes to comment out everything
     * in this main() function. /*/*/* Try it yourself! */*/*/
     */

    /*
    Note: The previous column of `*` was entirely for style. There's
    no actual need for it.
    */

    // You can manipulate expressions more easily with block comments
    // than with line comments. Try deleting the comment delimiters
    // to change the result:
    let x = 5 + /* 90 + */ 5;
    println!("Is `x` 10 or 100? x = {}", x);
}

``` -->
```rust, editável
fn main() {
    // Esse é um exemplo de comentário de linha
    // Existem duas barras no início da linha
    // E nada escrito dentros dessas será lido pelo compilador.

    // println!("Olá, mundo!");

    // Execute isso. Vê? Agora tente deletar as duas barras, e execute denovo.

    /* 
     * Esse é outro tipo de comentário, um comentário de bloco. E geral,
     * comentários de linha são o estilo de comentário recomendado. mas
     * comentários de bloco são extremamente úteis para desativar temporariamente
     * pedaços de código. /* Comentários de blocos podem ser /* aninhados, */ */
     * portanto são necessários apenas algumas tecla para comentar tudo
     * nesta função main(). /*/*/* Tente você mesmo! */*/*/
     */

    /*
    Observe: A coluna anterior de `*` era inteiramente de estilo.
    Não há necessidade atual para isso.
    */

    // Você pode manipular mais facilmente expressões com comentário de bloco
    // do que com comentário de linha. Tente excluir os delimitadores de comentário
    // para mudar o resultado:
    let x = 5 + /* 90 + */ 5;
    println!("`x` é 10 ou 100? x = {}", x);
}

```

<!-- ### See also:

[Library documentation][docs]

[docs]: ../meta/doc.md -->
### Veja também:

[Documentação da biblioteca][docs]

[docs]: ../meta/doc.md
