# FLAM-Assignment-for-Research-and-Development-AI

# Problem Statement:
Find the values of unknown variables in the given parametric equation of a curve :

$$x=\left(t*\cos(\theta)-e^{M\left|t\right|}\cdot\sin(0.3t)\sin(\theta)\ +X \right )$$
$$
y = \left (42 + t*\sin(\theta)+e^{M\left|t\right|}\cdot\sin(0.3t)\cos(\theta)\right)
$$
unknowns are : 
$$
\theta , M ,X
$$
Ranges :
$$
0 \deg<\theta<50 \deg \\
-0.05<M<0.05 \\
0<X<100\\
6<t<60
$$

# Approach:
The given equation is non-linear and so linear regression was not possible.
In the given x,y dataset t was not mentioned so I assumed t to be uniformly distributed.
## Plotting The graph:
plotted the raw x,y values and a scatterplot overlayed on it.
\
From the plot itself we can calculate a rough estimate of theta.

![alt text](image.png)

We can see that the plot is mostly dictated by 

$$ x \approx t \cdot \cos(\theta)+X $$
$$ y \approx t \cdot \sin(\theta) +42 $$
then the other terms would dictate the curves\
we can approximately find the slope
$$ start : (60,46)$$
$$end : (108,68)$$
$$ slope =  \frac{\Delta y}{\Delta x} = \frac{y_2 - y_1}{x_2 - x_1}$$
$$m \approx \frac{22}{48} \approx 0.458 $$ 
$$m=tan(\theta)$$
$$\theta = 24.6 approx$$

## Gridsearch:
My first bruteforce/Naive approach was to gridsearch.
Its given that the L1 distance has to be minimum. Using this the initial gridsearch gave me(4.2 sec) :

$$θ = 28.0$$
$$M = 0.020000000000000004$$
$$X = 55.0$$
$$L1 =  25.244341261851268$$

Now using this result i searched nearby using a finer grid search. (2 min)

$$θ = 28.125$$
$$M = 0.021400000000000006$$
$$X = 54.9$$
$$L1 =  25.24340278201307$$

## Minimization using grid search output:

Now that I did both grid search and a finer gridsearch I have arrived at an output.Now this output can still be minimized because maybe our values in gridsearch were too far apart. So here I use 2 minimization functions : powell and Nelder-Mead. I chose them because there are derivative free.

After running them and looking at the results these are my conclusion:
- Assuming this is the global minima this is the best answer you can get as both powell and Nelder-Mead converge to same value.

```
POWELL:
Optimization terminated successfully.
         Current function value: 25.243398
         Iterations: 1
         Function evaluations: 85
θ  :  28.120418061041402
M  :  0.021399674857236456
X  :  54.900061696638645
Min L1 :  25.24339796943881

NELDER-MEAD:
Optimization terminated successfully.
         Current function value: 25.243396
         Iterations: 93
         Function evaluations: 172
        θ  :  28.11842300222184
M  :  0.021388957351028685
X  :  54.9003484203334
Min L1 :  25.243395891701628
```
- Now the next step would be to find the best global minima and repeat above process of finding local minima.
# Citation
https://www.youtube.com/watch?v=N_8MyFjGc4A -> simplex method