# Out-of-Context Multi-Modal CheapFakes Detection

This study utilizes scene graphs and existing research in image-text matching to enable the model to identify inconsistencies based on similarity scores of image-caption pairs.

The project focuses on detecting *Out-of-Context (OOC)* media — cases where images or videos remain visually unedited, but misleading information is introduced via misaligned or contradictory captions. This challenge requires semantic understanding between image content and associated text.

Additionally, the system extracts and fuses features that represent semantic relationships between image and text modalities, then applies reasoning mechanisms to determine caption consistency.


## Detailed Overview

### 🔹 Thesis Summary
- **Institution**: VNUHCM - University of Science  
- **Degree**: Bachelor of Data Science  
- **Time**: Oct 2020 - Sep 2024  
- **Thesis Title**: CheapFakes Detection  
- **Goal**: Assist fact-checkers in identifying media used out of context via automatic multimodal detection systems.

### 🔹 Problem Description
Out-of-context detection focuses not on manipulated media, but on true images misused by misleading or contradictory textual descriptions. The goal is to predict whether one of two captions referencing the same image presents a contextually incorrect description.

### 🔹 Research Tasks
- Predict contextual consistency in image + (caption1, caption2) triplets.
- Explore two approaches: supervised learning and hybrid modeling.
- Evaluate the potential of hybrid methods for future model improvements.

### 🔹 Visual Scene Graphs
- Extracted using **Neural Motifs** and **PE-Net**.
- Selected top **N₀ = 36** objects and **Nᵣ = 25** relation predicates.
- Represented as:
  - **bbox**: bounding boxes for object coordinates.
  - **labels**: object class names.
  - **rels**: relationships between object pairs.

### 🔹 Textual Scene Graphs
- Built using **SPICE** for rule-based semantic parsing.
- For ~11.79% of captions where SPICE failed, **FACTUAL-T5** was used.
- Scene graphs were constructed over pairs of captions describing the same image.

### 🔹 Visual Encoder
- Scene graph encoded as G = (O, B, R), where:
  - O: object labels,
  - B: bounding boxes,
  - R: predicted relationships.
- Used **EfficientNet-B5** for feature extraction.
- **GCN** and **Swish activation** used to integrate visual features.

### 🔹 Textual Encoder
- Captions represented as scene graphs and processed via **LSTM**.
- Extracted relational structure from text graphs, fused similarly to visual encoding.

### 🔹 Natural Language Inference (NLI)
- Applied **DeBERTa-v3** and **RoBERTa** for inferring logical relationships between two captions.
- Captions were labeled as *Entailment*, *Contradiction*, or *Neutral*.

### 🔹 Experimental Results

| Visual Graph | NLI Model    | D1     | D2     | D3     | D4     |
|--------------|--------------|--------|--------|--------|--------|
| PE-Net       | RoBERTa      | 0.751  | 0.777  | 0.793  | 0.819  |
| PE-Net       | DeBERTa-v3   | **0.796** | **0.804** | **0.823** | **0.834** |
| Neural Motifs| RoBERTa      | 0.761  | 0.787  | 0.791  | 0.802  |
| Neural Motifs| DeBERTa-v3   | 0.770  | 0.792  | 0.810  | 0.822  |

### 🔹 Conclusion
The combination of **PE-Net + DeBERTa-v3** achieved the best result, reaching **83.4% accuracy** on the D4 dataset. This work demonstrates the promise of multimodal and semantic-reasoning approaches in combating misinformation via cheapfakes.

## Acknowledgements

- Based on methods from:
  - Neural Motifs (Zellers et al.)
  - PE-Net
  - EfficientNet (Tan & Le)
  - DeBERTa-v3 (Microsoft)
  - SPICE / FACTUAL-T5 for semantic parsing

## License


