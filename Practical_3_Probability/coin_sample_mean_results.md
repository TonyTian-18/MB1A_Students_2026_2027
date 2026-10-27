# Coin toss sample mean distribution

Assumption: 1,000 independent samples, each containing 10 fair coin tosses (10,000 tosses total). Heads = 1; tails = 0. This interprets 1,000 as the number of repeated samples, rather than a fixed pool of 1,000 tosses.

X is the number of heads in one sample: X ~ Binomial(10, 0.5).
The sample mean is X/10, taking values 0, 0.1, ..., 1.
P(sample mean = k/10) = choose(10, k) / 1024.

| Quantity | Simulation (seed 123) | Theory |
|---|---:|---:|
| Mean | 0.4975000 | 0.5000000 |
| Standard deviation of sample means | 0.1599041 | 0.1581139 |

The chart code below shows simulated relative frequencies as blue bars and exact binomial probabilities as red dots.

## Reproduce in R
No additional packages are required.

```r
set.seed(123)
heads <- rbinom(1000, size = 10, prob = 0.5)
sample_means <- heads / 10
frequencies <- tabulate(heads + 1, nbins = 11) / 1000
theory <- dbinom(0:10, size = 10, prob = 0.5)
bars <- barplot(frequencies, names.arg = (0:10)/10,
  col = "skyblue", ylim = c(0, 0.3),
  xlab = "Sample mean (proportion of heads in 10 tosses)",
  ylab = "Probability / relative frequency",
  main = "Sampling distribution: 1,000 samples of 10 tosses")
points(bars, theory, pch = 19, col = "red")
legend("topright", c("Simulation", "Binomial theory"),
  fill = c("skyblue", NA), pch = c(NA, 19),
  col = c("black", "red"), bty = "n", cex = 0.8)
c(mean = mean(sample_means), SD = sd(sample_means))
```
