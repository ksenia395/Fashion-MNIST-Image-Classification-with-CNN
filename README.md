Fashion-MNIST: From Linear Baseline to CNN

(Modeling, Errors, and Limits of Visual Classification)

1. Problem Overview

Fashion-MNIST is a standard image classification dataset consisting of 28×28 grayscale images of clothing items across 10 classes.
Although often considered a “simple” dataset, it introduces ambiguity absent in digit recognition tasks such as MNIST, especially for visually overlapping classes like shirts, coats, and pullovers.

The goal of this project was not only to maximize accuracy, but to understand the limitations of different model classes and analyze their errors.

2. Baseline: Logistic Regression
Approach

Images were flattened from 28×28 into 784-dimensional vectors.

A multinomial Logistic Regression model was trained with standard scaling.

Results

Test accuracy: ~0.83

Strong performance on structurally distinct classes (Trouser, Bag, Footwear)

Very weak performance on visually similar upper-body garments

Key Observation

The class Shirt achieved an F1-score of only ~0.58.
Errors were diffuse and poorly structured, indicating that the linear model failed to capture meaningful spatial relationships.

Conclusion:
Logistic Regression treats pixels as independent features and cannot model local visual patterns such as edges, contours, or garment structure.

3. Convolutional Neural Network (CNN)
Architecture

A minimal CNN was implemented:

Two convolutional blocks with ReLU and MaxPooling

Fully connected layer with Dropout

Softmax output layer

Results

Test accuracy: ~0.92

Significant improvement across all classes

Shirt F1-score increased to ~0.78

Interpretation

CNNs leverage local receptive fields and shared weights, enabling the model to learn:

garment contours

sleeve structure

relative spatial arrangements

Errors became semantically meaningful rather than random.

4. Regularization Experiments

To improve robustness and generalization, the following techniques were explored:

Batch Normalization

Added between Conv2D and ReLU layers

Stabilized training and reduced sensitivity to initialization

Data Augmentation

Mild translation and zoom were applied

Rotation was intentionally removed due to image resolution (28×28), where rotation often destroyed fine garment details

Dropout Tuning

Strong dropout (0.3) led to underfitting

Optimal performance achieved around Dropout = 0.1

Final Performance

Test accuracy: ~0.91

Balanced performance across classes

Stable convergence with EarlyStopping

5. Error Analysis: The “Shirt” Class

Despite improvements, Shirt remained the most difficult class.

Most frequent misclassifications:

Shirt → T-shirt/top

Shirt → Coat

Shirt → Pullover

Visual Inspection

Manual inspection of misclassified examples showed that:

Many samples are ambiguous even for humans

Variations in sleeve length, fabric thickness, and garment cut blur class boundaries

The dataset itself encodes a semantic overlap, not a clean visual separation

Key Insight

The remaining errors are not caused by insufficient model capacity,
but by intrinsic ambiguity in class definitions.

CNN errors were structured, interpretable, and aligned with human perception.

6. Final Conclusions

Linear models fail on Fashion-MNIST due to lack of spatial awareness.

CNNs dramatically improve performance by learning local visual features.

Regularization must be carefully balanced; excessive augmentation or dropout harms small-resolution datasets.

Some classification errors are irreducible without redefining labels or adding context.

This project demonstrates that accuracy alone is insufficient; understanding why a model fails is equally important.

7. Possible Extensions

CIFAR-10 (color, higher complexity)

Transfer learning with pretrained CNNs

Metric learning or hierarchical labels for ambiguous classes

📎 Kaggle Notebook
The full implementation and experiments are available on Kaggle:

👉 View the Kaggle Notebook https://www.kaggle.com/code/ksenia395/fashion-mnist/
