# test_DeployAndRunTestJiraMLC

## Metrics Jobs

Model code includes a metrics function used to compute Group and Bias metrics.
The metrics function expects a DataFrame with at lease the following three columns three columns: `score` (predicted), `label_value` (actual), and `gender` (protected attribute).

### Sample Inputs

Choose **one** of
 - `df_baseline_scored.json`


### Expected Output

The expected output of the metrics job when the input data is `df_sample_scored.json` should be 
```json
{
    "attribute_name": "gender", 
    "attribute_value": "female", 
    "ppr_disparity": 0.5042735042735043, 
    "pprev_disparity": 1.190763484881132, 
    "precision_disparity": 1.1072033898305087, 
    "fdr_disparity": 0.8871543264942017, 
    "for_disparity": 1.2228070175438595, 
    "fpr_disparity": 1.1736158578263842, 
    "fnr_disparity": 0.8414786967418546, 
    "tpr_disparity": 1.0501984126984127, 
    "tnr_disparity": 0.9317510076130765, 
    "npv_disparity": 0.9708045977011494
}
```

The included dmn file `bias_disparity_DMN.dmn` checks the returned `precision_disparity` value. The test will fail if this value is outside `[0.8, 1.25]`.
