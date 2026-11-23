# econ5200-lab15-bias-variance
# Bias, Variance and an Unbiased Cross-Validation Score

## Objective

Use cross-validation to pick a polynomial degree on a small simulated sample, then check how close the cross-validated score comes to the model's actual error on new data from the same simulation.

## Methodology

- Generated 80 points from a known simulation and fit polynomial regressions of degree 1 through 12.
- Cross-validated each degree and selected degree 5, which had a CV error of 0.1853 (MSE).
- Drew 20,000 new points from the same simulation and scored the degree-5 fit on them, giving a true error of 0.2330 (MSE).
- Ran nested cross-validation so that the degree choice happened inside each outer fold rather than once on the whole sample; this produced an estimate of 0.1910 (MSE).
- Split the expected error into bias squared, variance and noise by simulating repeatedly from the known data-generating process. The noise term on its own was 0.2025 (MSE).
- Wrote my own k-fold cross-validation function for scikit-learn estimators and ran it against the lab's implementation. With 10 folds, degree 5 gave 0.1921 (MSE).

## Key Findings

- Cross-validation picked degree 5, and the degree-5 fit scored 0.2330 on 20,000 fresh points while its CV error was 0.1853. The CV score was the more optimistic of the two.
- Nested cross-validation gave 0.1910. Moving the degree selection inside the folds raised the estimate, but not to the level of the measured error on new data.
- My own k-fold function returned 0.1921 at 10 folds, close enough to the lab's result that I take the implementation as correct.
- The noise term alone was 0.2025, larger than any of the three cross-validated estimates (0.1853, 0.1910, 0.1921). Since noise is irreducible, none of those estimates accounted for the full error the model actually showed on new data.
- Of the 0.2330 true error, noise is the largest single component; bias squared and variance together make up the remainder.
