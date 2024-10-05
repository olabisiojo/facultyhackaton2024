
---

## **1. Course Overview and Expectations**

### **Overview:**
This course will introduce you to the interdisciplinary field of bioinformatics, combining biology, computer science, and information technology to analyze and interpret biological data.

### **Expectations:**
- **Active Participation:** Engage in lectures, discussions, and hands-on labs.
- **Assignments:** Complete programming assignments and projects.
- **Prerequisites:** No prior coding experience required, but a willingness to learn Python and Bash is essential.
- **Tools:** Python programming language, Bash terminal, and various bioinformatics tools and databases.

---

## **2. Setting Up Your Environment**

Before diving into bioinformatics topics, it's crucial to set up your programming environment.

### **A. Installing Python**

**Step 1: Download Python**
- Visit the [official Python website](https://www.python.org/downloads/) and download the latest version of Python (preferably Python 3.8 or higher).

**Step 2: Install Python**
- **Windows:**
  - Run the installer and ensure you check the box **"Add Python to PATH"**.
  - Click **"Install Now"**.
- **macOS:**
  - Use the installer from the Python website or install via Homebrew:
    ```bash
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    brew install python
    ```
- **Linux:**
  - Most distributions come with Python pre-installed. To check, open the terminal and type:
    ```bash
    python3 --version
    ```
  - If not installed, use your package manager:
    ```bash
    sudo apt-get update
    sudo apt-get install python3
    ```

**Step 3: Verify Installation**
Open your terminal or command prompt and type:
```bash
python3 --version
```
You should see the Python version number.

### **B. Installing a Python IDE**

An Integrated Development Environment (IDE) helps write and debug code efficiently.

**Recommended IDE: Visual Studio Code (VS Code)**
- **Download:** [Visual Studio Code](https://code.visualstudio.com/)
- **Installation:**
  - Follow the installation prompts for your operating system.
- **Extensions:**
  - Open VS Code.
  - Go to the Extensions view (`Ctrl+Shift+X` or `Cmd+Shift+X`).
  - Search and install:
    - **Python** by Microsoft
    - **Code Runner** (optional, for running code snippets)

### **C. Installing Necessary Python Packages**

Bioinformatics often relies on specialized Python libraries.

**Using `pip` to Install Packages:**
Open your terminal or command prompt and execute:

```bash
pip install biopython pandas numpy matplotlib
```

- **Biopython:** Tools for biological computation.
- **Pandas:** Data manipulation and analysis.
- **NumPy:** Numerical operations.
- **Matplotlib:** Data visualization.

### **D. Introduction to Bash**

**What is Bash?**
Bash is a Unix shell and command language used for interacting with the operating system.

**Basic Commands:**
- **Navigating Directories:**
  ```bash
  pwd          # Print working directory
  ls           # List files and directories
  cd directory # Change directory
  ```
- **File Operations:**
  ```bash
  mkdir folder       # Create a new directory
  touch file.txt     # Create a new file
  cp source dest     # Copy files
  mv source dest     # Move or rename files
  rm file.txt        # Remove a file
  ```
- **Viewing File Contents:**
  ```bash
  cat file.txt       # Display file content
  less file.txt      # View file content page by page
  ```

**Running Python Scripts in Bash:**
```bash
python3 script.py
```

**Note for Windows Users:**
Consider using **Git Bash** or **Windows Subsystem for Linux (WSL)** for a Unix-like terminal experience.

---

## **3. Introduction to Bioinformatics**

### **What is Bioinformatics?**
Bioinformatics involves the use of computational tools to manage, analyze, and interpret biological data. It plays a crucial role in genomics, proteomics, drug discovery, and more.

### **Applications:**
- **Genome Sequencing:** Analyzing DNA sequences.
- **Protein Structure Prediction:** Determining protein shapes.
- **Phylogenetics:** Studying evolutionary relationships.
- **Drug Discovery:** Identifying potential drug targets.

### **Example:**
Analyzing the sequence of the human BRCA1 gene to identify mutations associated with breast cancer.

---

## **4. Introduction to Biological Databases**

### **Overview:**
Biological databases store a vast amount of biological data, including DNA/RNA sequences, protein structures, and more.

### **Key Databases:**
- **NCBI (National Center for Biotechnology Information):** Provides access to a variety of databases like GenBank, PubMed, and BLAST.
- **Ensembl:** Genome browser for vertebrate genomes.
- **UniProt:** Comprehensive resource for protein sequence and annotation data.
- **PDB (Protein Data Bank):** 3D structures of proteins and nucleic acids.

### **Example:**
Accessing the gene sequence of *Homo sapiens* BRCA1 from NCBI GenBank.

---

## **5. Access to Sequence Data and Information**

### **Using Biopython to Access Sequence Data**

**Example: Fetching a DNA Sequence from NCBI**

```python
from Bio import Entrez

# Provide your email
Entrez.email = "your.email@example.com"

# Fetch the sequence for BRCA1 gene (Gene ID: 672)
handle = Entrez.efetch(db="gene", id="672", retmode="xml")
records = Entrez.read(handle)

# Extract relevant information
for record in records:
    print(record['Entrezgene_gene']['Gene-ref']['Gene-ref_locus'])
```

### **Explanation:**
- **Entrez:** A module in Biopython for accessing NCBI databases.
- **efetch:** Retrieves data from specified databases.
- **Parsing XML:** Extract and process the returned data.

### **Hands-On Exercise:**
Fetch and display the protein sequence for *Homo sapiens* hemoglobin subunit alpha (UniProt ID: P69905).

---

## **6. Pairwise Sequence Alignment**

### **Introduction:**
Pairwise sequence alignment compares two sequences to identify regions of similarity, which may indicate functional, structural, or evolutionary relationships.

### **Types:**
- **Global Alignment:** Aligns entire sequences (e.g., Needleman-Wunsch algorithm).
- **Local Alignment:** Aligns subsequences (e.g., Smith-Waterman algorithm).

### **Example: Global Alignment Using Biopython**

```python
from Bio import pairwise2
from Bio.pairwise2 import format_alignment

seq1 = "GATTACA"
seq2 = "GCATGCU"

# Perform global alignment
alignments = pairwise2.align.globalxx(seq1, seq2)

# Display the first alignment
print(format_alignment(*alignments[0]))
```

### **Explanation:**
- **pairwise2:** A Biopython module for pairwise sequence alignment.
- **globalxx:** A simple global alignment without scoring.

### **Hands-On Exercise:**
Perform a local alignment between the sequences "ACCGT" and "CCGTT" and visualize the alignment.

---

## **7. Alignment Algorithms**

### **Overview:**
Understanding the algorithms behind sequence alignment is crucial for interpreting results and troubleshooting.

### **Key Algorithms:**
- **Needleman-Wunsch:** For global alignment; uses dynamic programming.
- **Smith-Waterman:** For local alignment; more computationally intensive.
- **BLAST (Basic Local Alignment Search Tool):** Fast local alignment tool optimized for large databases.

### **Example: Comparing Needleman-Wunsch and Smith-Waterman**

```python
# Global Alignment (Needleman-Wunsch)
global_align = pairwise2.align.globalxx(seq1, seq2)
print("Global Alignment:")
print(format_alignment(*global_align[0]))

# Local Alignment (Smith-Waterman)
local_align = pairwise2.align.localxx(seq1, seq2)
print("Local Alignment:")
print(format_alignment(*local_align[0]))
```

### **Explanation:**
- **globalxx vs. localxx:** Determines whether the alignment is global or local.
- **Dynamic Programming:** Both algorithms use this technique to efficiently compute alignments.

### **Hands-On Exercise:**
Implement a simple scoring system (match = +1, mismatch = -1, gap = -2) and perform a global alignment between two sequences.

---

## **8. BLAST (Basic Local Alignment Search Tool)**

### **Overview:**
BLAST is a widely-used tool for comparing an input sequence against a database to find regions of similarity.

### **Principles of BLAST Searching:**
- **Query Sequence:** The sequence you want to search with.
- **Database:** The collection of sequences to search against.
- **E-value:** Expectation value indicating the number of hits one can expect by chance.
- **Alignment Score:** Measures the quality of the alignment.

### **Using NCBI BLAST Web Interface:**

1. **Access BLAST:**
   - Navigate to [NCBI BLAST](https://blast.ncbi.nlm.nih.gov/Blast.cgi).

2. **Choose BLAST Type:**
   - **nucleotide BLAST (blastn)** for DNA/RNA sequences.
   - **protein BLAST (blastp)** for protein sequences.

3. **Input Query:**
   - Paste your sequence in the query box.

4. **Select Database:**
   - Choose the appropriate database (e.g., `nr`, `nt`).

5. **Run BLAST:**
   - Click on **"BLAST"** to execute the search.

6. **Interpret Results:**
   - Review alignments, E-values, and scores.

### **Hands-On Exercise:**
Perform a BLAST search using the sequence of *E. coli* lacZ gene and identify similar sequences in other organisms.

---

## **9. Principles of BLAST Searching**

### **Understanding BLAST Outputs:**

- **Alignment View:** Shows how your query aligns with database sequences.
- **Scores and E-values:**
  - **Score:** Higher scores indicate better alignments.
  - **E-value:** Lower E-values indicate more significant matches.
- **Identities and Positives:**
  - **Identities:** Exact matches between sequences.
  - **Positives:** Similar amino acids (for proteins).

### **Optimizing BLAST Searches:**

- **Choosing the Right Algorithm:** `blastn` for nucleotide, `blastp` for proteins, etc.
- **Adjusting Parameters:** E.g., word size, gap penalties.
- **Filtering Options:** Remove low-complexity regions to avoid false positives.

### **Example: Interpreting BLAST Output**

Review a BLAST result page and identify:
- The top hit with the lowest E-value.
- The percentage identity.
- The alignment length.

### **Hands-On Exercise:**
Modify BLAST parameters (e.g., change the database or adjust the E-value threshold) and observe how the results change.

---

## **10. Advanced Database Searching**

### **Overview:**
Beyond basic BLAST, advanced database searching involves using specialized tools and databases for specific types of analyses.

### **Advanced Tools:**
- **BLAT:** Faster than BLAST for certain applications.
- **HMMER:** Uses hidden Markov models for protein domain searches.
- **InterProScan:** Integrates multiple databases for protein classification.

### **Using HMMER to Search Protein Domains** (This only works if you have linux)

**Step 1: Install HMMER**
```bash
sudo apt-get install hmmer  # For Debian/Ubuntu
```

**Step 2: Download HMM Profiles**
- Visit the [Pfam database](http://pfam.xfam.org/) and download desired HMM profiles.

**Step 3: Perform a Search**
```bash
hmmscan --tblout output.tbl pfam_profiles.hmm protein_sequences.fasta
```

### **Explanation:**
- **hmmscan:** Searches a sequence against a database of HMM profiles.
- **Output:** `output.tbl` contains the search results.

### **Hands-On Exercise:**
Use HMMER to identify domains in a given protein sequence using the Pfam database.

---

## **11. Multiple Sequence Alignment (MSA)**

### **Overview:**
MSA aligns three or more biological sequences (DNA, RNA, or proteins) to identify conserved regions and infer evolutionary relationships.

### **Common Tools:**
- **Clustal Omega:** Fast and scalable MSA tool.
- **MAFFT:** Highly accurate and flexible.
- **MUSCLE:** Balanced speed and accuracy.

### **Performing MSA with Clustal Omega**

**Step 1: Install Clustal Omega**
```bash
sudo apt-get install clustalo  # For Debian/Ubuntu
```

**Step 2: Prepare Sequences**
Create a FASTA file (`sequences.fasta`) with your sequences:
```
>Seq1
ATGCGTA...
>Seq2
ATGCGCA...
>Seq3
ATGCGTT...
```

**Step 3: Run Clustal Omega**
```bash
clustalo -i sequences.fasta -o aligned.fasta --force
```

### **Explanation:**
- **-i:** Input file.
- **-o:** Output file.
- **--force:** Overwrites existing output.

### **Hands-On Exercise:**
Align multiple hemoglobin sequences from different species and identify conserved regions.

---

## **12. Phylogenetic Analysis**

### **Overview:**
Phylogenetic analysis studies the evolutionary relationships among various biological species or entities based on genetic information.

### **Key Concepts:**
- **Phylogenetic Trees:** Visual representations of evolutionary relationships.
- **Distance Methods:** Calculate genetic distances to infer tree topology (e.g., Neighbor-Joining).
- **Character-Based Methods:** Use specific genetic changes (e.g., Maximum Parsimony).

### **Example: Building a Phylogenetic Tree Using Biopython and Phylo**

```python
from Bio import Phylo
from Bio.Phylo.TreeConstruction import DistanceCalculator, DistanceTreeConstructor
from Bio import AlignIO

# Load the alignment
alignment = AlignIO.read("aligned.fasta", "fasta")

# Calculate the distance matrix
calculator = DistanceCalculator('identity')
distance_matrix = calculator.get_distance(alignment)

# Construct the tree using Neighbor-Joining
constructor = DistanceTreeConstructor()
tree = constructor.nj(distance_matrix)

# Display the tree
Phylo.draw(tree)
```

### **Explanation:**
- **AlignIO:** Reads sequence alignments.
- **DistanceCalculator:** Computes genetic distances.
- **DistanceTreeConstructor:** Builds the tree based on distances.

### **Hands-On Exercise:**
Construct a phylogenetic tree for a set of closely related bacterial 16S rRNA sequences.

---

## **13. CURE Project Overview**

### **What is CURE?**
CURE (Course-based Undergraduate Research Experience) integrates research projects into the curriculum, allowing students to engage in authentic research experiences.

### **CURE Components in This Course:**
- **Project Selection:** Choose a bioinformatics research question.
- **Data Collection:** Utilize biological databases and tools.
- **Analysis:** Apply computational methods to analyze data.
- **Presentation:** Share findings through reports and presentations.

### **Example CURE Projects:**
- **Genome Annotation:** Annotate genes in a newly sequenced genome.
- **Protein Structure Prediction:** Predict and validate protein structures using AlphaFold.
- **Comparative Genomics:** Compare genomes of different species to identify unique genes.

### **Hands-On Exercise:**
Form project groups and propose a bioinformatics research question to investigate during the course.

---

## **14. Introduction to Bioinformatics Programming - CURE**

### **Objective:**
Equip students with programming skills essential for bioinformatics research, focusing on Python and Bash scripting.

### **Python Programming Basics:**

**A. Variables and Data Types**
```python
# Variables
gene_length = 1500
gene_name = "BRCA1"
is_protein_coding = True

# Data Types
integer = 10
float_num = 3.14
string = "ATGCGTAC"
boolean = False
```

**B. Control Structures**
```python
# If-Else Statement
if gene_length > 1000:
    print("Long gene")
else:
    print("Short gene")

# For Loop
for base in string:
    print(base)
```

**C. Functions**
```python
def calculate_gc_content(dna_seq):
    gc_count = dna_seq.count('G') + dna_seq.count('C')
    return (gc_count / len(dna_seq)) * 100

# Usage
sequence = "ATGCGTAC"
gc_percentage = calculate_gc_content(sequence)
print(f"GC Content: {gc_percentage}%")
```

### **Bash Scripting Basics:**

**A. Creating a Simple Script**
```bash
#!/bin/bash
# script.sh

echo "Hello, Bioinformatics!"
```
- **Make Executable:**
  ```bash
  chmod +x script.sh
  ```
- **Run Script:**
  ```bash
  ./script.sh
  ```

**B. Using Variables and Loops**
```bash
#!/bin/bash
# count_bases.sh

sequence="ATGCGTAC"

for base in $(echo $sequence | fold -w1)
do
    echo $base
done
```

**C. Combining Python and Bash**
- **Running a Python Script from Bash:**
  ```bash
  #!/bin/bash
  python3 calculate_gc.py
  ```

### **Hands-On Exercise:**
Write a Python script to parse a FASTA file and calculate the GC content of each sequence. Create a Bash script to automate running this Python script on multiple FASTA files.

---

## **15. Machine Learning/Artificial Intelligence (AI) in Bioinformatics**

### **Overview:**
Machine Learning (ML) and Artificial Intelligence (AI) are transforming bioinformatics by enabling the analysis of large-scale biological data, prediction of complex biological phenomena, and automation of data-driven tasks.

### **Applications:**
- **Predicting Gene Expression:** Using ML models to predict gene expression levels.
- **Variant Calling:** Identifying genetic variants from sequencing data.
- **Protein Function Prediction:** Classifying protein functions based on sequence data.
- **Drug Discovery:** Identifying potential drug candidates using AI.

### **Example: Predicting Protein Secondary Structure Using ML**

**A. Data Preparation:**
- **Dataset:** Collect protein sequences with known secondary structures.
- **Features:** Encode amino acid sequences using one-hot encoding or physicochemical properties.
- **Labels:** Secondary structure annotations (e.g., alpha-helix, beta-sheet, coil).

**B. Building a Simple ML Model with Scikit-learn**

```python
import numpy as np
from sklearn.model_selection import train_test_split
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score

# Example data
X = np.array([[0,1,0], [1,0,1], [0,1,1], [1,1,0]])  # Feature vectors
y = np.array([0, 1, 1, 0])  # Labels

# Split data
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.25)

# Initialize and train model
clf = RandomForestClassifier()
clf.fit(X_train, y_train)

# Predict
y_pred = clf.predict(X_test)

# Evaluate
print(f"Accuracy: {accuracy_score(y_test, y_pred)}")
```

### **Explanation:**
- **RandomForestClassifier:** An ensemble ML method suitable for classification tasks.
- **Training and Testing:** Split data to evaluate model performance.
- **Accuracy:** Measures the proportion of correct predictions.

### **Hands-On Exercise:**
Use a publicly available dataset (e.g., gene expression data) to build and evaluate an ML model that predicts disease status.

---

## **16. Deep Learning in Bioinformatics - CURE**

### **Overview:**
Deep Learning (DL), a subset of ML, leverages neural networks with multiple layers to model complex patterns in large datasets, making it invaluable for bioinformatics tasks such as image analysis, sequence prediction, and more.

### **Applications:**
- **Genomic Sequence Analysis:** Predicting regulatory elements.
- **Protein Structure Prediction:** Enhancing accuracy beyond traditional methods.
- **Medical Image Analysis:** Diagnosing diseases from imaging data.

### **Example: Building a Simple Neural Network with TensorFlow/Keras**

**Step 1: Install TensorFlow**
```bash
pip install tensorflow
```

**Step 2: Import Libraries**
```python
import tensorflow as tf
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
import numpy as np
```

**Step 3: Prepare Data**
```python
# Example data: XOR problem
X = np.array([[0,0], [0,1], [1,0], [1,1]])
y = np.array([0, 1, 1, 0])
```

**Step 4: Build the Model**
```python
model = Sequential()
model.add(Dense(4, input_dim=2, activation='relu'))
model.add(Dense(1, activation='sigmoid'))
```

**Step 5: Compile and Train**
```python
model.compile(loss='binary_crossentropy', optimizer='adam', metrics=['accuracy'])
model.fit(X, y, epochs=1000, verbose=0)
```

**Step 6: Evaluate**
```python
loss, accuracy = model.evaluate(X, y)
print(f"Accuracy: {accuracy * 100:.2f}%")
```

### **Explanation:**
- **Sequential Model:** A linear stack of layers.
- **Dense Layers:** Fully connected neural network layers.
- **Activation Functions:** `relu` introduces non-linearity; `sigmoid` for binary classification.
- **Training:** The model learns to map inputs to outputs through backpropagation.

### **Hands-On Exercise:**
Build a deep learning model to classify DNA sequences as coding or non-coding regions using a suitable dataset.

---

## **17. AI in Drug Discovery - CURE**

### **Overview:**
AI accelerates drug discovery by predicting molecular interactions, optimizing drug candidates, and identifying potential therapeutic targets.

### **Applications:**
- **Virtual Screening:** Identifying potential drug molecules from large libraries.
- **De Novo Drug Design:** Designing novel drug molecules with desired properties.
- **Predicting Drug-Target Interactions:** Mapping how drugs interact with biological targets.

### **Example: Virtual Screening Using Machine Learning**

**A. Data Collection:**
- **Dataset:** Obtain a dataset of compounds with known activity against a target (e.g., ChEMBL database).

**B. Feature Extraction:**
- **Descriptors:** Calculate molecular descriptors (e.g., molecular weight, logP).
- **Fingerprints:** Generate molecular fingerprints representing chemical structures.

**C. Building a Predictive Model**

```python
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import classification_report
import pandas as pd

# Example: Load dataset
data = pd.read_csv("drug_activity.csv")
X = data.drop('active', axis=1)  # Features
y = data['active']               # Labels

# Split data
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

# Initialize and train model
clf = RandomForestClassifier(n_estimators=100)
clf.fit(X_train, y_train)

# Predict and evaluate
y_pred = clf.predict(X_test)
print(classification_report(y_test, y_pred))
```

### **Explanation:**
- **RandomForestClassifier:** Suitable for classification tasks in drug activity prediction.
- **Classification Report:** Provides precision, recall, f1-score for model evaluation.

### **Hands-On Exercise:**
Use a publicly available dataset to build an ML model that predicts the activity of compounds against a specific protein target.

---

## **18. AlphaFold - CURE**

### **Overview:**
AlphaFold, developed by DeepMind, is an AI system that predicts protein 3D structures from amino acid sequences with remarkable accuracy, revolutionizing structural biology.

### **Applications:**
- **Protein Structure Prediction:** Determining structures of proteins with unknown structures.
- **Understanding Protein Function:** Linking structure to biological function.
- **Drug Design:** Facilitating structure-based drug discovery.

### **Accessing AlphaFold Models:**
AlphaFold models are available through [AlphaFold Protein Structure Database](https://alphafold.ebi.ac.uk/).

### **Example: Using AlphaFold Predictions**

**Step 1: Access AlphaFold Database**
- Navigate to the AlphaFold website and search for a protein of interest (e.g., human hemoglobin).

**Step 2: Download the Predicted Structure**
- Download the PDB file for further analysis.

**Step 3: Visualize the Structure Using PyMOL**

**Installing PyMOL:**
- **Download:** [PyMOL](https://pymol.org/2/) (free educational version available).
- **Installation:** Follow platform-specific instructions.

**Viewing the Structure:**
```bash
# Open PyMOL
pymol

# In PyMOL, load the PDB file
File -> Open -> your_protein.pdb
```

### **Explanation:**
- **PyMOL:** A molecular visualization system used to view 3D structures.
- **Visualization:** Explore protein domains, active sites, and overall folding.

### **Hands-On Exercise:**
Download and visualize the AlphaFold-predicted structure of a protein implicated in a disease of your choice. Identify key structural features and hypothesize their functional significance.

---

## **19. ChatGPT in Bioinformatics**

### **Overview:**
ChatGPT, an AI language model developed by OpenAI, can assist in bioinformatics by providing explanations, generating code snippets, and offering insights into complex topics.

### **Applications:**
- **Coding Assistance:** Generate Python or Bash scripts for bioinformatics tasks.
- **Data Interpretation:** Explain results from analyses like BLAST or MSA.
- **Literature Review:** Summarize research papers or concepts.
- **Troubleshooting:** Help debug code or command-line issues.

### **Example: Using ChatGPT to Generate a Python Script for Parsing FASTA Files**

**Prompt to ChatGPT:**
*"Generate a Python script using Biopython to parse a FASTA file and print the sequence ID and length of each sequence."*

**Generated Script:**
```python
from Bio import SeqIO

def parse_fasta(file_path):
    for record in SeqIO.parse(file_path, "fasta"):
        seq_id = record.id
        seq_length = len(record.seq)
        print(f"Sequence ID: {seq_id}, Length: {seq_length}")

if __name__ == "__main__":
    fasta_file = "your_sequences.fasta"
    parse_fasta(fasta_file)
```

### **Explanation:**
- **SeqIO.parse:** Reads the FASTA file.
- **Record Attributes:** Access sequence ID and sequence data.
- **Functionality:** Prints each sequence's ID and length.

### **Hands-On Exercise:**
Use ChatGPT to help you write a Bash script that automates downloading multiple FASTA files from NCBI given a list of accession numbers.

---

## **Final Notes**

### **Additional Resources:**
- **Hugging Face:** You can find several AI models that you could use for your class: https://huggingface.co/models?sort=trending&search=bio
- **Biopython Documentation:** [Biopython](https://biopython.org/wiki/Documentation)
- **NCBI Tutorials:** [NCBI Education](https://www.ncbi.nlm.nih.gov/home/tutorials/)
- **GitHub Repositories:** 
	- https://github.com/liyu95/Deep_learning_examples
	- https://github.com/ossu/bioinformatics/blob/master/extras/other-resources.md
	- https://github.com/ossu/bioinformatics/blob/master/extras/free-courses.md
	- https://github.com/ossu/bioinformatics/blob/master/extras/free-books.md




# AsuramsTeam FacultyHackaton@Gateways24

This repository is for Albany State University Team of [https://sciencegateways.org/faculty-hackathon-2024](https://hackhpc.github.io/facultyhack-gateways24) with [SGX3](https://sciencegateways.org/). 

---

**Team Member:** Olabisi Ojo, PhD                                             
**Email:** [olabisi.ojo@asurams.edu](mailto:olabisi.ojo@asurams.edu)                                          
**LinkedIn:** [https://www.linkedin.com/in/olabisiojo/](https://www.linkedin.com/in/olabisiojo/)                                                            
![image](imgs/ojooo.png)
                  
**Team Mentor:** Hector Corzo.                                
**Email:**   
**LinkedIn:** 
![image](imgs/hectorc.png)

**Team Co-Mentor:** Sheryl Bradford.                                
**Email:**   
**LinkedIn:** 
![image](imgs/sherylb.png)
---
