# Code for the extension of the WeatherBench 2 to binary hydroclimatic forecasts

This repository contains the code for the manuscript "The extension of the WeatherBench 2 to binary hydroclimatic forecasts" that has been submitted to the Geoscientific Model Development.

There are four steps to reproduce the analysis of this manuscript.
- 1-Prepare_data.ipynb -> to prepare the data that are necessary for the following analysis
- 2-calculate_verification_metrics.ipynb -> to calculate verification metrics for binary forecsts
- 3-Calculate_statistical_significance.ipynb -> to calculate the statistical significance using the two-sided paired t test with cluster-robust standard errors
- 4-Visualize_results.ipynb -> to plot the scorecards, maps and other figures to help analyze the results

Each step is demonstrated in a separate Jupyter notebook that provides necessary annotation and intuitive results.

We highly recommend using Google Colab (https://colab.research.google.com) to run these notebooks, as it provides an easy-to-use environment with sufficient computational resources.

If you directly use the processed data we provide on Zenodo (https://doi.org/10.5281/zenodo.14688448), the files should be organized as the following hierarchy:
```plain
├──Data --> Directory contains continuous forecasts resampled from the WeatherBench 2
│   ├──

├──Extremes --> Directory contains binary forecasts generated from \
    the previous resampled continuous forecasts
│   ├──

├──Metrics --> Directory contains results of verification metrics for model comparison
│   ├── 

├──Figures --> Directory contains figures used to help analyze the results
│   ├── 

Threshold_tx24h_150_2020_era5.nc -> Percentile thresholds for the warm extremes \
    with the ERA5 as ground truth data
Threshold_tx24h_150_2020_hres0.nc -> Percentile thresholds for the warm extremes \ 
    with the initial ststes of the HRES as ground truth data
Threshold_tp24h_150_2020_era5.nc -> Percentile thresholds for the wet extremes \
    with the ERA5 as ground truth data
```

## 1. Preprocess the raw data of the WeatherBench 2 to binary forecasts

The first step involves processing the raw data in the Google Cloud bucket (https://console.cloud.google.com/storage/browser/weatherbench2) provided by the WeatherBench 2 [(Rasp et al., 2024)](https://agupubs.onlinelibrary.wiley.com/doi/10.1029/2023MS004019). The processing procedures include data resampling, threshold calculating and binary forecasts generating. 

However, if you prefer to skip this preprocessing step, you can directly download the processed data we provide on Zenodo. This will allow you to proceed to the next step without running the raw data processing script (1-Prepare_data.ipynb).

Option 1: Run the preprocessing script yourself
Open the provided notebook (1-Prepare_data.ipynb) in [Google Colab](https://colab.research.google.com)
Follow the instructions in the notebook to process the raw WeatherBench 2 data.

Option 2: Use the preprocessed data we provided
Download the preprocessed data (Extremes.tar.gz) from [Zenodo](https://doi.org/10.5281/zenodo.14688448).
Decompress the data and place them in the "Extremes" directory.
```bash
mkdir Extremes
tar -zxvf Extremes.tar.gz -C Extremes
```


## 2. Calculate the verification metrics for binary forecasts

The second step is to calculate the verification metrics for binary forecasts using the 7 base-rate-
dependent metrics and 9 base-rate-independent metrics that are introduced in this manuscript.

Also, if you prefer to skip this step, you can directly download the processed data we provide on Zenodo. This will allow you to proceed to the next step without running this calculating script (2-Calculate_verification_metrics.ipynb).

Option 1: Run the calculating script yourself
Open the provided notebook (2-Calculate_verification_metrics.ipynb) in [Google Colab](https://colab.research.google.com)
Follow the instructions in the notebook to calculate the verification metrics.

Option 2: Use the results we provided
Download the results data (Metrics.tar.gz) from [Zenodo](https://doi.org/10.5281/zenodo.14688448).
Decompress the data and place them in the "Metrics" directory.
```bash
mkdir Metrics
tar -zxvf Metrics.tar.gz -C Metrics
```


## 3. Calculate statistical significance for model comparison

The third step is to calculate the statistical significance for model comparison using the two-sided paired t test with cluster-robust standard errors.

Also, if you prefer to skip this step, you can directly download the processed data we provide on Zenodo. This will allow you to proceed to the next step without running this calculating script (3-Calculate_statistical_significance.ipynb).

Option 1: Run the calculating script yourself
Open the provided notebook (3-Calculate_statistical_significance.ipynb) in [Google Colab](https://colab.research.google.com)
Follow the instructions in the notebook to calculate the verification metrics.

Option 2: Use the results we provided
Download the results data (Significance_test.tar.gz) from [Zenodo](https://doi.org/10.5281/zenodo.14688448).
Decompress the data and place them in your project directory.
```bash
tar -zxvf Significance_test.tar.gz -C Metrics
```


## 4. Visualize the results to help analyze

This step is to plot the scorecards, maps and time series figures to help analyze the results.

You can run this notebook (4-Visualize_results.ipynb) step-by-step to reproduce all the figures in this manusrcipt. In the meantime, we provide these figures on [Zenodo](https://doi.org/10.5281/zenodo.14688448).


## Contributing

We welcome contributions to this project. Please fork the repository and submit pull requests for any improvements or bug fixes.

## License

This project is licensed under the  Apache License Version 2.0. See the [LICENSE](https://www.apache.org/licenses/LICENSE-2.0.txt) file for details.