# 🧬 Minia Genome Assembly Analysis

> **Bioinformatica** > *Assemblaggio di genomi tramite De Bruijn Graph: studio del sequenziamento, Bloom Filter e analisi dell'assemblatore Minia*

![Status](https://img.shields.io/badge/Status-Completed-success)
![Language](https://img.shields.io/badge/Language-C%2B%2B%20%2F%20GATB-blue)
![Focus](https://img.shields.io/badge/Focus-Bioinformatics%20%26%20Algorithms-green)

## 📄 Abstract
Questo progetto affronta il problema dell'assemblaggio genomico *de novo* analizzando l'efficienza degli approcci basati su **De Bruijn Graph (DBG)** e strutture dati probabilistiche. In particolare, è stato studiato l'assemblatore **Minia**, che utilizza i **Bloom Filter** per ridurre drasticamente il consumo di memoria (fino al 95% in meno rispetto agli approcci classici), mantenendo un'elevata accuratezza.

Il lavoro include un'analisi teorica degli algoritmi, lo studio del codice sorgente (basato su libreria GATB) e una validazione sperimentale su dataset reali di *Escherichia coli*.

## 🎯 Obiettivi
* Analizzare le sfide computazionali del sequenziamento NGS (Next Generation Sequencing).
* Studiare l'impatto dei **Bloom Filter** e la gestione dei **Falsi Positivi Critici** nell'assemblaggio.
* Validare le prestazioni di Minia in termini di consumo di memoria (RAM) e accuratezza biologica.

## 🛠️ Tecnologie e Strumenti
* **Assemblatore:** [Minia](https://github.com/GATB/minia) (basato su GATB Core).
* **Piattaforma di Testing:** Galaxy Europe.
* **Validazione:** QUAST (Quality Assessment Tool for Genome Assemblies).
* **Visualizzazione:** Icarus Viewer.

## 🧪 Disegno Sperimentale

### 1. Dataset
* **Organismo:** *Escherichia coli* (Genoma di riferimento: `REL606`).
* **Source:** NCBI SRA (Accession: `SRR2584866`).
* **Tipo:** Illumina Paired-End.
* **Dimensione:** 586.2 MB.

### 2. Preprocessing
Le reads *Forward* e *Reverse* sono state concatenate in un unico file FASTQ per massimizzare il pool di k-mer disponibili per la costruzione del grafo, bypassando i limiti di scaffolding dell'ambiente di test.

### 3. Parametri di Minia
| Parametro | Valore | Descrizione |
|-----------|--------|-------------|
| **K-mer size** | `31` | Compromesso tra specificità e gestione delle ripetizioni. |
| **Min Abundance** | `3` | Filtro per rimuovere k-mer spuri dovuti a errori di sequenziamento. |

## 📊 Risultati Principali

### Performance Computazionali
L'assemblaggio è stato completato con risorse minime, dimostrando l'efficacia dell'approccio probabilistico:
* **Tempo:** ~1 minuto (Wall Clock).
* **Memoria (Peak RAM):** 4.5 GB (incluso overhead ambiente Galaxy; algoritmo puro < 500MB).
* **CPU:** Utilizzo efficiente di 2 core.

### Validazione Biologica (QUAST)
Il confronto con il genoma di riferimento ha evidenziato un'alta fedeltà di ricostruzione:
* **Genome Fraction:** **90.06%** (Alto grado di completezza).
* **Misassemblies:** **2** (Errori strutturali quasi assenti).
* **Duplication Ratio:** **1.004** (Nessuna ridondanza artificiale).
* **N50:** 7,274 bp.

> **Nota:** La frammentazione dei contigs (osservata su Icarus) è attribuibile alla presenza di regioni ripetute che eccedono la lunghezza del k-mer (31) e alla mancanza di scaffolding avanzato dovuta alla concatenazione delle reads.

## 📂 Struttura della Repository
```text
├── docs/               # Documentazione e Presentazione 
├── results/            # Report di output (QUAST, metriche Galaxy)
├── images/             # Screenshot (Icarus, Galaxy workflow)
└── README.md           # Questo file
