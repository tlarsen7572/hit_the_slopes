## Hit The Slopes

![Logo](/hit_the_slopes.png "Hit The Slopes")

Calculate slope and r<sup>2</sup> in your dataset for a defined rolling window. This is useful if you want to see the evolution of trends in your dataset over time.

#### Install

Copy the repository to any directory on your PC and run the 'makeLink.bat' script. A symbolic link will be created in C:\ProgramData\Alteryx\Tools pointing to the folder containing the plugin files. You can find the new tool in the Laboratory tool category in Designer.

#### Some more details...

First off, you will notice that this custom tool is actually a macro, proof that I do not *always* reach for code when I create custom tools. I think I deserve some kudos for that.

But more importantly, what does this tool actually do?

Let's assume a dataset with the following data. Let's further assume X is a timeseries, such as the number of minutes since the beginning. Y can be any activity we are measuring over time.

|    X |    Y |
| ---: | ---: |
|    1 |  1.0 |
|    2 |  1.1 |
|    3 |  1.2 |
|    4 |  1.3 |
|    5 |  1.4 |
|    6 |  1.5 |
|    7 |  1.6 |
|    8 |  1.7 |
|    9 |  4.7 |
|   10 |  7.7 |
|   11 | 10.7 |
|   12 | 13.7 |
|   13 | 16.7 |
|   14 | 19.7 |
|   15 | 22.7 |
|   16 | 25.7 |
|   17 | 28.7 |
|   18 | 31.7 |
|   19 | 34.7 |
|   20 | 37.7 |

A chart of the data looks something like this. You will notice the distinctive elbow starting at time 9.

![line chart](/images/activity_over_time.PNG "Activity over time")

The custom tool essentially breaks up the data into rolling windows and calculates the slope of the data for each window. It also calculates r<sup>2</sup> of the fitted line, to provide a measure of the quality of the fit. If we decide to use a 6-minute rolling window, the output would be the following. The slope and r<sup>2</sup> calculated on each row is for the current and prior five rows.

|    X |    Y |  Slope | R Squared |
| ---: | ---: | -----: | --------: |
|    1 |  1.0 | <null> |    <null> |
|    2 |  1.1 | <null> |    <null> |
|    3 |  1.2 | <null> |    <null> |
|    4 |  1.3 | <null> |    <null> |
|    5 |  1.4 | <null> |    <null> |
|    6 |  1.5 |   0.10 |      1.00 |
|    7 |  1.6 |   0.10 |      1.00 |
|    8 |  1.7 |   0.10 |      1.00 |
|    9 |  4.7 |   0.51 |      0.54 |
|   10 |  7.7 |   1.18 |      0.73 |
|   11 | 10.7 |   1.92 |      0.88 |
|   12 | 13.7 |   2.59 |      0.97 |
|   13 | 16.7 |   3.00 |      1.00 |
|   14 | 19.7 |   3.00 |      1.00 |
|   15 | 22.7 |   3.00 |      1.00 |
|   16 | 25.7 |   3.00 |      1.00 |
|   17 | 28.7 |   3.00 |      1.00 |
|   18 | 31.7 |   3.00 |      1.00 |
|   19 | 34.7 |   3.00 |      1.00 |
|   20 | 37.7 |   3.00 |      1.00 |

If we chart the slope and r<sup>2</sup> alongside the X and Y values, we get the following.

![line chart](/images/slope_and_r_squared.PNG "Slope and r squared")

In this example, seeing the evolution of slope and r<sup>2</sup> over time lets you know that, initially, the data is very linear at a slope of 0.1. However, starting at time 9, the slope changes to become much steeper. We see r<sup>2</sup> degrade sharply and gradually recover as the slope increases to its new equilibrium. If we were viewing these charts in real time, we would be able to identify a change to our equilibrium starting at time 9. By time 13 we could identify the new equilibrium and begin to make assumptions about the future state of the system.
