# mFRR Activation Forecasting – Technical Task

OVERVIEW
--------
This submission contains a Jupyter notebook implementing a probabilistic
forecasting framework for mFRR Up and Down energy activation at quarter-hour
resolution.

The workflow includes:

- REST API data retrieval
- Data cleaning and validation
- Point-in-time availability controls using publication timestamps
- Construction of mFRR Up and Down activation targets
- Historical market-state feature engineering
- Leakage-safe training dataset construction
- Separate probabilistic models for Up and Down activation
- 24-hour / 96-quarter-hour activation probability forecasts


PYTHON VERSION
--------------
Python 3.10 or later is recommended.


SETUP
-----

1. Create a virtual environment:

Windows:

    python -m venv .venv
    .venv\Scripts\activate

macOS / Linux:

    python3 -m venv .venv
    source .venv/bin/activate


2. Install the required packages:

    pip install -r requirements.txt


3. Launch Jupyter:

    jupyter notebook


4. Open:

    mFRR_activation_forecasting.ipynb


DATA
----
The notebook retrieves the required market data directly from the REST API
provided as part of the technical exercise.

An active network connection to the API endpoint is therefore required when
running the data retrieval sections of the notebook.

To manage the API limits, the code loops over the API GET request in 6hr
windows until it captures all the required data. 


MODELLING NOTES
---------------
The forecast target is defined separately for mFRR Up and Down as a binary
activation event:

  activation = 1 if realised activation energy != 0 MWh
             = 0 otherwise

The corresponding realised MWh values are retained for analysis and potential
future conditional-volume modelling.

All predictor information is controlled using publication_time_utc to avoid
using information that was unavailable at the relevant historical forecast
origin.

Separate probabilistic classifiers are trained for mFRR Up and mFRR Down.
The resulting output is the estimated probability of activation for each of
the next 96 quarter-hour delivery periods.
