# Einfaches Sprachmodell mit PyTorch

## 1. Einleitung

In diesem Beispiel zeigen wir, wie man mit PyTorch ein einfaches Sprachmodell erstellt und trainiert. Das Modell wird auf Zeichenebene trainiert und verwendet ein LSTM, um die nächste Zeichenwahrscheinlichkeit vorherzusagen. Dies ist ein stark vereinfachtes Beispiel, um die Grundprinzipien der Sprachmodellierung zu demonstrieren.

## 2. Datenaufbereitung

Wir verwenden einen kleinen Beispielsatz und tokenisieren ihn auf Zeichenebene. Jedes Zeichen wird in einen Index umgewandelt, der als Eingabe für das Modell dient.

```python
import torch

# Beispielsatz
text = "hallo pytorch"

# Erstelle ein Vokabular (einzigartige Zeichen)
chars = sorted(list(set(text)))
vocab_size = len(chars)

# Mapping von Zeichen zu Index und umgekehrt
char2idx = {ch: idx for idx, ch in enumerate(chars)}
idx2char = {idx: ch for idx, ch in enumerate(chars)}

# Text in Indizes umwandeln
text_indices = [char2idx[ch] for ch in text]

# Eingabe- und Zielsequenzen erstellen
# Ziel ist das nächste Zeichen im Text
input_seq = torch.tensor(text_indices[:-1]).unsqueeze(0)  # Batch-Größe 1
target_seq = torch.tensor(text_indices[1:]).unsqueeze(0)
```

## 3. Modell-Definition

Wir definieren ein einfaches LSTM-basiertes Sprachmodell mit einem Embedding-Layer, einem LSTM und einem Linearlayer zur Vorhersage des nächsten Zeichens.

```python
import torch.nn as nn

class SimpleLSTMLanguageModel(nn.Module):
    def __init__(self, vocab_size, embedding_dim, hidden_dim):
        super(SimpleLSTMLanguageModel, self).__init__()
        self.embedding = nn.Embedding(vocab_size, embedding_dim)
        self.lstm = nn.LSTM(embedding_dim, hidden_dim, batch_first=True)
        self.fc = nn.Linear(hidden_dim, vocab_size)
        
    def forward(self, x, hidden=None):
        x = self.embedding(x)
        output, hidden = self.lstm(x, hidden)
        logits = self.fc(output)
        return logits, hidden

# Hyperparameter
embedding_dim = 10
hidden_dim = 20

model = SimpleLSTMLanguageModel(vocab_size, embedding_dim, hidden_dim)
```

## 4. Training-Loop

Wir definieren den Loss (CrossEntropyLoss) und den Optimizer (Adam) und führen mehrere Trainingsschritte durch.

```python
import torch.optim as optim

criterion = nn.CrossEntropyLoss()
optimizer = optim.Adam(model.parameters(), lr=0.01)

num_epochs = 100

for epoch in range(num_epochs):
    model.train()
    optimizer.zero_grad()
    
    # Vorwärtsdurchlauf
    logits, _ = model(input_seq)
    
    # CrossEntropyLoss erwartet Eingabe der Form (Batch*Seq_len, Klassen)
    loss = criterion(logits.view(-1, vocab_size), target_seq.view(-1))
    
    # Rückwärtsdurchlauf
    loss.backward()
    optimizer.step()
    
    if (epoch + 1) % 20 == 0:
        print(f"Epoch {epoch+1}/{num_epochs}, Loss: {loss.item():.4f}")
```

## 5. Text-Generierung

Nach dem Training können wir mit dem Modell neuen Text generieren, indem wir das vorhergesagte nächste Zeichen wieder als Eingabe verwenden.

```python
model.eval()

# Startzeichen für die Generierung
start_char = 'h'
input_idx = torch.tensor([[char2idx[start_char]]])

hidden = None
generated_text = start_char

# Generiere 20 Zeichen
for _ in range(20):
    logits, hidden = model(input_idx, hidden)
    probs = torch.softmax(logits[:, -1, :], dim=-1)
    next_idx = torch.multinomial(probs, num_samples=1).item()
    next_char = idx2char[next_idx]
    generated_text += next_char
    
    input_idx = torch.tensor([[next_idx]])

print("Generierter Text:")
print(generated_text)
```

## Glossar

- **Tokenisierung**  
  Zerlegung von Text in kleinere Einheiten, sogenannte Tokens (z.B. Wörter oder Zeichen), die vom Modell verarbeitet werden können.

- **Vokabular**  
  Die Menge aller Tokens, die das Modell kennt und verarbeiten kann. Im Beispiel sind dies die einzigartigen Zeichen des Textes.

- **Embedding**  
  Eine numerische Repräsentation von Tokens in einem kontinuierlichen Vektorraum, die es dem Modell ermöglicht, semantische Beziehungen zu lernen.

- **LSTM (Long Short-Term Memory)**  
  Eine spezielle Architektur von rekurrenten neuronalen Netzen (RNNs), die entwickelt wurde, um langfristige Abhängigkeiten in Sequenzen zu erfassen und das Problem des Verschwindens von Gradienten zu vermeiden.

- **Batch-Größe**  
  Die Anzahl der Sequenzen, die das Modell gleichzeitig verarbeitet. Im Beispiel ist die Batch-Größe 1.

- **Loss / CrossEntropyLoss**  
  Ein Maß für die Abweichung zwischen der Vorhersage des Modells und dem tatsächlichen Zielwert. CrossEntropyLoss wird häufig für Klassifikationsprobleme verwendet.

- **Optimizer (Adam)**  
  Ein Algorithmus zur Anpassung der Modellparameter basierend auf dem berechneten Loss, um das Modell zu trainieren und die Fehler zu minimieren.

- **Forward-Pass / Rückwärtsdurchlauf**  
  Forward-Pass bezeichnet die Berechnung der Ausgaben des Modells aus den Eingaben. Rückwärtsdurchlauf (Backpropagation) ist der Prozess, bei dem die Gradienten berechnet und die Modellgewichte angepasst werden.

- **Softmax**  
  Eine Funktion, die Rohwerte (Logits) in Wahrscheinlichkeiten umwandelt, sodass die Summe der Ausgabewahrscheinlichkeiten 1 beträgt.

- **Logits**  
  Die Rohwerte, die das Modell vor der Wahrscheinlichkeitsumwandlung (z.B. durch Softmax) ausgibt.

- **Hidden State**  
  Der interne Zustand eines LSTM, der Informationen über vorherige Eingaben speichert und somit Kontextinformationen für die Verarbeitung von Sequenzen bereitstellt.
