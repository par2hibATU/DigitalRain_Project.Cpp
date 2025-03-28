# Algorithm
### The program begins execution in main(). 

<img src="https://raw.githubusercontent.com/par2hibATU/DigitalRain_Project.Cpp/main/docs/assets/images/20.png" width="650" height="300">

- **Unicode Mode**: Wide character mode ensures complex Unicode symbols display properly.
    
- **Cursor Handling**: Prevents distraction by removing the blinking prompt.

<img src="https://raw.githubusercontent.com/par2hibATU/DigitalRain_Project.Cpp/main/docs/assets/images/21.png" width="650" height="300">

This sets the speed of the frame which is 100 milliseconds. start() starts the rain and stops()  just stops the animation and resets the console cursor.

<img src="https://raw.githubusercontent.com/par2hibATU/DigitalRain_Project.Cpp/main/docs/assets/images/22.png" width="650" height="300">

This sets the screen height and width.

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

<img src="https://raw.githubusercontent.com/par2hibATU/DigitalRain_Project.Cpp/main/docs/assets/images/28.png" width="650" height="300">

This increments the y-position of the drop and wraps around if it reaches the bottom and `draw()` function:

<img src="https://raw.githubusercontent.com/par2hibATU/DigitalRain_Project.Cpp/main/docs/assets/images/29.png" width="650" height="300">

This moves the cursor to the raindrop's current position and chooses a random green shade for visual effect. This is also responsible for printing a random symbol from the symbols vector.

<img src="https://raw.githubusercontent.com/par2hibATU/DigitalRain_Project.Cpp/main/docs/assets/images/30.png" width="750" height="300">


<img src="https://raw.githubusercontent.com/par2hibATU/DigitalRain_Project.Cpp/main/docs/assets/images/32.png" width="650" height="300">
This reads the **Keyboard input** using `_kbhit()` and `_getch()`. It allows the user to **Quit(q)**, **Increased speed (+)**, **Decreased speed (-)**, **Pause/Resume (p/P)**.




