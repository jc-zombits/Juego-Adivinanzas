# Procesando una Suposición

- La primera parte del programa del juego de adivinanzas, solicitará la entrada del usuario, procesará esa entrada y comprobará que esté en el formato adecuado. Para comenzar, permitiremos que el usuario ingrese una suposición.
> CodeExample:
use std::io;

fn main() {
    println!("Guess the number!");

    println!("Please input your guess.");

    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    println!("You guessed: {}", guess);
}


> La entrada **let mut guess = String::new();** ha creado una variable mutable que actualmente está vinculada a una nueva instancia vacía de **String**.

- Recibir entrada de usuario
> Recordemos que hemos incluido la funcionalidad de *entrada/salida* de la biblioteca standar **sdt::io;** en la primera línea. Ahora llamamos la función **stdin** desde el módulo **io** que permitirá gestionar la entrada del usuario.

> La línea **read_line(&mut guess)** llama al método *read_line* en el controlador de entrada estandar para obtener la entrada del usuario. También le pasamos **&mut guess** como argumento de *read_line* para indicarle en que cadena almacena la entrada del usuario.

> El **&** indica que este argumento es una referencia, lo que permite que varias partes del código accedan a una pieza de datos sin necesidad de copiar esos datos en la memoria varias veces.
> Como las referencias al igual que las variables son inmutables, por eso escribimos **&mut** para hacer que sea mutable.

# Generando un número secreto

- Para usar *rand* dentro del programa primero debemos darle a cargo la dependencia del mismo para así la pueda usar. Por lo que debemos modificar el arvhibo Cargo.toml.

# Generando un número aleatorio
> ExampleCode:

use std::io;
use rand::Rng;

fn main() {
    println!("Guess the number!");

    let secret_number = rand::thread_rng().gen_range(1..=100);

    println!("The secret number is: {secret_number}");

    println!("Please input your guess.");

    let mut guess = String::new();

    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    println!("You guessed: {guess}");
}

> Primero agregamos la línea **use rand::Rng();**
> *Rng* define los métodos que implementan los generadores de números aleatorios y este atributo debe estar dentro del alcance para poder usar esos métodos.
> La siguiente línea que agregamos **rand::thread_rng()** es una función que nos proporciona el generador de números aleatorios particular que vamos a utilizar.
> Luego llamamos al **gen_range** método en el generador de números aleatorios. Este toma una expresión de rango como argumento y genera un número aleatorio en el rango.
> El tipo de expresión de rango que estamos utilizando toma la forma **start..=end** y es inclusivo en los límites inferior y superior.

# Comparando la suposición con el número secreto

> CodeExample:

use rand::Rng;
use std::cmp::Ordering;
use std::io;

fn main() {
    // --snip--

    println!("You guessed: {guess}");

    match guess.cmp(&secret_number) {
        Ordering::Less => println!("Too small!"),
        Ordering::Greater => println!("Too big!"),
        Ordering::Equal => println!("You win!"),
    }
}

