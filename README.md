## Project Overview

This project demonstrates how to adapt a general-purpose large language model (LLM) for specialized German-to-French translation tasks. By leveraging parameter-efficient fine-tuning techniques, I transformed Microsoft's Phi-2 model (2.78B parameters) into an effective translation system while working within the constraints of free-tier Google Colab resources.

## Methodology

### Model Selection Process

After initial experiments with GPT-2 XL showed limited success due to its English-centric training, I selected Microsoft's Phi-2 model because of its:
- Strong multilingual capabilities
- 2.78 billion parameters (exceeding the 1B requirement)
- Better language detection performance compared to similar-sized models

### Dataset Strategy

I employed a two-phase data approach:

1. **Primary Dataset**: 
   - 11,852 verified German-French translation pairs from the Federal Foreign Office Berlin
   - News-oriented content from 2013-2015
   - Split into 80% training and 20% testing sets

2. **Synthetic Augmentation**:
   - Generated additional training pairs using Meta's Llama 3.3 (70B parameters)
   - Carefully filtered for duplicates and inconsistencies
   - Combined with original data to create an enhanced training set

### Efficient Fine-Tuning Approach

To overcome computational limitations, I implemented:

1. **PEFT with LoRA**:
   - Rank (r) = 32 for feature capture
   - Alpha = 64 for adaptation scaling
   - Dropout = 0.1 for regularization

2. **Memory Optimization**:
   - 8-bit quantization to reduce GPU memory usage
   - Progressive rank reduction (r=32 → r=8) when combining datasets

3. **Training Protocol**:
   - 3-5 epochs per model variant
   - Batch size optimized for Colab's free-tier GPUs

## Results and Analysis

The fine-tuned models showed consistent improvement:

1. **Quantitative Metrics**:
   - Baseline (Model A): BLEU 10.29 | BERTScore 0.639
   - Best Performance (Model C): BLEU 11.28 | BERTScore 0.711
   - Combined Data (Model D): Maintained semantic quality (BERTScore 0.711) despite slight BLEU decrease

2. **Key Findings**:
   - LoRA fine-tuning provided 8.1% BLEU improvement over baseline
   - Synthetic data enhanced model performance by 0.18 BLEU points
   - Semantic coherence (BERTScore) remained stable across variations
   - Resource constraints necessitated trade-offs between model capacity and data diversity

## Technical Reflections

1. **Challenges Encountered**:
   - Colab resource limitations impacted training options
   - Initial model selection required significant experimentation
   - Synthetic data generation needed careful prompt engineering

2. **Lessons Learned**:
   - Smaller, well-tuned models can outperform larger generic ones
   - Data quality matters more than quantity in translation tasks
   - Parameter-efficient methods enable meaningful adaptation on limited hardware

3. **Future Directions**:
   - Experiment with more diverse training data domains
   - Test alternative base models (e.g., Mistral 7B)
   - Explore dynamic LoRA configuration strategies

## Ethical Considerations

This work acknowledges that:
- Machine translation systems may inherit or amplify biases
- Performance varies across language varieties and domains
- Critical applications require human oversight
- Low-resource languages need special consideration

The project demonstrates how careful fine-tuning can adapt general LLMs for specific bilingual tasks while maintaining computational efficiency.
