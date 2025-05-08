# Birthday-Paradox

The birthday paradox states that in a group of just 23 people, there's about a 50% chance that at least two people share the same birthday. This seems counterintuitive to many people, who might expect you'd need many more people to reach such a high probability.
The mathematics behind it work like this:

Instead of calculating the probability of a match directly, we calculate the probability of no matches and subtract from 1
With 23 people, we have 253 pairs of people (23 × 22 ÷ 2)
For each pair, the probability they don't share a birthday is 364/365 (assuming 365 days in a year)
When we calculate the probability that none of these pairs share a birthday and subtract from 1, we get approximately 0.507

The probability grows surprisingly quickly:

With 23 people: ~50% chance of a shared birthday
With 50 people: ~97% chance
With 70 people: ~99.9% chance

###  Probability of No Shared Birthday*
- The first person can have any birthday:  
  \[
  P_1 = \frac{365}{365} = 1
  \]
- The second person must have a different birthday:  
  \[
  P_2 = \frac{364}{365}
  \]
- The third person must differ from the first two:  
  \[
  P_3 = \frac{363}{365}
  \]
- ...
- The \( n \)-th person must differ from all previous \( n-1 \) people:  
  \[
  P_n = \frac{365 - (n - 1)}{365}
  \]

The probability that **no two people share a birthday** is the product of these probabilities:
\[
P(\text{no match}) = \frac{365}{365} \times \frac{364}{365} \times \frac{363}{365} \times \dots \times \frac{365 - n + 1}{365}
\]

This can be written compactly using **factorials**:
\[
P(\text{no match}) = \frac{365!}{(365 - n)! \times 365^n}
\]

---

### Probability of At Least One Shared Birthday
The probability that **at least two people share a birthday** is the complement of the above:
\[
P(\text{match}) = 1 - P(\text{no match}) = 1 - \frac{365!}{(365 - n)! \times 365^n}
\]

---

### Approximation (for Large \( n \))
For large \( n \), computing factorials directly is impractical. Instead, we use the **Poisson approximation** or the **Taylor series expansion** of logarithms.

#### Approximation Using Exponentials
We know that:
\[
\ln(1 - x) \approx -x \quad \text{(for small \( x \))}
\]

Taking the natural log of \( P(\text{no match}) \):
\[
\ln P(\text{no match}) = \sum_{k=1}^{n-1} \ln \left( 1 - \frac{k}{365} \right) \approx -\sum_{k=1}^{n-1} \frac{k}{365} = -\frac{n(n-1)}{2 \times 365}
\]

Exponentiating both sides:
\[
P(\text{no match}) \approx e^{-\frac{n(n-1)}{730}}
\]

Thus:
\[
P(\text{match}) \approx 1 - e^{-\frac{n(n-1)}{730}}
\]

#### **Solving for \( P(\text{match}) = 0.5 \)**
Set \( P(\text{match}) = 0.5 \):
\[
0.5 = 1 - e^{-\frac{n(n-1)}{730}}
\]
\[
e^{-\frac{n(n-1)}{730}} = 0.5
\]
Take the natural log:
\[
-\frac{n(n-1)}{730} = \ln(0.5) \approx -0.6931
\]
\[
n(n-1) \approx 730 \times 0.6931 \approx 506
\]

Solving the quadratic equation \( n^2 - n - 506 = 0 \):
\[
n = \frac{1 \pm \sqrt{1 + 2024}}{2} = \frac{1 \pm 45}{2}
\]
\[
n \approx 23
\]

This confirms the famous result that **23 people** are needed for a >50% chance.


For \( d \) possible birthdays (e.g., \( d = 365 \)), the probability of at least one collision is:
\[
P(n, d) \approx 1 - e^{-\frac{n(n-1)}{2d}}
\]

