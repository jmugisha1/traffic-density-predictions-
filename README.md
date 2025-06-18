# Traffic Prediction Model for Rwanda

## Problem Statement
Rwanda's rapid urbanization, particularly in Kigali, has led to severe traffic congestion due to imported vehicles and infrastructure limitations. This affects public transportation efficiency and delivery logistics. This project develops a machine learning model to predict traffic conditions to enable route optimization, improve traffic light systems, and integrate with existing monitoring solutions.

## Dataset
The project uses a traffic dataset ([`traffic/Traffic.csv`](traffic/Traffic.csv )) containing time-based vehicle counts (cars, bikes, buses, trucks), temporal features (time of day, day of week), and traffic situation labels (low, normal, heavy, high). The dataset captures traffic patterns to help predict congestion levels at different times and locations.

## Model Comparison

| Model | Optimizer | Early Stopping | Regularization | Training Accuracy | Validation Accuracy | Training Loss | Validation Loss |
|-------|-----------|----------------|----------------|-------------------|---------------------|---------------|-----------------|
| Model 1 | Adam | Yes | L1L2 | 0.9568 | 0.9636 | 0.2853 | 0.2596 |
| Model 2 | Adam | No | L1L2 | 0.9532 | 0.9524 | 0.2845 | 0.2856 |
| Model 3 | RMSprop | No | L1L2 | 0.9382 | 0.9496 | 0.3112 | 0.2672 |
| Model 4 | Default | No | L1L2 | 0.9388 | 0.9706 | 0.3018 | 0.2594 |

## Detailed Model Metrics

| Training Instance | Optimizer Used | Regularizer Used | Epochs | Early Stopping | Number of Layers | Learning Rate | Accuracy | F1 Score |
|-------------------|----------------|------------------|--------|---------------|-----------------|--------------|----------|----------|
| Instance 1 | Adam | L1L2 (0.001, 0.001) | 100 | Yes (patience=15) | 3 | 0.002 | 0.9636 | 0.9530 |
| Instance 2 | Adam | L1L2 (0.001, 0.001) | 100 | No | 3 | 0.002 | 0.9524 | 0.9597 |
| Instance 3 | RMSprop | L1L2 (0.001, 0.001) | 100 | No | 3 | 0.002 | 0.9496 | 0.9413 |
| Instance 4 | Default (SGD) | L1L2 (0.001, 0.001) | 100 | No | 3 | Default | 0.9706 | 0.9547 |

## Findings

The neural network architecture consisted of:
- Input layer based on feature dimensions
- Two hidden layers (128 and 64 neurons) with ReLU activation
- Dropout layers (0.3) to prevent overfitting
- L1L2 regularization on all dense layers
- Output layer with softmax activation for multi-class prediction

### Best Performing Model
Model 1 with Adam optimizer and early stopping performed consistently well with high training accuracy (95.68%) and validation accuracy (96.36%), showing good generalization. The saved model (`best_model.keras`) can be loaded for predictions on new data.

Model 4 achieved the highest validation accuracy (97.06%) with the lowest validation loss (0.2594) despite using the default optimizer, demonstrating that sometimes simpler configurations can be effective.

### Implementation Insights
- Neural networks outperformed traditional ML algorithms for this problem due to their ability to capture complex non-linear relationships in traffic data
- Early stopping proved beneficial to prevent overfitting
- L1L2 regularization was crucial across all models to maintain generalization
- Data preprocessing (standardization for numerical features, one-hot encoding for categorical features) significantly improved model performance

This traffic prediction system can be integrated with existing technologies in Rwanda to optimize traffic flow, reduce congestion, and improve urban mobility.


###video link
https://www.youtube.com/watch?v=TU8Bd3gZG3c
