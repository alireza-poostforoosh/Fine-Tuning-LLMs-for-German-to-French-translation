# German-to-French Translation with Fine-Tuned LLMs

## Project Overview

This project demonstrates how I adapted Microsoft's Phi-2 model (2.78B parameters) to specialize in German-to-French translation using a carefully selected subset of data and parameter-efficient fine-tuning techniques - all within the constraints of free-tier Google Colab.

## Dataset Strategy

From the original "German-French website parallel corpus from the Federal Foreign Office Berlin" containing 11,852 translation pairs, I:

1. **Selected a Representative Subset**:
   - Chose 1,000 high-quality translation pairs through random sampling
   - Ensured balanced representation across different content types

2. **Data Partitioning**:
   - Split the 1,000 pairs into:
     - 800 samples for training (80%)
     - 200 samples for testing (20%)
   - Maintained proportional representation in both sets

3. **Data Processing**:
   - Parsed TMX files using BeautifulSoup
   - Validated language pairs
   - Stored processed data in JSON format (dataset_a_train.json and dataset_a_test.json)

## Key Advantages of This Approach

1. **Resource Efficiency**:
   - Enabled faster iteration cycles within Colab's free-tier limitations
   - Reduced GPU memory requirements during training

2. **Quality Control**:
   - Smaller dataset allowed for thorough manual inspection of samples
   - Easier to identify and remove potential anomalies

3. **Experimental Flexibility**:
   - Faster training cycles enabled more hyperparameter testing
   - Simplified combination with synthetic data later in the project

## Impact on Model Performance

Despite the smaller dataset size:
- Achieved meaningful improvements over baseline (BLEU +0.81)
- Demonstrated that quality fine-tuning can be achieved with carefully selected subsets
- The 80/20 split proved sufficient for both training and reliable evaluation

This selective approach balanced computational constraints with model performance needs, proving particularly valuable when working with limited resources. The success with 1,000 pairs suggests the model could effectively learn translation patterns even from this reduced dataset.
