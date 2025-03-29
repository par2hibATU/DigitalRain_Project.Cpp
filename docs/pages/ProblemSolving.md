
# Problem Solving
First problem I faced was scattered symbol printing all over the screen instead of falling in a proper cascading effect  and each raindrop updated its position randomly or inconsistently. I took references from a website and designed the code in a way where old raindrops were not being erased properly

Image 1: scattered  symbols

**Fix:** 

 1. **Raindrop Initialization:**  The raindrops were placed at completely random positions (`rand() % screenWidth, rand() %
    screenHeight`), causing the symbols to fall all over the screen.
    Also my printing method was not initialized. Then I reinitialized
    this function `initializeRaindrops()`  so that each raindrop starts
    at the top (`y=0` or near the top) instead of a random position.
 2. **Updating and Raindrops**: Then I updated this `update()` function to move raindrops downward smoothly and I fixed screen cleansing method.
 3. **Frame Rendering Optimization:** 
  image 2: renderFrame 
  Ensured this function to make sure the output is updated properly.
