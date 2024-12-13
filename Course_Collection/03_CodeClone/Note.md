# AI for detecting code plagiarism

The Code Clone Detector uses AI to identify similar code and detect plagiarism, even with modifications. It helps developers improve software quality and aids educators in quickly detecting student plagiarism. Currently, the Merry system is available for free trial use.

## What Are Code Clones?

Two code fragments form a clone pair if they are similar enough according to a given definition of similarity.

### Types of Clones (Syntactic Based)

- **Type 1:** Identical except for layout, white space, and comments.
- **Type 2:** Identical except for literals, identifiers, data types, layout, white space, and comments.
- **Type 3:** Similar with added, changed, or removed statements.
- **Type 4:** Same functionality but different syntax or algorithms.

## Why Detect Code Clones?

- Source code plagiarism detection.
- Code Clones can be harmful in software maintenance.
- To improve code quality by reducing code redundancy (usually occur 7-23% in software).
- Some clones can be beneficial (e.g. software product line, well-written code).
- We need to detect clones so that we can manage them.

## Code Clone Detection Process

1. **Preprocessing:** Standardizes source code format (e.g., formatting layout).
2. **Transformation:** Converts code fragments into vectors using machine learning.
3. **Match Detection:** Identifies clones based on predefined similarity criteria.
4. **Formatting:** Formats detected results for presentation.
5. **Post Processing Filtering:** Removes unnecessary data from results.
6. **Aggregation:** Combines results for user review.

## Problem Statements

- The existing techniques and tools are still facing challenges when detecting clones with several modifications (e.g., added/deleted/modified statements).
- Existing clone detection and plagiarism detection tools are difficult to use because it is command line based tool.

## Objectives

1. To create a **code clone detection tool** using machine learning techniques and study its effectiveness.
2. To enhance the user experience of code clone detection tools
   - providing code clone detection as a **web application** to users.
   - providing visualization of clone results.

## Merry: Web-Based Code Clone Detection System

### Features

- **Machine Learning Models:** Comparing between Decision Tree, Random Forest, SVM, and SVM with Sequential Minimal Optimization (SMO).
- **Metrics:**
  - **Syntactic Metrics** (e.g., number of tokens, unique identifiers).
  - **Semantic Metrics** (via code2vec).
- **BigCloneBench:** Largest and credible clone database with labeled clone pairs.
- **Web-Based Tool:**
  - User-friendly interface with GitHub integration.
  - Visual reports for better insights.

## Building the Merry Engine

### Data Collection and Preparation

- **BigCloneBench Dataset:**
  - Derived from 25,000 Java projects with true and false clone pairs labeled.
  - Includes stratified training and testing datasets for machine learning models.
- Training Set and Testing Set Splitting
  - The dataset is split into Training Data (22,663 true clone pairs) and Testing Data (4,724 true clone pairs).

### Metrics Extraction

- **Syntactic Metrics:** Analyzes structural aspects of code (e.g., tokens, operators, lines of code).
- **Semantic Metrics:** Captures behavior using code2vec, a neural model trained on 12M real-world software methods.

## Using the Merry Engine

- Processes Java projects by parsing methods and converting source code into vectors or tokens.
- Extracted metrics are processed through the trained machine learning model to detect code clones.
- Provides results via a web application with an intuitive interface, enabling users to view clone detection outcomes, visualize results, and generate detailed reports.

## Evaluation

### Accuracy

- **BigCloneBench Dataset:** Evaluated using precision, recall, and F1-score.
- **Real-World Software Projects:** Performance varied based on project size and complexity.

### User Adoption

- Compared Merry's web-based system with command-line tools like Simian in terms of:
  - **Ease of Understanding:** Clarity in setup and results.
  - **Ease of Use:** Accessibility and functionality.

## Conclusion

- **Merry Tool:** Provides an accurate, user-friendly code clone detection system with machine learning integration and GitHub support.
- **Challenges:** Current implementation supports only Java, and runtime performance of code2vec requires optimization.

## Future Work

- Expand the tool to detect clones in other languages.
- Improve the code2vec run-time.
- Create dedicated machine learning model per clone type.
- Solve the MongoDB limitation by query a part of MongoDB document at a time.
