Numerical Pattern Analysis

A self-contained Python program for a blinded Monte Carlo analysis of a fixed 4 x 3 numerical configuration.

The program asks whether a specified set of numerical relationships occurs more often than expected under a defined randomization model. It estimates:

•	individual pass rates for each property;

•	pairwise co-occurrence rates;

•	the probability that all properties hold simultaneously;

•	a Wilson score 95% confidence interval for the simultaneous result.

Model

The configuration contains:

•	Column A: four fixed values;

•	Column B: a uniformly random permutation of four fixed values;

•	Column C: eight independent uniform draws from {3, 4, 5, 6, 7, 8, 9, 10}.

Rows are formed from corresponding positions in Columns A, B, and C.
By default, Column A remains in its original order. Set PERMUTE_COLUMN_A = True in the source file to permute its four values among the four Column A positions instead.

Properties tested

•	P01: All values in Columns A and B are odd.

•	P02: In each of Columns A and B, the sum of the first and last values equals the sum of the two middle values, and all four sums are equal.

•	P03: The four Column A + Column B row sums can be reordered into an arithmetic progression. The four values formed by adding each row sum to its matched Column C unique value can also be reordered into an arithmetic progression. The two progressions do not need the same common difference.

•	P05: Among the eight values in Columns A and B, exactly two distinct values occur twice. Each duplicated value occurs once in each column. One duplicated value appears in the upper half of both columns, and the other appears in the lower half of both columns. All other values occur once.

•	P06: The upper and lower quadrants each contain one duplicated value. After subtracting one occurrence of that value from the quadrant total, the adjusted upper and lower totals are equal.

•	P07: Column C consists of four consecutive pairs. One value occurs once in every pair, and the other value in each pair is unique within Column C.

•	P08: For each row, the product of the two values in the corresponding Column C pair equals the sum of the Column A and Column B values in that row.

•	P11: The sum of the four unique Column C values equals half of the Column A total and half of the Column B total.

•	P12: The four differences and four sums formed from each unique Column C value and the common Column C value can each be reordered into arithmetic progressions.

•	P13: For Columns A, B, the row sums, the unique Column C values, the differences from P12, and the additions from P12, the first plus last value equals the sum of the two middle values. This must hold both in the original row order and in the row order 2, 4, 1, 3.

Installation

Python 3.9 or later is required. No third-party packages are needed.
git clone https://github.com/<your-username>/numerical-pattern-analysis.git
cd numerical-pattern-analysis
python --version

Usage
Run a 1,000,000-trial simulation:
python src/blinded_family_b_analysis.py --trials 1000000 --seed 20261027

Run a larger simulation:
python src/blinded_family_b_analysis.py --trials 10000000 --seed 20261027

Check that the reference configuration satisfies every property before
interpreting simulation output:
python src/blinded_family_b_analysis.py --trials 10000000 --seed 20261027 --check-reference

Example output
All-properties result
--------------------------------------------
Simultaneous passes: 0
Estimated probability: 0.00000000%
Wilson 95% CI: [0.00000000%, 0.00038414%]

This means that no generated configuration satisfied every property in
1,000,000 trials. The one-sided 95% upper bound is approximately
3.84 x 10^-6, or about 1 in 260,000.
Interpretation
A result of zero successes does not prove that the probability is exactly
zero. With N trials and zero successes, the Wilson score method gives an
upper confidence bound; increasing the number of trials tightens that bound.
Because the full conjunction of properties is highly restrictive, use a large
number of trials, for example 10 million or more, when reporting a final
estimate.
License
MIT License. See LICENSE.
