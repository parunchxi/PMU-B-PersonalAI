# Mental disorder detection from social media data

The "Predicting Mental Health Disorders from Social Media Data" project aims to detect depression through social media posts. By analyzing user expressions from platforms like Facebook, Twitter, and Instagram, it identifies individuals at risk of depression, enabling timely support and intervention.

## Problem Statement

Many people express their thoughts and feelings on social media. What if we could analyze the emotions conveyed in these posts? This could promote better mental health by identifying signs of distress and providing appropriate support.

## Data Collection

### Types of Social Media

- **Forums:** Online discussion boards where users create and reply to topics. (e.g., Quora, Reddit)
- **Microblogs:** Platforms with character-limited posts, often including media and links. (e.g., Twitter, Weibo)
- **Product/Service Reviews:** Websites where users evaluate products and share reviews. (e.g., Amazon, Yelp)
- **Social Networks:** Platforms for connecting and sharing with others through profiles, posts, and interactions. (e.g., Facebook, VK)
- **Photo Sharing:** Platforms focused on uploading, captioning, and sharing images. (e.g., Instagram, Flickr)

### Social Media Matrix

| **Type**          | **Customised Message**                                                                                                                      | **Broadcast Message**                                                                                                                      |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| **Profile-based** | **Relationship**: Allowing users to connect, reconnect, communicate, and build relationships. (e.g., Facebook, LinkedIn)                    | **Self-Media**: Allowing users to broadcast their updates and others to follow. (e.g., Twitter, Weibo)                                     |
| **Content-based** | **Collaboration**: Allowing users to collaboratively find answers, advice, help, and reach consensus. (e.g., Quora, Reddit, Yahoo! Answers) | **Creative Outlets**: Allowing users to share their interests, creativity, and hobbies with each other. (e.g., YouTube, Flickr, Pinterest) |

### Data Collection Process

1. **User Data Collection:** Direct collection from participants (e.g., questionnaires, EHR).
   Aggregation from public posts.
2. **Social Media Data Collection:** Searching phrases like "I was diagnosed with [condition]" and annotating relevant posts.

## Data Exploration & Preprocessing

### Domain Knowledge

Understanding relevant concepts (e.g., mental disorders) is essential for analyzing social media data effectively.

### Symptoms of Depression

- Has lost interest in doing things they normally enjoy.
- Seems to be feeling down or hopeless.
- Has slower speech and movements or is more fidgety and restless than usual.
- Feels tired or does not have much energy.
- Is overeating or has lost their appetite.
- Is sleeping more than usual or is not able to sleep.
- Has trouble concentrating.

### Feature Extraction

Using tools like CountVectorizer or LIWC for analyzing text:

- Extract word counts and patterns.
- Identify linguistic markers such as pronouns, sentiment words, and negative/positive expressions.

## Predictive Models

The predictive modeling process involves applying NLP techniques with supervised learning to classify or predict outcomes based on social media data.

### Workflow

1. Input Data: Collect and preprocess raw social media data.
2. Feature Extraction: Use tools like CountVectorizer to transform text into numerical features. Analyze word frequency, positive/negative sentiment, and other linguistic features.
3. Supervised Machine Learning: Train models using labeled data to classify posts or predict mental health outcomes. Common algorithms include Decision Trees, Random Forests, and Logistic Regression.
4. Output Prediction: Generate predictions, such as whether a user is likely experiencing depression.

## Model Evaluation

The model's performance is assessed using two key metrics:

1. **Accuracy:** Measures the proportion of correctly predicted outcomes compared to the total predictions. It indicates the overall correctness of the model.

2. **ROC Curve (Receiver Operating Characteristic):**

   - A graphical representation of the model's performance across different classification thresholds.
   - It plots the **True Positive Rate (Sensitivity)** against the **False Positive Rate (1-Specificity)**.
   - The Area Under the Curve (AUC) quantifies the model's ability to distinguish between classes, with a higher AUC indicating better performance.

By combining accuracy and the ROC curve, we can evaluate both the model's precision and its robustness in classifying users with or without mental health conditions.

- Depression prediction accuracy: ~72.38%.
- Feature reduction improves model performance by removing conflicting variables.
- Time-based comparisons may yield better results for specific models.

## Future Work

Develop AI systems that:

- Analyze user behavior and emotions through social media posts.
- Predict mental health issues like depression or anxiety.
- Offer support and connect users to medical professionals or resources.
