# Project Repository

This repository contains code for creating clusters for relations, experimenting with different clustering approaches and embedding models. The process involves multiple iterations of clustering and classification, utilizing various models to achieve optimal results. It includes several tasks ranging from clustering relationships from private Jio news summaries datasets to classifying relations from the public CoNLL04 dataset. The repository is organized into several folders to structure the tasks, utilities, input data, output results, etc. Below is a detailed description of each folder and file in the repository.

## Repository Structure

### 1. `src` Folder
Contains six Python files for various tasks. Each task focuses on clustering or classification using relation embeddings.

- **`set1_data_clustering (iteration1).py`**  
  - **Description:** Performs clustering of relations of Set 1 Jio news summaries dataset. Assigns clusters to relations by calculating the cosine similarity between the relation embedding and the mean embedding of each pre-defined cluster.
  - **Input:** Pre-defined clusters and Set 1 Jio news summaries data (from the `data/` folder).  
  - **Output:** Cluster assignments for Set 1 relations and updated relation clusters are saved (in the `output/` folder).  
  - **Model:** Uses the `paraphrase-MiniLM-L6-v2` embedding model from the `transformers` library.

- **`gpt4_relations_clustering (iteration2).py`**  
  - **Description:** Assigns top 5 clusters to GPT-generated relations based on cosine similarities between relation embeddings and the mean embeddings of the original clusters.  
  - **Input:** Updated cluster results from iteration 1 and GPT-generated relations from the `data/` folder.  
  - **Output:** Cluster assignments for GPT-generated relations are saved in five separate Excel files in the `output/` folder for results corresponding different embedding models.  
  - **Evaluation:** The cluster assignments for all five models are evaluated using functions from `evaluation_utils.py`.  
  - **Models:** Embedding models are specified in `models.json` (in the `configs/` folder).

- **`set2_mean_clustering (iteration3).py`**  
  - **Description:** Clusters relations of Set 2 Jio news summaries dataset. Assigns top 5 clusters to relations by calculating the top 5 cosine similarities between the relation embedding and the mean embedding of each base cluster.
  - **Input:** Updated clusters from iteration 2 (using the `all-mpnet-base-v2` model) and Set 1 Jio news summaries data from the `data/` folder.  
  - **Output:** Cluster assignments for Set 2 relations and updated clusters are saved in the `output/` folder.  
  - **Model:** Uses `all-mpnet-base-v2` from `transformers`.  
  - **Evaluation:** Evaluation is performed using functions from `evaluation_utils.py`.

- **`set2_median_clustering (iteration3).py`**  
  - **Description:** Similar to the previous script but uses the median of embeddings instead of the mean for assigning clusters.  
  - **Input/Output/Model:** Same as above, except with median clustering.

- **`set2_classification (iteration4).py`**  
  - **Description:** Uses a Random Forest classifier to predict the top 5 clusters for relations of Set 2 Jio news summaries dataset based on embeddings. The model is trained on embeddings from previous iterations.  
  - **Input:** Updated clusters from iteration 2  (using the `all-mpnet-base-v2` model) and Set 1 Jio news summaries data from the `data/` folder.  
  - **Output:** Cluster assignments for Set 2 relations and updated clusters are saved in the `output/` folder.  
  - **Model:** Uses `all-mpnet-base-v2` embedding model from `transformers`.
  - **Evaluation:** Evaluation is performed using functions from `evaluation_utils.py`.

- **`conll04_classification.py`**  
  - **Description:** Applies the classification method to relations from the CoNLL04 dataset, training a Random Forest classifier to predict classes for relations.  
  - **Input/Output:** Similar to other classification tasks but uses the CoNLL04 dataset.  
  - **Model:** Random Forest Classifier and embeddings from `all-mpnet-base-v2`.

### 2. `scripts` Folder
Contains a preprocessing script for Set 2 data:

- **`set2_data_preprocessing.py`**  
  - **Description:** Preprocesses Set 2 data to extract common samples from ground truth and LLM-predicted datasets.  
  - **Output:** The common samples are saved in the `output/` folder.  
  - **Usage:** This file is required for the Set 2 relations clustering and classification tasks.

### 3. `utils` Folder
Houses utility functions used across the tasks:

- **`helpers.py`**  
  - Contains utility functions for loading embedding models, computing cosine similarities, and saving data.

- **`data_processing_utils.py`**  
  - Functions for loading, processing, and extracting data from various datasets.

- **`embedding_utils.py`**  
  - Functions for generating embeddings for clusters and relations using different models.

- **`cluster_assignment_utils.py`**  
  - Functions for assigning clusters to relations using either mean or median embedding-based clustering.

- **`evaluation_utils.py`**  
  - Contains functions for evaluating the cluster assignments using various evaluation metrics.

- **`model_utils.py`**  
  - Functions for training and predicting using the Random Forest classifier for cluster classification tasks.

### 4. `configs` Folder
Contains configuration files for the models used:

- **`models.json`**  
  - Lists the embedding models used in `gpt4_relations_clustering (iteration2).py` and their corresponding output files.

### 5. `data` Folder
Stores input data files required for various tasks such as Set 1 relations, GPT-generated relations, Set 2 data, and pre-defined cluster files.

### 6. `data/output` Folder
Stores all output files, including updated clusters, cluster assignments, and evaluation results. Files generated by each task in the `src/` folder are saved here in Excel format.

### 7. `requirements.txt` 
Lists all the dependencies required to run the project. The key libraries used include:

- `transformers` (for embedding models like `paraphrase-MiniLM-L6-v2`, `all-mpnet-base-v2`)
- `flair`
- `torch`
- `scikit-learn` (for Random Forest classifier)
- `pandas` (for handling Excel data)
- `numpy` (for numerical computations)
- `datasets` (for loading CoNLL04 dataset)

Install them using the following command:

```bash
pip install -r requirements.txt
