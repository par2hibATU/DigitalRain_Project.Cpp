[Home](/index.md)

# Algorithm

<img src="https://raw.githubusercontent.com/par2hibATU/DigitalRain_Project.Cpp/main/docs/assets/images/33.png" width="650" height="300">


<img src="https://raw.githubusercontent.com/par2hibATU/DigitalRain_Project.Cpp/main/docs/assets/images/Screenshot 2025-04-04 042058.png" width="650" height="300">

### The program begins execution in main(). 

<img src="https://raw.githubusercontent.com/par2hibATU/DigitalRain_Project.Cpp/main/docs/assets/images/20.png" width="650" height="300">

- **Unicode Mode**: Wide character mode ensures complex Unicode symbols display properly.
    
- **Cursor Handling**: Prevents distraction by removing the blinking prompt.

<img src="https://raw.githubusercontent.com/par2hibATU/DigitalRain_Project.Cpp/main/docs/assets/images/21.png" width="650" height="300">

This sets the speed of the frame which is 100 milliseconds. start() starts the rain and stops()  just stops the animation and resets the console cursor.

<img src="https://raw.githubusercontent.com/par2hibATU/DigitalRain_Project.Cpp/main/docs/assets/images/Screenshot 2025-04-04 041743.png" width="650" height="300">

This sets the screen height and width. This method is called when the rain starts.
```
srand(static_cast<unsigned int>(time(0)));
```
This seeds the random number generator so raindrops are not always the same each time when program restarted.
```
for (int i = 0; i < screenWidth / 2; ++i) {
    rainStreams.emplace_back(rand() % screenWidth, rand() % screenHeight, rand() % 10 + 5);
}
```
This `for` loop through and each iteration randomly pick an x and y position with a length (random) and create a `Raindrop` and pushed into the `rainStream` vector.
But if things go wrong; for example- `emplace_back()` allocates memory. If the system is under pressure or screenWidth is crazy big, then allocation can fail, throwing error.
```
} catch (const std::exception& e) {
    std::wcerr << L"Error initializing raindrops: " << e.what() << L"\n";
    running = false;
}
```
To cope with such errors, `Exceptions` comes to the scene and handle the error with meaningful message so that the we can catch the problem and fix it as soon as possible.


<img src="https://raw.githubusercontent.com/par2hibATU/DigitalRain_Project.Cpp/main/docs/assets/images/23.png" width="650" height="300">

This randomly places multiple raindrops across the screen and each raindrop has a random position and length. A random length between 5 and 14 characters.

<img src="https://raw.githubusercontent.com/par2hibATU/DigitalRain_Project.Cpp/main/docs/assets/images/24.png" width="650" height="300">

This function picks a random characters from allowedCharacters and ensures variety in raindrop symbols. 
`rand()` generates a random number between 0 and RAND_MAX. This modulus operator `%` ensures that the result is within a valid index of the array.
`rand() % 50` , `32145` then `32145 % 50 = 45`. Since `% 50` guarantees values from 0 to 49, it ensures that we only pick a valid index from `allowedCharacters`. 

<img src="https://raw.githubusercontent.com/par2hibATU/DigitalRain_Project.Cpp/main/docs/assets/images/25.png" width="650" height="300">

This constructor fills the stream with characters using this function.

<img src="https://raw.githubusercontent.com/par2hibATU/DigitalRain_Project.Cpp/main/docs/assets/images/26.png" width="650" height="300">

In every frame, this function check paused state and if the function is not paused it renders frame and process keyboard input. 

<img src="https://raw.githubusercontent.com/par2hibATU/DigitalRain_Project.Cpp/main/docs/assets/images/27.png" width="650" height="300">

This function calls `update()` and `draw()` function where `update()` function:

This function is responsible  for visually rendering a single character of a raindrop at a specific `(x, y)` position on the console screen, with a randomly chosen colour.
```
void Raindrop::draw() const {
    HANDLE hConsole = GetStdHandle(STD_OUTPUT_HANDLE);
    ConsoleUtils::setCursorPosition(x, y);
```
This functions get the Console Handle and set the Cursor to Raindrop position. This ensures that the character is printed at the right location on the screen.
```
int color;
int randVal = rand() % 3;
if (randVal == 0)
    color = FOREGROUND_GREEN | FOREGROUND_INTENSITY;  // Bright green
else if (randVal == 1)
    color = FOREGROUND_GREEN;  // Darker green
else
    color = FOREGROUND_GREEN | FOREGROUND_BLUE;  // Bluish-green
```
This block adds colour diversity to the rain effect. It randomly chooses one of 3 greenish shades and the combinations are made using Windows Console API flags.

```
SetConsoleTextAttribute(hConsole, color);
```
Then this sets the current console text colour and any character printed afterward uses this colour.
```
std::wcout << symbols[rand() % symbols.size()];
SetConsoleTextAttribute(hConsole, 7); // Reset to default color
```
This logic here randomly  pick one of its characters to print on each frame and this adds dynamic randomness. This randomness makes the rain constantly change as it falls, contributing to the illusion of activity. Finally the `SetConsoleTextAttribute` resets the console colour to the system default.

<img src="https://raw.githubusercontent.com/par2hibATU/DigitalRain_Project.Cpp/main/docs/assets/images/28.png" width="650" height="300">

This increments the y-position of the drop and wraps around if it reaches the bottom and `draw()` function:

<img src="https://raw.githubusercontent.com/par2hibATU/DigitalRain_Project.Cpp/main/docs/assets/images/29.png" width="980" height="100">

This moves the cursor to the raindrop's current position and chooses a random green shade for visual effect. This is also responsible for printing a random symbol from the symbols vector.

<img src="https://raw.githubusercontent.com/par2hibATU/DigitalRain_Project.Cpp/main/docs/assets/images/30.png" width="850" height="150">


<img src="https://raw.githubusercontent.com/par2hibATU/DigitalRain_Project.Cpp/main/docs/assets/images/32.png" width="650" height="300">

This reads the **Keyboard input** using `_kbhit()` and `_getch()`. It allows the user to **Quit(q)**, **Increased speed (+)**, **Decreased speed (-)**, **Pause/Resume (p/P)**.
**Pause/Resume (p/P)** maintains a bool paused flag. When p is pressed, the flag flips: 
```paused = !paused;```
In the main loop inside `start():`
```
if (!paused) {
    renderFrame(); 
}
```

So when `paused == true`, the animation freezes, but the program still runs in the background, checking for further process.
**Quit(q)** exits the animation gracefully by setting the `running` flag to `false`. Once `running` becomes `false`, the loop exits and the program executes the `stop()` function and the result is cursor is repositioned, console text colour is reset with a `goodbye` message. 
`+` Increase speed, logically, Decrease delay. 
```
if (speed > 10) speed -= 10;
```
This functions speed up the falling rain animation by reducing the delay between frames. `speed` variable is involved here which is an `int` representing **milliseconds of delay** between frames. When `+` is pressed, the delay between frames decreases by 10 ms- so more frames are rendered per second. There is a lower bound `(speed > 10)` to prevent the animation from going too fast or even hitting zero.

`-` Decrease  speed, logically, Increase delay.
Each press on this function `speed +=10`, increases the sleep duration by 10 ms.

