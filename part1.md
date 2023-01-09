# Math 113B - Math Biology, W23
## Part 1

### Logistics

- Not everyone took MATH113A, but logistics are similar.
- Homework uploaded to Gradescope, due on Fridays.
- Quizzes on Thursdays during discussion.
- One midterm. Final project.
- No participation points.
- Many complained about the book. It's still the best book available. 
- In syllabus, I add references to other books for every topic if you want to consult. I'll also draw homework problems from other books. 
- Feedback last quarter also was that students want more biology. This is tricky. We need to study both model construction (need to learn biology) and model analysis (need to learn math). I'll try to strike a balance. 

## Intro to Continuous Models (Chapter 4 in Edelstein-Keshet) 

### Warmup: growth of bacteria

- Suppose we are growing bacteria in a flask.
- We can count how many there are at given times.
- We want to understand (via modeling) how many there are after a certain amount of time. 
- Call $N(t)$ the number of bacteria after time $t=0$. 
- One big caveat of most of the modeling we will do in this class is that  $N(t)$ will take on continuous values. That is, $N(t)$ could be $10.1$. What does this mean if we are counting something?
- Ignoring this for now, how do we model this? 
- In 113A, we used **difference equations**. The idea there was that we think about $N(t)$ at regular time intervals $t_0, t_1, t_2$, where $t_1 = t_0 + \Delta t$ and $t_2 = t_1 + \Delta t$, and relate $N(t_n)$ to $N(t_{n-1})$.  
- The simplest model we might think of is that a single bacterial cell divides, its daughters divide, some die, so on average, each bacteria gives rise to $K$ new ones per time. In this class, we will emphasize the **units** of parameters.
- When we say $K$ has units of rate, that means it is something *per time*. Specifically, it the number of new offspring *per bacteria, per time*. 
-  We would say that - $N(t_{n+1}) = N(t_n) + K N(t)\Delta t$. That is, the new amount of bacteria is the old amount, plus the new amount changed in the time window. 
-  Are the units right? On the left hand side we have number of bacteria. On the right hand side we have  bacteria/(bacteria x time)(bacteria)(time) = bacteria. That looks good.
-  These types of models were fine in ecology when we observe stuff rarely. In cell and molecular biology, technology has facilitated the ability to make observations, in this case, making $\Delta t$ small. 
-  If we rearrange a little, we get
$$
\frac{N(t+\Delta t) - N(t)}{\Delta t} = KN(t).
$$
- We wrote this in a suggestive way. What happens when we take $\lim_{t\to\Delta t}$? The left hand side is exactly the derivative, $\mathrm{d}N/\mathrm{d}t=N'(t)$.
- As the time between observations becomes small, we are left with
  $$ N'(t) = KN(t).$$
- This will be our simplest model of population growth, but it is a nice starting point.
- Despite its simplicity, it is very important! 
- The model is attributed to Robert Malthus in 1798, in one of the first attempts to quantify populations. 
- Quoting Wikipedia: "By now, it is a widely accepted view to analogize Malthusian growth in Ecology to Newton's First Law of uniform motion in physics.
- That is, it is a simple starting point but a nice thing to compare more complex models to.
- What type of equation is this? It is no longer a difference equation, it is a **differential equation**. 
- We can solve differential equations *sometimes* but not usually. In this case, we can solve it. 
- What does it mean to *solve* a differential equation?  
- The equation we have implicitly describes $N(t)$ but it does not explicitly tell you what the population is after 10 days, e.g. $N(10)$. To figure this out, we must solve.
- This differential equation is *separable*. You might remember this trick from Calc 2. We can (not correctly, but it works) think of $\mathrm{d}N/\mathrm{d}t$ as a fraction and rearrange, and integrate:
  $$
  \frac{\mathrm{d}N}{N} = k \mathrm{d} t\\
    \int \frac{\mathrm{d}N}{N} =\int  k \mathrm{d} t\\
    \log N(t) - \log N(0) = kt \\
    N(t) = N(0)e^{kt}.
  $$
  - Equipped with this solution, so long as we know the initial condition $N(0)$, we can predict the population at any future time. That is one advantage of a model. 

- If our prediction is "right" we can feel assured that our model is plausible (but it may not be the only model!)

- If our prediction is "wrong" (compared with say, experimental data), we can conclude that our model is not capturing the right behavior and we might want to rethink it.

- There are lots of variations we could consider here. 

- Should the production rate $K$ stay constant the whole time? 

- What determines $K$? Presumably the bacterial cells need food, and might run out of it?

- Therefore, we could consider $K(t)$ instead. But what do we specify as $K(t)$? 

- Now we need a model for $K(t)$ as well! 

- One simple explanation is that $K$ depends on the *concentration* of the food, so let's say $K = \kappa C$.  

- Our updated population equation would then be 
  $N'(t) = \kappa C N$. But what is $C$? 
  
- We can write down another differential equation for how we think $C$ changes. Suppose we think $\alpha$ units of nutrient are consumed per each unit of bacterial cell change. This translates into $C' = -\alpha   N' = -\alpha \kappa C N$. 

- Now we have a **system** of (coupled) differential equations. The differential equations for $N, C$ both depend on each other. 

- Through a trick that works on no other problem (so don't feel bad if you don't see it), we can integrate
$$
  \int C' = \int -\alpha   N'\\
  C(t) = -\alpha N(t) + C_0,
$$
where  $C(0) = -\alpha N(0) + C_0$.
-  We can substitute this into the equation for $N'$  and we're left with
  $$N' = \kappa (C_0-\alpha N)N.$$
- This is separable! Sparing you the details of integrating it, our solution is
$$
N(t) = \frac{N_0 (C_0/\alpha)}{N_0 + (B-N_0)e^{-\kappa C_0 t}}.
$$
- How does this model behave? As $t$ gets large, We see this population approaches $N(t) \to C_0/\alpha$. This is called the "carrying capacity". 
- Another observation is that if $N_0$ is small, then this approximately grows approximately exponentially, like Malthus predicted.
- It turns out this model works pretty well! See the data and the fit below.

<img src="fig41.png" alt="fig41" style="zoom:75%;" />

- While I understand it's a bit challenging to discern general lessons from this first warmup, I want to recap what I think some of the lessons are:
    - This class will be about modeling using differential equations.
    - Differential equations are (in my opinion), easier to use, and more mathematically interesting than difference equations. Therefore, these are much more popular in mathematical biology. 
    - They typically take the form of $\text{rate of change in stuff}=\cdots$. 
    - We can construct models based on *hypotheses* about how we think biology works. We then study the model behavior to validate or reject our model. 
    - Most models will not be this simple, so we will need new mathematical tools to study their behavior. This is what our class is about!  