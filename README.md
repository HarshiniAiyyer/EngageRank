# EngageRank: User Engagement Analysis and Graph-Based Recommendation System

This repository contains a complete workflow for analyzing user engagement data and building a graph-driven recommendation system. The project includes two Jupyter notebooks, associated datasets, and a written guide. The goal is to understand user behavior, define novel engagement metrics, and generate improved content recommendations using graph methods and a hybrid LightFM model.

## Repository Structure

```
data_growth_trial_task_submission/
│
├── data/
│   ├── data_task_related_entries_of_users.xlsx
│   ├── data_task_users.xlsx
│   ├── udf1.xlsx
│   ├── rdf1.xlsx
│
├── notebooks/
│   ├── Data_Analysis_+_Novel_Metrics.ipynb
│   ├── Recommendation_System.ipynb
│
└── Guide to the Jupyter Notebooks.docx
```

# Datasets

All datasets are stored in the `data/` directory.

## 1. data_task_related_entries_of_users.xlsx
Contains event logs of user interactions with content. The variables typically include:
- user_id: Unique identifier for a user
- post_id: Unique identifier for a post or content item
- event_type: Type of interaction such as view, click, like, or similar engagement signals
- event_timestamp: Recorded timestamp of the interaction
- session_id: Identifier for the user's session
- platform: Specifies the device or platform if present
- additional interaction attributes depending on schema

This dataset is used primarily for engagement analysis and construction of interaction matrices.

## 2. data_task_users.xlsx
Contains metadata about users. The variables include:
- user_id: Primary key linking with interaction logs
- user_account_properties such as signup information, status flags, or demographic attributes (depending on availability)
- internal tags or traits used for segmentation

This dataset is used for joining with engagement records and deriving user-level metrics.

## 3. udf1.xlsx
Represents a user data frame in simplified form for recommendation modeling. The variables typically include:
- user_id
- item_id or post_id
- interaction_value, representing binary or weighted interactions

This dataset is used in building the interaction matrix for the LightFM model.

## 4. rdf1.xlsx
Represents a relational data frame used for graph construction. The variables include:
- source: A node in the graph (user, post, or entity)
- target: A node connected to the source
- relationship_type: Defines the semantic meaning of the edge (for example, user_viewed_post, post_has_entity)
- edge_weight, if applicable

This dataset is used to create a multi-layer graph for graph-based recommendations.

# Notebook Documentation

## Notebook 1: Data_Analysis_+_Novel_Metrics.ipynb

### Purpose
To process raw datasets, explore user and content behavior, build derived features, and compute novel engagement metrics.

### Key Sections
1. Library Imports  
   Imports core libraries such as pandas, numpy, matplotlib, seaborn, networkx, neo4j, and pyvis.

2. Data Loading  
   Loads all datasets and converts them into cleaned data frames suitable for analysis.

3. Data Processing  
   Includes handling of missing values, normalization of timestamps, creation of categorical indicators, and merging of datasets on keys such as user_id and post_id.

4. SQLite Connection and Querying  
   Moves data into a SQLite environment to run SQL queries for aggregations and metrics.

5. Novel Metrics  
   The notebook computes several derived metrics, including:  
   - engagement_depth: Measures intensity of user interaction across posts  
   - engagement_diversity: Measures variety in the types of interactions  
   - recency_weighted_engagement: Measures engagement adjusted for time decay  
   - user_activity_index: Summary of user involvement across sessions  
   - post_performance_score: Aggregates interaction counts and quality  
   Names and formulas may vary depending on the final implementation inside the notebook.

6. Visualizations  
   Uses matplotlib and seaborn to produce distributions, frequency charts, engagement plots, and other exploratory visualizations.

### Output  
This notebook generates cleaned datasets, aggregated tables, and intermediate metrics required for recommendation modeling.

# Notebook 2: Recommendation_System.ipynb

### Purpose
To build a recommendation system using graph-based methods and the LightFM hybrid model.

### Key Sections
1. Library Installations  
   Installs ipython-sql, sqlalchemy, prettytable, networkx, and LightFM.

2. Data Upload  
   Prompts for uploading rdf1.csv and udf1.csv in Colab. These originate from the rdf1.xlsx and udf1.xlsx datasets.

3. Graph Construction  
   Uses networkx to construct:
   - User to post edges
   - Post to entity edges
   - Additional edges defined by rdf1.xlsx

   Typical graph structures include bipartite and tripartite configurations.

4. Graph-Based Recommendations  
   Implements methods such as:
   - Jaccard similarity between nodes  
   - Personalized PageRank  
   - Neighborhood-based ranking  

   Outputs top recommended posts for a sample of users.

5. LightFM Hybrid Model  
   Builds a LightFM model using collaborative filtering with optional content features.

   Steps include:
   - Creating user and item mappings
   - Building the interaction matrix from udf1  
   - Fitting the LightFM model  
   - Generating top-n recommendations  

6. Evaluation  
   Uses standard metrics such as:  
   - precision_at_k  
   - recall_at_k  
   - rank-based evaluation  
   Depending on the dataset and configuration.

### Output  
Recommended items for users, graph structures, visualization of graph components, and LightFM evaluation metrics.

# Guide Document

The file titled "Guide to the Jupyter Notebooks.docx" describes:
- How notebooks are organized
- The purpose and workflow of each notebook
- Required dependencies
- Instructions for running the analysis from start to finish

It serves as a written companion to the notebooks.

# How to Reproduce the Project

1. Clone the repository or download the project folder.
2. Install all required Python dependencies in a virtual environment.
3. Open the notebooks in Jupyter or Google Colab.
4. For the recommendation notebook, upload the udf1 and rdf1 files when prompted.
5. Run the cells sequentially.

A Python 3.8 or higher environment is recommended.

