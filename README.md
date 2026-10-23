# Top Ratings and Airline Passenger Satisfaction: SHAP Attribution Patterns by Travel Purpose

Code and saved results for the paper of the same title by Sara Mohammed Meraj Zaki
(Department of Computer Science, Gulf University for Science and Technology, Kuwait).

The study compares logistic regression, random forest, XGBoost and LightGBM on the public Airline Passenger
Satisfaction survey (129,880 passengers) under leakage-controlled five-fold cross-validation, and uses
out-of-fold TreeSHAP values to describe how model attributions change across service-rating levels and between
business and personal travellers and returning and first-time customers. The results are predictive
associations within one public dataset, not causal effects of service improvements.

## Repository contents

| Path | Contents |
|---|---|
| `Airline_Satisfaction.ipynb` | The complete analysis, with the outputs of the run reported in the paper |
| `requirements.txt` | Package versions used for the reported results |
| `results_air/` | Every table and array the notebook saves (CSV and NumPy files) |
| `figures/` | Figs. 1–3 of the paper, as produced by Cell 35 |
| `LICENSE` | Licence for the code |

The dataset itself is not redistributed; see Data below.

## How to reproduce

1. Install Python 3.13 and the packages in `requirements.txt` (`pip install -r requirements.txt`).
2. Download `airline_passenger_satisfaction.csv` from Kaggle (see Data below) and place it next to the notebook.
3. Open `Airline_Satisfaction.ipynb` and run all cells in order. No GPU is needed. Random seeds are fixed (42);
   two runs in different environments gave identical results.

The last cell (Cell 34) only zips `results_air/` for download on Google Colab; skip it elsewhere.

## Data

The analysis uses the Airline Passenger Satisfaction dataset distributed on Kaggle:
https://www.kaggle.com/datasets/mysarahmadbhat/airline-passenger-satisfaction

Download `airline_passenger_satisfaction.csv` and place it in the repository's root folder, next to
`Airline_Satisfaction.ipynb`. Cell 2 checks that it has 129,880 rows and 24 columns, no duplicate records,
393 missing values in `Arrival Delay`, and 43.45% "Satisfied".

## Where each result comes from

| Paper item | Notebook cell | Saved file |
|---|---|---|
| Table I (segments) | Cell 4 | `table_segments.csv` |
| Zero-rating counts | Cell 3 | `table_zero_ratings.csv` |
| Table II (search spaces) and chosen configurations | Cells 5, 16, 24 | `search_space_*.csv`, `table_chosen_hyperparameters.csv` |
| Table III (model comparison), McNemar and Friedman tests | Cells 8–16 | `fold_results.csv`, `table_main_results.csv`, `table_statistical_tests.csv` |
| Corrected resampled t-test (LightGBM vs XGBoost) | Cell 31 | `table_corrected_ttest.csv` |
| Zero-as-score sensitivity check | Cell 17 | `table_zero_sensitivity.csv` |
| Out-of-fold SHAP values (15,000 passengers) | Cell 18 | `shap_values_oof.npy`, `shap_passenger_index.npy`, `shap_mean_abs.csv` |
| Grouped SHAP importance | Cell 26 | `shap_mean_abs_grouped.csv` |
| Fig. 2 and rating-level SHAP means | Cells 19, 26 | `table_shap_by_rating.csv` |
| Adjacent-rating contrasts | Cell 27 | `table_adjacent_contrasts.csv` |
| Table IV (satisfaction by rating) and Wi-Fi by travel purpose | Cell 25 | `table_satisfaction_by_rating.csv`, `table_wifi_by_travel.csv` |
| Spearman correlations among ratings | Cell 26 | `table_spearman_ratings.csv` |
| Table V, Fig. 3 and segment differences | Cell 22 | `table_top_rating_effects.csv`, `table_segment_differences.csv` |
| Table VI: class-stratified and class-standardised differences | Cell 29 | `table_class_stratified_contrasts.csv`, `table_class_standardised_differences.csv` |
| Table VI: refit without zero ratings | Cell 30 | `table_sensitivity_no_zero_ratings.csv` |
| Supplementary penalty-reward analysis | Cells 20, 21, 28 | `table_asymmetry.csv`, `table_asymmetry_corrected.csv`, `table_factor_types_by_segment.csv` |
| Figs. 1–3 | Cell 35 | `figures/*.png` |

## Main results

- LightGBM: mean accuracy 0.9659 and ROC-AUC 0.9957; XGBoost: 0.9651 and 0.9956. The corrected resampled
  t-test found no significant difference on any metric (p from 0.053 to 0.871).
- Mean SHAP attributions for in-flight Wi-Fi and online boarding change little across ratings 1–3 and rise over
  ratings 4 and 5; for Wi-Fi the step from 4 to 5 (4.66 log-odds) is larger than the step from 3 to 4 (2.51).
- The 4–5 versus 1–3 contrast for Wi-Fi is larger for personal than for business travellers (difference 1.95,
  95% bootstrap interval 1.76–2.16); the difference is 1.60 (1.32–1.91) after standardising for cabin class and
  1.98 (1.81–2.17) after refitting without passengers who gave any zero rating.

## Notes on the data

The outcome merges "neutral" and "dissatisfied" passengers. Ratings of 0 are undocumented and strongly associated
with the outcome (99.7% of passengers with a zero Wi-Fi rating are satisfied). Among personal travellers,
satisfaction is 0% at Wi-Fi ratings 1–3 and 100% at rating 5, which suggests that the file may have been
constructed or edited by its distributors. These properties are discussed in the paper and limit what the
results say about real passengers.

## Citation

If you use this code, please cite the paper (citation details will be added on publication):

> S. M. M. Zaki, "Top Ratings and Airline Passenger Satisfaction: SHAP Attribution Patterns by Travel Purpose," under review.

## Contact

Sara Mohammed Meraj Zaki, zaki.s@gust.edu.kw
