# Intelligente Untertitel: Adaptive Untertiteldarstellung

Dieses Repository enthält die Implementation einer Pipeline zur adaptiven Anzeige von Untertiteln basierend auf Audio- und Textverständlichkeit. Das System analysiert Audio und Text, um Untertitel nur dann einzublenden, wenn sie für das Verständnis wirklich notwendig sind.

## Features

- Dynamische Anpassung der Untertiteldarstellung
- Analyse von 5 Kernmerkmalen:
  - Audiokomplexität (basierend auf Whisper ASR)
  - Wortkomplexität (CEFR-Level basiert)
  - Satzkomplexität (ModernBERT-basierte Analyse)
  - Wortwichtigkeit (Kontext-basierte Analyse)
  - Wortvorkommen (Häufigkeitsanalyse)
- Zweisprachige Untertitel-Unterstützung (EN/DE)
- Neuronales Netz zur Entscheidungsfindung

## Modell-Performance

- F2-Score: 0.5812
- Balanced Accuracy: 0.8459
- ROC-AUC: 0.8994
- Recall (Klasse 1): 0.89
- Präzision (Klasse 1): 0.24

## Installation

1. Repository klonen:
`git clone https://github.com/dieBaerigenBerchtesgadener/IntelligentSubtitles`

2. Abhängigkeiten installieren:
`pip install -r requirements.txt`


## Verwendung

Das Hauptnotebook `main.ipynb` enthält die komplette Pipeline-Implementation und das Training. Das trainierte Modell ist in `model.pth` gespeichert.

### Pipeline-Struktur

1. Eingabe: Audio + Original-Untertitel
2. Feature-Extraktion:
   - Audio-Transkription (Whisper)
   - CEFR-Level-Analyse
   - Satz-/Wortanalyse (ModernBERT)
   - Häufigkeitsanalyse
3. Übersetzung (OPUS-MT)
4. Neuronales Netz zur Entscheidungsfindung

## Modellarchitektur

- Eingabe: 5 Features
- Hidden Layer:
  - Layer 1: 64 Neuronen (ReLU)
  - Layer 2: 128 Neuronen (ReLU)
  - Layer 3: 64 Neuronen (ReLU)
- Batch-Normalisierung und Dropout in allen Hidden Layers
- Ausgabe: Sigmoid-Layer mit Bias

## Anforderungen

- Python 3.8+
- PyTorch
- Transformers
- Whisper
- ModernBERT
- OPUS-MT
- SimAlign

## Limitationen

- Trainingsset basiert auf einem einzelnen Sprachverständnisniveau
- Hoher Recall (0.89) aber niedrige Präzision (0.24) für relevante Untertitel
- Rechenintensive Pipeline

## Zukünftige Verbesserungen

- Erweiterung des Trainingsdatensatzes
- Integration detaillierterer Audioinformationen
- Optimierung der Pipeline-Effizienz
- Verbesserung der Präzision für relevante Untertitel

