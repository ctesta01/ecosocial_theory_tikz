# Practicing TikZ 

Recently I've had something of an obsession with the TikZ figure rendering system that comes with $\LaTeX$. 
To better focus my learning and practice, I thought I'd work on recreating a relatively complicated figure that
was originally done in PowerPoint. 

While I think I'd make different stylistic or design choices, my thinking is that if I can replicate this figure's style,
that's good practice towards being able to replicate other styles in general. 

### The Original Figure 

<img src="ecosocial_theory.png" alt='the original figure' width="300px" />

### The TikZ Rendering 

<img src="ecosocial theory 2.png" alt='the tikz rendered output' width="300px" />


### Lessons Learned Along The Way

These aren't really listed in any order, but these are some of the things I figured out as I went along: 

Bigger lessons learned: 

  * It helped a lot to define reference coordinates by variables using syntax like `\coordinate (LevelsBoxCenter) at (7.45, .1);`
    and later write code like `\filldraw [fill=mycyan, draw=black] ([shift=({-1.25,1.825})]LevelsBoxCenter) rectangle ([shift=({1.25,-1.825})]LevelsBoxCenter);`
    (emphasis on the `shift` part) so I could move essentially what I'd call "grouped objects" together just by adjusting the definition of the
    `LevelsBoxCenter` variable.
  * `\begin{scope} ... \end{scope}` is a super powerful pattern — for example I used it in two places: one to horizontally reflect the curvey arrow drawn (using `[xscale=-1]`) and
    another time to define a `clip` on an ellipse with text inside it so it doesn't go outside the boundary of the outer rectangular permiter box.
  * `\tikzset` is also quite powerful:  in this example, I used it to set all of the text used to sans-serif and bold.
  * It still blows my mind that you can write `\for` loops in tikz. Moreover, the idea of using options like `[remember=\y as \lasty (initially 1.8)]` (like in the following bit) still feels a bit like magic. 
    * `\foreach \y/\ytext [remember=\y as \lasty (initially 1.8)] in {1.4/national, 1.0/regional, 0.6/area, 0.2/household, -0.2/individual}`

Minor lessons learned: 

  * You can't use `\\` to create a linebreak within a `\node` inside tikz unless the `\node` has an `[align=left]` (or middle or right)
    property set.
  * Maybe this is obvious to others, but I found I couldn't break text across lines inside a `\node` if that text was inside a `\Large` or similar
    formatting block — instead, I had to do something like this: `\node [...] at (...) {\Large{first line goes here}\\ \Large{second line goes here}}`
    (e.g., make separate `\Large` calls for each line). Maybe there's a better way to do this?
  * I went a long time thinking I was going to settle for the predefined colors, but importing the `xcolor` package and then defining my own colors
    was very easy once I pulled out the RGB colors (using [this tool](https://www.w3schools.com/colors/colors_rgb.asp)) using an eyedropper tool (any color eyedropper tool that lets you copy/paste hex codes works). 


### References 

  - Define coordinates as a variable <https://tex.stackexchange.com/a/12862/298630>
  - Arrows <https://tikz.dev/tikz-arrows>
  - Programmatically shifting variable coordinates <https://tex.stackexchange.com/questions/98924/transform-defined-coordinates-in-tikz>
  - Shading <https://tikz.dev/library-shadings>
  - Color and color variables <https://en.wikibooks.org/wiki/LaTeX/Colors>
  - Creating a thick arrow <https://tex.stackexchange.com/questions/215831/tikz-large-curved-arrow-filled-with-border>
  - Path decoarations <https://tikz.dev/tikz-decorations>
  - Clipping <https://tex.stackexchange.com/questions/53184/tikz-clip-shapes-with-another-built-in-shape>
  - Drawing ellipses <https://tex.stackexchange.com/questions/65018/how-to-draw-an-ellipse>
