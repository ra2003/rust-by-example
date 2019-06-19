# Debug

Все типы, которые будут использовать `типажи (traits)` форматирования `std::fmt` требуют
их реализации для возможности печати. Автоматическая реализация предоставлена только для
типов из `стандартной библиотеки (std)`. Все остальные типы *должны* иметь собственную реализацию.

C помощью `типажа` `fmt::Debug` это сделать очень просто. *Все* типы могут
`выводить` (автоматически создавать) реализацию `fmt::Debug`.
Сделать подобное с `fmt::Display` невозможно, он должен быть реализован вручную.

```rust
// Эта структура не может быть напечатана с помощью `fmt::Display`
// или с помощью `fmt::Debug`
struct UnPrintable(i32);

// Атрибут `derive` автоматически реализует
// необходимые методы, чтобы была возможность
// печатать данную `структуру` с помощью `fmt::Debug`.
#[derive(Debug)]
struct DebugPrintable(i32);
```

Все типы в `стандартной библиотеке (std)` могут быть напечатаны с `{:?}`:

```rust,editable
// Вывод и реализация `fmt::Debug` для `Structure`.
// `Structure` - это структура, которая содержит в себе один `i32`.
#[derive(Debug)]
struct Structure(i32);

// Добавим структуру `Structure` в структуру `Deep`.
// Реализуем для `Deep` возможность вывода с помощью fmt::Debug`.
#[derive(Debug)]
struct Deep(Structure);

fn main() {
    // Вывод с помощью `{:?}` аналогичен `{}`.
    println!("{:?} месяцев в году.", 12);
    println!("{1:?} {0:?} - это имя {actor:?}.",
             "Слэйтер",
             "Кристиан",
             actor="актёра");

    // `Structure` теперь можно напечатать!
    println!("Теперь {:?} будет выведена на экран!", Structure(3));

    // Проблема с `выводом (derive)`, в том, что у нас не будет контроля
    // над тем, как будет выглядеть результат.
    // Что если мы хотим напечатать просто `7`?
    println!("А теперь напечатаем {:?}", Deep(Structure(7)));
}
```

Так что 'fmt:: Debug' определенно делает это для печати, но жертвует некоторыми
изящество. Rust также обеспечивает "красивую печать " с помощью" {:#?}'.

```rust,editable
#[derive(Debug)]
struct Person<'a> {
    name: &'a str,
    age: u8
}

fn main() {
    let name = "Peter";
    let age = 27;
    let peter = Person { name, age };

    // Pretty print
    println!("{:#?}", peter);
}
```

Можно вручную реализовать 'fmt:: Display' для управления отображением.

### Смотрите также

[атрибуты][attributes], [`derive`][derive], [`std::fmt`][fmt],
and [`структуры`][structs]

[attributes]: https://doc.rust-lang.org/reference/attributes.html
[derive]: trait/derive.html
[fmt]: https://doc.rust-lang.org/std/fmt/
[structs]: custom_types/structs.html
