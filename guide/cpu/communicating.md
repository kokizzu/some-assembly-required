# Communicating with the CPU

One way we can communicate with the CPU is by writing instructions for it in a format called assembly language. Assembly language is the lowest level of abstraction in computers where the code you write is still human readable. You may disagree about the human readable part when you first see it, but I promise you it's better than what the computer is looking at!

What do we mean by an abstraction? Well, an abstraction is a layer above something else that makes that thing easier to do.

<p align="center">
  <br />
  <img width="460" height="300" src="https://www.familyhandyman.com/wp-content/uploads/2019/05/08.jpg">
  <br />
  <span>
    <em>
      just a placeholder image to break up the content!
    </em>
  </span>
</p>
<br />

For example, let's take a steering wheel. A steering wheel makes driving simple - you just turn left and right, and the amount you turn maps to how much your tires turn. But, what’s happening underneath? The steering wheel is an abstraction layer on top of rods, levers, and whatever else is happening inside that car, simplifying the act of turning for you. Or something like that. I clearly don't know anything about cars.

In our case, assembly is the steering wheel, and the rods, levers, and other hidden stuff is our machine code.

Here's the thing about computers. They can actually only understand numbers. So, machine code is just a bunch of numbers that the CPU reads to figure out what instructions to execute and on what data. It's the computer-readable code.

Since we humans like to read text, assembly is a text based language, consisting of acronyms that represent instructions to the computer. Alas, since they are text, they are not directly readable by the CPU. So that text file gets translated, through something called the assembler, into the numbers that the computer can then read.

It’s like if you were an American and you were giving your Icelandic friend a cake recipe. Americans write recipes in imperial measurements (eg cups, tablespoons, etc.), and Icelandic people write recipes in metric measurements (grams, liters, etc.).

<p align="center">
  <br />
  <img width="460" height="300" src="https://www.wikihow.com/images/thumb/e/ec/Write-a-Recipe-Step-12.jpg/v4-460px-Write-a-Recipe-Step-12.jpg">
  <br />
  <span>
    <em>
      just a placeholder image to break up the content!
    </em>
  </span>
</p>
<br />

Line by line you’d translate the recipe until you have a new recipe for your friend to use. You’d take the first measurement, 2 cups of flour (assembly language), convert it to grams (the assembler), and then write the converted recipe to use 68 grams of flour (machine code). Look at you go - you’re the assembler here!

You could skip all of this assembly shenanigans by writing the machine code directly, but machine code looks something like this in binary (we will talk about [what binary is](#binary) a little bit later):

```
01000111 00000000 11110010 10101110 11110010 00000001 11000011 11100010 00001011
```

Assembly, on the other hand, looks something like:

```asm
mov r12, r13
add r12, 4
```

I know this doesn’t look extremely friendly, especially compared to the high level programming languages we have today. However, I promise you it is far friendlier than just writing a bunch of numbers!

All programming languages are some level of abstraction above machine code. But, in the end, all human written code has to be converted into numbers for your CPU to be able to read.  Your CPU is able to read these numbers with the help of something called a decoder.

### Decoding our instructions

<p align="center">
  <br />
  <img width="460" height="300" src="https://cloud-cr3teqva6-hack-club-bot.vercel.app/0screen_shot_2022-05-26_at_1.07.48_pm.png">
  <br />
  <span>
    <em>
      just a placeholder image to break up the content!
    </em>
  </span>
</p>
<br />

A decoder is a specialized device on the CPU that takes input and decodes what it’s trying to do. These tasks are represented as our assembly instructions.

A CPU has a mapping from number to instruction, something like:


| Number | Instruction |
| ------ | ----------- |
| 1      | `add`       |
| 2      | `sub`       |
| ...    | ...         |

The decoder grabs the next instruction to execute, which looks like a bunch of numbers. It looks at the first number, and let's say it sees the number 2. The decoder is then able to map the number 2 to the subtraction instruction. So now the decoder can send the data along to the right places to do the subtraction.

How does the decoder know how to decode these things? It’s actually built physically into the chip itself, where the circuitry determines the instruction set.

#### Putting it all together

You may be wondering what this might look like. If you are, you’re in luck! Let’s map our last `add` line to machine code. This is a completely fictional example, but it's a demonstration of how the computer decodes the numbers.

In order to explain this, let's briefly talk about registers. We will get into this [more later](#saving-data), but for this example, they're places where you can store numbers temporarily.

```asm
add r12, 4; Add 4 to the number saved in register 12
```

In machine code, this may end up looking like this in [binary](#binary) (we will cover what binary is later), or base 2:

```
00000001 00001100 00001100 00000100
```

Which, in [base 10](#number-systems) (how we normally talk about numbers!), is:

```
1 12 4
```

The decoder would see the first `1`, and it would know that the first number it receives should map to an instruction. Let's say instruction 1 is `add`.

The decoder knows that the `add` instruction's first argument is both:

- the save destination
- and the location of the first number to add

The decoder then sees that the next piece of data has the value `12`, so it knows that its save destination is register 12 (`r12`). It can then grab the number stored in `r12` for the math part.

The decoder knows that next comes the argument for the number to add. It sees `4`, then adds `4` to whatever is in `r12`, and saves that new value to `r12`. Voila, maths!

<br />

---

<a href="/guide/cpu/physical-world.md">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://cloud-5aq8uo1rv-hack-club-bot.vercel.app/0backd.png">
    <img align="left" width="60" src="https://cloud-5v3nvbscw-hack-club-bot.vercel.app/0backl.png" />
  </picture>
</a>

<p align="right">
  <em>
    <b>
      <a href="/guide/writing-code/writing-code.md">
        Let's write some code →
      </a>
    </b>
  </em>
</p>