# Modern C++ insight & reflection

This project is a great example of how code may be made more efficient and clean using contemporary C++ features. Utilising `constexpr` for the character array was one of the wise decisions. it locks the permitted symbols at compile time, allowing the compiler to optimise and preventing unintentional mutations. `constexpr` is a powerful keyword introduced in C++11 and expanded in later standards, and it plays a key role in modern C++ programming. It tells the compiler that a value or function can  be evaluated at compile time rather than at runtime. This leads to faster execution, lower memory usage, and fewer runtime errors, especially when used correctly.
In my project, I have used `constexpr` to define the `allowedCharacters` array:

```cpp
constexpr static wchar_t allowedCharacters[] = {
    L'1', L'2', L'3', L'4', L'5', L'6', L'7', L'8', L'9', L'0', L' ', L' ', L' ', L' ',
    L'a', L'b', L'c', L'd', L'e', L'f', L'g', L'h', L'j', L'k', L'l',
    L'Ƣ', L'Ʃ', L'Ʊ', L'Ƹ', L'ǂ', L'ƽ', L'ǌ', L'Ȣ', L'Ⱦ', L'Ƚ', L'ɑ', L'ɤ', L'ʑ',
    L'ʫ', L'ʥ', L'ʮ', L'λ', L'ε', L'Ϡ', L'Ϟ', L'Ϡ', L'ϰ', L'Є'
};
```

In modern C++, `constexpr` is a way to clearly express the intent of telling the compiler that these values are fixed and known in advance.

Additionally, memory handling became safer and more versatile by using `std::vector` to store raindrop symbols rather than raw arrays. Everything is kept organised and manageable by the code's clean division into classes like `Raindrop` and `MatrixRain`. For instance, `MatrixRain` manages the overall control, rendering, and user input, whereas `Raindrop` concentrates just on symbol production and movement.

I also used `std::this_thread::sleep_for` and `<chrono>` to manage the animation speed in a more modern and type-safe way compared to old-style delays. Simple additions like control flags for `paused` and `running` and static helper functions for symbol creation (`getRandomSymbol()`) keep the logic simple without adding unnecessary complexity. Additionally, it was a conscious decision to make the visual output more dynamic, even though I used Windows-specific APIs for colour changes and pointer movement.  So overall, the code is not just functional—it shows how thoughtful use of modern C++ can lead to better structure, safety, and performance.
