## Understanding Distribution Shifts in MLOps

### Explained in a Manufacturing Scenario 🏭
(October 2024)

**My prompt:**

```
I want to gain Understanding to the different types of distribution shifts in an MLOps lifecycle in AI development. 

Let X denote the input to a model and Y its output. In supervised learning,  the training data is a set of samples drawn from the joint distribution P(X,Y), while the model learns the conditional distribution P(Y|X).

Give me examples for the key types of drift: concept drift, covariate shift, label drift.

As an example use a production scenario where the AI system that has been developed is responsible to distinguish OK images from NOK images.
```

**ChatGPTs answer** (o1-preview):

Understanding distribution shifts in an MLOps lifecycle is crucial for maintaining the performance of AI models over time. In the context of an AI system responsible for distinguishing between OK (acceptable) images and NOK (not acceptable) images, let's explore the key types of drift: **covariate shift**, **concept drift**, and **label drift**.

---

### **1. Covariate Shift**

**Definition**: Covariate shift occurs when the distribution of the input data \( P(X) \) changes between the training and production environments, but the relationship between the inputs and outputs \( P(Y|X) \) remains the same.

**Example**:

- **Scenario**: The AI system was trained on images of products taken with a specific camera under controlled lighting conditions. In production, a new camera with different specifications is installed, or the lighting conditions change due to seasonal effects (e.g., more natural light during summer months).
- **Impact**: The input images \( X \) now have different characteristics (resolution, brightness, color balance) compared to the training data.
- **Consequence**: The model may perform poorly because it's receiving inputs from a different distribution, even though the way it should classify images (the mapping \( P(Y|X) \)) hasn't changed.

---

### **2. Concept Drift**

**Definition**: Concept drift happens when the relationship between inputs and outputs \( P(Y|X) \) changes over time. This means that the underlying concept the model is trying to learn has evolved.

**Example**:

- **Scenario**: The definition of what constitutes an NOK image changes due to updated quality standards or the introduction of new product models with different features.
    - For instance, a defect that was previously acceptable becomes unacceptable, or new types of defects appear that were not present in the training data.
- **Impact**: The conditional distribution \( P(Y|X) \) has changed because the same input \( X \) might now correspond to a different output \( Y \).
- **Consequence**: The model's predictions become less accurate over time because it hasn't learned the new mapping between inputs and outputs.

---

### **3. Label Drift**

**Definition**: Label drift refers to changes in the distribution of the output labels \( P(Y) \) over time, while the relationship \( P(Y|X) \) remains constant.

**Example**:

- **Scenario**: The proportion of OK to NOK images shifts due to changes in the manufacturing process.
    - For example, if production quality improves, there might be a higher percentage of OK images and fewer NOK images than in the training data.
- **Impact**: The marginal distribution of the labels \( Y \) changes, affecting metrics like precision and recall, especially if the model was calibrated on the original label distribution.
- **Consequence**: The model might become biased toward predicting the majority class (e.g., predicting more images as OK), leading to potential oversight of NOK images.

---

### **Mitigation Strategies**

- **For Covariate Shift**:
    - Implement input data normalization and augmentation techniques.
    - Retrain the model with new data reflecting the current input distribution.
- **For Concept Drift**:
    - Continuously monitor model performance and retrain when significant drift is detected.
    - Use online learning algorithms that can adapt to changes in \( P(Y|X) \).
- **For Label Drift**:
    - Adjust the model's decision thresholds based on the current label distribution.
    - Rebalance the training dataset to reflect the new label proportions.

---

### **Conclusion**

Identifying and understanding these types of distribution shifts allow you to take proactive measures to maintain the effectiveness of your AI system. Regular monitoring, data collection, and model updates are essential components of a robust MLOps strategy.