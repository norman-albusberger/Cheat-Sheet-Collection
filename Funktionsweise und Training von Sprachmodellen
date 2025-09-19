# Funktionsweise und Training von Sprachmodellen

## 1. Einführung in Sprachmodelle
- Sprachmodelle sind KI-Systeme, die natürliche Sprache verstehen und erzeugen können.
- Sie basieren auf statistischen und neuronalen Methoden, um Muster in Textdaten zu erkennen.

## 2. Architektur von Sprachmodellen
- Moderne Sprachmodelle verwenden neuronale Netze, insbesondere Transformer-Architekturen.
- Transformer bestehen aus Encoder- und Decoder-Schichten, die Aufmerksamkeit (Attention) nutzen, um Kontext zu erfassen.
- Die Bausteine eines Transformers umfassen Multi-Head Self-Attention, die es dem Modell ermöglicht, verschiedene Teile des Eingabetexts gleichzeitig zu betrachten, Feedforward Layer zur nichtlinearen Verarbeitung der Informationen, Residual Connections, die den Informationsfluss verbessern und das Training stabilisieren, Layer Normalization zur Normalisierung der Zwischenergebnisse und Positional Encoding, das die Reihenfolge der Tokens im Text repräsentiert.
- Große Sprachmodelle (LLMs) nutzen meist Decoder-Only-Architekturen, bei denen die Ausgabe Token für Token berechnet wird.

## 3. Trainingsprozess
- Das Training erfolgt auf großen Textkorpora, um Wahrscheinlichkeiten für Wortfolgen zu lernen.
- Es wird zwischen überwachten, unüberwachten und selbstüberwachten Lernmethoden unterschieden.
- Optimierungsalgorithmen wie Adam werden verwendet, um die Modellparameter anzupassen.

## 4. Reinforcement Learning und Feinabstimmung
- Reinforcement Learning from Human Feedback (RLHF) ist eine Methode, bei der menschliches Feedback genutzt wird, um das Modell zu trainieren und nützlichere sowie sicherere Antworten zu erzeugen.
- Dabei werden Belohnungssignale aus menschlichen Bewertungen verwendet, um das Modellverhalten zu optimieren.
- Zusätzlich wird Instruction Tuning eingesetzt, um das Verständnis und die Ausführung von spezifischen Aufgaben durch das Modell zu verbessern.

# Nach dem Grundtraining kann das Modell auf spezifische Aufgaben oder Domänen angepasst werden.
- Dies verbessert die Leistung in spezialisierten Anwendungen.

## 5. Herausforderungen und Grenzen
- Sprachmodelle können Vorurteile aus Trainingsdaten übernehmen.
- Sie benötigen große Rechenressourcen und können Fehler oder Halluzinationen erzeugen.

## 6. Anwendungsbereiche
- Maschinelle Übersetzung, Textgenerierung, Chatbots, Sentiment-Analyse und mehr.

## 7. Speicherung von Wissen im Modell
- Das Wissen wird nicht explizit gespeichert, sondern verteilt in Milliarden von Parametern wie Gewichten und Biases.
- Fakten sind nicht in einer Tabelle abgelegt, sondern als Wahrscheinlichkeitsmuster im Parameterraum kodiert.
- Das Modell hat durch Vorwärtspropagation Zugriff auf diese Muster und kann so auf gespeichertes Wissen zugreifen.

## 8. Vergleich: Menschliches vs. künstliches neuronales Netz
Biologische neuronale Netze bestehen aus Neuronen, die durch Synapsen verbunden sind. Diese Synapsen übertragen Signale mittels Neurotransmittern, chemischen Botenstoffen, die die Kommunikation zwischen Neuronen ermöglichen. Die Plastizität des Gehirns erlaubt es, Verbindungen zu verstärken oder abzuschwächen, was Lernen und Anpassung ermöglicht.

Künstliche neuronale Netze (KNNs) bestehen aus Knoten (Neuronen), die durch gewichtete Verbindungen verbunden sind. Diese Gewichte werden durch Aktivierungsfunktionen verarbeitet, die bestimmen, ob und wie stark ein Signal weitergegeben wird.

Zentrale Unterschiede sind:

- **Komplexität**: Das menschliche Gehirn umfasst Milliarden von Neuronen, während KNNs typischerweise Millionen bis Billionen von Parametern besitzen.
- **Signalübertragung**: Biologische Netze nutzen elektrochemische Signale, während KNNs mathematische Matrixmultiplikationen durchführen.
- **Lernmechanismen**: Biologische Netze lernen durch Hebb’sches Lernen und Neuroplastizität, während KNNs auf Backpropagation und Gradientenabstieg basieren.
- **Energieeffizienz**: Das Gehirn arbeitet mit etwa 20 Watt, während GPUs und Tensor Cores für große Modelle oft im Megawatt-Bereich Energie benötigen.
- **Flexibilität**: Das Gehirn kann multimodal, adaptiv und selbstregulierend lernen; KNNs sind meist domänenspezifisch und weniger flexibel.
- **Robustheit**: Biologische Netze sind fehlertolerant und können mit Störungen umgehen, KNNs sind oft sensitiv gegenüber adversarialen Beispielen.

Abschließend lässt sich sagen, dass künstliche neuronale Netze zwar von biologischen inspiriert sind, jedoch stark vereinfachte mathematische Modelle darstellen, die kein Bewusstsein besitzen.

## 9. Wort- und Subwort-Tokenisierung
Tokenisierung ist der Prozess, Rohtext in Einheiten (Tokens) zu zerlegen, die das Modell verarbeiten kann. 

Bei der Wort-Tokenisierung werden klassische Ansätze wie Whitespace-Splitting oder linguistisch motivierte Segmentierung verwendet, um den Text in einzelne Wörter zu unterteilen. Diese Methode stößt jedoch auf Probleme wie Out-of-Vocabulary (OOV)-Wörter, Schwierigkeiten mit der Morphologie und Herausforderungen bei Sprachen mit komplexer Wortbildung.

Subwort-Tokenisierung wurde eingeführt, um diese Probleme zu umgehen. Verfahren wie Byte-Pair Encoding (BPE), WordPiece und SentencePiece zerlegen Wörter in kleinere Einheiten, sogenannte Subwörter. BPE funktioniert dabei durch iteratives Zusammenführen häufiger Zeichenfolgen zu neuen Tokens, bis eine vorgegebene Zielvokabulargröße erreicht ist.

Die Vorteile der Subwort-Tokenisierung liegen in der Reduktion von OOV-Problemen, der Kompaktheit des Vokabulars und einer besseren Generalisierung bei unbekannten Wörtern. Ein Beispiel hierfür ist das Wort „Autobahnausfahrt“, das in die Subwörter [„Auto“, „bahn“, „aus“, „fahrt“] zerlegt werden kann.

Tokenisierer enthalten typischerweise 30.000 bis 100.000 Subwörter, die im Vokabular als IDs gespeichert sind.
