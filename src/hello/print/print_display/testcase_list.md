<!-- # Testcase: List

Implementing `fmt::Display` for a structure where the elements must each be
handled sequentially is tricky. The problem is that each `write!` generates a
`fmt::Result`. Proper handling of this requires dealing with *all* the
results. Rust provides the `?` operator for exactly this purpose.

Using `?` on `write!` looks like this:

```rust,ignore
// Try `write!` to see if it errors. If it errors, return
// the error. Otherwise continue.
write!(f, "{}", value)?;
```

Alternatively, you can also use the `try!` macro, which works the same way. 
This is a bit more verbose and no longer recommended, but you may still see it in
older Rust code. Using `try!` looks like this:

```rust,ignore
try!(write!(f, "{}", value));
```

With `?` available, implementing `fmt::Display` for a `Vec` is
straightforward: -->
# Casos de teste: Listas

Implementando `fmt::Display` para uma estrutura onde cada um dos elementos deve ser 
manipulado sequencialmente é complicado. O problema é que cada `write!` gera um
`fmt::Result`. A manuseio adequedo disso exige lidar com todos os *results*.
Rust fornece o operador `?` exatamente para esse propósito .

Usando `?` no `write!` se parece com isso:

```rust, ignore
// Tente `write!` para ver se há erros. Se tiver erros, retorne
// o erro. De outra forma, continue.
write!(f, "{}", value)?;
```

Alternativamente, você também pode usar a macro `try!`, que trabalha da mesma maneira. 
Isso é um pouco menos detalhado e não é mais recomendado, mas você ainda poode ver em
códigos Rust antigos. Usando `try!` se parece com isso:

```rust,ignore
try!(write!(f, "{}", value));
```

Com `?` disponível, implementar `fmt::Display` para um `Vec` é
simples:
```rust,editable
use std::fmt; // Importe o módulo `fmt`.

// Defina uma estrutura chamada `List` contendo um `Vec`.
struct List(Vec<i32>);

impl fmt::Display for List {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        // Extrai o valor usando a indexão de tupla,
        // e crie uma referência para `vec`.
        let vec = &self.0;

        write!(f, "[")?;

        // Itere sobre `v` em `vec` enquanto enumera a iteração
        // count em `count`.
        for (count, v) in vec.iter().enumerate() {
            // Para cada elemento exceto o primeiro, adicione vírgula.
            // Use o operador ?, or *try!*, para retornar erros.
            if count != 0 { write!(f, ", ")?; }
            write!(f, "{}", v)?;
        }

        // Feche as chaves abertas e retorne um valor fmt::Result.
        write!(f, "]")
    }
}

fn main() {
    let v = List(vec![1, 2, 3]);
    println!("{}", v);
}
```

<!-- ### Activity

Try changing the program so that the index of each element in the vector is also printed. The new output should look like this:

```rust,ignore
[0: 1, 1: 2, 2: 3]
```

### See also:

[`for`][for], [`ref`][ref], [`Result`][result], [`struct`][struct],
[`?`][q_mark], and [`vec!`][vec]

[for]: ../../../flow_control/for.md
[result]: ../../../std/result.md
[ref]: ../../../scope/borrow/ref.md
[struct]: ../../../custom_types/structs.md
[q_mark]: ../../../std/result/question_mark.md
[vec]: ../../../std/vec.md
 -->

 ### Atividade

Tente mudar o programa para que o índice de cada elemento no vetor também seja exibido. A nova saída se parece com isso:

```rust,ignore
[0: 1, 1: 2, 2: 3]
```

### Veja também:

[`for`][for], [`ref`][ref], [`Result`][result], [`struct`][struct],
[`?`][q_mark], and [`vec!`][vec]

[for]: ../../../flow_control/for.md
[result]: ../../../std/result.md
[ref]: ../../../scope/borrow/ref.md
[struct]: ../../../custom_types/structs.md
[q_mark]: ../../../std/result/question_mark.md
[vec]: ../../../std/vec.md
