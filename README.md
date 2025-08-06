# XDetect_PLC-Transformer-based-Detection-of-Malicious-PLC-Code


| Tool                     | Purpose                         |
| ------------------------ | ------------------------------- |
| HuggingFace Transformers | Model & tokenization            |
| Datasets                 | Data loading/splitting          |
| PyTorch                  | Deep learning backend           |
| wandb                    | Experiment tracking             |
| xmltodict                | XML to string conversion        |
| CodeBERT                 | Pretrained transformer for code |

Here's a complete **Markdown-style explanation** of your project `XDetect_PLC`, which detects malicious programmable logic controller (PLC) ladder diagrams using transformer-based models like CodeBERT.

---

# 🛡️ XDetect\_PLC: Transformer-based Detection of Malicious PLC Code

## 📌 Project Summary

`XDetect_PLC` is a deep learning-based security system designed to detect **malicious modifications in PLC ladder diagrams**. By leveraging transformer models like **CodeBERT**, it distinguishes between **legitimate** and **malicious** XML representations of industrial control logic.

The goal is to enhance cybersecurity in industrial systems by identifying cyber-attacks that tamper with PLC code.

---

## 🗂️ Dataset

The project uses the open-source [PLC-LD Dataset](https://github.com/UniboSecurityResearch/PLC-LD-dataset) which contains:

* **Legitimate samples**: Stored in `PLC-LD-dataset/legitimate`
* **Malicious samples**: Corresponding malicious versions in `PLC-LD-dataset/malicious`

Each sample is an **XML file** representing ladder logic. Matching filenames are used to pair legitimate and malicious code snippets.

---

## 🧱 Project Structure

### 1. **Configuration**

A `Config` class is defined with all parameters like model name, batch size, learning rate, file paths, etc. Example:

```python
model_name: microsoft/codebert-base
train_batch_size: 16
eval_batch_size: 32
epochs: 100
```

### 2. **Environment Setup**

* Clones the dataset from GitHub
* Installs required packages like `transformers`, `datasets`, `optuna`, `wandb`, etc.

### 3. **Data Loading**

Each `.xml` file is converted to a string using `xmltodict`. For each legitimate file, a corresponding malicious file (with the same name prefix) is loaded to form a **binary classification dataset**.

### 4. **Preprocessing**

* Tokenization with `AutoTokenizer` from HuggingFace (CodeBERT tokenizer)
* Truncation and padding to max length (512 tokens)
* Creation of HuggingFace `Dataset` objects

### 5. **Training Setup**

* Uses HuggingFace `Trainer` API
* Evaluation metrics: **Accuracy** and **F1 Score**
* Uses `wandb` for live monitoring of experiments
* Supports gradient accumulation, FP16 training, weight decay, and checkpointing

### 6. **Model**

* `AutoModelForSequenceClassification` with `num_labels=2` (legit/malicious)
* Fine-tunes `codebert-base` on PLC code data

### 7. **Evaluation & Export**

* Evaluates model on validation set
* Saves model and tokenizer to disk

---

## 📈 Metrics

<img width="1053" height="98" alt="Screenshot 2025-08-06 171825" src="https://github.com/user-attachments/assets/6fe8ab2d-f87a-4780-aaa2-f27898d37f63" />
<img width="655" height="110" alt="Screenshot 2025-08-06 174218" src="https://github.com/user-attachments/assets/6ed821c6-74f6-4a6d-a13e-235181e803b6" />


0-legitimate


1-malicious


---

## 💻 Technologies Used

| Tool                     | Purpose                         |
| ------------------------ | ------------------------------- |
| HuggingFace Transformers | Model & tokenization            |
| Datasets                 | Data loading/splitting          |
| PyTorch                  | Deep learning backend           |
| wandb                    | Experiment tracking             |
| xmltodict                | XML to string conversion        |
| CodeBERT                 | Pretrained transformer for code |

---

## 📦 Output

* Fine-tuned model saved to: `model_output/`
* Zip of model for download: `model_output.zip`

---

## ✅ How to Run

1. Clone the repo and install dependencies:

   ```bash
   !git clone https://github.com/UniboSecurityResearch/PLC-LD-dataset
   !pip install transformers datasets accelerate torch xmltodict evaluate peft optuna wandb scikit-learn
   ```

