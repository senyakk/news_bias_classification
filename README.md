# US News Bias Classification: Encoder vs Decoder Models

This project focuses on analyzing and fine-tuning large language models (LLMs) to classify political bias in text. Bias is classified as 'left', 'right', or 'center'. The project includes various experiments with models such as RoBERTa and Gemma, along with prompt engineering techniques to improve classification performance.

This project uses both fine-tuning and prompt engineering methods for political bias classification in news articles. The experiments involve:

- Baseline and Fine-Tuning of two LLMS: RoBERTa (encoder-only) and Gemma-2b (decoder-only).
- Prompt Engineering to guide model outputs for bias detection.
- LoRA (Low-Rank Adaptation) as a PEFT technique to improve model efficiency during fine-tuning (by almost 30%).

The best accuracy results for the selected dataset were 63%-64% with similar performance for the models, especially in the LoRA condition. Essentially, Gemma-2b can perform on par with RoBERTa for a given task, native for encoders.

<div align="center">
  <img width="560" alt="Screenshot 2025-06-20 at 10 46 10" src="https://github.com/user-attachments/assets/1bfbd579-2a42-4dec-9d56-59388a3e2d2e" />
</div>

---

## Data

The dataset was obtained from [Allsides](https://github.com/irgroup/Qbias/blob/main/allsides_balanced_news_headlines-texts.csv), which is the aggregator
of news coverage that has experts tagging the ideological affiliation of the viewpoints. The dataset contains 21,747 U.S. news samples. For bias rating, there are 47.2% samples tagged as left, 33.2% tagged as right, and 19.6% as center.

---

## Structure

```
.
└── data/: Folder with the datasets.
│ ├── raw/: Folder with the raw data.
│ └── processed/: Folder with the processed data.
│
├── src/: Folder with the code.
│ └── data/: Folder with the data pipeline scripts.
│    ├── `csv_finder.py`: Utility script to locate specific CSV files.
│    ├── `data_loader.py`: Script for loading and preparing data.
│    ├── `data_preprocessing.py`: Script for data cleaning and preprocessing.
│    └── 'main.py': script to preprocess data
│
├── notebooks/: Folder with the Jupyter notebooks.
│ └── Data analysis/: Notebook for model comparison.
│   └── `model_comparison.ipynb`
│
│ ├── Gemma/: Notebooks for Gemma model experiments.
│ │ ├── `gemma_baseline.ipynb`: Baseline model notebook.
│ │ ├── `gemma_lora.ipynb`: LoRA fine-tuning for Gemma.
│ │ ├── `gemma-fine-tuned.ipynb`: Fully fine-tuned Gemma model.
│ │ ├── `prompt_eng_no_center.ipynb`: Prompt engineering no center.
│ │ └── `prompt_eng_version_2.ipynb`: Includes 2 versions of prompt engineering.
│ │ 
│ └── Roberta/: Notebooks for RoBERTa model experiments.
│   ├── `Roberta_lora.ipynb`: LoRA fine-tuning for RoBERTa.
│   ├── `Roberta-baseline.ipynb`: Baseline model notebook.
│   └── `Roberta-fine-tuned.ipynb`: Fully fine-tuned RoBERTa model.
│
├── results/: Folder with model performance results.
│ ├── `gemma_fine_tune.csv`: Results for fine-tuning Gemma.
│ ├── `gemma_lora.csv`: Results for LoRA fine-tuning on Gemma.
│ ├── `political_bias_results_prompt_1.json`: JSON results for prompt engineering (first version).
│ ├── `political_bias_results_prompt_2.json`: JSON results for prompt engineering (second version).
│ ├── `prompt_no_center.json`: JSON results for prompt engineering without center bias.
│ ├── `roberta_fine_tuning.csv`: Results for fine-tuning RoBERTa.
│ └── `roberta_lora.csv`: Results for LoRA fine-tuning on RoBERTa.
│
├── README.md
│
├── requirements.txt: File with the list of dependencies.
```

---

## Getting Started

Prerequisites:

Python 3.8 or higher

Required packages listed in ```requirements.txt```

Install dependencies with:
```bash
pip install -r requirements.txt
```


---

## Running the Code

### 1. Data Preprocessing
To preprocess the raw data, run the following script:

```bash
python src/data/main.py
```
This will clean and process the raw dataset, saving the output to `data/processed/clean_data.csv`.

### 2. Model Training and Experiments
All model training and experiments are organized in Jupyter notebooks. Open the relevant notebook in the `Notebooks/` directory and run the cells interactively:

- For Gemma experiments: use notebooks in `Notebooks/Gemma/`
- For RoBERTa experiments: use notebooks in `Notebooks/Roberta/`
- For model comparison and analysis: use `Notebooks/Data analysis/model_comparison.ipynb`

Each notebook contains step-by-step code for training, fine-tuning, prompt engineering, and evaluation.

### 3. Viewing Results
Results from model runs are saved in the `results/` directory as CSV or JSON files. You can open these files directly or use the analysis notebook to visualize and compare model performance.

---

# Limitations

 The systems tailored to classifying the political bias might suffer greatly from the lack of reliability or scalability. In particular, our system limitation is the spatially limited source of the data – the political environment of the USA. In the context of USA's politics, the distinction "left" or "right" might take the form of e.g. "pro-democrat" or "pro-republican", which loses scalability for other political contexts, outside of this environment.
