
=======
Version Information
=======

Application: DengX
Version: v1.0.0
Release type: First public Windows release
Developer: Dr. David Knut Bengtsson-Asgarali
Contact: bengtsson.asgarali@gmail.com

=======
Intro
=======

Thank you for downloading the DengX application!

This text file provides a step-by-step guide on how to install and use the application.

First, as this is the first publicly available version, there may be bugs and updates that we are currently working on. These include UI scale issues, figure title editing, altering the training and testing period, and other usability improvements. We welcome and encourage all feedback.

You can contact me at: bengtsson.asgarali@gmail.com

=======
DengX Application Overview
=======

The DengX application is a dengue-climate forecasting and analysis tool. It allows disease datasets and climate datasets to be loaded, analyzed, and used for training XGBoost models. The application supports exploratory statistical analysis, model performance evaluation (Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), coefficient of determination (R^2)), SHAP-based model interpretation (beeswarm plot, 2D dependency plots, and detecting discrete climatic thresholds associated with increased dengue transmission). The app supports figure and table exports, to help streamline research workflows.

DengX was designed for researchers, public health professionals, epidemiologists, students, and analysts interested in understanding the relationship between dengue trends and environmental or climate variables.

For a more detailed overview of the application please refer to the following youtube video: https://youtu.be/_JNGc-75DE8?si=ZW0di6LkimZ0spuA


For use case reference for DengX refer to my current research on the topic, all data analysis is made by DengX is paper 2, while paper 1 served as a preliminary research: 

1. Bengtsson-Asgarali DK. Modeling the Climate–Dengue Nexus with XGBoost: A Retrospective Time Series Analysis Using Syndromic and Environmental Data. Zenodo; 2026. doi:10.5281/zenodo.18687341.

2. Bengtsson-Asgarali DK. Modeling the Climate-Dengue Nexus with XGBoost in Central and South American Nations: Costa Rica. Zenodo; 2026. doi:10.5281/zenodo.19225433.

3. Bengtsson-Asgarali D. Designing Dengue-Climate Nexus Research for Machine Learning Modeling. Zenodo; 2026. doi:10.5281/zenodo.18167625.


=======
Important Notice
=======

In the article "An Introduction to Building the DengX Framework for Dengue Forecasting" I discuss data and system property conditions for using Predictive Artificial Intelligence: "...the conditions
necessary for predictive AI to be effective in public health...1) To use Predictive AI, the phenomenon of study should be well understood, as should the forces that drive it...2) Predictive AI requires access to data sufficient in temporal resolution, accuracy, and non-zero dominance (that optimally supports geospatial analysis). 3) Data selection and research design should be informed by a well conducted literature review on the phenomenon in question..." 

The output of any model depends on the system under study, our understanding of the system and its variables, the quality of data, and research design.

Please refer to the original article for full context: Bengtsson-Asgarali D. An Introduction to Building the DengX Framework for Dengue Forecasting. Zenodo; 2026. https://doi.org/10.5281/zenodo.18319078

=======
Installation Instructions
=======

1. Extract the ZIP file you downloaded.

2. Open the extracted folder.

3. Double-click:

   DengX_Setup.exe

4. Follow the installer prompts.

5. Once installation is complete, open DengX from either:

   - The Start Menu
   - The desktop shortcut, if you selected that option during installation

6. If Windows SmartScreen appears, click:

   More info → Run anyway

   This may appear because this is an early Windows release and the application may not yet be code-signed by a recognized publisher.


=======
Input File Requirements
=======

DengX requires two main files for the primary analysis workflow:

1. Disease cases, or Y variable, file
2. Climate or environmental X-feature file

Both files should contain a date column that allows the records to be aligned over time.

Recommended file structure:

Dengue outcome file:
- A date column
- A dengue outcome column, such as suspected dengue cases, confirmed dengue cases, or another numeric dengue indicator. Note, Y variable file must contain only one disease value column.

Climate/X-feature file:
- A date column
- One or more numeric climate or environmental feature columns.

Examples of possible climate variables include:

- Mean temperature
- Maximum temperature
- Minimum temperature
- Relative humidity
- Precipitation
- Dew point
- Wind speed
- NDVI or other environmental indicators

Other x feature variables  include:
- Land use
- Urbanization
- Heat islands

Before loading files, check that:


=======
Basic Workflow
=======

1. Open DengX.

2. Press "Select Y File" and load dengue outcome "Y" file.

3. Press "Select X File" and load the X-feature "X" file.

4. Press "Advanced File Calibration (Manual Only)". In the opened dialog window, in the "Manual Mapping" section, press the drop down to the right of "Y variable column:" and select the name of disease data column. The column name is "dengue_y" if "PAHO_Weekly_Dengue_Converter" was used to collect dengue data.

5. In the same dialog window, in the "X Feature Selection" section, select non-datetime variables as independent variables for analysis.  Select the climate or environmental feature columns to include in the analysis.

6. In the same dialog window, press "Apply" After completing steps 4 and 5.

7. Press "Cross-correlation Lag Configuration". In the opened dialog window, press "Detect Lags". In the generated table, ensure that negative values (e.g., -8, -2) in the "Lag (editable)" column are manually made positive (e.g., 8, 2). Lags can be modified beyond detected cross-correlation.

8. "Advanced Model Configuration" allows hyperparameter optimization, I recommend leaving this untouched unless making evidence-based changes.

9. Press "Run Analysis". Program might print "Not Responding" momentarily, just wait.

10. Analyzed data can be viewed across the four tabs and exported by pressing "Export Images" button in the top right.


=======
Piecewise function forecasting Workflow
=======

DengX supports out-of-sample forecasting. Conceptually, this applies the concept of ambient space and ambient input space to use decision trees of an "old" model on the X feature data of a "new" or "future" time period. For long-term forecasting, this assumes a certain degree of boundedness and ergodicity of the domain and codomain of the system in question. These assumptions are accepted for this research for dengue in particular, due to the non-linear, threshold dependent, climate sensitivity of the dengue transmission system. 
 
For given Y and X datasets encompassing the temporal period t to t^n, the Piecewise function forecasting Workflow requires t^n + 1 of Y and X datasets. The X dataset is applied to the decision trees of the "old" model, generating a y hat prediction for the new time period, allowing climate-based disease prediction years away.

The practical workflow is as follows:

1. Collect future Y and X datasets
2. In the "4. Piecewise function" tab, inside the "MA1" subtab, inside the "MA1 New X File" section, press "Add future Y file" and load future Y file
3. In the same section, press "Add future X file" and load future X file
4. Press "Apply"

=======
Main Analysis Outputs
=======

After running the main analysis, DengX may generate several types of outputs depending on the selected workflow and available data.

These may include:

- Time-series plots of observed dengue values.
- XGBoost model predictions.
- Actual versus predicted dengue plots.
- Train/test split visualization.
- MAE and RMSE model performance values.
- SHAP beeswarm plots.
- SHAP dependency plots.
- LOWESS-smoothed SHAP response curves.
- Positive-risk ranges for selected climate variables.
- Baseline and aberration threshold overlays.
- Excel exports containing statistical summaries and analysis tables.


=======
Understanding the XGBoost Model Approaches

DengX uses XGBoost regression models to estimate relationships between dengue outcomes and selected X features. Four different Model Approaches (MA) are used for training and testing. Constant across all were dengue data as the dependent variable. MA1 included only climate variables as X features. MA2 included Dengue_y_lag_1 and climate variables as X features. MA3 replaced X features with a column, in which each cell was a constant value of 1, producing the baseline value. MA4 included only Dengue_y_lag_1 as X features.

=======
Understanding SHAP Outputs
=======

SHAP outputs are used to interpret how model features contribute to predicted dengue values.

In general:

- Positive SHAP values indicate that a feature value is increasing the model prediction.
- Negative SHAP values indicate that a feature value is decreasing the model prediction.
- SHAP dependency plots show how the contribution of a climate variable changes across its observed range.
- LOWESS smoothing is used to help visualize general response patterns.
- Positive-risk ranges indicate ranges where the smoothed SHAP effect is positive or strongly positive.

These outputs are useful for identifying possible climate conditions associated with increased dengue risk in the trained model.

=======
Reset Buttons
=======

DengX includes reset functions to help users run new analyses without restarting the application.

The main reset button clears loaded files, mappings, analysis outputs, tabs, and export state.

The MA1 reset button clears only the MA1 future workflow, including future Y files, future X files, Apply outputs, advanced reports, and MA1 future export state.

Use reset before loading a completely new dataset.

