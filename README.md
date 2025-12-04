# hive_fract-ol
fract-ol project for Hive, Helsinki

<img width="500" height="500" alt="Screenshot 2025-12-04 at 23 38 20" src="https://github.com/user-attachments/assets/4dd6d653-5e52-4124-be0c-da386c7c425b" />
<img width="500" height="500" alt="Screenshot 2025-12-04 at 23 39 14" src="https://github.com/user-attachments/assets/c57fcd31-d485-4d38-9dcb-a8b1e9e6efd6" />
<img width="500" height="500" alt="Screenshot 2025-12-04 at 23 39 43" src="https://github.com/user-attachments/assets/9ba46bfd-18a6-4f2d-8cc1-ca0de1a4ec60" />
<img width="500" height="500" alt="Screenshot 2025-12-04 at 23 44 30" src="https://github.com/user-attachments/assets/825e89f7-c9ac-4e00-81e1-d67d36b89a00" />

## Usage
Specify which fractal set you wish to visualise.

### Mandelbrot
For the Mandelbrot set pass "m", "M", "mandelbrot" or "Mandelbrot" as an argument. e.g. "./fractol m"

### Julia
For the Julia set pass "j", "J", "julia", or "Julia" as the first argument PLUS 2 float values (best results between -1.0 and 1.0) for the constant in the order c-real, c-imaginary. e.g. "./fractol julia 0.1 -0.7"

For help with controls use the argument:
"-help". e.g. "./fractol -help"

## Fractals
...are super cool. That's why I chose this project. The internet doesn't need more videos of zooming through nether regions of the mandlebrot any more than it needs more pictures of cats. But the challenge of calculating and visualising fractals using C was fun challenge and it tickled my mathmatical fancy (and I got to do some nether noodling while I was at it).

## History
It's lovely when the threads are long and winding, such as is true for the Mandelbrot and Julia sets. Julia for instance being discovered with only the aid of pen and paper by a certain Gaston Julia who had the perculiar distinction of having no nose. Or the fact that the Mandelbrot set was first visualised at IBM's Research Centre by Benoit Mandelbrot. Watch this video for starters if you want to follow this rabbit hole: [What's so special about the Mandelbrot Set? - Numberphile](https://www.youtube.com/watch?v=FFftmWSzgmk)

## Graphical Libraries
This was my first C project that involved graphics, in this case, anything more than terminals, binary and text. We had the choice of two graphics library APIs, miniLibX and MLX42, both of which are built upon GLFW and OpenGL (two HUGE graphics libraries). MLX42 was the obvious choice as it is far better documented, maintained and features better portability across platforms. Practically this meant I could show my flatmates what I was actually doing all day from the comfort of our kitchen. MLX42 was nonetheless alot to get to grips with as a first-time graphical API, from setting up the window to drawing pixels and handling the buffer.

## Maths
We were required to represent the Mandelbrot and Julia sets, two classic fractals. These two sets are essentially two expressions of the same formula <sub>c</sub>(z)=z<sup>2</sup>+c where Mandelbrot is a plot of values of C starting from a constant Z of 0, and Julia is a plot of values of Z with a constant C set at any number. The coolest aspect of this being that if we were to create a composite picture of all the Julia sets mapped to their C value coordinates, then that composite picture would look like a pixelised Mandelbrot (see the video above if you don't believe me).

## Representing in C
The challenge of visualising Mandelbrot and Julia in C was relatively trivial. A refactored version of the above equation is found in the functions `mandel_pixel()` and `julia_pixel()` (note the similarity). These equations simply work out how many times the equation will take to grow beyond an arbitrary max value (commonly 4), or as the video above puts it, "How long before it blows up?" This value then becomes the colour of the pixel.

## Colour Fun
I spent the most time on a side quest implementing a custom colour wheel, which can be found in the file `color.c`. This abstracts an RGB colour wheel with 6 equal regions of ramping up and down individual channels. Each channel is max for 1/3 of the circle, min for another 1/3 then ramping up for 1/6 and ramping down for another 1/6. Each channel's 'phase' is offset by a third. This overlapping pattern creates points of pure R, G and B (where each of the other colours have both ramped down to zero) and points of secondary colours (purple, green and orange) where two colours hit a max simultaneously. To try out an exmaple, check out this web-based tool: [Color Picker Wheel](https://pickerwheel.com/tools/random-color-generator/). As I have a background in photography and photoshop, the function that selected the colour (based upon the above 'blow up' value) naturally inherited a name from that world, thus the `color_picker()` was born.

## More is More
Finally, after seeing the above video, I also NEEDED my own version of the Julia rotate. This is where the C constant is rotated around the zero point of the axis. Becuase, because, it looks pretty. For this I avoided using the permitted maths.h library, both becuase I had heard it to be "slow" from peers and because I felt up to the challenge. The result is a separate `maths.c` file with custom implementations of sine, cosine, square root and atan. These allow me to calculte any given C constant's distance from the centre of the axis and thus rotate the point. The atan is (VERY) rough, anything more felt like overkill at this point. So you will see some jankyness when beginning a rotation.

## Lessons
This project was fun and challenging for a great many things:
- Learning to draw a window and pixels within
- Simplifying seemingly complex maths to short easy to use formulae
- Getting me working with floating points for the 1st time
- Hitting practical limitations due to computational limits for the 1st time also, and having to find efficiency savings to make my program run smoother and faster
- Providing the inspiration for a colour wheel, a true concept that I tried to abstract using maths that I could comprehend with pen and paper

So to anyone thinking about doing their own implementation of fractals in C, I highly recommend! If anything, just for the pretty colours.

*Oscar Roff October 2025*
