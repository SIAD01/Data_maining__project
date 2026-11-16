# Data_maining__project
f1-win-lose-cause


f1-win-lose-cause/
├── README.md                 # problem, method, results, how to run
├── requirements.txt
├── LICENSE                   # MIT
├── .gitignore
├── data/
│   ├── README.md             # source + description of the data
│   ├── raw/archive.zip       # your original 14 CSV files
│   └── processed/            # f1_cleaned.csv is created here by the notebook
├── notebooks/
│   └── 01_cleaning_eda_modelling.ipynb   # cleaning + EDA + models
└── app/
    └── index.html            # your interactive page

Description :
       This project asks a simple question: why does a Formula 1 driver win or lose a race? Three factors compete to explain a result: the driver’s skill, the car’s quality, and the starting position. Using every race from 2003 to 2024, I cleaned and merged the official F1 data, explored it, and built statistical models to measure how much each factor matters. The final model powers an interactive web page where anyone can pick a driver, a car, a season and a grid slot, and see the win probability and the main reason for the result.
    
