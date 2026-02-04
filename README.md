# AI-Generated Product Review Detection Model

## Project Overview

This project develops a **hybrid ensemble machine learning model** to detect AI-generated fake product reviews on e-commerce platforms. With the proliferation of LLM-generated content, distinguishing authentic customer reviews from synthetic ones has become critical for maintaining consumer trust and platform integrity.

### Problem Statement
AI-generated fake reviews erode consumer trust, mislead purchasing decisions, and unfairly advantage sellers who use artificial inflation tactics. This detection system aims to restore trust in online review ecosystems by identifying synthetic reviews with high accuracy.

### Project Objectives
1. **Data Collection**: Scrape genuine reviews from multiple e-commerce platforms (Amazon, Daraz, eBay, Temu) and generate synthetic reviews using GPT-4/GPT-5
2. **Model Development**: Implement a hybrid ensemble approach combining:
   - **DistilBERT**: For semantic text analysis and linguistic pattern detection
   - **Random Forest**: For metadata-based behavioral analysis
3. **Model Evaluation**: Test and fine-tune models using accuracy, F1-score, and recall metrics, with emphasis on adversarial robustness
4. **Deployment**: Build a Streamlit web application for real-time review authenticity verification

---

## Key Features

- **Multilingual Support**: Handles English, Sinhala, and Singlish reviews (particularly from Daraz platform)
- **Hybrid Detection**: Combines deep learning (DistilBERT) with traditional ML (Random Forest) for robust classification
- **Metadata Analysis**: Incorporates review length, emoji frequency, and rating patterns as behavioral signals
- **Real-world Dataset**: 30,000+ reviews from 4 major e-commerce platforms
- **Web Interface**: User-friendly Streamlit app for instant review verification (under development)
- **Adversarial Testing**: Evaluated against "humanized" AI reviews to assess robustness

---

## Methodology

The collected review dataset underwent comprehensive **exploratory data analysis (EDA)** to understand text characteristics, rating distributions, and linguistic patterns that distinguish human from AI-generated content. Key findings revealed that AI reviews exhibit significantly lower emoji usage, more consistent length patterns, higher lexical diversity, and more formal vocabulary compared to human reviews.

Following EDA, a detailed **data preprocessing pipeline** was applied:
1. **Text Cleaning**: Removal of URLs, special characters, and excessive whitespace; lowercasing; stopword removal (English + Sinhala)
2. **Missing Value Handling**: Rule-based sentiment analysis for imputing missing ratings on Daraz, eBay, and Temu reviews
3. **Feature Engineering**: 
   - Text features via TF-IDF vectorization (max 5,000 features, unigrams + bigrams)
   - Metadata features including review length, emoji count, rating, word count, punctuation density, and capitalization ratio
4. **Normalization**: StandardScaler applied to metadata features
5. **Class Balance Strategy**: Preserved natural 7.1:1 (Human:AI) imbalance during preprocessing; SMOTE applied during model training

The **hybrid ensemble model** combines two complementary approaches:
- **DistilBERT**: Fine-tuned transformer for semantic text analysis, capturing linguistic patterns and contextual meaning
- **Random Forest**: Traditional ML classifier for metadata-based behavioral analysis, leveraging engineered features

Both models are integrated via a **soft voting mechanism**, where their probability outputs are weighted and combined to produce the final classification. This architecture provides robustness—if AI reviews become more semantically human-like, metadata features (emoji usage, length variance) remain discriminative.

Models are trained using stratified cross-validation (k=5) with hyperparameter tuning via grid search. Performance is evaluated using **F1-score, precision, recall, and AUROC**, with particular emphasis on recall (minimizing false negatives—undetected AI reviews). Adversarial testing is conducted on "humanized" AI reviews (paraphrased GPT outputs) to assess model robustness.


**Rationale for Hybrid Approach**:
- **Complementary Strengths**: DistilBERT excels at capturing semantic nuances; Random Forest handles structured behavioral signals
- **Adversarial Defense**: Metadata features are harder for AI to mimic convincingly (e.g., emoji usage patterns)
- **Interpretability**: Random Forest provides feature importance; DistilBERT can be explained via LIME/SHAP
- **Literature Gap**: Most existing work uses single-model approaches; hybrid semantic + behavioral detection is a novel contribution

---

## User Interface

A user-friendly **Streamlit web application** is under development with an intuitive design for real-time review authenticity verification. The interface features:

### Core Functionality
- **Single Review Input**: Text area for users to paste or type a product review
- **Instant Classification**: Real-time model inference displaying authenticity verdict (Human/AI) with confidence score
- **Visual Feedback**: Color-coded results (green for human, red for AI) with probability meters

### Enhanced Features (Planned)
- **Batch Processing**: CSV file upload for analyzing multiple reviews simultaneously
- **Feature Visualization**: 
  - Word clouds highlighting discriminative terms
  - Emoji usage comparison charts
  - Review length distribution plots
- **Explanation Dashboard**: 
  - LIME-generated explanations showing which words influenced the prediction
  - Metadata feature breakdown (review length, emoji count, etc.)
  - Confidence intervals and prediction reliability scores
- **Review History**: Optional local storage of analyzed reviews for comparison
- **Export Functionality**: Downloadable PDF reports with analysis results

### Design Philosophy
- **Minimalist Interface**: Clean, professional aesthetic with clear call-to-action buttons
- **Accessibility**: High contrast ratios, responsive design for mobile/desktop compatibility
- **Performance**: Sub-2-second inference time; cached model loading for instant predictions
- **Educational Value**: Tooltips and help sections explaining detection methodology

### Technology Stack
- **Frontend**: Streamlit (Python framework for rapid ML app development)
- **Deployment**: Streamlit Cloud (free tier) for public accessibility
- **Model Integration**: Pickle-serialized ensemble model loaded on app initialization
- **Visualization**: Plotly for interactive charts, Matplotlib for static plots


## Current Progress (45% Complete)

### Completed Tasks
- [x] Data collection from Amazon, Daraz, eBay, and Temu
- [x] AI review generation using GPT-4/5 with structured prompts
- [x] Comprehensive data preprocessing pipeline
- [x] Rule-based sentiment analysis for missing ratings
- [x] Feature engineering (TF-IDF, metadata features)
- [x] Dataset balancing and labeling
- [x] Exploratory data analysis with statistical validation

### In Progress
- [ ] Hybrid ensemble model development (DistilBERT + Random Forest)
- [ ] Model training on GPU (Google Colab)
- [ ] Hyperparameter tuning and optimization

###  Upcoming Tasks
- [ ] Model testing on withheld "humanized" AI reviews
- [ ] Streamlit application development
- [ ] User Acceptance Testing (UAT)
- [ ] Final deployment and documentation

---
## Disclaimer

**This project is developed solely for academic and research purposes as part of the BSc (Hons) Data Science and Analytics program at the University of Westminster.**
