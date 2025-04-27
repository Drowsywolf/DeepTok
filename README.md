# FakeSV: Multimodal Misinformation Detection in COVID-19 Short Videos

## **Team DeepTok**  
- Zhiwei He(zhiwei_he@brown.edu)
- Jinjia Zhang(jinjia_zhang@brown.edu)
- Xulong Xiao(xulong_xiao@brown.edu)
- Zhangchi Fan(zhangchi_fan@brown.edu)



## **Introduction**  
- Short video platforms (e.g., TikTok) have become hotspots for spreading fake news, which exacerbates societal harm. Existing research faces two challenges: (1) lack of large-scale multimodal datasets with social context, and (2) insufficient utilization of multimodal features for detection. This project aims to address these gaps by constructing **FakeSV**, the largest Chinese short video dataset for fake news detection, and proposing **SV-FEND**, a multimodal model leveraging news content and social context.  

- This is a **binary classification task** (fake vs. real news) using multimodal data (text, audio, video, user profiles, comments).  



## **Related Work**  

-  (Shang et al. 2021) use the extracted speech text to guide the feature learning of visual frames, use MFCC features to enhance the speech text, and then use a co-attention module to fuse the visual and speech information.
https://ieeexplore.ieee.org/document/9671928

-  (Choi and Ko 2021) propose a well-designed model that uses pre-trained models to extract features of video frames, title, and comments. The difference in topic distribution between title and comments is used to fuse these two modalities and a topic-adversarial classification is used to guide the model to learn topic-agnostic features for good generalization.
https://dl.acm.org/doi/abs/10.1145/3459637.3482212

- 


## **Data**  
**Original Dataset (FakeSV):**  
- **Source:** Crawled from Douyin (TikTok) and Kuaishou, combined with fact-checking articles.  
- **Size:** 5,538 videos (1,827 fake, 1,827 real, 1,884 debunked) across 738 events.  
- **Features:**  
  - **News Content:** Video frames, audio, titles, transcripts.  
  - **Social Context:** User comments, publisher profiles (verified status, activity metrics).  
- **Preprocessing:** Manual annotation, text extraction.  



## **Methodology**  
**Model Architecture (SV-FEND):**  
1. **Multimodal Feature Extraction:**  
   - **Text:** BERT for titles/transcripts.  
   - **Audio:** VGGish for acoustic features.  
   - **Video:** VGG19 (frames) and C3D (motion).  
   - **Social Context:** BERT for user profiles, weighted comment features.  
2. **Cross-Modal Fusion:**  
   - Co-attention transformers to align text, audio, and visual features.  
   - Self-attention to integrate social context.  
3. **Classification:** Fully connected layer with softmax.  



**Training:**  
- Pretrained models (BERT, VGGish) for feature extraction.  
- Five-fold cross-validation with event-level splits.  
- Loss: Binary cross-entropy.  

**Hardest Part of Implementation:**  
- Changing some models (e.g. viggish) into tensorflow versions.  
- Efficient fusion of six modals.  



## **Metrics**  
- Planned Experiments:
Evaluate our tensorflow version SV-FEND against existing SV-FEND on the original FakeSV dataset, measuring and comparing accuracy, F1-score, precision, and recall.
Analyze the performance on another existing dataset.

- While accuracy is applicable, F1-score, Precision, Recall are also critical for fake news detection. A high F1-score balances precision can avoid false accusations of real news as "fake", a high recall can minimize undetected fake content, and a high precision can avoid over-censorship. Therefore, all these 4 metrics are appropriate. 

- The authors were hoping to find the effectiveness of multimodal fusion over single-modality approaches for fake news detection. They use 4 metrics (Accuracy, macro F1-score, precision, and recall) to quantify the results. 

- Base, target, and stretch goals: 
The base goal is to replicate the core SV-FEND architecture in tensorflow. 
The target is to achieve similar metrics (Accuracy, macro F1-score, precision, and recall) scores on FakeSV. 
The stretch goal is to test our model on another existing dataset to validate its effectiveness.



## **Ethics**  
1. **What broader societal issues are relevant to your chosen problem space?**  
   - Fake news on short video platforms exacerbates public harm by spreading health, political, and economic misinformation, undermines trust in legitimate media, and disproportionately targets vulnerable populations. Detection systems must balance ethical challenges like censorship concerns and algorithmic biases while addressing societal divisions.  

2. **Who are the major “stakeholders” in this problem, and what are the consequences of mistakes made by your algorithm?**  
   - Stakeholders include platform users, publishers, and fact-checkers. False positives could unfairly penalize creators, while false negatives perpetuate misinformation.   



## **Division of Labor**  
- —Zhiwei He
- —Jinjia Zhang
- —Xulong Xiao
- —Zhangchi Fan

