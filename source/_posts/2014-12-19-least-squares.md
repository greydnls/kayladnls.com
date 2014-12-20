---
title: Method of Least Squares: Using squares to calculate a hat. 
categories:
    - Machine Learning
    - Nerd
use:
    - posts_tags
    - posts_categories
---

In my previous [post on Machine Learning](http://kayladnls.com/2014/12/11/machine-learning/), I mentioned supervised and unsupervised methods. We also discussed the two main kinds of supervised methods: continuous and categorical. Today we're going to talk about one of the continuous methods: **Method of Least Squares.** (LSM). LSM is a method of linear regression, which was also briefly mentioned in the previous post. 

> Linear Regression is the process of finding a line/curve that best fits a set of data. 

LSM is probably the most popular technique in statistics, and also one of the oldest. How does it work? It operates off the principle that the mean of a distribution is the value that minimizes the sum of squared deviations of the scores. [1]

Now, maybe you're thinking: say what?  Great! Then I'm not the only one. 

So what is it really saying? The goal, when doing regression is to try to find a line (or curve) that best fits your training dataset. The idea being that this line will provide a reasonable estimate for future real world data, and that you will be able to make predictions based on that line. Given a value (x) you will be able to estimate the resultant (y) value, also referred to as Y-hat.  

With LSM, you draw that line by minimizing the squared distance between each point in your distribution (dataset) and your estimate. Why squares and not just the distance value itself? Squares allow all of the residuals to be treated as a continuous differentiable quantity [2]. 

The values along the x axis are referrred to as the dependant variable, and the y axis is the independant variable. 

You want to create a function that best estimates future y, given an x value. That function can be represented by a line. In slope intercept form:

(1) ![image](http://chart.apis.google.com/chart?cht=tx&chl=%5Chat%7BY%7D%20%3D%20a%20%2BbX)

Where `Y` is the **predicted value**, `m` is the **slope** and `b` is the **y-intercept** of the line,  

You want a line that is going to be closest to your data, that is, where the distance between the points and the estimation line is the smallest. The distance between the actual points and your estimation line is the error, and obviously, you want to minimize error, to increase accuracy. 

(2) ![image](http://chart.apis.google.com/chart?cht=tx&chl=%5Cvarepsilon%20%3D%20%3D%5Csum_%7Bi%7D%20(Y_%7Bi%7D%20-%20%5Chat%7BY%7D_%7Bi%7D)%5E2%20%3D%20%5Csum_%7Bi%7D%20%5B%20Y_%7Bi%7D%20-%20(a%20%2B%20bX_%7Bi%7D)%5D%5E2)  
Where E represents the error. you're minimizing. 

Knowing that a quadratic equation reaches it's minimum when as it's derivatives approaches zero, we'll take the derivative of E with respect to both unknowns, a and b and set each of them to 0. These are called the normal equations.

(3) ![image](http://chart.apis.google.com/chart?cht=tx&chl=%5Cpartial%20%20%5Cvarepsilon%20%2F%20%5Cpartial%20a%20%3D%202Na%20%2B%202b%20%5Csum%20X_%7Bi%7D%20-%202%5Csum%20Y_%7Bi%7D%20%3D%200) 

and 

(4) ![image](http://chart.apis.google.com/chart?cht=tx&chl=%5Cpartial%20%20%5Cvarepsilon%20%2F%20%5Cpartial%20b%20%3D%202b%20%5Csum%20X%5E2_%7Bi%7D%20%2B%202a%20%5Csum%20X_%7Bi%7D%20-%202%20%5Csum%20Y_%7Bi%7DX%7Bi%7D%20%3D%200)

Solve those normal equations and you will end up with:     

(5) ![image](http://chart.apis.google.com/chart?cht=tx&chl=a%20%3D%20M_%7By%7D%20-%20bM_%7Bx%7D)  
Where My and Mx are the mean of x and y, respectively. 

and 

(6) ![image](http://chart.apis.google.com/chart?cht=tx&chl=b%20%3D%20%5Csum%20(Y_%7Bi%7D-M_%7By%7D)(X_%7Bi%7D-M_%7Bx%7D)%2F%20%5Csum%20(X_%7Bi%7D%20-%20M_%7Bx%7D)%5E2)

Now, all of that is a rather math-y representation of the problem, with greek letters a-plenty. It's hard to read, and a bit hard to understand, in my opinion. I much prefer to look at it in code. 

###Show me the codez
1. Calculate the mean (average) of x and y. (bar-x and bar-y, respectively. These values were M<sub>y</sub> and M<sub>x</sub> in the equations above)   
2. Take the distance from each observation in your training data, to the bar-x and the bar-y.  
3. Find the slope `m`.   
4. Use the point where bar-x and bar-y intersect (**mean-intersect**), along with the slope to calculate the y-intercept of your line.   
5. Tada! You have a function. Punch in x values and out pop estimated y values ( Y-Hat).    

I want to show you what that looks like in code. I've included the table below as a reference, so you can see all of the values that I will be using for this example, as well as bar-x and bar-y. 

<table class="table table-bordered table-striped">
<thead>
<tr>
  <th>X</th>
  <th>Y</th>
  <th>x - bar-x</th>
  <th>y - bar-y</th>
  <th>(x-bar-x)<sup>2</sup></th>
  <th>(x-bar-x)(y-bar-y)</th>
</tr>
</thead>
<tbody>
<tr>
  <td>1</td>
  <td>2</td>
  <td>-2</td>
  <td>-2</td>
  <td>4</td>
  <td>4</td>
</tr>
<tr>
  <td>2</td>
  <td>4</td>
  <td>-1</td>
  <td>0</td>
  <td>1</td>
  <td>0</td>
</tr>
<tr>
  <td>3</td>
  <td>5</td>
  <td>0</td>
  <td>1</td>
  <td>0</td>
  <td>0</td>
</tr>
<tr>
  <td>4</td>
  <td>4</td>
  <td>1</td>
  <td>0</td>
  <td>1</td>
  <td>0</td>
</tr>
<tr>
  <td>5</td>
  <td>5</td>
  <td>2</td>
  <td>1</td>
  <td>4</td>
  <td>2</td>
</tr>
</tbody>
</table>

Step 1: Calculate bar-x and bar-y:

```
 $mean_x = $this->mean($x);
 $mean_y = $this->mean($y);
 
 function mean(array $vals) {
        return array_sum($vals) / count($vals);
}
```


Step 2: Calculate the distance between each point and bar-x and bar-y
Here we're constructing two arrays that will hold the distance to bar-x and bar-y, for each value of x and y. Keep in mind that each x and y correspond to the x and y coordinates of points on a graph.  

```
$x_minus_barx = array_map(function($x) use($mean_x) {
                return $x - $mean_x;
            }, $x);
            
$y_minus_bary = array_map(function($y) use($mean_y) {
                return $y - $mean_y;
            }, $y);
```
Step 3: Find the slope:
To calculate the slope, you sum the square of $x_minus_barx, this becomes your denimonator. You then sum the values of $x_minus_barx and $y_minus_bary, this becomes your numerator. This fraction becomes your slope.  

This corresponds directly to equation (6) above. 

```
$slope = $this->calcSlope($x_minus_barx, $y_minus_bary);

function calcSlope($x_minus_barx, $bary)
{
    $barxsq = $this->squareArr($x_minus_barx);

    $barx_times_bary = $this->multArrs($x_minus_barx, $y_minus_bary);

    return array_sum($barx_times_bary) / array_sum($barxsq);
}
```

Step 4: Use the mean-intercept and the slope to calculate the Y Intercept. 
The mean intercept is the point where bar-x and bar-y meet. All regression lines must pass through this point. Since we know that point is on our line, we can you it's X and Y values to calculate the Y-intercept of the line. You do this by rearranging the `Y = mX+b` function into : `b = Y - Mx`. 

This corresponds directly to equation (5) above. 

```
$y_int = $this->calcYInt($this->slope, $mean_intercept);
function calcYInt($slope, $mean_intercept)
{
    return $mean_intercept[1] - ($slope * $mean_intercept[0]);
}
```

Step 5: Tada;
At this point, we know the values for our Y-intercept `b`, and our slope: `m`. Given any value for X, we can calculate Y. 

```
function estimate($x)
{
    return $this->y_int + ($this->slope * $x);
}
```

Given the input points `{1, 2}, {2, 4}, {3, 5}, {4, 4}, {5, 5}`, we find that the slope = .6 and the y-intercept is 2.2.
 
Graphically this looks like this:   
![image](/img/lms.png)

Each point on the graph represents a datapoint, and the line represents our estimation line. You can see that the line intercepts the y-axis just where we said it would (2.2). 

###What does this all mean?
![image](http://managedaccount.blog.com/files/2012/10/double-rainbow-what-does-this-mean-women-s-t-shirts_design.png)

Let me take a moment to illustrate with an arbitrary example. You have a house you want to sell, you also have the sales data for houses in your town, along with their square footage. Train your function on this dataset, such that square footage vales are along the x-axis and price is along the y-axis. Input the square footage of your soon to be sold home and out comes a reasonable estimate of what your home would sell for. 


**A little further reading**  
[Ian Barber](https://twitter.com/ianbarber) did a [post covering Linear Regression](http://phpir.com/linear-regression-in-php/) that uses a different alogirthm. I wanted to verify my results against his.  If you punch in his input data: 

```
// data x, y
$data = array(
    array(5, 21),
    array(6, 25),
    array(7, 30),
    array(8, 31),
    array(10, 41),
    array(12, 50)
);
```
 You can verify that the method I've outlined here results in `y = 0.29 + 4.08x`, which is consistent with the results that he got. The post he wrote is a very good one, and I highly suggest reading it. 

There are many other flavors of Least Squares that I will cover in later posts. This method can be extended to non-linear functions, and also to apply to more than one variable, but that will have to wait for another day. 

Hopefully you've learned a lot, and as always, feel free to ask questions if anything is unclear. 

> References  
> 1. Abdi, Herve, The Method of Least Squares [http://www.utd.edu/~herve/Abdi-LeastSquares06-pretty.pdf ](http://www.utd.edu/~herve/Abdi-LeastSquares06-pretty.pdf)  
> 2. Least Squares Fitting, Wolfram Math World, [http://mathworld.wolfram.com/LeastSquaresFitting.html](http://mathworld.wolfram.com/LeastSquaresFitting.html)