# Team Error 404 (UM Hackathon 2025)
Hi, everyone! Welcome to our group's `GitHub` repo. All our ideas, documents and code will be recorded here.

**Note: The presentation slides (in both PPTX and PDF format) are located in the `Preliminary Round PPT Slides` folder.**<br>
You may also access the presentation slides [here](Preliminary%20Round%20PPT%20Slides/Prelim_Slides.pptx).

---

## Preliminary Round - Domain 2
For the preliminary round, our group has prepared a conceptual diagram to demonstrate our approach to the problem in Domain 2.

---

## Problem and Objective Statement
Attached is the problem and objective statement for Domain 2 for reference if needed (UMHackathon, 2025).

>### Problem Statement
>Alpha Strategies Using HMM or ML
>
>### Objective
>Develop a Machine Learning (ML) model that analyzes on-chain data from various sources (e.g. CryptoQuant, Glassnode, Coinglass) to generate an alpha trading strategy that maximizes profit.
>The model should effectively extract implicit indicators from noisy data to generate profitable trading signals.

---

## Assumptions
For this project, our team has outlined a few assumptions to offer clarify on minor details:

- It is assumed that the datasets obtained do not contain any entry errors (e.g. incorrect values or outliers). All data accurately reflects the actual market movement at their respective timestamps.

- It is assumed that the risk-free rate used in the calculation of the Sharpe ratio is 0% (with reference to `InvestmentAsleep8365` from [Reddit](https://www.reddit.com/r/quant/comments/1fvbhle/what_risk_free_rate_should_i_use_to_calculate/)).

---

## Conceptual Diagram
Our conceptual diagram is as shown:

![Architectural Diagram](https://github.com/user-attachments/assets/4e333784-7722-447e-b7af-b770664ea48a)

The PDF Version of the diagram can be retrieved here: [Conceptual Diagram.pdf](https://github.com/user-attachments/files/19682125/Arc.Diagram.pdf)

The diagram can be divided into three parts:
- Input
- Backtest Library
- Output

The explanation for each part is detailed in the following section.

Also, throughout our implementation, our team will be using various external libraries. The potential libraries to be used include:
- `pandas` (for data preprocessing)
- `backtrader` (for backtest trading simulation)
- `sklearn` (for machine learning)

---

## Input
To use the backtest library, we will need to provide a few inputs, including:

- **Trading Data**<br>
  *Dataset that will be used for backtesting. This dataset can be retrieved from various sources (e.g. CryptoQuant, Glassnode, Coinglass) via API calls.*

  
- **Timeframe**<br>
  *Act as a filter to include only the records within the specific timeframe for backtesting (e.g. given a dataset from year 2000 to 2024, we can set the timeframe as 2020 to 2024 to only include data within the year range).*

  
- **Requirements**<br>
  *Additional requirements that should be taken into consideration while performing backtesting (e.g. trading fees of 0.06%).*

  
- **Strategies**<br>
  *The strategy that will be used to perform backtesting. An example would be:*
  >*BUY when flow_total > 0.01*<br>
  >*SELL when flow_total < 8*<br>
  >*HOLD for other conditions*
  

- **Trained Model**<br>
  *The various machine learning (ML) models that was trained beforehand before applied to the backtesting library.<br>*
  *For more details on how the ML models are built, please click [here](#Pre-trained-Model).*
  

---

## Backtest Library
The backtest library consists of four components, as detailed:

- **Data Import and Preprocessing**<br>
  *Dataset (with trading data) will first be loaded into the library, and the necessary data preprocessing actions will be taken. These include:<br>*
  - *Remove data that does not fall within the specified timeframe*
  - *Convert the data into the correct format (e.g. from text to numbers)*
  - *Remove any unused attributes / columns for testing*
  - *Perform normalization on data (if needed)*
  
  
- **Fitting Data to Model**<br>
  *The next step will be applying the model to the cleaned dataset. Actions to be performed include:*
  - *Splitting the dataset into intervals (e.g. into years) for backtesting purpose.*
    - *This will act as the backtest data*
  - *Use the trained model to predict future data, which includes:*
    - *Predict the market regime that might take place (e.g. bull, bear, neutral)*
    - *Based on the predicted market regime, predict the market trends of the future*
    - *This will act as the forward-testing data*

  
- **Backtesting and Forward Testing**<br>
  *With everything prepared, we can now begin testing by applying these steps:*
  - *First, apply the strategy on the backtest data*
    - *Perform and record all the transactions that has been taken place*
    - *Might consider using parallel processing techniques to potentially improve execution speed*
  - *Then, apply the strategy on the forward-testing data*
    - *Similar to what is done on the backtest data, perform and record all transactions*<br>

  
- **Performance Evaluation**<br>
  *To evaluate the validity of the strategy, all the recorded transactions are processed and additional metrics were calculated. The actions include:*
  - *Calculate the summary statistics of the transactions*
  - *Apply formula and calculate the associated metrics*
  - *Generate a report with the calculated results*


---

## Output
A final report will be produced from the backtest library with the following details:<br>
- **Performance metrics**, including:
  - Sharpe ratio (SR)
  - Maximum drawdown (MDD)
  - Profit and Loss (PnL)
  
- **Graphs** and charts, such as:
  - Equity curve
  - Trade signal timeline

- Full list of **trade records** / transactions

---

## Pre-trained Model
This section details how the machine learning model is trained before applied into the backtest library.<br>
The flowchart below summarizes the steps taken:

![Training flowchart](https://github.com/user-attachments/assets/35a1644d-65a8-4841-bbea-559786942d70)

The PDF version of the flowchart can be retrieved [here](https://github.com/user-attachments/files/19710024/How.to.train.your.model.pdf)


---

### Step 1: Integrate data from multiple sources
Multiple datasets from different sources (e.g. CryptoQuant, Glassnode, Coinglass) were retrieved and combined together for training purposes.

---

### Step 2: Label each interval with market regime
Using algorithm, we will label each divided data with a market regime (e.g. bull, bear, neutral).<br>
Some of the approaches / techniques considered include using:
- Clustering methods (e.g. k-means clustering)
- HMM models (by specifying it to discover three different states)

---

> Note:
> The overall idea is to have three models:
> - One to identify the market regime represented by each data interval (`model 1` in Step 2)
> - One to predict market regimes (`model 2` in Step 3a)
> - One to predict market trend (`model 3` in Step 3b)
>
> 
> The purpose behind this is that, in the backtest library:
> - `model 1` can first be applied to identify the market regime represented by different intervals (whether if it's bull, bear or neutral market).
> - `model 2` can then be used to predict the market regime that might take place.
> - This is followed by `model 3` to predict the trend for each specific regime (the fluctuations, i.e. the ups and downs of the market).

### Step 3a: Train model on market regime prediction
With the regimes labelled, we will start to train our model to predict market regime based on previous data. The steps involved include:
1. Split the data into two: 70% for training and 30% for testing
2. Apply a classification algorithm (e.g. random forest, XGBoost) to train model on prediction
3. Evaluate the results of different models (e.g. perform cross-validation or via ROC curve)
4. Repeat Step 2 - 3 if improvement is required (e.g. hyperparameter tuning / switching to another algorithm)

---

### Step 3b: Train model on market trend prediction
Another model to predict market trend is also trained via the following steps:
- Take data from Step 3 (data categorized into intervals with labelled market regime)
- Within each interval, split the data into two: 70% for training and 30% for testing
- Apply a regression algorithm (e.g. polynomial regression) or time-series model (e.g. LSTM model) to train the data
- Validate the model and perform adjustments if necessary (e.g. hyperparameter tuning)

---

### Step 4: Validate and output the models
With the models trained, they are outputted and saved so that it can be imported into the backtest library later.

---

This marks the end of our explanation! Thank you for your time and patience for reading this documentation. ^_^
