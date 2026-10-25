# NLP-driven anomaly detection and alerting in BGL system logs
- **Module:** COS 802
- **Topic 14:** Anomaly Detection in Industrial IoT Sensor Networks
- **Student:** Shreya Bharat (u19031786)

This project aims to convert system anomaly log lines into window-level anomaly alerts that can then read as natural-langauge alerts. 

## Research questions
- **RQ1:** Does parser-free representation match or outperform Drain-template representations for semi-supervised and unsupervised anomaly detection?
- **RQ2:** How do training methods (semi-supervised and unsupervised) and data splitting techniques (chronological vs random) affect detection performance over the seven-month log? 
- **RQ3:** Can window-level log anomalies be translated into interpretable natural-language alerts that correctly identify the root-cause anomaly in the message?

To answer these research questions, seven representations were compared: four template-based (Drain3 template counts, TF-IDF over lemmatised template words, fastText, MiniLM sentence embeddings of templates) and three parser-free (TF-IDF over lemmatised masked-message words, character n-gram TF-IDF, and MiniLM embeddings of regex-masked messages).

Both tokenisation and lemmatisation were applied as preprocessing techniques to both pipelines. Each representation was scored using isolation forest, an autoencoder, and PCA, and were trained using a 70/15/15 train/validation/test split, both unsupervised and semi-supervised. 

## Setup guide
```bash
git clone https://github.com/ShreyaB143/COS802-Project
cd cos802-project
python3.11 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
```

## Data
BGL comes from Loghub (Zhu et al., ISSRE 2023), [Zenodo record 8196385](https://zenodo.org/records/8196385), CC BY 4.0. The original source is Oliner & Stearley (DSN 2007). BGL is an open dataset of logs collected from a BlueGene/L supercomputer system at Lawrence Livermore National Labs (LLNL) in Livermore, California, with 131,072 processors and 32,768GB memory. The first field of each line is `-` for a non-alert message and an alert category (e.g. `KERNDTLB`) for an alert.

```bash
mkdir -p data/raw
curl -L --fail --retry 3 -o data/raw/BGL.zip "https://zenodo.org/records/8196385/files/BGL.zip?download=1"
unzip -o data/raw/BGL.zip -d data/raw
wc -l data/raw/BGL.log  # expect 4747963
shasum -a 256 data/raw/BGL.log  
```

## Pipeline
xxx

## Reproducibility
xxx

## Repository layout
xxx

## Citation
+ Adam J. Oliner, Jon Stearley. [What Supercomputers Say: A Study of Five System Logs](http://ieeexplore.ieee.org/document/4273008/), in Proc. of IEEE/IFIP International Conference on Dependable Systems and Networks (DSN), 2007.
+ Jieming Zhu, Shilin He, Pinjia He, Jinyang Liu, Michael R. Lyu. [Loghub: A Large Collection of System Log Datasets for AI-driven Log Analytics](https://arxiv.org/abs/2008.06448). IEEE International Symposium on Software Reliability Engineering (ISSRE), 2023.