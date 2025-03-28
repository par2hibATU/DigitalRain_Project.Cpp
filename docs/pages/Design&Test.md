
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
