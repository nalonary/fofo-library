# fofo

Hello there! 👋 Welcome to my library **fofo**.

Yeah, it might sound like a strange name, but honestly, this was the only name I could think of that was easy to remember and (hopefully) nobody had already taken. 😭

You might be here because you want an easy way to make your own games and apps in C without having to deal with a huge amount of complicated code.

I really appreciate you being here!

Keep in mind that this is only **V0.1**, so there will definitely be bugs, missing features, and things that could be improved. Stay tuned for future updates and new features!

---

# Quick Tutorial

Let's see how you can use fofo. :)

## 1. Creating a Window

Obviously, the first step to making a game or app is actually having a window instead of just letters appearing in the terminal.

Here's a basic example:

```c
#include "fofo.h"

int main()
{
    fofo_init(750, 500);
    fofo_window("little game");
    fofo_windowed();

    while (fofo_running)
    {
        fill_screen(black);
        events();

        fofo_update();
    }

    fofo_quit();
}
```

### How does this work?

**1. `#include "fofo.h"`**

This includes the fofo library so you can use its functions.

**2. `int main()`**

The main function of your C/C++ program. I hope you already know this one. :D

**3. `fofo_init(width, height)`**

Initializes fofo with the width and height you provide.

```c
fofo_init(750, 500);
```

This creates a 750×500 drawing area.

**4. `fofo_window("name")`**

Sets the name of your window.

```c
fofo_window("little game");
```

You can put whatever name you want between the `" "`.

**5. `while (fofo_running)`**

This keeps your application running.

Without the main loop, your program would create the window and then immediately finish.

**6. `fill_screen(color)`**

Fills the screen with the selected color.

```c
fill_screen(black);
```

fofo includes some basic colors, but you can also use a hexadecimal color value if supported by your setup.

**7. `fofo_update()`**

Updates the window every frame.

This is important when making anything that moves or changes on the screen.

For example, you can clear the previous frame with `fill_screen()` and then draw everything in its new position before calling `fofo_update()`.

**8. `fofo_exit()`**

Closes the fofo window and cleans things up when your program finishes.

---

# 2. Drawing Things

Now that we have a window, let's actually put something in it!

### Rectangle

```c
draw_rect(x, y, width, height, color);
```

This is your bread and butter for making shapes.

The `x` and `y` coordinates specify the top-left corner of the rectangle.

Example:

```c
draw_rect(100, 100, 50, 50, red);
```

---

### Circle

```c
draw_circle(cx, cy, size, color);
```

Draws a circle using the custom bitmap system used by fofo.

Example:

```c
draw_circle(300, 200, 100, green);
```

---

### Triangle

```c
draw_triangle(x, y, base, height, color);
```

Draws an upward-facing triangle.

Example:

```c
draw_triangle(300, 200, 100, 100, blue);
```

---

### Text

```c
draw_text(x, y, "your text", size, color);
```

One of the features I'm most proud of. :)

fofo uses a custom **30×30 bitmap font** that I made for the library.

The `size` value controls how large the characters are.

```c
draw_text(50, 50, "hello world", 2, blue);
```

---

### 2D Maps

```c
draw_map(rows, cols, map_array, size, gaps, color);
```

Want to make a simple 2D game like Pac-Man or Snake?

You can create a 2D array containing `1`s and `0`s.

The library will draw a tile wherever the array contains a `1`.

You control the number of rows and columns, tile size, gap between tiles, and color.

---

# 3. Keyboard and Mouse Input

Now let's make things move.

First, you **must** put:

```c
events();
```

inside your `while (fofo_running)` loop.

This tells fofo to process keyboard and mouse events every frame.

After that, checking the keyboard is very simple.

For example:

```c
if (w == pressed)
{
    player_y -= 5;
}

if (d == pressed)
{
    player_x += 5;
}
```

You can do this with the letters `a` through `z`.

### Mouse

Mouse input works in a similar way.

You can check whether the left mouse button was clicked:

```c
if (leftclick == clicked && inrange(x, width, y, height))
{
    // Do something!
}
```

`inrange()` lets you check whether the mouse is inside a particular area.

You can also access:

```c
press_x
press_y
```

to get the mouse position.

---

# 4. Background Timer

Normally, using a delay in a game can stop everything while the program waits.

fofo has a timer that runs separately so your main game loop can continue running.

Start a timer with:

```c
start_timer(5);
```

Then you can check whether it has finished:

```c
if (timer_on == 1 && timer_value == 0)
{
    // 5 seconds have passed!
}
```

This lets you make things happen after a certain amount of time without stopping the rest of your game.

---

# 5. Window Modes

You can change how your window behaves while the program is running.

### Fullscreen / Windowed

```c
fofo_fullscreen();
fofo_windowed();
```

For example:

```c
if (z == pressed)
{
    fofo_fullscreen();
}

if (x == pressed)
{
    fofo_windowed();
}
```

Press Z → fullscreen.

Press X → back to a normal window.

---

### Window Borders

```c
bordered_window(state);
```

Use:

```c
bordered_window(0);
```

to remove the window borders.

And:

```c
bordered_window(1);
```

to bring them back.

---

# 6. Drawing Images

You aren't limited to basic shapes!

You can also draw pixel-art images that have been converted into C arrays.

For example:

```c
draw_image(x, y, width, height, image_array);
```

Example:

```c
draw_image(200, 200, 100, 100, cat_array);
```

Just provide the position, size, and image array.

fofo also has bounds checking so an image going outside the window shouldn't cause it to access invalid screen memory.

---

# 7. Lines

Sometimes you just need a straight line without drawing an entire rectangle.

### Horizontal line

```c
draw_hline(x, y, length, color);
```

Draws a horizontal line.

### Vertical line

```c
draw_vline(x, y, length, color);
```

Draws a vertical line.

---

# And that's it!

You now know the basics of using **fofo** to make your own games and applications in C.

This is only **V0.1**, so there will be plenty of improvements and new features in the future.

Thanks for checking out my library.

**Have fun making stuff! ❤️**

### Prerequisites
Because fofo is a hardware-accelerated engine, it relies on SDL3 to talk to your computer's graphics card. You must install SDL3 and SDL3_image before compiling!

**For Linux (Ubuntu/Debian):**
Run these commands in your terminal to install the required libraries:
sudo apt-get update
sudo apt-get install libsdl3-dev libsdl3-image-dev

**For MacOS:**
Using Homebrew, run:
brew install sdl3 sdl3_image

**For Windows:**
We recommend using MSYS2 or vcpkg to install SDL3, or downloading the pre-compiled developer binaries directly from the official SDL GitHub page.

**How to Compile:**
Once installed, compile your game using gcc and pkg-config:
gcc main.c $(pkg-config --cflags --libs sdl3 sdl3-image) -o mygame

