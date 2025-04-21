# RetentionModel.mlmodel

## Overview

`RetentionModel.mlmodel` is a Core ML machine learning model developed by **EGK IsaacLab Industry4.0** to predict employee retention within an organization. Using a Feature Vectorizer + Tree Ensemble Classifier architecture, this model analyzes key employee attributes to predict whether an employee is likely to stay or leave. It aligns with Industry 4.0 principles by enabling data-driven decision-making, automation of HR analytics, and predictive insights to improve workforce management.

This model is optimized for on-device inference on Apple devices, making it suitable for integration into iOS, macOS, tvOS, watchOS, and visionOS applications. It can be used by HR teams, managers, and organizations to proactively address employee turnover, enhance engagement strategies, and optimize retention efforts.

## Features

- **Retention Prediction**: Predicts whether an employee will stay or leave based on input features.
- **Core ML Compatibility**: Supports iOS 11.0+, macOS 10.13+, tvOS 11.0+, watchOS 4.0+, and visionOS 1.0+.
- **Input Features**:
  - `age`: Employee’s age (Double).
  - `tenure`: Years at the company (Double).
  - `salary`: Annual salary in USD (Double).
  - `engagement_score`: Engagement score on a 1-5 scale (Double).
  - `promotions`: Number of promotions received (Double).
- **Output**:
  - `classLabel`: Predicted class (`Stay` or `Leave`) as an Int64.
  - `classProbability`: Dictionary mapping each class to its probability (e.g., `{"Stay": 0.7, "Leave": 0.3}`).
- **Model Size**: Compact at 629 KB, ensuring efficient on-device performance.
- **Industry 4.0 Integration**: Supports smart HR analytics through predictive modeling and automation.

## Model Details

- **Architecture**: Feature Vectorizer + Tree Ensemble Classifier, a robust combination for handling structured tabular data with high interpretability.
- **Training Data**: Trained on a synthetic or anonymized dataset of employee records, including features like age, tenure, salary, engagement scores, and promotion history. The dataset is balanced to ensure fair prediction across `Stay` and `Leave` classes.
- **Classes**:
  - `Stay` (0): Employee is predicted to remain with the organization.
  - `Leave` (1): Employee is predicted to leave the organization.
- **Performance**: Evaluated using standard metrics like accuracy, precision, recall, and F1-score on a held-out test set (specific metrics not provided in the model metadata but can be computed during evaluation).

## Requirements

- **Platform**:
  - iOS 11.0 or later
  - macOS 10.13 or later
  - tvOS 11.0 or later
  - watchOS 4.0 or later
  - visionOS 1.0 or later
- **Dependencies**:
  - Core ML framework (built into Apple OS).
- **Hardware**: Apple devices with an A9 chip or later for optimal performance.
- **Input Data**:
  - A dictionary or struct containing the five features (`age`, `tenure`, `salary`, `engagement_score`, `promotions`) as Double values.

## Installation

1. **Add to Xcode Project**:
   - Drag `RetentionModel.mlmodel` into your Xcode project.
   - Ensure the model is added to your app’s target under "Build Phases" > "Copy Bundle Resources."
2. **Generate Swift Interface**:
   - Xcode will generate a Swift class (e.g., `RetentionModel`) for the model.
   - Check the model’s input/output specifications in Xcode’s model inspector.
3. **Set Up Dependencies**:
   - Import Core ML in your Swift file:
     ```swift
     import CoreML
     ```

## Usage

### 1. Prepare Input Data
Ensure your input data matches the expected feature types (all Doubles). For example:

- `age`: 30.0
- `tenure`: 5.0
- `salary`: 60000.0
- `engagement_score`: 4.2
- `promotions`: 2.0

### 2. Run Inference
Here’s a sample Swift code snippet to run inference using the model:

```swift
import CoreML

// Load the model
guard let model = try? RetentionModel(configuration: MLModelConfiguration()) else {
    fatalError("Failed to load RetentionModel")
}

// Prepare input data
let input = RetentionModelInput(
    age: 30.0,
    tenure: 5.0,
    salary: 60000.0,
    engagement_score: 4.2,
    promotions: 2.0
)

// Perform prediction
guard let output = try? model.prediction(input: input) else {
    fatalError("Failed to perform prediction")
}

// Access results
let predictedLabel = output.classLabel // 0 (Stay) or 1 (Leave)
let classProbabilities = output.classProbability
let stayProbability = classProbabilities[0] ?? 0.0
let leaveProbability = classProbabilities[1] ?? 0.0

// Map the label to a human-readable string
let labelString = predictedLabel == 0 ? "Stay" : "Leave"
print("Predicted Retention: \(labelString) (Stay: \(stayProbability), Leave: \(leaveProbability))")
```

### 3. Interpret Output
- **classLabel**: The predicted class as an Int64 (`0` for `Stay`, `1` for `Leave`).
- **classProbability**: A dictionary mapping each class to its probability (e.g., `{"0": 0.7, "1": 0.3}` means 70% chance of staying, 30% chance of leaving).

### 4. Example Application
Integrate this model into an HR analytics app:
- Collect employee data (age, tenure, salary, engagement score, promotions).
- Use `RetentionModel.mlmodel` to predict retention likelihood.
- Display results in the app, e.g., "Employee X has a 70% chance of staying."
- Automate retention strategies (e.g., send engagement surveys to employees predicted to leave).

## Training and Fine-Tuning

- **Training Data**: Expand the dataset with more employee records, including diverse demographics and job roles, to improve model generalization.
- **Fine-Tuning**: Use Core ML’s on-device training capabilities (iOS 13+) to adapt the model to organization-specific data.
- **Evaluation**: Compute metrics like accuracy, precision, recall, and F1-score on your dataset to assess model performance.

## Limitations

- **Feature Dependency**: Predictions rely on the quality and completeness of input features. Missing or noisy data (e.g., incorrect salary) may reduce accuracy.
- **Generalization**: The model may not generalize well to industries or roles not represented in the training data.
- **Static Model**: Does not account for temporal changes (e.g., recent engagement score trends); consider retraining with updated data.

## Contributing

1. Fork the repository: `https://github.com/EGK-IsaacLab/RetentionModel.git`.
2. Create a feature branch (`git checkout -b feature/new-feature`).
3. Commit changes (`git commit -m "Add new feature"`).
4. Push to the branch (`git push origin feature/new-feature`).
5. Open a pull request.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

## About EGK IsaacLab Industry4.0

**EGK IsaacLab Industry4.0** is a team dedicated to advancing smart automation and data-driven solutions through Industry 4.0 principles. We focus on leveraging machine learning, IoT, and predictive analytics to solve real-world challenges, such as workforce management and health monitoring. This model is part of our initiative to empower organizations with actionable insights for employee retention.

## References

- Core ML Documentation: [Apple Developer](https://developer.apple.com/documentation/coreml).
- Industry 4.0 Principles: General knowledge on smart HR analytics and automation.