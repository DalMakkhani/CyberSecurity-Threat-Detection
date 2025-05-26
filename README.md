# 🚨 Real-Time Cybersecurity Threat Detection using Hadoop + Spark + TabNet

This project implements a real-time cybersecurity intrusion detection system that leverages Wireshark for packet capture, Apache Hadoop for distributed data storage, Apache Spark for scalable preprocessing, and a TabNet deep learning model for accurate attack classification.

---

📁 realtime-threat-detection/
'''bash
├── datasets/
│   ├── combined_dataset.csv          # Combined and final dataset (CSE-CIC-IDS2018, 1000 samples per attack)
│   └── preprocessed_dataset.csv      # Preprocessed data used for model training (from Preprocessing.ipynb)
│
├── source_code/
│   ├── Preprocessing.ipynb           # Spark-based preprocessing and feature engineering
│   └── Model_Training.ipynb          # TabNet model training and evaluation notebook
│
├── README.md                         # Project documentation
└── requirements.txt                  # Python dependencies
'''
---

## 💡 System Overview

The system performs the following steps in real time:

1. **Live Packet Capture**: Network packets are captured via Wireshark and exported in `.pcap` format using tshark or other automation scripts.
2. **Data Ingestion to HDFS**: These packet files are automatically ingested into HDFS (Hadoop Distributed File System), ensuring fault tolerance and horizontal scalability.
3. **Spark-Based Preprocessing**: Apache Spark processes and transforms the raw network packet data into a structured format using feature engineering techniques defined in `Preprocessing.ipynb`.
4. **Attack Classification**: The processed data is passed through a pre-trained TabNet model that classifies whether the packet is benign or a type of attack.

---

## 🧠 Attack Types Trained On

The model is trained on a balanced subset of the [SCE-CIC-IDS2018](https://www.unb.ca/cic/datasets/ids-2018.html) dataset with **1000 samples each** from the following attack types:

- Brute Force - SSH
- Brute Force - Web
- DoS (Denial of Service)
- DDoS (Distributed Denial of Service)
- Botnet Activity
- Infiltration
- PortScan
- SQL Injection
- XSS (Cross-Site Scripting)
- Heartbleed
- Benign (Normal) Traffic

Each category is carefully curated and combined to ensure a fair and accurate training environment.

---

## ⚙️ Why Hadoop & Spark?

- **Apache Hadoop**: Offers distributed, fault-tolerant storage through HDFS, making it ideal for handling high-volume packet data ingested from Wireshark.
- **Apache Spark**: Provides in-memory processing and horizontal scalability. Its integration with Hadoop allows real-time transformation of raw pcap-derived data before classification.

Together, they enable a **high-throughput, low-latency pipeline** for network threat detection in real-time scenarios.

---

## 🚀 How It Works

1. Wireshark captures live packets.
2. Packet files are written to a shared folder synced with HDFS.
3. A daemon script automatically ingests new `.pcap` or converted CSV files into HDFS.
4. Apache Spark processes new data batches using the preprocessing pipeline.
5. The processed features are streamed into the trained TabNet model (saved in `Model_Training.ipynb`).
6. The system outputs the prediction for each data point as **Benign** or specific **Attack Type**.

---

## 🛠️ Getting Started

1. **Clone this repo:**

   ```bash
   git clone https://github.com/yourusername/realtime-threat-detection.git
   cd realtime-threat-detection
2. **Install dependencies:**

   '''bash
   pip install -r requirements.txt

3. **Run preprocessing on sample data:**
   Open source_code/Preprocessing.ipynb and run all cells.

4.**Train or load model:**
   Execute Model_Training.ipynb to train or load the TabNet model.

**Stream real-time data from Wireshark into HDFS** (daemon script expected here, based on your future implementation).
