# econ3916-lab19-random-forests
# Tree-Based Models: Random Forests

## Objective
I compared a single decision tree, OLS, Ridge and a random forest on the California Housing data to see whether the forest's extra complexity gives better predictions than simpler models.

## Methodology
- Split the 20,640 block groups into training rows (80%) and test rows (20%), using the same split for every model.
- Fit four models on the training rows: a single decision tree with no depth limit, OLS, Ridge with scaled features, and a random forest of 100 trees, then scored each on the test rows.
- Read the forest's out-of-bag score, which scores each training row using only the trees that never saw it.
- Measured feature importance for the forest two ways: impurity (MDI), computed from the training rows, and permutation importance, computed by shuffling one feature at a time in the test rows.
- Tuned the forest's max_depth and max_features by 3-fold cross-validation.
- Wrote my own prompt asking an AI for a function that computes and charts permutation importance, then checked its output against my own numbers.

## Key Findings
- The single tree memorised its training rows and reached a test R² of only 0.6161. Ridge reached 0.5758, and the forest reached 0.8044 with the same eight features, so house values do not follow a straight-line relationship with these features.
- MDI and permutation importance ranked the features differently. Latitude scored 0.0889 by MDI but 0.4465 by permutation, because location splits happen deeper in the trees and reach fewer training rows, while the predictions still depend on them heavily.
- Tuning by cross-validation raised the forest's test R² to 0.8116. The gain came from letting each split choose from half the features instead of all of them.
- I went 2 rounds with the AI. Every line of the check matched in both rounds, and the function fitted no forests, but it relied on the notebook's RANDOM_STATE instead of setting the seed itself.
