
# Design and Testing
This project follows a modular and object-oriented design paradigm, splitting responsibilities across different classes and utility namespaces. The three main components are:

 - **Raindrop class** – Models a single stream of falling characters.
 - **MatrixRain class** – Controls all raindrops, animation logic, and user input.
 - **ConsoleUtils namespace** – Manages low-level console behaviors (cursor movement and visibility).

An effective and interactive terminal-based animation loop is made possible by the combination of these elements.

## Character Selection
To maintain consistency, reduce runtime overhead, and prevent accidental modification, the available symbols for rain rendering are defined as a **compile-time constant** using `constexpr`
> **constexpr** static wchar_t allowedCharacters[]

 - Wide Unicode character support is ensured by using wchar_t, enabling a vast range of symbols.
 - By ensuring that this array is evaluated at compile time, constexpr enhances both efficiency and security.

> wchar_t Raindrop::getRandomSymbol() {
    return allowedCharacters[rand() % (sizeof(allowedCharacters) / sizeof(wchar_t))];
}

This design ensures that character retrieval during animation


## Raindrop Class 
Each falling stream is an instance of the Raindrop class, initialized with random characters sequences. 
> Raindrop::Raindrop(int x, int y, int length) : x(x), y(y), length(length) 

This uses an initializer list to initialize the object's properties.
> void Raindrop::update()


The update() function advances the y-position of each stream cyclically using module % arithmetic.
> void Raindrop::draw() 

The draw() method renders characters using randomized colour shades.

## MatrixRain Class 
The MatrixRain class orchestrates the overall simulation.
> void MatrixRain::initializeRaindrops()

This streams are initialized randomly across screen columns and each raindrop has a random position and length.
> void MatrixRain::start()

This runs the main animation loop and renders raindrops continuously unless paused. It waits for a certain amount of time and handles user input.
>void MatrixRain::stop()

Stops the animation and resets the console cursor.
>void MatrixRain::handleInput()

This function reads the keyboard input using `_kbhit()` and `_getch()`
