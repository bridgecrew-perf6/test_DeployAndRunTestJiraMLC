# test_DeployAndRunTestJiraMLC

## Metrics Jobs

Model code includes a metrics function used to compute Group and Bias metrics.
The metrics function expects a DataFrame with at lease the following three columns three columns: `score` (predicted), `label_value` (actual), and `gender` (protected attribute).

### Sample Inputs

Choose **one** of
 - `df_sample_scored.json`


### Expected Output

The expected output of the metrics job when the input data is `df_sample_scored.json` should be 
```json
{
    "attribute_name": "gender",
    "attribute_value": "female",
    "ppr_disparity": 0.5,
    "pprev_disparity": 0.888888888888889,
    "precision_disparity": 1.3599999999999999,
    "fdr_disparity": 0.7567567567567567,
    "for_disparity": 1.6097560975609757,
    "fpr_disparity": 0.7648073605520413,
    "fnr_disparity": 1.32,
    "tpr_disparity": 0.8976000000000001,
    "tnr_disparity": 1.1500366837857667,
    "npv_disparity": 0.9158957106812448
}
```

The included dmn file `bias_disparity_DMN.dmn` checks the returned `precision_disparity` value. The test will fail if this value is outside `[0.8, 1.25]`.