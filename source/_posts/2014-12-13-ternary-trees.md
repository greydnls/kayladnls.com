---
title: Ternary Trees -- An Excursion over mountains. 
categories:
    - Machine Learning
    - Nerd
    - Trees
use:
    - posts_tags
    - posts_categories
---

TIL: Mathematicians may be outdoorsy people. They have words like trees, excursion, bridge, walk, path, meander. We're going to use all of these words rather frequently in this post. If you read it fast enough, it might even feel like we're talking about hiking. 

Most of what I learned in research for this post came from Donald Knuth's 20th Anniversary Christmas Tree lecture [1]. Go, watch it, enjoy it, let it blow your mind. It's 76 minutes long and I was able to savor it for pretty much an entire day, and I can't promise that I won't be going back for seconds at some later date. 

####Trees
Today our main focus is going to be trees. As computer scientists, trees are highly important, and there are many different varieties. Trees with one node are called unary trees, two nodes are binary trees. three nodes are ternary, so forth and so on. Really, a tree can be made from any number. You can have pi-ary trees, 3/2-ary (said three-halfs-ary) trees, etc. 

Today we wil focus primarily on ternary trees. For every node on a ternary tree, it will either be empty, or have three more ternary trees below it.  That looks something like this: 

![image](/img/t-tree.jpg)  
Each circle represents a node, each square is empty. 

To process a tree, we walk it, and generally we do that using a stack. For a ternary tree, when you encounter a square, you add one, when you encounter a circle, you subtract two. Every ternary tree will start out with an empty stack, and will end with an empty stack. This kind of walk is alled an **excursion**. 

Let me take a minute to define the four main different kinds of walks:   
![image](/img/walks.png)  
This image is a screen shot taken from Knuth's video. It's taken from a paper written by Cyril Banderier and Phillepe Flajolet [2] . 

You can read the above as this:   
**walk(*W*)** : a walk that can fall above or below the x axis, and ends anywhere it pleases.   
**bridge (*B*)**:  just like a walk, but it MUST end at 0.   
**meander (*M*)**:  similar to a walk, except that MUST stay above the x axis. It can end where it pleases, though.   
**excursion (*E*)**: like a meander, in that it must be above the x axis, but like a bridge in that it must also end at 0. 

So, when I say that a good ternary tree is an **excursion** what I mean is that it **MUST** stay above the x axis (y is always >= 0), and that it **MUST** end at (y == 0). 

####Walks over Mountains
A good visual of this is:   
![image](/img/mountains.png)  
Also taken from Knuth's video

Remember from the previous drawing that our squares are +1 and our circles are -2. He's numbered the squares and lettered the circles for the above drawing. With that in mind, you can see that each time you encounter a number (square), you add one to the stack, and y increases by 1. Each time you encounter a letter (circle), you subtract 2, and y decrease by 2. 

So how many possible ways are there are walking a ternary tree? 

As we go through this, picture a graph in your mind, much like the mountains pictured above. 

Exponents represent points on that graph, where **z's** exponent is the x coordinant and **u's** exponent is the y axis. **z<sup>3</sup>u<sup>4</sup>** represents a pt (3,4) on that graph. 

Coefficients will represent the different number of ways we could have gotten to that point at that step of the walk. **3u** means there were 3 different ways to get to u. 

To help with this visualization, I will write both the exponential form of the step, but also the point that it would represent on the graph. 

We start at the origin 0 == 1 (0, 0)  
1. **First step** our only option is to go right one, and up one. --> z<sup>1</sup>u<sup>1</sup> --> (1, 1)  
2. **Second step**, our only option is right one, up one    --> z<sup>2</sup>u<sup>2</sup> --> (2, 2)  
3. **Third step**, we can either go up one, or down two            --> z<sup>3</sup>(1 + u<sup>3</sup>) --> possible points here are (3, 0), (3, 3)   
4. **Fourth step**, remember from the previous line that we're currently either sitting at 0, or 3. So, we can go up one to u<sup>1</sup>, or down two to u<sup>1</sup>, or up one to u<sup>4</sup>)  --> z<sup>4</sup>(2u + u<sup>4</sup>), three options: (4, 1), (4,1), (4, 4);  
5. **Fifth step**,  there are three ways to get to u<sup>2</sup> and one way to get to u<sup>5</sup> --> z<sup>5</sup>(3u<sup>2</sup>+u<sup>5</sup>) (5, 2), (5, 2), (5, 2) (5, 5)  
6. **Sixth step** There are 3 ways to get to zero, 5 ways to get to u<sup>3</sup> and one way to get to u<sup>6</sup> --> z<sup>6></sup>(3 + 4u<sup>4</sup> + u<sup>6</sup>) (6, 0), (6, 0), (6, 0), (6, 3), (6, 3), (6, 3), (6, 3), (6, 6)

So far, we are 6 steps into our walk, and we have following equation.

**z<sup>1</sup>u<sup>1</sup> + z<sup>2</sup>u<sup>2</sup> + z<sup>3</sup>(1 + u<sup>3</sup>) + z<sup>4</sup>(2u + u<sup>4</sup>) + z<sup>5</sup>(3u<sup>2</sup>+u<sup>5</sup>) + z<sup>6</sup>(3 + 4u<sup>4</sup> + u<sup>6</sup>)**

At this point, if you remove the z's and u's and focus solely on the coefficients and exponents of u, you are able to place them into a table. Treating each row as an "iteration" and each column as a point u<sup>x</sup>, you can see the various different ending points that would be available on any artbitrary z-length **meander** along a ternary tree. 

Each number on the following graph represents the number of possibilities your meander would have to end at that point, given that length (z). 

<table class="table table-striped">
<thead>
<tr>
  <th>z = 0</th>
  <th>1</th>
  <th></th>
  <th></th>
  <th></th>
  <th></th>
  <th></th>
  <th></th>
  <th></th>
  <th></th>
</tr>
</thead>
<tbody>
<tr>
  <td>z == 1</td>
  <td>0</td>
  <td>1</td>
  <td></td>
  <td></td>
  <td></td>
  <td></td>
  <td></td>
  <td></td>
  <td></td>
</tr>
<tr>
  <td>z == 2</td>
  <td>0</td>
  <td>0</td>
  <td>1</td>
  <td></td>
  <td></td>
  <td></td>
  <td></td>
  <td></td>
  <td></td>
</tr>
<tr>
  <td>z == 3</td>
  <td>1</td>
  <td>0</td>
  <td>0</td>
  <td>1</td>
  <td></td>
  <td></td>
  <td></td>
  <td></td>
  <td></td>
</tr>
<tr>
  <td>z == 4</td>
  <td>0</td>
  <td>2</td>
  <td>0</td>
  <td>0</td>
  <td>1</td>
  <td></td>
  <td></td>
  <td></td>
  <td></td>
</tr>
<tr>
  <td>z == 5</td>
  <td>0</td>
  <td>0</td>
  <td>3</td>
  <td>0</td>
  <td>0</td>
  <td>1</td>
  <td></td>
  <td></td>
  <td></td>
</tr>
<tr>
  <td>z == 6</td>
  <td>3</td>
  <td>0</td>
  <td>0</td>
  <td>4</td>
  <td>0</td>
  <td>0</td>
  <td>1</td>
  <td></td>
  <td></td>
</tr>
<tr>
  <td>z == 7</td>
  <td>0</td>
  <td>7</td>
  <td>0</td>
  <td>0</td>
  <td>5</td>
  <td>0</td>
  <td>0</td>
  <td>1</td>
  <td></td>
</tr>
<tr>
  <td>z == 8</td>
  <td>0</td>
  <td>0</td>
  <td>12</td>
  <td>0</td>
  <td>0</td>
  <td>6</td>
  <td>0</td>
  <td>0</td>
  <td>1</td>
</tr>
<tr>
  <td></td>
  <td>u<sup>0</sup></td>
  <td>u<sup>1</sup></td>
  <td>u<sup>2</sup></td>
  <td>u<sup>3</sup></td>
  <td>u<sup>4</sup></td>
  <td>u<sup>5<sup></sup></sup></td>
  <td>u<sup>6</sup></td>
  <td>u<sup>7</sup></td>
  <td>u <sup>8</sup></td>
</tr>
</tbody>
</table>


What patterns can we see here? As you move onto the next row, you look at the row above you. 

We know that we are constrained to steps of either +1, -2. In this case, adding moves you to the left, subtracting moves you to the right.  So, to determine each cell in a new row, look at the cell directly above it. Go one cell back, then go two cells forward, add those two numbers, and that's the number that goes in the cell in question. 

Look at row 8. How did we get 12? Up one, left one (+1), up one, right 2 (-2) gives up 7 and 5, those combine to equal 12. 

If you're looking for a function to generate such a table, have no fear! I have you covered: 

```
$rows = array();

$line1 = array(1);
$rows[] = $line1;

$iterations = 25;

for ($row = 1; $row< $iterations; $row++)
{
    $line = array();
    for($column = 0; $column <= $row; $column++)
    {
         $first_number  = isset($rows[$row - 1 ][$column - 1 ]) ? $rows[$row - 1 ][$column - 1 ] : 0;
         $second_number = isset($rows[$row - 1 ][$column + 2 ]) ? $rows[$row - 1 ][$column + 2 ] : 0;

        $line[] = $first_number + $second_number;
    }
    $rows[] = $line;
}

foreach ($rows as $row)
{
    foreach ($row as $cell)
    {
        echo $cell."\t";
    }
    echo "\n";
}        

```

Okay, so this is all good and fine. You can draw a tree with circles and squares, and you can walk that tree to make a nice mountain picture. You can even manually calculate each possibilities, to a certain extent. Lovely. But what if I asked you to tell me how many different mountain pictures you could draw, with a tree of X nodes? How would you be able to tell me? 

Or, perhaps I ask you to tell me what position of y you might be at, after you've "walked" 4 steps? 

Sure, you could draw all of those mountains and walk all of those trees, but that sounds awfully tiring. It would be much better if you knew a formula to do that. Even better still if you could translate that formula into some code and make your computer do all the legwork, right? 

Great, let's do that. 

####These computes were made for walkin... 
There are some fairly famous numbers called Catalan numbers that are used to find the number of binary trees with N nodes. These numbers were defined by Eugene Charles Catalan[3] (he's a cool cat, you should look him up). 

Catalan numbers are defined as follows:  
![image](/img/catalan.jpg)


For anyone who needs a refresher (I was completely lost here for a bit, so let me save you the trouble), the (2n n) is a binomial coefficient, which is calculated as follows:   
![image](/img/bico.jpg)

with n! denoting a factorial. 

When you run that function for a given N, you're able to find out the number of binary trees with N many nodes. The sequence of those values are known as the Catalan numbers:  1, 1, 2, 5, 14, 42, 132.. etc etc etc. 

Wait,... why am I talking about Catalan numbers? Those only apply to binary trees, and we're interested in ternary trees, right?  Well, you can generalize that catalan function to work for other trees as well! 

That generalized function looks like this:   
![image](/img/fuss-catalan.jpg)

Where x denotes the type of tree (1 for unary, 3 for ternary, etc) and n denotes the number of nodes we're asking about. If I want to know how many ternary trees with 4 internal nodes, I would do x = 3 (for ternary) and n = 4.  As promised, let's have our computer take care of the heavy lifting: 

```
$n = 4;
function ternary($n)
{
    return pow(((2*$n) + 1), -1) * binomialCoefficient((3*$n), $n);
}

echo ternary($n);
```
The answer? 55. 

So, that's neat, and you can feel free to play around with it, popping in different values for x and n. But what about the sequence? There is a sequence of Catalan numbers corresponding to each n internal nodes on a binary tree. Can we do the same thing for our ternary trees? But of course we can!

The function to generate the sequence for ternary trees looks like this:   
![image](/img/tofz.jpg)

Where t is the number denoting the type of tree (just like x did above), k is the number of "steps" you want to take (just like n above) and r is the number of trees you want to consider (yes, you can do more than one tree at a time). 

```
$t = 3;
$r = 1;
$k = 4;

$arr = array_fill(0, $k, 0);

$string_answer = "1 +";
foreach ($arr as $idx => $value)
{
    $i = $idx + 1;
    $n1 = ($t*$i) + $r;
    $n2 = $i;

    $bc = binomialCoefficient($n1, $n2);
    $answer = $bc * ($r/(($t*$i) +$r));

    $string_answer .= strval($answer)."z^".$i." + ";
}
```
What comes out?   **1 + 1z<sup>1</sup> + 3z<sup>2</sup> + 12z<sup>3</sup> + 55z<sup>4</sup>**  
You can see from this that the sequence of the first 4 numbers for ternary trees is: 1, 1, 3, 12, 55, 

One last thing, the icing on the cake, if you will. Take a look back up at the table that we built earlier. You can see we only got 8 steps in manually, but if you run the code provided I took it out to 25 steps. Remove all of the zeroes, and then look at the left most column. 

What do you see? 1, 1, 3, 12, 55. That looks familiar, doesn't it? That's because that column corresponds to the times when your walk ends at u<sup>0</sup> or y == 0. Recall that terniary trees are all **excursions** and must begin their walk at 0, and all of them must complete their walk at 0, and this makes perfect sense. 

For a little extra   
![image](http://i3.kym-cdn.com/entries/icons/original/000/009/993/tumblr_m0wb2xz9Yh1r08e3p.jpg)  
The row second from the left corresponds to the sequence of numbers for **B<sub>3</sub>(z)<sup>2</sup>** that is, squared ternary trees. The third row from the left corresponds to the cubed function, so on and so forth. You can use the code above to prove that, switching out the different numbers for r. 

> Notes  
> 1. Yes, I know my hand writing is attrocious.   
> 2. Galaxy note pen is awesome for this stuff.   
> 3. It took me about 10 hours to watch that 76 minute video and glean this knowledge, so if it doesn't 'click' don't worry .  
> 4. There's a lot in the video I didn't cover here. Specifically anything having to do with 3/2-trees as well as Duchon numbers, but I do have notes on all of it, if you're interested.   
> 5. If you have questions on any of this, feel free to reach out, I'm happy to answer them [email](mailto:kayladnls@gmail.com) or [twitter](http://twitter.com/kayladnls)

> References:   
> [1] Donald Knuth's 20th Annual Christmas Tree Lecture: (3/2)-ary Trees, [https://www.youtube.com/watch?v=P4AaGQIo0HY](https://www.youtube.com/watch?v=P4AaGQIo0HY)  
> [2] Basic Analytic combinators of directed lattice paths, Bandierier, Cyril & Flajolet, Phillippe  
> [3] Eugène Charles Catalan, [http://en.wikipedia.org/wiki/Eug%C3%A8ne_Charles_Catalan](http://en.wikipedia.org/wiki/Eug%C3%A8ne_Charles_Catalan)  