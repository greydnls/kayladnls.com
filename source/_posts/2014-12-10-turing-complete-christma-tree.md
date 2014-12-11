---
title: Undecidable Turing-Complete Christmas Tree Automata in Practice
categories:
    - Code
    - Nerd
use:
    - posts_tags
    - posts_categories
---

Undecidable Turing-Complete Christmas Tree Automata in Practice
===========

####"Have you ever heard of Rule 30?"
A friend chirped me in skype asking if I was familiar with "Rule 30". He's going in for a job interview and they'd asked him to code this Rule 30 as an exercise. I hadn't heard of it, but I was intruiged, and I'm always one to try to help a friend. Off to the Google-Mobile, Batman!

As I would learn, `Rule 30` refers to something introduced by  [Stephen Wolfram](http://en.wikipedia.org/wiki/Stephen_Wolfram) in 1983]<sup> (1)</sup>.  Even if you're not familiar with Wolfram, you're probably familiar with his work. Especially, if you took any [college level Calculus classes](http://www.wolframalpha.com/). He was a computer scientist, and word is he was pretty good at the maths. If you don't know him, check him out, cool dude. 

Anyway, on to this Rule 30 business. Rule 30 is one of many rules that pertains to binary cellular automaton<sup> (2)</sup>. Now, when I read that the first time, they lost me halfway through binary. If you're like me, never fear!

####Elementary Celluar Automaton
So, how's this work? For each cell there are two possible values: 1 or 0. Each of Wolfram's "Rules" (there are 255 of them) defines a list of rules that tell you how to determine whether a given cell is 1 or 0. It does this by analyzing the "neghborhood" of the cell in question. What is meant by neighborhood is discussed in more detail below. 

####What it means to be 1D
You may be famliar with other Cellular Automata, such as Conway's game of life Game of Life<sup>(3)</sup>. This method is similar, but there is a primary difference. Game of Life is 2-dimensional, with a third dimension of time. That means that as the rules are applied and the pattern progresses, the "board" is refreshed. 

Rule 30 and it's siblings are 1-Dimensional. In this case, the y axis is, in fact, time. That means that as the program is run the new output is appended to the old, rather than the entire "board" refreshing. 

####Why "Rule 30"?
Since there are`2×2×2 = 8` possible binary states for the three cells neighboring a given cell, there are a total of `2^8=256` elementary cellular automata, each of which can be indexed with an 8-bit binary number. 

So, Binary: 00011110 = decimal 30. Therefore, Rule 30. This holds true for all of the other rules, too, by the way. Not terribly important, but I found it interesting, so there you have it. Moving on. 

####Ruleception
Yes! Rules inside rules!

![image](/img/rule30.gif)

Above are the rules given for Rule 30. This is how you determine whether your "cell" is a 1 or a 0. Upon first inspection, this made absolutely 0 sense to me. (binary pun possibly intended?). 

What you need to understand here is what is meant by "neighborhood". When you're determining the 1/0ness of a cell, you look at it's neighborhood and compare that against the rules. Neighborhood being the three cells above it. So, 111 = 0, 110 = 0, so forth and so on. Once you get your mind around that, you're off to the races. 

Once you have your rules, you apply them to the given input (in this case a single "line" of the grid with at least one cell set to "1"). What do you get?

![image](/img/rule30graph.png)

So Pretty. 

But how do you DO it? Well, let me show you. 

####The Codez.

*** Warning!** I have absolutely no intention of using OO practices here. No classes will be made, no injection will be used. I will interface nothing. If this makes you uncomfortable, you may want to stop reading.*

End result, I want to create this cool looking graph thing. That's how a picture it, a graph, or grid, Once you're there, it becomes a matter of some setup, and then some iteration. It looks like this: 

<div>  </div>

```
//First thing's first, let's codify those rules. 
$rules = array(
    '111'=> 0,
    '110' => 0,
    '101'=> 0,
    '100' => 1,
    '011'=> 1,
    '010' => 1,
    '001'=> 1,
    '000' => 0
);

//create an empty array to hold your grid
$lines = array();

//set up that first line 
$first_line = array_fill(0, 51, 0);

// make sure you set at least one of those cells to 1,
// or this will going no where fase. 
$first_line[24] = 1;

//now add your line to the grid. 
$lines[] = $first_line;

//Lets compile that grid

// I'm doing 10 iterations, you can do as many as you like. 
for ($i = 0; $i< 10; $i++)
{
    // make a new line
    $line = array();
    
    for($j = 0; $j< 51; $j++)
    {
        // The "pattern" is determined by the "neighborhood" or the 3 cells in the 
        // generation (row) above our cell in question. 
        $pattern = (string)implode('', array_slice(end($lines), $j - 1, 3));
 
         // if we have a valid value, great. Elsewise, give is a 0. 
         $line[] = (strlen($pattern) == 3 && isset($rules[$pattern])) ? $rules[$pattern] : 0;
    }
    
    Add the new line into the grid
    $lines[] = $line;
}

// Now, let's output it
foreach ($lines as $line)
{
    foreach ($line as $piece)
    {
        echo $piece;
    }
    echo "\n";
}
```
![image](/img/rule30output.png)

Tada! 

####Merry Christmas!

For mine, I changed 1 to '/' and 0 to '*'. Why? Because it's December, and it looks festive, that's why. I just taught you how to output a Christmas tree in your terminal!

Clearly, with the added nerdery, this is no longer a Christmas Tree. This is what we call a FSM Tree. The perfect DIY gift for your budget conscious nerd. 


![image](http://media.giphy.com/media/14cUTtBgAXn7J6/giphy.gif)

And there you have it. Merry Christmas, Nerds. 

####Post Script
You may be wondering why the post title references Turing completeness<sup>(4)</sup>. As I mentioned before, our beloved Rule 30 has 254 siblings. One of these siblings is known as Rule 110, and this rule is turing complete. 

The process for running through Rule 110 is the same as Rule 30 (that holds true for all 255 rules, by the by), the only change is the rules. So, if you're interested, here are the rules for Rule 110 (in Christmas tree format, of course)

<div>  </div>

~~~~~~~~~~~~~~~~~~~~~

$rules = array(
    '///'=> '*',
    '//*' => '/',
    '/*/'=> '/',
    '/**' =>'*',
    '*//'=> '/',
    '*/*' => '/',
    '**/'=> '/',
    '***' => '*'
);
~~~~~~~~~~~~~~~~~~~~~

Go forth and make a Turing machine. 


References

1. Wolfram, S., "Statistical mechanics of cellular automata", http://journals.aps.org/rmp/abstract/10.1103/RevModPhys.55.601 }
 2. Elementary Cellular Automaton, http://mathworld.wolfram.com/ElementaryCellularAutomaton.htm}
 3. Conway's game of life, http://en.wikipedia.org/wiki/Conway%27s_Game_of_Lif}
 4. Turing Complete, http://c2.com/cgi/wiki?TuringComplet}