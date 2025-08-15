# Graph Attention Networks for Modeling Multi-Sensor Relationships in Early Prediction of Critical Events in ICU Patients

### 1. Abstract
This project presents a deep learning solution for the automated and early detection of six critical cardio-respiratory conditions in Intensive Care Unit (ICU) patients: Sepsis Onset, Cardiac Arrest Imminent, Acute Hypotension, Respiratory Failure, and Atrial Arrhythmia. Utilizing a comprehensive approach, multiple physiological signals, including ECG, ABP, and SpO2, are used as input. These signals are transformed into graph neural networks, where each node represents a signal within a time window, and edges denote physiological correlations and temporal relationships. To process this complex structure, an advanced Graph Attention Network (GAT) model is employed. This model is capable of learning local and global patterns within the graph to make a holistic, patient-level prediction. Initial results indicate promising performance in detecting these critical conditions, marking a significant step towards improving patient monitoring and decision-making in the ICU.

### 2. Introduction
Monitoring patients in the ICU is one of the most challenging tasks in clinical medicine. Conditions such as sepsis and cardiac arrest require rapid detection and intervention. Currently, diagnosis relies heavily on human interpretation of vital signs, which can be prone to error due to the large volume of data and staff fatigue. The objective of this project is to develop an intelligent model that automates and enhances this process by analyzing simultaneously recorded, interconnected physiological signals. Our proposed method, by modeling the relationships between signals as a graph, emulates the complex pathophysiology of these diseases.

### 3. Methodology
##### 3.1. Graph Structure
Each patient is transformed into a single graph. In this graph:

- Nodes: Each node represents a single physiological signal (e.g., ECG) within a 5-minute time window.
- Edges: Edges represent two types of connections: 
    - Physiological Edges: Created based on the Pearson correlation between different signals within a single time window.
    - Temporal Edges: Connect each signal to its counterparts in successive time windows to model changes over time.

##### 3.2. GNN Model Architecture
Our core model is a GATClassifier designed for graph-level classification. This model uses multiple ```GATv2Conv``` layers that combine information from neighboring nodes with dynamic attention weights. For the final prediction:

Node Embeddings: The GAT layers transform the features of each node (signal) into information-rich embedding vectors.

Global Pooling: A ```global_mean_pool``` layer aggregates these embeddings from all nodes within a graph into a single vector representing the entire patient.

Final Classification: This final vector is passed through a linear layer to classify the patient into one of the six disease classes.

##### 3.3. Training and Evaluation
The model is trained on a dataset of 900 patients. The data is split at the patient level into training, validation, and test sets to prevent data leakage. To address class imbalance, SMOTE is used alongside class weighting in the ```CrossEntropyLoss``` function.

### 4. Results and Discussion
Here you should insert the quantitative results of your model:

- Accuracy and F1-Score: The overall performance of the model on the training and test sets.
- Multi-class ROC-AUC: The AUC score for each class, indicating the model's ability to distinguish each class from the others.
- Confusion Matrix: A visual representation of the model's performance, highlighting which classes the model confuses with one another.

### 5. Conclusion and Future Work
This project demonstrates a powerful graph-based approach for detecting critical conditions in the ICU. The model's ability to understand physiological relationships makes it a valuable tool. In the future, the model's performance can be improved by:

- Using more complex architectures, such as GAT with GRU layers, to better model the temporal dimension.
- Adding hand-crafted features to the nodes to increase information richness.
- Experimenting with more advanced pooling algorithms like Global Attention Pooling.

### 6. Prerequisites
To run this project, you need to install the following libraries in the ```requirements.txt``` file.

To install, run the following command:
```pip install -r requirements.txt```
