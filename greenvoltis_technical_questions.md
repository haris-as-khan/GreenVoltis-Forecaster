"Assume your forecasting model is live in production, but the market volatility undergoes a 
significant Distribution Shift (or Regime Change).

Q1:
What techniques would you employ to dynamically adjust your prediction confidence 
intervals to ensure they maintain valid statistical coverage guarantees during these periods?" 

A1:
Regime changes eradicates the assumption that the historical forecast-error distribution remains stable and therefore usable as a predictor. I would
therefore use an adaptive conformal prediction framework in which non-confirmity scores are recalibrated using a rolling or exponentially weighted
window of recent forecast errors. This allows intervals to widen automatically when recent errors increase and contract when conditions stabilise. 


"The activation of ancillary services is typically a sparse event, resulting in highly 
imbalanced datasets.

Q2:
How would you design the loss function or sampling strategy to train a predictive 
model that handles this extreme data imbalance, while ensuring the model's predictive 
validity (e.g., avoiding high False Positives)?

A2:
Because mFRR activation is a sparse event, a high accuracy score could be mislead as a model that predicts no activation in also all windows
could achieve a high accuracy, even though it is commercially useless. So instead I would formulate the task a cost-sensitive binary 
classification and initially use weighted binary cross-entropy, assigning greater weights to the minority activation class. 


