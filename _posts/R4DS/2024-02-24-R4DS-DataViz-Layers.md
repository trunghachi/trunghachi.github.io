---
layout: post
title: R for Data Science
subtitle: Day 4. Layers
tags: [R, Data Science, Data Visualisation, DataViz]
comments: true
categories: R DataScience DataViz
author: Chí Trung HÀ
---

## Introduction

In Chapter 1, you learned much more than just how to make scatterplots, bar charts, and boxplots. You learned a foundation that you can use to make any type of plot with ggplot2.

In this chapter, you’ll expand on that foundation as you learn about the layered grammar of graphics. We’ll start with a deeper dive into aesthetic mappings, geometric objects, and facets. Then, you will learn about statistical transformations ggplot2 makes under the hood when creating a plot. These transformations are used to calculate new values to plot, such as the heights of bars in a bar plot or medians in a box plot. You will also learn about position adjustments, which modify how geoms are displayed in your plots. Finally, we’ll briefly introduce coordinate systems.

We will not cover every single function and option for each of these layers, but we will walk you through the most important and commonly used functionality provided by ggplot2 as well as introduce you to packages that extend ggplot2.



```R
library(tidyverse)
library(gridExtra)
```

## Aesthetic mappings

Remember that the mpg data frame bundled with the ggplot2 package contains 234 observations on 38 car models.

Among the variables in `mpg` are:

* `displ`: A car’s engine size, in liters. A numerical variable.
* `hwy`: A car’s fuel efficiency on the highway, in miles per gallon (mpg). A car with a low fuel efficiency consumes more fuel than a car with a high fuel efficiency when they travel the same distance. A numerical variable.
* `class`: Type of car. A categorical variable.

And remember that:
* The name of a color as a character string, e.g., color = "blue"
* The size of a point in mm, e.g., size = 1
* The shape of a point as a number, e.g, shape = 1.

You can learn more about all possible aesthetic mappings in the aesthetic specifications vignette at https://ggplot2.tidyverse.org/articles/ggplot2-specs.html.


```R
mpg
```


<table class="dataframe">
<caption>A tibble: 234 x 11</caption>
<thead>
	<tr><th scope=col>manufacturer</th><th scope=col>model</th><th scope=col>displ</th><th scope=col>year</th><th scope=col>cyl</th><th scope=col>trans</th><th scope=col>drv</th><th scope=col>cty</th><th scope=col>hwy</th><th scope=col>fl</th><th scope=col>class</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>audi     </td><td>a4                </td><td>1.8</td><td>1999</td><td>4</td><td>auto(l5)  </td><td>f</td><td>18</td><td>29</td><td>p</td><td>compact</td></tr>
	<tr><td>audi     </td><td>a4                </td><td>1.8</td><td>1999</td><td>4</td><td>manual(m5)</td><td>f</td><td>21</td><td>29</td><td>p</td><td>compact</td></tr>
	<tr><td>audi     </td><td>a4                </td><td>2.0</td><td>2008</td><td>4</td><td>manual(m6)</td><td>f</td><td>20</td><td>31</td><td>p</td><td>compact</td></tr>
	<tr><td>audi     </td><td>a4                </td><td>2.0</td><td>2008</td><td>4</td><td>auto(av)  </td><td>f</td><td>21</td><td>30</td><td>p</td><td>compact</td></tr>
	<tr><td>audi     </td><td>a4                </td><td>2.8</td><td>1999</td><td>6</td><td>auto(l5)  </td><td>f</td><td>16</td><td>26</td><td>p</td><td>compact</td></tr>
	<tr><td>audi     </td><td>a4                </td><td>2.8</td><td>1999</td><td>6</td><td>manual(m5)</td><td>f</td><td>18</td><td>26</td><td>p</td><td>compact</td></tr>
	<tr><td>audi     </td><td>a4                </td><td>3.1</td><td>2008</td><td>6</td><td>auto(av)  </td><td>f</td><td>18</td><td>27</td><td>p</td><td>compact</td></tr>
	<tr><td>audi     </td><td>a4 quattro        </td><td>1.8</td><td>1999</td><td>4</td><td>manual(m5)</td><td>4</td><td>18</td><td>26</td><td>p</td><td>compact</td></tr>
	<tr><td>audi     </td><td>a4 quattro        </td><td>1.8</td><td>1999</td><td>4</td><td>auto(l5)  </td><td>4</td><td>16</td><td>25</td><td>p</td><td>compact</td></tr>
	<tr><td>audi     </td><td>a4 quattro        </td><td>2.0</td><td>2008</td><td>4</td><td>manual(m6)</td><td>4</td><td>20</td><td>28</td><td>p</td><td>compact</td></tr>
	<tr><td>audi     </td><td>a4 quattro        </td><td>2.0</td><td>2008</td><td>4</td><td>auto(s6)  </td><td>4</td><td>19</td><td>27</td><td>p</td><td>compact</td></tr>
	<tr><td>audi     </td><td>a4 quattro        </td><td>2.8</td><td>1999</td><td>6</td><td>auto(l5)  </td><td>4</td><td>15</td><td>25</td><td>p</td><td>compact</td></tr>
	<tr><td>audi     </td><td>a4 quattro        </td><td>2.8</td><td>1999</td><td>6</td><td>manual(m5)</td><td>4</td><td>17</td><td>25</td><td>p</td><td>compact</td></tr>
	<tr><td>audi     </td><td>a4 quattro        </td><td>3.1</td><td>2008</td><td>6</td><td>auto(s6)  </td><td>4</td><td>17</td><td>25</td><td>p</td><td>compact</td></tr>
	<tr><td>audi     </td><td>a4 quattro        </td><td>3.1</td><td>2008</td><td>6</td><td>manual(m6)</td><td>4</td><td>15</td><td>25</td><td>p</td><td>compact</td></tr>
	<tr><td>audi     </td><td>a6 quattro        </td><td>2.8</td><td>1999</td><td>6</td><td>auto(l5)  </td><td>4</td><td>15</td><td>24</td><td>p</td><td>midsize</td></tr>
	<tr><td>audi     </td><td>a6 quattro        </td><td>3.1</td><td>2008</td><td>6</td><td>auto(s6)  </td><td>4</td><td>17</td><td>25</td><td>p</td><td>midsize</td></tr>
	<tr><td>audi     </td><td>a6 quattro        </td><td>4.2</td><td>2008</td><td>8</td><td>auto(s6)  </td><td>4</td><td>16</td><td>23</td><td>p</td><td>midsize</td></tr>
	<tr><td>chevrolet</td><td>c1500 suburban 2wd</td><td>5.3</td><td>2008</td><td>8</td><td>auto(l4)  </td><td>r</td><td>14</td><td>20</td><td>r</td><td>suv    </td></tr>
	<tr><td>chevrolet</td><td>c1500 suburban 2wd</td><td>5.3</td><td>2008</td><td>8</td><td>auto(l4)  </td><td>r</td><td>11</td><td>15</td><td>e</td><td>suv    </td></tr>
	<tr><td>chevrolet</td><td>c1500 suburban 2wd</td><td>5.3</td><td>2008</td><td>8</td><td>auto(l4)  </td><td>r</td><td>14</td><td>20</td><td>r</td><td>suv    </td></tr>
	<tr><td>chevrolet</td><td>c1500 suburban 2wd</td><td>5.7</td><td>1999</td><td>8</td><td>auto(l4)  </td><td>r</td><td>13</td><td>17</td><td>r</td><td>suv    </td></tr>
	<tr><td>chevrolet</td><td>c1500 suburban 2wd</td><td>6.0</td><td>2008</td><td>8</td><td>auto(l4)  </td><td>r</td><td>12</td><td>17</td><td>r</td><td>suv    </td></tr>
	<tr><td>chevrolet</td><td>corvette          </td><td>5.7</td><td>1999</td><td>8</td><td>manual(m6)</td><td>r</td><td>16</td><td>26</td><td>p</td><td>2seater</td></tr>
	<tr><td>chevrolet</td><td>corvette          </td><td>5.7</td><td>1999</td><td>8</td><td>auto(l4)  </td><td>r</td><td>15</td><td>23</td><td>p</td><td>2seater</td></tr>
	<tr><td>chevrolet</td><td>corvette          </td><td>6.2</td><td>2008</td><td>8</td><td>manual(m6)</td><td>r</td><td>16</td><td>26</td><td>p</td><td>2seater</td></tr>
	<tr><td>chevrolet</td><td>corvette          </td><td>6.2</td><td>2008</td><td>8</td><td>auto(s6)  </td><td>r</td><td>15</td><td>25</td><td>p</td><td>2seater</td></tr>
	<tr><td>chevrolet</td><td>corvette          </td><td>7.0</td><td>2008</td><td>8</td><td>manual(m6)</td><td>r</td><td>15</td><td>24</td><td>p</td><td>2seater</td></tr>
	<tr><td>chevrolet</td><td>k1500 tahoe 4wd   </td><td>5.3</td><td>2008</td><td>8</td><td>auto(l4)  </td><td>4</td><td>14</td><td>19</td><td>r</td><td>suv    </td></tr>
	<tr><td>chevrolet</td><td>k1500 tahoe 4wd   </td><td>5.3</td><td>2008</td><td>8</td><td>auto(l4)  </td><td>4</td><td>11</td><td>14</td><td>e</td><td>suv    </td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>toyota    </td><td>toyota tacoma 4wd</td><td>3.4</td><td>1999</td><td>6</td><td>auto(l4)  </td><td>4</td><td>15</td><td>19</td><td>r</td><td>pickup    </td></tr>
	<tr><td>toyota    </td><td>toyota tacoma 4wd</td><td>4.0</td><td>2008</td><td>6</td><td>manual(m6)</td><td>4</td><td>15</td><td>18</td><td>r</td><td>pickup    </td></tr>
	<tr><td>toyota    </td><td>toyota tacoma 4wd</td><td>4.0</td><td>2008</td><td>6</td><td>auto(l5)  </td><td>4</td><td>16</td><td>20</td><td>r</td><td>pickup    </td></tr>
	<tr><td>volkswagen</td><td>gti              </td><td>2.0</td><td>1999</td><td>4</td><td>manual(m5)</td><td>f</td><td>21</td><td>29</td><td>r</td><td>compact   </td></tr>
	<tr><td>volkswagen</td><td>gti              </td><td>2.0</td><td>1999</td><td>4</td><td>auto(l4)  </td><td>f</td><td>19</td><td>26</td><td>r</td><td>compact   </td></tr>
	<tr><td>volkswagen</td><td>gti              </td><td>2.0</td><td>2008</td><td>4</td><td>manual(m6)</td><td>f</td><td>21</td><td>29</td><td>p</td><td>compact   </td></tr>
	<tr><td>volkswagen</td><td>gti              </td><td>2.0</td><td>2008</td><td>4</td><td>auto(s6)  </td><td>f</td><td>22</td><td>29</td><td>p</td><td>compact   </td></tr>
	<tr><td>volkswagen</td><td>gti              </td><td>2.8</td><td>1999</td><td>6</td><td>manual(m5)</td><td>f</td><td>17</td><td>24</td><td>r</td><td>compact   </td></tr>
	<tr><td>volkswagen</td><td>jetta            </td><td>1.9</td><td>1999</td><td>4</td><td>manual(m5)</td><td>f</td><td>33</td><td>44</td><td>d</td><td>compact   </td></tr>
	<tr><td>volkswagen</td><td>jetta            </td><td>2.0</td><td>1999</td><td>4</td><td>manual(m5)</td><td>f</td><td>21</td><td>29</td><td>r</td><td>compact   </td></tr>
	<tr><td>volkswagen</td><td>jetta            </td><td>2.0</td><td>1999</td><td>4</td><td>auto(l4)  </td><td>f</td><td>19</td><td>26</td><td>r</td><td>compact   </td></tr>
	<tr><td>volkswagen</td><td>jetta            </td><td>2.0</td><td>2008</td><td>4</td><td>auto(s6)  </td><td>f</td><td>22</td><td>29</td><td>p</td><td>compact   </td></tr>
	<tr><td>volkswagen</td><td>jetta            </td><td>2.0</td><td>2008</td><td>4</td><td>manual(m6)</td><td>f</td><td>21</td><td>29</td><td>p</td><td>compact   </td></tr>
	<tr><td>volkswagen</td><td>jetta            </td><td>2.5</td><td>2008</td><td>5</td><td>auto(s6)  </td><td>f</td><td>21</td><td>29</td><td>r</td><td>compact   </td></tr>
	<tr><td>volkswagen</td><td>jetta            </td><td>2.5</td><td>2008</td><td>5</td><td>manual(m5)</td><td>f</td><td>21</td><td>29</td><td>r</td><td>compact   </td></tr>
	<tr><td>volkswagen</td><td>jetta            </td><td>2.8</td><td>1999</td><td>6</td><td>auto(l4)  </td><td>f</td><td>16</td><td>23</td><td>r</td><td>compact   </td></tr>
	<tr><td>volkswagen</td><td>jetta            </td><td>2.8</td><td>1999</td><td>6</td><td>manual(m5)</td><td>f</td><td>17</td><td>24</td><td>r</td><td>compact   </td></tr>
	<tr><td>volkswagen</td><td>new beetle       </td><td>1.9</td><td>1999</td><td>4</td><td>manual(m5)</td><td>f</td><td>35</td><td>44</td><td>d</td><td>subcompact</td></tr>
	<tr><td>volkswagen</td><td>new beetle       </td><td>1.9</td><td>1999</td><td>4</td><td>auto(l4)  </td><td>f</td><td>29</td><td>41</td><td>d</td><td>subcompact</td></tr>
	<tr><td>volkswagen</td><td>new beetle       </td><td>2.0</td><td>1999</td><td>4</td><td>manual(m5)</td><td>f</td><td>21</td><td>29</td><td>r</td><td>subcompact</td></tr>
	<tr><td>volkswagen</td><td>new beetle       </td><td>2.0</td><td>1999</td><td>4</td><td>auto(l4)  </td><td>f</td><td>19</td><td>26</td><td>r</td><td>subcompact</td></tr>
	<tr><td>volkswagen</td><td>new beetle       </td><td>2.5</td><td>2008</td><td>5</td><td>manual(m5)</td><td>f</td><td>20</td><td>28</td><td>r</td><td>subcompact</td></tr>
	<tr><td>volkswagen</td><td>new beetle       </td><td>2.5</td><td>2008</td><td>5</td><td>auto(s6)  </td><td>f</td><td>20</td><td>29</td><td>r</td><td>subcompact</td></tr>
	<tr><td>volkswagen</td><td>passat           </td><td>1.8</td><td>1999</td><td>4</td><td>manual(m5)</td><td>f</td><td>21</td><td>29</td><td>p</td><td>midsize   </td></tr>
	<tr><td>volkswagen</td><td>passat           </td><td>1.8</td><td>1999</td><td>4</td><td>auto(l5)  </td><td>f</td><td>18</td><td>29</td><td>p</td><td>midsize   </td></tr>
	<tr><td>volkswagen</td><td>passat           </td><td>2.0</td><td>2008</td><td>4</td><td>auto(s6)  </td><td>f</td><td>19</td><td>28</td><td>p</td><td>midsize   </td></tr>
	<tr><td>volkswagen</td><td>passat           </td><td>2.0</td><td>2008</td><td>4</td><td>manual(m6)</td><td>f</td><td>21</td><td>29</td><td>p</td><td>midsize   </td></tr>
	<tr><td>volkswagen</td><td>passat           </td><td>2.8</td><td>1999</td><td>6</td><td>auto(l5)  </td><td>f</td><td>16</td><td>26</td><td>p</td><td>midsize   </td></tr>
	<tr><td>volkswagen</td><td>passat           </td><td>2.8</td><td>1999</td><td>6</td><td>manual(m5)</td><td>f</td><td>18</td><td>26</td><td>p</td><td>midsize   </td></tr>
	<tr><td>volkswagen</td><td>passat           </td><td>3.6</td><td>2008</td><td>6</td><td>auto(s6)  </td><td>f</td><td>17</td><td>26</td><td>p</td><td>midsize   </td></tr>
</tbody>
</table>




```R
# Left
p1 <- ggplot(mpg, aes(x = displ, y = hwy, color = class)) +
  geom_point()

# Right
p2 <- ggplot(mpg, aes(x = displ, y = hwy, shape = class)) +
  geom_point()

options(repr.plot.width = 10, repr.plot.height = 5)
grid.arrange(p1, p2, ncol=2)
```

    Warning message:
    "[1m[22mThe shape palette can deal with a maximum of 6 discrete values because more
    than 6 becomes difficult to discriminate
    [36mi[39m you have requested 7 values. Consider specifying shapes manually if you need
      that many have them."
    Warning message:
    "[1m[22mRemoved 62 rows containing missing values (`geom_point()`)."



    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_4_1.png)
    



```R
# Left
p1 <- ggplot(mpg, aes(x = displ, y = hwy, size = class)) +
  geom_point()
#> Warning: Using size for a discrete variable is not advised.

# Right
p2 <- ggplot(mpg, aes(x = displ, y = hwy, alpha = class)) +
  geom_point()
#> Warning: Using alpha for a discrete variable is not advised.

options(repr.plot.width = 10, repr.plot.height = 5)
grid.arrange(p1, p2, ncol=2)
```

    Warning message:
    "[1m[22mUsing [32msize[39m for a discrete variable is not advised."
    Warning message:
    "[1m[22mUsing alpha for a discrete variable is not advised."



    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_5_1.png)
    



```R
ggplot(mpg, aes(x = displ, y = hwy)) + 
  geom_point(color = "blue")
```


    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_6_0.png)
    


### Exercise 9.2
1. Create a scatterplot of hwy vs. displ where the points are pink filled in triangles.



```R
print("hello")
```

    [1] "hello"


2. Why did the following code not result in a plot with blue points?


```R
ggplot(mpg) + 
  geom_point(aes(x = displ, y = hwy, color = "blue"))
```


    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_10_0.png)
    


3. What does the stroke aesthetic do? What shapes does it work with? (Hint: use ?geom_point)


```R

```

4. What happens if you map an aesthetic to something other than a variable name, like aes(color = displ < 5)? Note, you’ll also need to specify x and y.


```R

```

## Geometric objects (geom)



```R
# Left
p1 <- ggplot(mpg, aes(x = displ, y = hwy)) + 
  geom_point()

# Right
p2 <- ggplot(mpg, aes(x = displ, y = hwy)) + 
  geom_smooth()
#> `geom_smooth()` using method = 'loess' and formula = 'y ~ x'
options(repr.plot.width = 20, repr.plot.height = 5)
grid.arrange(p1, p2, ncol=2)
```

    [1m[22m`geom_smooth()` using method = 'loess' and formula = 'y ~ x'



    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_16_1.png)
    



```R
# Left
p1 <- ggplot(mpg, aes(x = displ, y = hwy, shape = drv)) + 
  geom_smooth()

# Right
p2 <- ggplot(mpg, aes(x = displ, y = hwy, linetype = drv)) + 
  geom_smooth()

grid.arrange(p1, p2, ncol=2)
```

    [1m[22m`geom_smooth()` using method = 'loess' and formula = 'y ~ x'
    [1m[22m`geom_smooth()` using method = 'loess' and formula = 'y ~ x'



    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_17_1.png)
    



```R
ggplot(mpg, aes(x = displ, y = hwy, color = drv)) + 
  geom_point() +
  geom_smooth(aes(linetype = drv))

options(repr.plot.width = 10, repr.plot.height = 5)
```

    [1m[22m`geom_smooth()` using method = 'loess' and formula = 'y ~ x'



    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_18_1.png)
    



```R
# Left
p1 <- ggplot(mpg, aes(x = displ, y = hwy)) +
  geom_smooth()

# Middle
p2 <- ggplot(mpg, aes(x = displ, y = hwy)) +
  geom_smooth(aes(group = drv))

# Right
p3 <- ggplot(mpg, aes(x = displ, y = hwy)) +
  geom_smooth(aes(color = drv), show.legend = FALSE)

options(repr.plot.width = 20, repr.plot.height = 5)
grid.arrange(p1, p2, p3, ncol=3)
```

    [1m[22m`geom_smooth()` using method = 'loess' and formula = 'y ~ x'
    [1m[22m`geom_smooth()` using method = 'loess' and formula = 'y ~ x'
    [1m[22m`geom_smooth()` using method = 'loess' and formula = 'y ~ x'



    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_19_1.png)
    



```R
ggplot(mpg, aes(x = displ, y = hwy)) + 
  geom_point(aes(color = class)) + 
  geom_point( 
    aes(color = class), 
    shape = "circle open", 
    size = 3

    
  ) +
  geom_smooth()
options(repr.plot.width = 10, repr.plot.height = 5)
```

    [1m[22m`geom_smooth()` using method = 'loess' and formula = 'y ~ x'



    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_20_1.png)
    



```R
ggplot(mpg, aes(x = displ, y = hwy)) + 
  # Draw all black points
  geom_point() +
  # Draw red points of class 2seater
  geom_point(
    data = mpg |> filter(class == "2seater"), 
    color = "red"
  ) +
  # draw red circle around points of class 2seater
  geom_point(
    data = mpg |> filter(class == "2seater"), 
    shape = "circle open", size = 3, color = "red"
  ) +
    # Draw blue points of class compact
  geom_point(
    data = mpg |> filter(class == "compact"), 
    color = "blue"
  ) +
  # draw blue circle around points of class compact
  geom_point(
    data = mpg |> filter(class == "compact"), 
    shape = "circle open", size = 3, color = "blue"
  )
```


    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_21_0.png)
    


### Exercises 9.3
1. What geom would you use to draw a line chart? A boxplot? A histogram? An area chart?

2. Earlier in this chapter we used show.legend without explaining it:

What does show.legend = FALSE do here? What happens if you remove it? Why do you think we used it earlier?


```R
ggplot(mpg, aes(x = displ, y = hwy)) +
  geom_smooth(aes(color = drv), show.legend = FALSE)
```

    [1m[22m`geom_smooth()` using method = 'loess' and formula = 'y ~ x'



    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_24_1.png)
    


3. What does the `se` argument to `geom_smooth()` do?

4. Recreate the R code necessary to generate the following graphs. Note that wherever a categorical variable is used in the plot, it’s `drv`.


```R
p1 <- ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point() + 
  geom_smooth(se = FALSE)

p2 <- ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point() + 
  geom_smooth(mapping = aes(x = displ, y = hwy, group = drv), se = FALSE)

p3 <- ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + 
  geom_point(size = 4) + 
  geom_smooth(mapping = aes(x = displ, y = hwy, group = drv, linewidth = 2), se = FALSE)

p4 <- ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point(mapping = aes(color = drv, size = 4)) + 
  geom_smooth(se = FALSE)

p5 <- ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + 
  geom_point(size = 4) + 
  geom_smooth(mapping = aes(x = displ, y = hwy, group = drv, linewidth = 2, lty = drv), se = FALSE)

p6 <- ggplot(data = mpg, mapping = aes(x = displ, y = hwy, fill = drv)) + 
  geom_point(shape=21, color="white", size=4)  # alpha = factor(cyl)

options(repr.plot.width = 20, repr.plot.height = 15)
grid.arrange(p1, p2, p3, p4, p5, p6, ncol=2, nrow = 3)
```

    [1m[22m`geom_smooth()` using method = 'loess' and formula = 'y ~ x'
    [1m[22m`geom_smooth()` using method = 'loess' and formula = 'y ~ x'
    [1m[22m`geom_smooth()` using method = 'loess' and formula = 'y ~ x'
    [1m[22m`geom_smooth()` using method = 'loess' and formula = 'y ~ x'
    [1m[22m`geom_smooth()` using method = 'loess' and formula = 'y ~ x'



    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_27_1.png)
    


## Facets
* `facet_wrap()`: splits a plot into subplots that each display one subset of the data based on a categorical variable.
* `facet_grid()`: facet the plot with the combination of two variables. The first argument of facet_grid() is also a formula, but now it’s a double sided formula likes: `rows ~ cols`.


```R
ggplot(mpg, aes(x = displ, y = hwy)) + 
  geom_point() + 
  facet_wrap(~cyl)

options(repr.plot.width = 10, repr.plot.height = 5)
```


    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_29_0.png)
    



```R
ggplot(mpg, aes(x = displ, y = hwy)) + 
  geom_point() + 
  facet_grid(drv ~ cyl)
```


    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_30_0.png)
    



```R
ggplot(mpg, aes(x = displ, y = hwy)) + 
  geom_point() + 
  facet_grid(drv ~ cyl, scales = "free_x") # free, free_x, free_y
```


    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_31_0.png)
    


### Exercises 9.4

1. What happens if you facet on a continuous variable?

2. What do the empty cells in the plot above with `facet_grid(drv ~ cyl)` mean? Run the following code. How do they relate to the resulting plot?


```R
ggplot(mpg) + 
  geom_point(aes(x = drv, y = cyl))
```


    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_33_0.png)
    


3. What plots does the following code make? What does `.` do?



```R
ggplot(mpg) + 
  geom_point(aes(x = displ, y = hwy)) +
  facet_grid(drv ~ .)

ggplot(mpg) + 
  geom_point(aes(x = displ, y = hwy)) +
  facet_grid(. ~ cyl)
```


    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_35_0.png)
    



    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_35_1.png)
    


4. Take the first faceted plot in this section. What are the advantages to using faceting instead of the color aesthetic? What are the disadvantages? How might the balance change if you had a larger dataset?


```R
ggplot(mpg) + 
  geom_point(aes(x = displ, y = hwy)) + 
  facet_wrap(~ class, nrow = 2)
```


    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_37_0.png)
    


5. Read `?facet_wrap`. What does nrow do? What does ncol do? What other options control the layout of the individual panels? Why doesn’t `facet_grid()` have `nrow` and `ncol` arguments?


```R
?facet_wrap
```

    facet_wrap               package:ggplot2               R Documentation
    
    _W_r_a_p _a _1_d _r_i_b_b_o_n _o_f _p_a_n_e_l_s _i_n_t_o _2_d
    
    _D_e_s_c_r_i_p_t_i_o_n:
    
         'facet_wrap()' wraps a 1d sequence of panels into 2d. This is
         generally a better use of screen space than 'facet_grid()' because
         most displays are roughly rectangular.
    
    _U_s_a_g_e:
    
         facet_wrap(
           facets,
           nrow = NULL,
           ncol = NULL,
           scales = "fixed",
           shrink = TRUE,
           labeller = "label_value",
           as.table = TRUE,
           switch = deprecated(),
           drop = TRUE,
           dir = "h",
           strip.position = "top"
         )
         
    _A_r_g_u_m_e_n_t_s:
    
      facets: A set of variables or expressions quoted by 'vars()' and
              defining faceting groups on the rows or columns dimension.
              The variables can be named (the names are passed to
              'labeller').
    
              For compatibility with the classic interface, can also be a
              formula or character vector. Use either a one sided formula,
              '~a + b', or a character vector, 'c("a", "b")'.
    
    nrow, ncol: Number of rows and columns.
    
      scales: Should scales be fixed ('"fixed"', the default), free
              ('"free"'), or free in one dimension ('"free_x"',
              '"free_y"')?
    
      shrink: If 'TRUE', will shrink scales to fit output of statistics,
              not raw data. If 'FALSE', will be range of raw data before
              statistical summary.
    
    labeller: A function that takes one data frame of labels and returns a
              list or data frame of character vectors. Each input column
              corresponds to one factor. Thus there will be more than one
              with 'vars(cyl, am)'. Each output column gets displayed as
              one separate line in the strip label. This function should
              inherit from the "labeller" S3 class for compatibility with
              'labeller()'. You can use different labeling functions for
              different kind of labels, for example use 'label_parsed()'
              for formatting facet labels. 'label_value()' is used by
              default, check it for more details and pointers to other
              options.
    
    as.table: If 'TRUE', the default, the facets are laid out like a table
              with highest values at the bottom-right. If 'FALSE', the
              facets are laid out like a plot with the highest value at the
              top-right.
    
      switch: By default, the labels are displayed on the top and right of
              the plot. If '"x"', the top labels will be displayed to the
              bottom. If '"y"', the right-hand side labels will be
              displayed to the left. Can also be set to '"both"'.
    
        drop: If 'TRUE', the default, all factor levels not used in the
              data will automatically be dropped. If 'FALSE', all factor
              levels will be shown, regardless of whether or not they
              appear in the data.
    
         dir: Direction: either '"h"' for horizontal, the default, or
              '"v"', for vertical.
    
    strip.position: By default, the labels are displayed on the top of the
              plot. Using 'strip.position' it is possible to place the
              labels on either of the four sides by setting 'strip.position
              = c("top", "bottom", "left", "right")'
    
    _E_x_a_m_p_l_e_s:
    
         p <- ggplot(mpg, aes(displ, hwy)) + geom_point()
         
         # Use vars() to supply faceting variables:
         p + facet_wrap(vars(class))
         
         # Control the number of rows and columns with nrow and ncol
         p + facet_wrap(vars(class), nrow = 4)
         
         
         # You can facet by multiple variables
         ggplot(mpg, aes(displ, hwy)) +
           geom_point() +
           facet_wrap(vars(cyl, drv))
         
         # Use the `labeller` option to control how labels are printed:
         ggplot(mpg, aes(displ, hwy)) +
           geom_point() +
           facet_wrap(vars(cyl, drv), labeller = "label_both")
         
         # To change the order in which the panels appear, change the levels
         # of the underlying factor.
         mpg$class2 <- reorder(mpg$class, mpg$displ)
         ggplot(mpg, aes(displ, hwy)) +
           geom_point() +
           facet_wrap(vars(class2))
         
         # By default, the same scales are used for all panels. You can allow
         # scales to vary across the panels with the `scales` argument.
         # Free scales make it easier to see patterns within each panel, but
         # harder to compare across panels.
         ggplot(mpg, aes(displ, hwy)) +
           geom_point() +
           facet_wrap(vars(class), scales = "free")
         
         # To repeat the same data in every panel, simply construct a data frame
         # that does not contain the faceting variable.
         ggplot(mpg, aes(displ, hwy)) +
           geom_point(data = transform(mpg, class = NULL), colour = "grey85") +
           geom_point() +
           facet_wrap(vars(class))
         
         # Use `strip.position` to display the facet labels at the side of your
         # choice. Setting it to `bottom` makes it act as a subtitle for the axis.
         # This is typically used with free scales and a theme without boxes around
         # strip labels.
         ggplot(economics_long, aes(date, value)) +
           geom_line() +
           facet_wrap(vars(variable), scales = "free_y", nrow = 2, strip.position = "top") +
           theme(strip.background = element_blank(), strip.placement = "outside")
         

6. Which of the following plots makes it easier to compare engine size (displ) across cars with different drive trains? What does this say about when to place a faceting variable across rows or columns?


```R
ggplot(mpg, aes(x = displ)) + 
  geom_histogram() + 
  facet_grid(drv ~ .)

ggplot(mpg, aes(x = displ)) + 
  geom_histogram() +
  facet_grid(. ~ drv)
```

    [1m[22m`stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
    [1m[22m`stat_bin()` using `bins = 30`. Pick better value with `binwidth`.



    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_41_1.png)
    



    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_41_2.png)
    


7. Recreate the following plot using `facet_wrap()` instead of `facet_grid()`. How do the positions of the facet labels change?




```R
ggplot(mpg) + 
  geom_point(aes(x = displ, y = hwy)) +
  facet_grid(drv ~ .)
```


    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_43_0.png)
    


## Statistical transformations



```R
ggplot(diamonds, aes(x = cut)) + 
  geom_bar()
```


    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_45_0.png)
    


### Exercises 9.5



```R

```

## Position adjustments
You can color a bar chart using either the `color` aesthetic, or, more usefully, the `fill` aesthetic:


```R
# Left
p1 <- ggplot(mpg, aes(x = drv, color = drv)) + 
  geom_bar()

# Right
p2 <- ggplot(mpg, aes(x = drv, fill = drv)) + 
  geom_bar()

options(repr.plot.width = 10, repr.plot.height = 5)
grid.arrange(p1, p2, ncol=2)
```


    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_49_0.png)
    



```R
ggplot(mpg, aes(x = drv, fill = class)) + 
  geom_bar()

options(repr.plot.width = 5, repr.plot.height = 5)
```


    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_50_0.png)
    


The stacking is performed automatically using the position adjustment specified by the `position` argument. If you don’t want a stacked bar chart, you can use one of three other options: "`identity`", "`dodge`" or "`fill`".
* `position = "identity"` will place each object exactly where it falls in the context of the graph. This is not very useful for bars, because it overlaps them. To see that overlapping we either need to make the bars slightly transparent by setting `alpha` to a small value, or completely transparent by setting `fill = NA`.


```R
# Left
p1 <- ggplot(mpg, aes(x = drv, fill = class)) + 
  geom_bar(alpha = 1/5, position = "identity")

# Right
p2 <- ggplot(mpg, aes(x = drv, color = class)) + 
  geom_bar(fill = NA, position = "identity")

options(repr.plot.width = 10, repr.plot.height = 5)
grid.arrange(p1, p2, ncol=2)
```


    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_52_0.png)
    


The identity position adjustment is more useful for 2d geoms, like points, where it is the default.

* `position = "fill"` works like stacking, but makes each set of stacked bars the same height. This makes it easier to compare proportions across groups.

* `position = "dodge"` places overlapping objects directly *beside* one another. This makes it easier to compare individual values.


```R
# Left
p1 <- ggplot(mpg, aes(x = drv, fill = class)) + 
  geom_bar(position = "fill")

# Right
p2 <- ggplot(mpg, aes(x = drv, fill = class)) + 
  geom_bar(position = "dodge")

options(repr.plot.width = 10, repr.plot.height = 5)
grid.arrange(p1, p2, ncol=2)
```


    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_54_0.png)
    



```R
# overplotting and jittering
ggplot(mpg, aes(x = displ, y = hwy)) + 
  geom_point(position = "jitter") # or geom_jitter()
```


    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_55_0.png)
    


### Exercises 9.6
1. What is the problem with the following plot? How could you improve it?


```R
ggplot(mpg, aes(x = cty, y = hwy)) + 
  geom_point()
```


    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_57_0.png)
    


2. What, if anything, is the difference between the two plots? Why?


```R
p1 <- ggplot(mpg, aes(x = displ, y = hwy)) +
  geom_point()
p2 <- ggplot(mpg, aes(x = displ, y = hwy)) +
  geom_point(position = "identity")

options(repr.plot.width = 10, repr.plot.height = 5)
grid.arrange(p1, p2, ncol=2)
```


    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_59_0.png)
    


3. What parameters to `geom_jitter() `control the amount of jittering?

4. Compare and contrast `geom_jitter()` with `geom_count()`.

5. What’s the default position adjustment for `geom_boxplot()`? Create a visualization of the mpg dataset that demonstrates it.

## Coordinate systems



```R
nz <- map_data("nz")

p1 <- ggplot(nz, aes(x = long, y = lat, group = group)) +
  geom_polygon(fill = "white", color = "black")

p2 <- ggplot(nz, aes(x = long, y = lat, group = group)) +
  geom_polygon(fill = "white", color = "black") +
  coord_quickmap()

options(repr.plot.width = 10, repr.plot.height = 5)
grid.arrange(p1, p2, ncol=2)
```


    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_62_0.png)
    



```R
bar <- ggplot(data = diamonds) + 
  geom_bar(
    mapping = aes(x = clarity, fill = clarity), 
    show.legend = FALSE,
    width = 1
  ) + 
  theme(aspect.ratio = 1)

p1 <- bar + coord_flip()
p2 <- bar + coord_polar()
options(repr.plot.width = 10, repr.plot.height = 5)
grid.arrange(p1, p2, ncol=2)
```


    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_63_0.png)
    


### Exercises 9.7
1. Turn a stacked bar chart into a pie chart using `coord_polar()`.

3. What’s the difference between `coord_quickmap()` and `coord_map()`?

4. What does the following plot tell you about the relationship between city and highway mpg? Why is `coord_fixed()` important? What does `geom_abline()` do?


```R
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) +
  geom_point() + 
  geom_abline() +
  coord_fixed()
```


    
![png](/assets/img/R4DS-DataViz-Layers_files/R4DS-DataViz-Layers_65_0.png)
    


## The layered grammar of graphics
```
ggplot(data = <DATA>) + 
  <GEOM_FUNCTION>(
     mapping = aes(<MAPPINGS>),
     stat = <STAT>, 
     position = <POSITION>
  ) +
  <COORDINATE_FUNCTION> +
  <FACET_FUNCTION>
```

## Summary

* Very useful [Cheatsheets](https://posit.co/resources/cheatsheets/)
* [ggplot2 package website](https://ggplot2.tidyverse.org).

