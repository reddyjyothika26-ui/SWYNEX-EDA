# EDA Findings — Iris Dataset

## Dataset quality and structure
- **Shape:** 150 rows × 5 columns.
- **Missing values:** 0 missing values across all columns.
- **Exact duplicate rows:** 1.
- **Species counts:**
  - Iris-setosa: 50 (33.3%)
  - Iris-versicolor: 50 (33.3%)
  - Iris-virginica: 50 (33.3%)

## Insights and implications

1. **The three classes are balanced.** Each species has 50 examples (one-third of the dataset). This is helpful for a first classification experiment; preserve the class proportions with a stratified train/test split.

2. **Petal measurements differ substantially by species.** The mean petal length and petal width are:

   - **Iris-setosa:** mean petal length 1.46 cm; mean petal width 0.27 cm.
   - **Iris-versicolor:** mean petal length 4.25 cm; mean petal width 1.32 cm.
   - **Iris-virginica:** mean petal length 5.52 cm; mean petal width 2.03 cm.

   These features are promising predictors for a species classifier, as also shown by the scatter plot.

3. **Petal length and petal width are strongly correlated.** Their Pearson correlation is 0.95. This means they carry overlapping information. Compare models with both features against a simpler feature set if interpretability or simplicity matters.

4. **Sepal length is strongly associated with petal measurements.** Correlation is 0.86 with petal length and 0.80 with petal width. This may help classification, but evaluate feature usefulness using validation rather than correlation alone.

5. **Sepal width has weaker linear relationships with several other features.** Its correlation with sepal length is -0.12 and with petal length is -0.42. It may provide complementary information; test its value empirically.

6. **There is a suspicious setosa measurement to review.** One row labelled `Iris-setosa` has petal width 1.3 cm, while the usual setosa values in this file are much smaller. Verify the row against the source dataset before changing it; do not silently overwrite a value.

7. **One exact duplicate exists.** Review the duplicate row and decide whether it represents a repeated observation or an accidental duplicate. If identical rows are split between training and testing, evaluation could be overly optimistic.

8. **Potential outliers should be reviewed, not automatically removed.** Box plots and an IQR rule can flag unusual values, but unusual does not necessarily mean incorrect. Review measurements in their species context and against the source.

## Recommended next steps
- Verify the suspicious measurement and duplicate against the original dataset.
- Document any cleaning decisions instead of making silent changes.
- For a model, use a stratified split or stratified cross-validation.
- Report a confusion matrix and per-class precision, recall, and F1-score alongside accuracy.
- Fit any scaling or other preprocessing on training data only to avoid data leakage.

## Conclusion
This is a balanced dataset with clear species-related patterns, especially in petal measurements. Before modelling, investigate the suspicious setosa measurement and the exact duplicate. The visualizations and statistics provide a useful baseline for a multi-class classification workflow.
