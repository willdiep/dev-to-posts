---
title: Machine Learning Basics
published: true
---

### Introduction to Linear Regression
The purpose of machine learning is often to create a model that explains some real-world data, so that we can predict what may happen next, with different inputs.

The simplest model that we can fit to data is a line. When we are trying to find a line that fits a set of data best, we are performing Linear Regression.

We often want to find lines to fit data, so that we can predict unknowns. For example:

- The market price of a house vs. the square footage of a house. Can we predict how much a house will sell for, given its size?
- The tax rate of a country vs. its GDP. Can we predict taxation based on a country’s GDP?
- The amount of chips left in the bag vs. number of chips taken. Can we predict how much longer this bag of chips will last, given how much people at this party have been eating?
Imagine that we had this set of weights plotted against heights of a large set of professional baseball players:

```python
import codecademylib3_seaborn
import matplotlib.pyplot as plt

months = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
revenue = [52, 74, 79, 95, 115, 110, 129, 126, 147, 146, 156, 184]

plt.plot(months, revenue, "o")

plt.title("Sandra's Lemonade Stand")

plt.xlabel("Months")
plt.ylabel("Revenue ($)")
month_13 = 200
plt.show()
```

### Points and Lines
In the last exercise, you were probably able to make a rough estimate about the next data point for Sandra’s lemonade stand without thinking too hard about it. For our program to make the same level of guess, we have to determine what a line would look like through those data points.

A line is determined by its slope and its intercept. In other words, for each point y on a line we can say:

y = m x + by=mx+b
where m is the slope, and b is the intercept. y is a given point on the y-axis, and it corresponds to a given x on the x-axis.

The slope is a measure of how steep the line is, while the intercept is a measure of where the line hits the y-axis.

```python
import codecademylib3_seaborn
import matplotlib.pyplot as plt
months = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12]
revenue = [52, 74, 79, 95, 115, 110, 129, 126, 147, 146, 156, 184]

#slope:
m = 10
#intercept:
b = 53

y = [m*x + b for x in months]

plt.plot(months, revenue, "o")
plt.plot(months, y)

plt.show()

```

###  Loss
When we think about how we can assign a slope and intercept to fit a set of points, we have to define what the best fit is.

For each data point, we calculate loss, a number that measures how bad the model’s (in this case, the line’s) prediction was. You may have seen this being referred to as error.

We can think about loss as the squared distance from the point to the line. We do the squared distance (instead of just the distance) so that points above and below the line both contribute to total loss in the same way:

```python
x = [1, 2, 3]
y = [5, 1, 3]

#y = x
m1 = 1
b1 = 0

#y = 0.5x + 1
m2 = 0.5
b2 = 1

y_predicted1 = [m1*x_val + b1 for x_val in x]
y_predicted2 = [m2*x_val + b2 for x_val in x]

total_loss1 = 0
total_loss2 = 0

for i in range(len(y)):
  total_loss1 += (y[i] - y_predicted1[i])**2
  total_loss2 += (y[i] - y_predicted2[i])**2
  
print(total_loss1, total_loss2)
better_fit = 2
```

### Minimizing Loss
The goal of a linear regression model is to find the slope and intercept pair that minimizes loss on average across all of the data.

The interactive visualization in the browser lets you try to find the line of best fit for a random set of data points:

The slider on the left controls the m (slope)
The slider on the right controls the b (intercept)
You can see the total loss on the right side of the visualization. To get the line of best fit, we want this loss to be as small as possible.

To check if you got the best line, check the “Plot Best-Fit” box.

Randomize a new set of points and try to fit a new line by entering the number of points you want (try 8!) in the textbox and pressing Randomize Points.

### Gradient Descent for Intercept
As we try to minimize loss, we take each parameter we are changing, and move it as long as we are decreasing loss. It’s like we are moving down a hill, and stop once we reach the bottom:

![](https://www.andreaperlato.com/img/gradientderivate.png)

<sub>[Image credits to andreaperlato](https://www.andreaperlato.com/theorypost/gradient-descent-step-by-step/)</sub>


The process by which we do this is called gradient descent. We move in the direction that decreases our loss the most. Gradient refers to the slope of the curve at any point.

For example, let’s say we are trying to find the intercept for a line. We currently have a guess of 10 for the intercept. At the point of 10 on the curve, the slope is downward. Therefore, if we increase the intercept, we should be lowering the loss. So we follow the gradient downwards.

```python
def get_gradient_at_b(x, y, m, b):
    diff = 0
    N = len(x)
    for i in range(0, len(x)):
      y_val = y[i]
      x_val = x[i]
      diff += (y_val - ((m * x_val) + b))

    b_gradient = -2/N * diff
    return b_gradient
```

### Gradient Descent for Slope
We have a function to find the gradient of b at every point. To find the m gradient, or the way the loss changes as the slope of our line changes, we can use this formula:

\frac{2}{N}\sum_{i=1}^{N}-x_i(y_i-(mx_i+b)) 
N
2
​	  
i=1
∑
N
​	 −x 
i
​	 (y 
i
​	 −(mx 
i
​	 +b))
Once more:

N is the number of points you have in your dataset
m is the current gradient guess
b is the current intercept guess
To find the m gradient:

we find the sum of x_value * (y_value - (m*x_value + b)) for all the y_values and x_values we have
and then we multiply the sum by a factor of -2/N. N is the number of points we have.
Once we have a way to calculate both the m gradient and the b gradient, we’ll be able to follow both of those gradients downwards to the point of lowest loss for both the m value and the b value. Then, we’ll have the best m and the best b to fit our data!


```python
def get_gradient_at_m(x, y, m, b):
    diff = 0
    N = len(x)
    for i in range(N):
      y_val = y[i]
      x_val = x[i]
      diff += x_val*(y_val - ((m * x_val) + b))
    m_gradient = -2/N * diff
    return m_gradient
```