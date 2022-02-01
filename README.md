
<!-- README.md is generated from README.Rmd. Please edit that file -->

## Under Construction

This is a placeholder document for the work-in-progress 2022 residential
assessment model.

To see the 2021 residential assessment model, visit the
[2021-assessment-year](https://gitlab.com/ccao-data-science---modeling/models/ccao_res_avm/-/tree/2021-assessment-year)
git tag.

## Athena Guide

#### Table Universe

| Athena Table         | Observation Unit                   | Primary Key                                                                  | Notes                                                                                                                                                                     |
|:---------------------|:-----------------------------------|:-----------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| metadata             | model run                          | year, run_id                                                                 | Information about each run                                                                                                                                                |
| parameter_search     | model cv fold                      | year, run_id, configuration, fold_id                                         | Each row is the result from one fold assessment from one iteration                                                                                                        |
| parameter_final      | model run                          | year, run_id                                                                 | Best hyperparameters for each run, as chosen by tune::select_best()                                                                                                       |
| parameter_range      | parameter                          | year, run_id, parameter_name                                                 | CV search range per parameter per run                                                                                                                                     |
| assessment           | improvement                        | year, run_id, township_code, meta_pin, meta_card_num                         | Assessment results at the improvement level. Multi-card PINs will have more than one row. NOTE: Each run adds new partitions to S3 which must be added via a Glue crawler |
| performance          | geography \[by class\]             | year, run_id, stage, geography_type, geography_id, by_class, class           | Peformance metrics (optionally) broken out by class for different levels of geography                                                                                     |
| performance_quantile | geography \[by class\] by quantile | year, run_id, stage, geography_type, geography_id, by_class, class, quantile | Performance metrics by quantile within class and geography                                                                                                                |
| shap                 | improvement                        | year, run_id, township_code, meta_pin, meta_card_num                         | SHAP values for each feature of each improvement in the assessment data. NOTE: Each run adds new partitions to S3 which must be added via a Glue crawler                  |
| timing               | model run                          | year, run_id                                                                 | Timings for whole run. Each row represents one run, while columns represent the stages                                                                                    |

#### Run Outputs

| Athena Table         | Run On Type Automated | Run On Type Experiment | Run On Type Candidate | Run On Type Final |
|:---------------------|:----------------------|:-----------------------|:----------------------|:------------------|
| metadata             | TRUE                  | TRUE                   | TRUE                  | TRUE              |
| parameter_search     | FALSE                 | TRUE                   | TRUE                  | TRUE              |
| parameter_final      | TRUE                  | TRUE                   | TRUE                  | TRUE              |
| parameter_range      | FALSE                 | TRUE                   | TRUE                  | TRUE              |
| assessment           | FALSE                 | FALSE                  | TRUE                  | TRUE              |
| performance          | TRUE                  | TRUE                   | TRUE                  | TRUE              |
| performance_quantile | TRUE                  | TRUE                   | TRUE                  | TRUE              |
| shap                 | FALSE                 | FALSE                  | TRUE                  | TRUE              |
| timing               | TRUE                  | TRUE                   | TRUE                  | TRUE              |
