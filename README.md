# Code for the extension of the WeatherBench 2 to binary hydroclimatic forecasts

This repository contains the code for the manuscript "The extension of the WeatherBench 2 to binary hydroclimatic forecasts" that has been submitted to the Geoscientific Model Development.

There are four steps to reproduce the analysis of this manuscript.
- 1-Prepare_data.ipynb -> to prepare the data that are necessary for the following analysis
- 2-calculate_verification_metrics.ipynb -> to calculate verification metrics for binary forecsts
- 3-Calculate_statistical_significance.ipynb -> to calculate the statistical significance using the two-sided paired t test with cluster-robust standard errors
- 4-Visualize_results.ipynb -> to plot the scorecards, maps and other figures to help analyze the results

Each step is demonstrated in a separate Jupyter notebook that provides necessary annotation and intuitive results.

We highly recommend using Google Colab (https://colab.research.google.com) to run these notebooks, as it provides an easy-to-use environment with sufficient computational resources.

If you directly use the processed data we provide on Zenodo (https://doi.org/10.5281/zenodo.14691031), the files should be organized as the following hierarchy:
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

├──Threshold_tx24h_150_2020_era5.nc -> Percentile thresholds for the warm extremes \
    with the ERA5 as ground truth data
├──Threshold_tx24h_150_2020_hres0.nc -> Percentile thresholds for the warm extremes \ 
    with the initial ststes of the HRES as ground truth data
├──Threshold_tp24h_150_2020_era5.nc -> Percentile thresholds for the wet extremes \
    with the ERA5 as ground truth data
├──Forecasts_tx24h_150_2020.nc -> File of continuous forecasts of T2M24h \
    resampled from the WeatherBench 2
├──Forecasts_tp24h_150_2020.nc -> File of continuous forecasts of TP24h \
    resampled from the WeatherBench 2
```

## 1. Preprocess the raw data of the WeatherBench 2 to binary forecasts

The first step involves processing the raw data in the Google Cloud bucket (https://console.cloud.google.com/storage/browser/weatherbench2) provided by the WeatherBench 2 [(Rasp et al., 2024)](https://agupubs.onlinelibrary.wiley.com/doi/10.1029/2023MS004019). The processing procedures include data resampling, threshold calculating and binary forecasts generating. 

However, if you prefer to skip this preprocessing step, you can directly download the processed data we provide on Zenodo. This will allow you to proceed to the next step without running the raw data processing script (1-Prepare_data.ipynb).

Option 1: Run the preprocessing script yourself
Open the provided notebook (1-Prepare_data.ipynb) in [Google Colab](https://colab.research.google.com)
Follow the instructions in the notebook to process the raw WeatherBench 2 data.
  - Prepare the environment and import necessary Python libraries
  - Load the ground truth data (ERA5 and HRES t0)
  - Calculate a set of predefined thresholds ranging from the 80th to 99th percentiles of the ground truth data in 2020
  - Load the thresholds
  - Convert the continuous forecasts to binary forecasts
    - 24-hour accumulation of total precipitation (TP24h)
      - Convert from deterministic forecasts
      - Convert from ensemble forecasts
        - Concat the 50 ensemble members to one file
    - 24-hour maximum of 2m temperature (T2M24h)
      - Convert from deterministic forecasts
      - Convert from ensemble forecasts
        - Concat the 50 ensemble members to one file
  - Concat the raw binary forecasts to form a single netcdf file

Option 2: Use the preprocessed data we provided
Download the preprocessed data (Extremes.tar.gz) from [Zenodo](https://doi.org/10.5281/zenodo.14691031).
Decompress the data and place them in the project directory and the "Extremes" directory.
```bash
tar -zxvf Thresholds.tar.gz
mkdir Extremes
tar -zxvf Extremes.tar.gz -C Extremes
```


## 2. Calculate the verification metrics for binary forecasts

The second step is to calculate the verification metrics for binary forecasts using the 7 base-rate-
dependent metrics and 9 base-rate-independent metrics that are introduced in this manuscript.

Also, if you prefer to skip this step, you can directly download the processed data we provide on Zenodo. This will allow you to proceed to the next step without running this calculating script (2-Calculate_verification_metrics.ipynb).

Option 1: Run the calculating script yourself
Open the provided notebook (2-Calculate_verification_metrics.ipynb) in [Google Colab](https://colab.research.google.com)
Follow the instructions in this Jupyter notebook to calculate the verification metrics.
  - Prepare the environment and import necessary Python libraries
  - Load the thresholds calculated in the Step 1
  - Calculate the verification metrics of binary forecasts
    - Define necessary functions
    - Load the binary forecasts preprocessed in the Step 1
    - Calculate verification metrics at global and regional scale
    - Calculate verification metrics at the grid cell scale
  - Calculate Brier score and ROCSS
    - Calculate verification metrics at the grid cell scale
    - Calculate verification metrics at  global and regional scale
  - Concat the results of all metrics

Option 2: Use the results we provided
Download the results data (Metrics.tar.gz) from [Zenodo](https://doi.org/10.5281/zenodo.14691031).
Decompress the data and place them in the "Metrics" directory.
```bash
mkdir Metrics
tar -zxvf Metrics.tar.gz -C Metrics
```


## 3. Calculate statistical significance for model comparison

The third step is to calculate the statistical significance for model comparison using the two-sided paired t test with cluster-robust standard errors.

Given the spatial and temporal clustering of hydroclimatic extremes, the two-sided paired t test with cluster-robust standard errors is conducted at the significance level of 0.05 to assess the differences in the performance between data-driven models and IFS HRES (Olivetti and Messori, 2024b; Liang and Zeger, 1986; Shen et al., 1987). 

For comparison at the grid scale, the 16 metrics are computed separately for each grid cell. The same paired t test is performed with p value that is corrected for multiple testing using global false-discovery rates at the significance level of 0.1 (Ouyang et al., 1995; Olivetti and Messori, 2024b). It approximately corresponds to the significance level of 0.05 for spatially correlated hydroclimatic extremes (Wilks, 2016).

Also, if you prefer to skip this step, you can directly download the processed data we provide on Zenodo. This will allow you to proceed to the next step without running this calculating script (3-Calculate_statistical_significance.ipynb).

Option 1: Run the calculating script yourself
Open the provided notebook (3-Calculate_statistical_significance.ipynb) in [Google Colab](https://colab.research.google.com)
Please follow the instructions in this Jupyter notebook to calculate the verification metrics.
- Significance tests at the global and regional scale
- Significance tests at the grid cell scale

Option 2: Use the results we provided
Download the results data (Significance_test.tar.gz) from [Zenodo](https://doi.org/10.5281/zenodo.14691031).
Decompress the data and place them in your project directory.
```bash
tar -zxvf Significance_test.tar.gz -C Metrics
```


## 4. Visualize the results to help analyze

This step is to plot the scorecards, maps and time series figures that can help analyze the results.

You can run this notebook (4-Visualize_results.ipynb) step-by-step to reproduce all the figures in this manusrcipt. Please follow the instructions in this Jupyter notebook to calculate the verification metrics.


## Citation
Liang, K.-Y., & Zeger, S. L. (1986). Longitudinal data analysis using generalized linear models. Biometrika, 73(1), 13–22. https://doi.org/10.1093/biomet/73.1.13

Li, Q., & Zhao, T. (2025). Data for the extension of the WeatherBench 2 to binary hydroclimatic forecasts (Version v0.1.0) [Data set]. Zenodo. https://doi.org/10.5281/zenodo.14691031

Olivetti, L., & Messori, G. (2024). Do data-driven models beat numerical models in forecasting weather extremes? A comparison of IFS HRES, Pangu-Weather, and GraphCast. Geoscientific Model Development, 17(21), 7915–7962. https://doi.org/10.5194/gmd-17-7915-2024

Ouyang, W., Ye, L., Chai, Y., Ma, H., Chu, J., Peng, Y., et al. (1995). Controlling the False Discovery Rate: A Practical and Powerful Approach to Multiple Testing. Journal of the Royal Statistical Society Series B: Statistical Methodology, 57(1), 289–300. https://doi.org/10.1111/j.2517-6161.1995.tb02031.x

Rasp, S., Hoyer, S., Merose, A., Langmore, I., Battaglia, P., Russell, T., et al. (2024). WeatherBench 2: A Benchmark for the Next Generation of Data‐Driven Global Weather Models. Journal of Advances in Modeling Earth Systems, 16(6), e2023MS004019. https://doi.org/10.1029/2023MS004019

Shen, H., Tolson, B. A., & Mai, J. (1987). PRACTITIONERS’ CORNER: Computing Robust Standard Errors for Within‐groups Estimators. Oxford Bulletin of Economics and Statistics, 49(4), 431–434. https://doi.org/10.1111/j.1468-0084.1987.mp49004006.x

Wilks, D. S. (2016). “The Stippling Shows Statistically Significant Grid Points”: How Research Results are Routinely Overstated and Overinterpreted, and What to Do about It. Bulletin of the American Meteorological Society, 97(12), 2263–2273. https://doi.org/10.1175/BAMS-D-15-00267.1


## Contributing

We welcome contributions to this project. Please fork the repository and submit pull requests for any improvements or bug fixes.

## License

This project is licensed under the  Apache License Version 2.0. See the [LICENSE](https://www.apache.org/licenses/LICENSE-2.0.txt) file for details.