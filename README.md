# Movie Revenue Prediction Project

## Albert School

**Team Members**: Ali CHERIFI ALAOUI, Fodié NIAKATE

### Table of Contents

- [Business Use Case](#business-use-case)
- [Dataset Description](#dataset-description)
- [Baseline Model](#baseline-model)
- [Iteration Process](#iteration-process)

## Business Use Case

This project aims to predict movie revenue using machine learning models to help production companies make better decisions. Ali and Fodié decided to take on this project because of the high-risk nature of the movie industry, where financial and reputational stakes are huge. The success of a movie can be very unpredictable, influenced by factors like buzz, controversies, or even just good timing. So, having a model that can help estimate the potential performance of a movie could be a real game-changer. The main goals here are to reduce financial risk, optimize marketing strategies, make smarter decisions, and ultimately, maximize profits.

The film industry is both highly rewarding and highly unpredictable. A movie can either soar like Christopher Nolan's blockbusters or face controversies that impact its box office, like some movies linked to the Weinstein brothers. Predicting movie success could help producers and studios make better choices and navigate through uncertainties.

We measure a movie's success from two perspectives:

1. **Financial Success**: This is the most important one for production companies. A movie is considered a success if it makes at least double its initial budget.
2. **Critical Success**: This is about whether the audience enjoyed it and recommended it.

Our project focuses mainly on **financial success** (profit and ROI). We define ROI like this:

\\[ ROI = (adjusted revenue - budget) / budget \\]

According to IMDb Pro, a movie has to make at least double its budget to be profitable. We use this rule to classify movies as successes or not.

## Dataset Description

As the dataset is quite huge, we have decided to export it on  Google Drive, you can have access to it throught this link: https://drive.google.com/drive/folders/1-Yf8ahtdtktCf1ecuUxkFBmofDylIzws
Note : Please download all the folder 'data', and not only the csv file, you'll need to follow this step to ensure that your code will work properly.

The dataset we used includes a lot of information about different movies, such as:

- **id**: Unique identifier for each movie in TMDB.
- **title**: The official title of the movie.
- **vote_average**: Average rating of the movie out of 10 on TMDB.
- **vote_count**: Number of votes contributing to the rating on TMDB.
- **status**: Current release status (e.g., Released, Post Production).
- **release_date**: Official release date of the movie.
- **revenue**: Box office earnings.
- **runtime**: Length of the movie in minutes.
- **budget**: The budget allocated for the movie.
- **imdb_id**: IMDb identifier.
- **original_language**: Original production language.
- **original_title**: The movie's original title.
- **overview**: A brief summary of the plot.
- **popularity**: Popularity score on TMDB.
- **tagline**: Official tagline of the movie.
- **genres**: The genres that the movie belongs to.
- **production_companies**: Companies involved in making the movie.
- **production_countries**: Countries where the movie was produced.
- **spoken_languages**: Languages spoken in the movie.
- **cast**: All cast members.
- **director**: All directors of the movie.
- **director_of_photography**: Cinematographers (Directors of Photography).
- **writers**: All writers involved.
- **producers**: Producers and executive producers.
- **music_composer**: Music composer(s).

## Baseline Model

### Features & Pre-processing

For our baseline model, we used features like **budget**, **release date**, **cast**, **director**, **genres**, **production companies**, **runtime**, **popularity**, and **IMDb ratings**. We also derived some features such as **title length**, **release season**, and **weekend release**.

In terms of pre-processing, we made sure to normalize financial features by using **CPI data** for inflation adjustments. We also extracted features like **release year**, **month**, and **day of the week** from release dates, and used custom encoders like **TopNEntitiesExtractor** for categorical data. We applied **OneHotEncoder** for certain features, while numerical ones were scaled using **MinMaxScaler**.

### Model Selection

We tested different models including:

- **RandomForest**
- **Gradient Boosting**
- **CatBoost**
- **LightGBM**
- **XGBoost**
- **Histogram-Based Gradient Boosting Regressors**

In the end, **RandomForest** worked best for our baseline, with an R² score of 0.45 and an RMSE of 3.2 million on the test set. It showed a good balance between cross-validation R² (0.701) and test R² (0.653), which means it generalized well compared to the other models.

| Model                | Mean CV R² | Test R² | Test MSE | Test RMSE |
| -------------------- | ---------- | ------- | -------- | --------- |
| RandomForest         | 0.699      | 0.650   | 1.62e+16 | 127.34 M  |
| GradientBoosting     | 0.699      | 0.656   | 1.58e+16 | 125.78 M  |
| HistGradientBoosting | 0.678      | 0.600   | 1.86e+16 | 136.50 M  |
| CatBoost             | 0.717      | 0.622   | 1.76e+16 | 132.69 M  |
| LightGBM             | 0.682      | 0.609   | 1.82e+16 | 134.92 M  |
| XGBoost              | 0.675      | 0.603   | 1.83e+16 | 135.47 M  |

## Feature Selection and Scenario Testing for Revenue Impact

After model selection, we conducted an additional step to enhance interpretability and explore the potential impact of feature adjustments on revenue:

1. **Select Top Features**: Using `SelectKBest`, we identified features most strongly correlated with revenue. This selection helped reduce the dimensionality and improved focus on critical variables.

2. **Modify Key Features for Scenario Analysis**: We allowed controlled modifications to top features (e.g., cast, genre) in a selected movie’s profile to simulate and predict the revenue impact. This "what-if" analysis tested if altering influential factors could change a movie’s success probability.

3. **Comparison and Impact Analysis**: By comparing the model’s predictions before and after modifications, we could gauge how changes in specific influential features impact revenue and success classification. This provided insights into practical levers (e.g., budget, casting decisions) for improving a movie’s financial performance.

##

This approach clarified which features most directly influence revenue, informing actionable insights for stakeholders aiming to maximize their movie's financial success. By understanding the impact of key variables, production companies can make informed decisions to optimize their movie's performance and profitability.
```
