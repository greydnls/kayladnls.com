---
title: The Product of Permutations in Cycle Notation and Other Words That Don't Make Sense. 
categories:
    - TAoCP
    - Algorithms
    - Nerd
use:
    - posts_tags
    - posts_categories
---

####Permutations. 

What is a permutation you ask?

According to Mathworld [1]:
>A permutation, also called an "arrangement number" or "order," is a rearrangement of the elements of an ordered list S into a one-to-one correspondence with S itself. The number of permutations on a set of n elements is given by n!

Great, now in english please? It's essentially a rearrangement of a set of things. 

So, you have a set `S` = `{a, b, c}` a permutation of that could be one of 6 different options (which is, 3 factorial or 3!) : 
 `abc`, `acb`, `bac`, `bca`, `cab`, `cba`
 
When you think of permutations from the point of "rearrangment" or "renaming" of these objects, it makes sense to show the transition from before, to after. This is often done in two-line notation which looks something like this: 
 
 ![image](http://latex.codecogs.com/gif.latex?\binom{a&space;b&space;c&space;d&space;e&space;f}{c&space;d&space;f&space;b&space;e&space;a})
 
The top line here is the "before", and the bottom line is the "after".  So you would read this as "a becomes c, b becomes d, c becomes f" etc. 

You can also apply permutations one after the other. This is actually called "multiplying permutations". Personally, I think that's rather odd, as I don't see any actual multiplication going on, but I'll defer to brains bigger than my own and just go with it. You can feel free to do the same. Moving on. 

If you have:   

![image](http://latex.codecogs.com/gif.latex?\binom{a&space;b&space;c&space;d&space;e&space;f}{c&space;d&space;f&space;b&space;e&space;a}&space;X&space;\binom{a&space;b&space;c&space;d&space;e&space;f}{c&space;a&space;e&space;d&space;f&space;b})

You apply the first permutation, and then the second.   

You end up with this:   
![image](http://latex.codecogs.com/gif.latex?\binom{a&space;b&space;c&space;d&space;e&space;f}{c&space;d&space;f&space;b&space;e&space;a}&space;X&space;\binom{a&space;b&space;c&space;d&space;e&space;f}{c&space;a&space;e&space;d&space;f&space;b}&space;=&space;\binom{a&space;b&space;c&space;d&space;e&space;f}{c&space;d&space;f&space;b&space;e&space;a}&space;X&space;\binom{c&space;d&space;f&space;b&space;e&space;a}{c&space;a&space;e&space;d&space;f&space;b}&space;=&space;\binom{a&space;b&space;c&space;d&space;e&space;f}{c&space;a&space;e&space;d&space;f&space;b})

If that's still a bit fuzzy, let me explain it in a different way.   
Step 1: we start with  `a b c d e f`  
Step 2: That becomes `c d f b e a`  
Step 3: Step 2 becomes `c a e d f b`

So the final result of that multiplication can be read as `a b c d e f` becomes `c a e d f b`

 Also, it ought to be noted that this multiplication is not commutative. That is, 
 
 ![image](http://latex.codecogs.com/gif.latex?\binom{a&space;b&space;c&space;d&space;e&space;f}{c&space;d&space;f&space;b&space;e&space;a}&space;X&space;\binom{a&space;b&space;c&space;d&space;e&space;f}{c&space;a&space;e&space;d&space;f&space;b})
 is not equal to 
 ![image](http://latex.codecogs.com/gif.latex?\binom{a&space;b&space;c&space;d&space;e&space;f}{c&space;a&space;e&space;d&space;f&space;b}&space;X&space;\binom{a&space;b&space;c&space;d&space;e&space;f}{c&space;d&space;f&space;b&space;e&space;a})
 
 In this case, the order matters!
 

####Cycle Notation

As I stated earlier, the notation we've been using up until now is called **two-line notation**, for obvious reasons. There is another notation which is a little harder to read at first, but I actually prefer it: **cycle notation**. 

Going back to our first example:   

 ![image](http://latex.codecogs.com/gif.latex?\binom{a&space;b&space;c&space;d&space;e&space;f}{c&space;d&space;f&space;b&space;e&space;a})
 
 This can be written in cycle notation as: `(acf)(bd)` This represents two "cycles", each enclosed in `()`. Each character in a cycle becomes the character to it's right, with the last character in the cycle becoming the first character, in a circular fashion. 
 
 It looks something like this:   
 ![image](/img/cycleNotation.jpg)
 
 So again, just as with the two-line notation: a becomes c, c becomes f, f becomes a.
  
 Permutations in cycle notation can be written in a number of different ways. `(bd)(acf)`, `(cfa)(bd)` and `(db)(fac)` are all equivalent, however `(afc)(db)` wouldn't be because it says `a` becomes `f`. 
 
 Looking at that, you might think I'm mistaken. I mean, I JUST said that order in multiplication of permutations matters, didn't I? Generally, in cycle notation, that's still true. However, the two cycles above (`(bd)` and `(acf)`) don't intersect. That is, neither of them have any letters in common. So, in this case, order doesn't matter. 
 
 Now, if you compare the cycle notation representation of `(acf)(bd)` to the original set `(abcdef)` you should notice that one letter is missing: e. This is because in the permutation, e becomes e, or doesn't change. You can see that easily in the two line notation. This is called a singleton cycle, and can be included or left off in cycle notation. 
 
> Interesting side note: A permutation that's made up entirely of singleton cycles is called an ***identity permutation***, and it's usually denoted as `()`. 
 
####Multiplication in Cycle form. 
The above multiplcation problem that we did in two-line form can be easily translated into cycle notation as follows:   
![image](http://latex.codecogs.com/gif.latex?\binom{a&space;b&space;c&space;d&space;e&space;f}{c&space;d&space;f&space;b&space;e&space;a}&space;X&space;\binom{a&space;b&space;c&space;d&space;e&space;f}{c&space;a&space;e&space;d&space;f&space;b})

 Becomes: 
 `(acf)(bd)(abd)(ef) = (acefb)`
 
 We don't need that pesky `x` sign here either, since it's pretty clear that `(acf)(bd)` means `(acf)` times `(bd)`. 
 
 Let's walk through this together. We know from our earlier definition that the multiplication of permutations is just applying one after the other. 
 
Our alorithm will terminate once each character in the input has been seen, so we 'tag' each character as they become the "current" character. Once the number of unique characters in the input == the number of tags,  we have determined the final positions of each of the input characters, and so we're done. That's why I use the words "tag" and "untag" here. 

 
1. Starting at the left, Select the first (untagged) character of the input, in this case: `a`. We'll call this our "current" item. We're trying to find out what happens to that letter as each of the permutations is applied to it. 
2. Move to the right 1. We have `a` becomes `c`   
>The final position of `a` isn't necessarily `c`, though. We need to continue moving to the right along the input to see what `c` becomes, because that will be the final stop for `a`.  In this case, `c` doesn't appear again. After step 2, our output is `(ac`.  
3. Remember that we read this partial output as "a becomes c", The next logical question is what happens to c? `c` becomes our 'current' character, and we move back to step 2.
4. Eventually, you will come to a point where the last letter of the output "becomes" the first letter of the current cycle. This is a "closed cycle", you output a right parenthesis to indicate that the cycle is closed. If there is more input to be processed, you start a new cycle. 

These 4 steps above are repeated until all of the input characters have been tagged, and we have found our answer. 

We can walk through the above example:  `(acf)(bd)(abd)(ef)`  
a -> c   
c -> f -> e  
e -> f  
f  -> a -> b   
b -> d -> a  
d -> b -> d
and so, our final answer is: `(a c e f b)`, in this case, `d` is a singleton cycle and can be left off or included as you please. 

This is easy enough to do by hand, and it doesn't take very long to do it. But, let's be honest:
![image](http://img.pandawhale.com/post-6769-aint-nobody-got-time-for-that-yIus.gif) 

So instead, we create an algorithm that can handle this work for us. 

####Building an Algorithm

Let's find the product of the following permutations:

`(acfg)(bcd)(aed)(fade)(bgfae)`

**Step 1: Clean the input: ** Remember that once you reach the end of a cycle, the last letter points back in a circular fasion to the first letter of the cycle? That's a bit irritating to explain to a computer. Instead, we'll replace all right parentheses with the first character of that cycle. Remove all left parentheses. After this step, our original input looks like this: 

`acfga bcdb aeda fadef bgfaeb`

 Notice that all the parentheses are gone, and we've copied the first letter of each cycle to the end: `acfg` became `acfga`, etc. 
 
 In code this is pretty simple: 

```
function parseInput($input)
{
    $input = explode(')(', $input);

    $input_array = array_map(
        function ($piece)
        {
            $piece = trim($piece, '()');
            $piece = $piece . $piece[0];

            return $piece;
        },
        $input
    );

    $character_array = preg_split('//', implode('', $input_array), -1, PREG_SPLIT_NO_EMPTY);

    return $character_array;
}
```
 
 **Step 2 Open the cycle:** Searching from left to right, find the first untagged element of input. Define a variable `$start` equal to this value, and tag it. Add a left parentheses and the element to the output. 
 
```
function openPermutation($character_array, $tags)
{
    list($initial_position, $start) = getNextUntaggedElement($character_array, $tags);
    $tags[] = $start;

    $position = $initial_position + 1;
    $current = $character_array[$position];

    $output[] = '(';
    $output[] = $start;
}
```

 You can see from these first two steps that I've chosen to construct both the output and input as arrays. Why? Because I like arrays. I'd be very happy to hear other implementations using different data structures. (Yup, there are more ways to skin this cat, as with every cat)
  
 At this point, output should be `['(', 'a'] `
 
 **Step 3**: Set the current equal to the next untagged element in the input. 
 This step was actually also performed above by `$current = $character_array[$position]`
 
 **Step 4: Find the next right instance** Continuing left to right, scan the input until you either reach the end, or you find an element equal to the current. In the latter case, tag that element and return to step 3. 
 
```
list($position, $current) = findNextRightInstance($character_array, $current, $position);
```

**Step 5: Check Current Against start?** At this point `$current` holds the character that we are currently searching for. `$start` holds the first character of the current cycle.   

**5a.** If `$current` DOESN'T == start, we aren't ready to close the cycle. So, add `$current` to the output array and go back to step 4. 

```
$output[] = $current;
$tags[$current] = $current;
$position = array_search($current, $character_array);

$position++;
$current = $character_array[$position];
```

**5b:** If `$current` DOES == `$start`, then we have reached the end of this cycle. Add a right parenthesis to the output and go back to Step 2. 

```
if ($current == $start)
{
    $output[] = ")";
}
```

You keep going through that round about until all of the elements in the input appear in the tagged array. At that point, you're finished. 

Given our initial input of `(acfg)(bcd)(aed)(fade)(bgfae)` you end up with `(adg)(ceb)(f)`

Because I'm a curious soul, I wanted to see how this work with different kinds of permutations. Knowing what we do about multiplication, we know that `$a x $b x $c` is equal to `($a x $b) x $c`. Does the same hold true of Permutations? 

I implemented my algorithm so that the `multiply()` function would work with a single string representation of the permutation, as seen above, or two separate permutations to be multiplied together. 

The first method, with a single string Permutation:

````
$p6 = new Permutation('(acfg)(bcd)(aed)(fade)(bgfae)');
echo multiply($p6)->raw();
````

This indeed outputs what we expected:    

```
(adg)(ceb)(f)
```

However, when I did it with each permutation separately: 

```
$p1 = new Permutation("(acfg)");
$p2 = new Permutation("(bcd)");
$p3 = new Permutation("(aed)");
$p4 = new Permutation("(fade)");
$p5 = new Permutation("(bgfae)");
echo multiply(multiply(multiply(multiply($p1, $p2), $p3), $p4), $p5)->raw();
```

This time it gave a slightly different output: 

```
(adg)(bce)(f)
```

Looking out those two outputs, the only difference is the second cycle `ceb` vs `bce`. As we discussed earlier, these are actually equivalent. In both cases, c becomes e, b becomes c, and e becomes b. 

Tada! We've now written an algorithm to calculate the product of permutations in cycle notation. Go forth, conquer the world. As always, if you want to discuss this or you have questions, feel free to find me on the twitter: [@kayladnls](http://twitter.com/kayladnls)

If you'd like to see the full code that I used to implement this, [go here.](https://gist.github.com/kayladnls/0857b47a11b915f5d354)
 
> References  
 1. [Permutation, Wolfram Mathworld,](http://mathworld.wolfram.com/Permutation.html) http://mathworld.wolfram.com/Permutation.html  
 2. The majority of this information, including the algorithm and a deeper explanation of permutations was learned from [The Art Of Computer Programming, Vol 1 by Donald E Knuth](http://www.amazon.com/The-Art-Computer-Programming-Vol/dp/0201896834). Find it, buy it, read it, love it, and then come find me so we can talk about it. 