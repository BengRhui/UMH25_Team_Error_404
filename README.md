# Team Error 404 (UM Hackathon 2025)
Hi, everyone! Welcome to our group's `GitHub` repo. All our ideas, documents and code will be recorded here.

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

## Conceptual Diagram
Our conceptual diagram is as shown:

![Arc Diagram](https://github.com/user-attachments/assets/b46f376b-42b3-48f6-bde3-9fd4cb78e4fe)

The PDF Version of the diagram can be retrieved here: [Conceptual Diagram.pdf](https://github.com/user-attachments/files/19682125/Arc.Diagram.pdf)

The diagram can be divided into three parts:
- Input
- Backtest Library
- Output

The explanation for each part is detailed in the following section.

---

## Input
To use the backtest library, we will need to provide a few inputs, including:
- **Trading Data**<br>
  *Dataset that will be used for backtesting. This dataset can be retrieved from various sources (e.g. CryptoQuant, Glassnode, Coinglass) via API calls.*
  <br>
  
- **Timeframe**<br>
  *Act as a filter to include only the records within the specific timeframe for backtesting (e.g. given a dataset from year 2000 to 2024, we can set the timeframe as 2020 to 2024 to only include data within the year range).*
  <br>
  
- **Requirements**<br>
  *Additional requirements that should be taken into consideration while performing backtesting (e.g. trading fees of 0.06%).*
  <br>
  
- **Strategies**<br>
  *The strategy that will be used to perform backtesting. An example would be:*
  >*BUY when flow_total > 0.01*<br>
  >*SELL when flow_total < 8*<br>
  >*HOLD for other conditions*
  

- **Trained Model**<br>
  *The machine learning (ML) model that was trained beforehand before applied to the backtesting library.*<br>
  *For more details on how the ML model is built, please click [here](#Pre-trained-Model).*
  <br>

## Backtest Library
ABC

## Output
ABC

---

## Pre-trained Model
