# Music Recommendation System

## 📌 Project Overview

This project implements a robust Music Recommendation Engine using **Python** and **Turi Create**. The system is designed to analyze user listening history and generate song suggestions using two distinct paradigms:

1. **Popularity-Based Filtering:** Solves the "Cold Start" problem by recommending universally popular songs to new users.
2. **Item-Similarity Collaborative Filtering:** Provides personalized recommendations by finding correlations between songs based on user listening patterns.

The project also includes a performance evaluation module to compare the precision and recall of both models.

## 📂 Dataset

The system relies on the `song_data.sframe` dataset. The data is processed using Turi Create's SFrame and contains the following features:

* **user_id**: Unique identifier for the user.
* **song_id**: Unique identifier for the song.
* **listen_count**: Frequency of user interaction with the song.
* **title**: Song title.
* **artist**: Artist name.

## 🛠 Technologies Used

* **Language:** Python 3.8+
* **Core Library:** [Turi Create](https://github.com/apple/turicreate) (for scalable machine learning and SFrame manipulation)
* **Environment:** Jupyter Notebook

## ⚙️ Installation & Setup

To run this project, you must have a Python environment capable of running Turi Create (supports macOS and Linux best, or WSL on Windows).

1. **Clone the repository:**
```bash
git clone https://github.com/your-username/music-recommender.git
cd music-recommender

```


2. **Create a Virtual Environment (Recommended):**
```bash
# Turi Create requires specific python versions
conda create -n turienv python=3.8
conda activate turienv

```


3. **Install Dependencies:**
```bash
pip install turicreate jupyter

```


4. **Launch the Notebook:**
```bash
jupyter notebook "Song recommender.ipynb"

```



## 🚀 Methodology

The notebook performs the following steps:

### 1. Data Preprocessing

* Loads the SFrame data.
* Splits the dataset into Training (80%) and Testing (20%) sets to ensure valid model evaluation.

### 2. Popularity Model (Baseline)

This model calculates the most frequently listened-to tracks across the entire user base.

* **Use Case:** Default recommendations for new users with no history.
* **Example Output:** *Sehr kosmisch (Harmonia), Undo (Björk)*.

### 3. Personalized Model (Item Similarity)

This model computes the similarity between items based on users who liked both items (typically using Jaccard or Cosine similarity).

* **Use Case:** Tailored suggestions for existing users.
* **Feature:** Can also query specific songs to find "Similar Items" (e.g., inputting "With Or Without You - U2" returns other U2 tracks or similar genre hits).

## 📊 Model Evaluation

The project utilizes `tc.recommender.util.compare_models` to benchmark performance on the test set.

* **Metrics:** Precision and Recall at specific cutoffs.
* **Comparison:** The notebook generates a summary table comparing the Popularity Model vs. the Personalized Model to visualize the improvement in recommendation quality for specific users.

## 📝 Usage Example

```python
import turicreate as tc

# Load data
train_data, test_data = song_data.random_split(.8, seed=0)

# Create a Personalized Model
personalized_model = tc.item_similarity_recommender.create(
    train_data,
    user_id='user_id',
    item_id='song'
)

# Make a recommendation for a specific user
recommendations = personalized_model.recommend(users=[users[0]])
print(recommendations)

```

**Author:** BAIHICH Mohamed
