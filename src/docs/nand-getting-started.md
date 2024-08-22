# Getting started with the NANDboard

## History

The original NANDboard was designed by Professor [Simon Hollis](http://www.cs.bris.ac.uk/home/simon) for the University
of Bristol Undergraduate-level, 1st year (or "freshman") Computer Architecture unit. Although the module always had a
practical emphasis, there was motivation to make the topic: a) more engaging, but also b) to promote ethos and skills
that are of general use. Such general use skills include promoting students to participate more actively in
[maker-like](http://en.wikipedia.org/wiki/Maker_culture), hardware-based (vs. software-only) projects.

As Professor Simon Hollis left Bristol University at the end of the 2014/15 academic year, the project was subsequently
taken over by Dr Daniel Page. More recently, the NAND board has been redesigned by Elliptic Systems and distributed by
Tinkerstruct as a joint, open source project with Bristol University.

## Concept

Although fundamentally important in Computer Science, [Boolean algebra](http://en.wikipedia.org/wiki/Boolean_algebra) is
a notoriously dry topic. The problem is exacerbated when hands-on experience amounts to solving paper-and-pencil
exercises; the typical result is for students to be increasingly uninterested and disengaged. The underlying causes are
varied, and differ from student to student. However, anecdotally at least, the following are common:

- There is a disconnection between theory and practice, in the sense it is unclear how Boolean algebra directly relates
  to intuitively useful forms of computation; this typically leads to students disengaging, based on the view that said
  theory has no practical use (to them).
- Paper-and-pencil exercises are of a necessarily small scale, which can
  mean [toy problems](http://en.wikipedia.org/wiki/Toy_problem) dominate;
  this typically leads to students disengaging, e.g., because they can easily solve said problems so avoid any deeper
  investigation of physical constraints and properties, and unusual designs (
  e.g., a [C-element](https://en.wikipedia.org/wiki/C-element)).
- In part due to the wealth of resources available, modern students
  are used to and excited by the immediacy of software development;
  this is often direct motivation for studying Computer Science in
  the first place, with Boolean algebra feeling like a regression
  towards Mathematics (which, for some, is less popular).

Put another way, this approach is similar, by analogy, to learning
[C](http://en.wikipedia.org/wiki/C_(programming_language)) by studying the language
and ["hello world"](https://en.wikipedia.org/wiki/"Hello,_World!"_program)
style programs *without* ever actually compiling and executing them.

An obvious alternative is to connect theory and practice directly, by
supporting genuinely hands-on, experimental tasks. One way to do so
might be to equip each student with a breadboard and some
[7400 series](https://en.wikipedia.org/wiki/List_of_7400_series_integrated_circuits)
ICs. However, for us at least, this presented some problems:
a) our large cohort sizes (of 150 or so students) make the logistics
involved quite challenging,
b) said cohorts are typically unfamiliar with, and sometimes have an
outright dislike for electronics.
The NANDboard attempts to manage these problems. Conceptually, it is
just a USB-powered breadboard pre-populated with NAND gates: it could
be viewed as a form of NAND-only
[PLA](http://en.wikipedia.org/wiki/Programmable_logic_array),
st. implementation of a Boolean expression (cf. programming the PLA)
amounts to connecting pin headers (i.e., the gate inputs and outputs)
using jumper wire. There are, of course, some gratuitous
[blinkenlights](http://en.wikipedia.org/wiki/Blinkenlights)
to visualise the inputs and outputs.

#### The NAND group(s)

Viewed from left-to-right,
each NAND group comprises

- an 8x2 input pin header,
- an [IC](http://www.ti.com/lit/gpn/sn74ac00) that houses 4 NAND gates,
- an 8x2 output pin header, and
- 4 output LEDs,

so can be thought of conceptually as the following block diagram:

```

    input pins                NAND gates             output pins         LEDs
    _____|_____        ___________|__________        _____|_____        __|__
   /           \      /                      \      /           \      /     \

   +-----+-----+      +----------------------+      +-----+-----+
   | x_0 | x_0 | ~~~> |                      |      | r_0 | r_0 |      +-----+
   +-----+-----+      | r_0 = ~( x_0 & y_0 ) | ~~~> +-----+-----+ ~~~> | l_0 |
   | y_0 | y_0 | ~~~> |                      |      | r_0 | r_0 |      +-----+
   +-----+-----+      |                      |      +-----+-----+
   | x_1 | x_1 | ~~~> |                      |      | r_1 | r_1 |      +-----+
   +-----+-----+      | r_1 = ~( x_1 & y_1 ) | ~~~> +-----+-----+ ~~~> | l_1 |
   | y_1 | y_1 | ~~~> |                      |      | r_1 | r_1 |      +-----+
   +-----+-----+      |                      |      +-----+-----+
   | x_2 | x_2 | ~~~> |                      |      | r_2 | r_2 |      +-----+
   +-----+-----+      | r_2 = ~( x_2 & y_2 ) | ~~~> +-----+-----+ ~~~> | l_2 |
   | y_2 | y_2 | ~~~> |                      |      | r_2 | r_2 |      +-----+
   +-----+-----+      |                      |      +-----+-----+
   | x_3 | x_3 | ~~~> |                      |      | r_3 | r_3 |      +-----+
   +-----+-----+      | r_3 = ~( x_3 & y_3 ) | ~~~> +-----+-----+ ~~~> | l_3 |
   | y_3 | y_3 | ~~~> |                      |      | r_3 | r_3 |      +-----+
   +-----+-----+      +----------------------+      +-----+-----+
   
```

The basic idea is:

- Each group houses 4 replicated instances of the same structure,
  the `i`-th of which computes
  `r_i = ~( x_i & y_i )`.  
  We use on the 0-th, top-most instance as an example throughout
  the following.

- The computation of
  `r_0 = ~( x_0 & y_0 )`
  relates to the top 4 pins (i.e., top 2 rows) of both the input
  and output pins headers: the input pins marked `x_0` and `y_0`
  provided an input to the NAND gate, which produces a result
  reflected on the output pins marked `r_0`.  
  Each output pin is also connected to an LED, allowing the state
  (i.e., 0 or 1) to be visualised.

- Note there are 2 pins marked `x_0` and `y_0` on the input pin
  header: since they are connected together, either of the 2 pins
  (i.e., the left- *or* right-hand pin marked `x_0`) can be used
  to provide the associated input. Likewise, there are 4 pins
  marked `r_0` on the output pin header: the NAND gate output is
  replicated on each of those pins.

- Each input pin is
  [pulled-down](http://en.wikipedia.org/wiki/Pull-up_resistor),
  meaning that `x_0` and `y_0` are 0 and `r_0` is 1 by default.  
  However, an input pin can be freely connected (via jumper wire)
  to any other

    - input pin,
    - output pin,
      or
    - constant pin,

  elsewhere on the board.

#### The input    group

Viewed from left-to-right,
the input group comprises

- 4 [switches](http://en.wikipedia.org/wiki/Switch) (or buttons),
- an 8x2 output pin header,
  and
- 4 output LEDs,

so can be thought of conceptually as the following block diagram:

   ```
   switches       output pins         LEDs
    __|__         _____|_____        __|__
   /     \       /           \      /     \

                 +-----+-----+
   +-----+       | s_0 | s_0 |      +-----+
   | s_0 | ~~~>  +-----+-----+ ~~~> | l_0 |
   +-----+       | s_0 | s_0 |      +-----+
                 +-----+-----+
   +-----+       | s_1 | s_1 |      +-----+
   | s_1 | ~~~>  +-----+-----+ ~~~> | l_1 |
   +-----+       | s_1 | s_1 |      +-----+
                 +-----+-----+
   +-----+       | s_2 | s_2 |      +-----+
   | s_2 | ~~~>  +-----+-----+ ~~~> | l_2 |
   +-----+       | s_2 | s_2 |      +-----+
                 +-----+-----+
   +-----+       | s_3 | s_3 |      +-----+
   | s_3 | ~~~>  +-----+-----+ ~~~> | l_3 |
   +-----+       | s_3 | s_3 |      +-----+
                 +-----+-----+
   ```

The basic idea is: each switch is connected to 4 output pins which
switch state, i.e., when the switch is pressed (resp. not pressed)
the pins are 1 (resp. 0).
Each output pin is also connected to an LED, allowing the state
(i.e., 0 or 1) to be visualised.
The purpose of this group is to allow convenient control of inputs
at a fixed location on the board.
It is obviously possible to control each input to a design using a
jumper wire, then manually connecting it to (resp. disconnected it
from) a constant pin to produce a 1 (resp. 0); a switch offers the
same functionality, but is far easier to use.

#### The output   group

Viewed from left-to-right,
the output group comprises

- an 8x2 input pin header,
  and
- 4 output LEDs,

   ```
    input pins          LEDs
    _____|_____        __|__
   /           \      /     \

   +-----+-----+
   | x_0 | x_0 |      +-----+
   +-----+-----+ ~~~> | l_0 |
   | x_0 | x_0 |      +-----+
   +-----+-----+
   | x_1 | x_1 |      +-----+
   +-----+-----+ ~~~> | l_1 | 
   | x_1 | x_1 |      +-----+
   +-----+-----+
   | x_2 | x_2 |      +-----+
   +-----+-----+ ~~~> | l_2 |
   | x_2 | x_2 |      +-----+
   +-----+-----+
   | x_3 | x_3 |      +-----+
   +-----+-----+ ~~~> | l_3 |
   | x_3 | x_3 |      +-----+
   +-----+-----+
   ```

The basic idea is:
each input pin is connected to an LED, allowing the state
(i.e., 0 or 1) to be visualised.
The purpose of this group is to allow visualisation of outputs at a
fixed location on the board, rather than via one of the NAND groups
(the location of which may change, as the design evolves).

#### The constant group

The constant group comprises
an 8x2 output pin header,
so can be thought of conceptually as the following block diagram:

   ```
   constant pins
    _____|_____ 
   /           \

   +-----+-----+
   |  1  |  1  |
   +-----+-----+
   |  1  |  1  |
   +-----+-----+
   |  1  |  1  |
   +-----+-----+
   |  1  |  1  |
   +-----+-----+
   |  1  |  1  |
   +-----+-----+
   |  1  |  1  |
   +-----+-----+
   |  1  |  1  |
   +-----+-----+
   |  1  |  1  |
   +-----+-----+
   ```

The basic idea is: each constant pin is 1. That's it!
The purpose of this group is related to the fact that elsewhere, an
input pin is 0-by-default. Imagine that rather than
`r_0 = ~( x_0 & y_0 )`,
you need to compute
`r_0 = ~( x_0 & 1   )`
for some reason: a reasonable approach is to connect the `y_0` input
pin of the NAND gate to a 1-by-default pin in the constant group.

