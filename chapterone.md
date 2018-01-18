## Chapter One - Probability
#### Q1
If _μ_ is a probability measure then for any integer _n_ ≥ 2, and disjoint sets _A_<sub>1</sub>, ..., _A_<sub>n</sub>

<img src="https://latex.codecogs.com/gif.latex?\mu(\bigcup\limits_{i=1}^nA_i)&space;=&space;\sum\limits_{i=1}^n\mu(A_i)" title="\mu(\bigcup\limits_{i=1}^nA_i) = \sum\limits_{i=1}^n\mu(A_i)" />

---

<img src="https://latex.codecogs.com/gif.latex?\mu(\bigcup\limits_{i=1}^nA_i)&space;=&space;\mu(A_1&space;\cup&space;\bigcup\limit_{i=2}^n&space;A_i)&space;\\&space;=&space;\mu(A_i)&space;&plus;&space;\mu(\bigcup\limit_{i=2}^n&space;A_i)$,&space;as&space;$A_i,&space;...,&space;A_n&space;$are&space;disjoint$\\&space;\vdots&space;\\&space;=&space;\mu(A_i)&space;&plus;&space;\ldots&space;&plus;&space;\mu(A_n)&space;\\&space;=&space;\sum\limits_{i=1}^n(A_i)" title="\mu(\bigcup\limits_{i=1}^nA_i) = \mu(A_1 \cup \bigcup\limit_{i=2}^n A_i) \\ = \mu(A_i) + \mu(\bigcup\limit_{i=2}^n A_i)$, as $A_i, ..., A_n $are disjoint$ \\ \vdots \\ = \mu(A_i) + \ldots + \mu(A_n) \\ = \sum\limits_{i=1}^n(A_i)" />

#### Q2
Simulate 6000 dice rolls. Count the number of 1's, 2's, ..., 6's

```r
x <- sample(6, 6000, replace=T)
for (i in 1:6) {
  print(sum(x == i))
}

#[1] 1038
#[1] 1007
#[1] 963
#[1] 1021
#[1] 974
#[1] 997
```

About how often would you expect to get more than 1030 1's? Run an `R` simulation to estimate the answer.

```r
x <- rep(0, 1000)
for (i in 1:1000) {
  y <- sample(6, 6000, replace=T)
  x[i] <- sum(y == 1)
}

sum(x > 1030)
#[1] 153
```

#### Q3
In the board game _Risk_ players place their armies in different countries and try eventually to control the whole world by capturing countries one at a time from other players. To capture a country, a player must attack it from an adjacent country. If player A has _A_ ≥ 2 armies in country _A_, she may attack adjacent country _D_. Attacks are made with from 1 to 3 armies. Since at least 1 army must be left behind in the attacking country, A may choose to attack with a minimum of 1 and a maximum of min(3, _A_ − 1) armies. If player D has _D_ ≥ 1 armies in country _D_, he may defend himself against attack using a minimum of 1 and a maximum of min(2, _D_) armies. It is almost always best to attack and defend with the maximum permissible number of armies.
When player A attacks with _a_ armies she rolls _a_ dice. When player D defends with _d_ armies he rolls _d_ dice. A’s highest die is compared to D’s highest. If both players use at least two dice, then A’s second highest is also compared to D’s second highest. For each comparison, if A’s die is higher than D’s then A wins and D removes one army from the board; otherwise D wins and A removes one army from the board. When there are two comparisons, a total of two armies are removed from the board.

If A attacks with one army (she has two armies in country A, so may only attack
with one) and D defends with one army (he has only one army in country D)
what is the probability that A will win?

```r
x <- rep(0, 36)
for (i in 1:6) {
  for (j in 1:6) {
    if (i > j) {
      x[(i - 1) * 6 + j] <- 1
    } else {
      x[(i - 1) * 6 + j] <- 0
    }
  }
}

sum(x == 1) / length(x)

#[1] 0.4166667
```

Suppose that Player 1 has two armies each in countries C<sub>1</sub>, C<sub>2</sub>, C<sub>3</sub> and C<sub>4</sub>, that Player 2 has one army each in countries B<sub>1</sub>, B<sub>2</sub>, B<sub>3</sub> and B<sub>4</sub>, and that country C<sub>i</sub> attacks country B<sub>i</sub>. What is the chance that Player 1 will be successful in at least one of the four attacks?

<img src="https://latex.codecogs.com/gif.latex?P($at&space;least&space;one&space;win$)&space;=&space;1&space;-&space;P($no&space;wins$)&space;\\&space;P($at&space;least&space;one&space;win$)&space;=&space;1&space;-&space;(0.4166667)^4&space;=&space;0.884211" title="P($at least one win$) = 1 - P($no wins$) \\ P($at least one win$) = 1 - (0.4166667)^4 = 0.884211" />
