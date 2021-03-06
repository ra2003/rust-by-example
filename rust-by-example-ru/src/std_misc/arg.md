# Аргументы программы

## Стандартная библиотека

Аргументы командной строки могут быть доступны при помощи 
`std::env::args`, который возвращает итератор, который 
выдаёт `String` для каждого аргумента:

```rust,editable
use std::env;

fn main() {
    let args: Vec<String> = env::args().collect();

    // Первый аргумент - путь, используемый для вызова программы.
    println!("Мой путь {}.", args[0]);

    // Оставшиеся аргументы - переданные в командной строке параметры.
    // Вызов программы выглядит так:
    //   $ ./args arg1 arg2
    println!("У меня {:?} аргумента: {:?}.", args.len() - 1, &args[1..]);
}
```

```shell
$ ./args 1 2 3
Мой путь ./args.
У меня 3 аргумента: ["1", "2", "3"].
```

## Крейты

В качестве альтернативы, существует несколько крейтов, которые 
предоставляют дополнительную функциональность при создании 
приложений командной сроки. [Rust Cookbook](https://rust-lang-nursery.github.io/rust-cookbook/cli/arguments.html) показывает 
лучшие практики, как использовать один из самых популярных 
крейтов для аргументов командной строки, `clap`.
