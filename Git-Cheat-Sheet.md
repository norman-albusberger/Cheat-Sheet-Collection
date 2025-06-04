 🗂 Git Cheat Sheet
______

## 🚀 Grundbefehle
```bash
git init         # Neues Repository initialisieren
git clone URL    # Repository klonen
git status       # Status anzeigen
git add .        # Änderungen zum Commit vormerken
git commit -m "Nachricht"   # Commit ausführen
git push         # Änderungen hochladen
git pull         # Änderungen holen und mergen


⸻

🧪 Branching & Merging

git branch               # Liste aller Branches
git checkout -b feature  # Neuen Branch erstellen & wechseln
git merge feature        # Branch in aktuellen mergen
git rebase main          # Rebase auf main (statt merge)
git stash                # Änderungen zwischenspeichern
git stash pop            # Änderungen wiederherstellen


⸻

🔍 Historie & Rückgängig

git log --oneline        # Kompakte History
git diff                 # Unterschiede anzeigen
git checkout <commit>    # Alten Stand ansehen

Commit zurücksetzen

git reset --soft HEAD~1     # Letzten Commit behalten (Stage)
git reset --mixed HEAD~1    # Letzten Commit rückgängig (unstaged)
git reset --hard HEAD~1     # Letzten Commit komplett verwerfen


⸻

📄 .gitignore

Beispiel .gitignore für JetBrains IDE:

# JetBrains IDE Ordner ignorieren
.idea/

Nachträglich ignorieren:

git rm -r --cached .idea
git commit -m "Remove .idea from repo"


⸻

📐 Best Practices
	•	Nutze .gitignore von Anfang an
	•	Schreibe kleine, sinnvolle Commits mit sprechenden Nachrichten
	•	Schütze den main-Branch (z. B. keine Force-Pushes)
	•	Nutze rebase statt merge für eine lineare History
	•	Benenne Branches konsistent (z. B. feature/login, bugfix/image-loader)
	•	Verwende git stash, bevor du den Kontext wechselst
	•	Richte pre-commit Hooks ein (z. B. für Linter oder Tests)

⸻

🔍 Tipps & Spezialfunktionen
	•	.gitattributes zur Steuerung von Zeilenendungen und Merge-Strategien
	•	git bisect zur schrittweisen Fehlersuche
	•	git reflog um gelöschte oder verlorene Commits wiederzufinden
	•	git cherry-pick um gezielt Commits zwischen Branches zu übertragen

⸻

📦 Nützliche Tools
	•	CLI: tig (Terminal Git-UI)
	•	Editor: GitLens (VS Code)
	•	GUI: GitKraken, Sourcetree
	•	CI/CD: GitHub Actions, GitLab CI

⸻

📚 Quellen
	•	https://git-scm.com/docs
	•	https://github.com/github/gitignore
	•	https://www.atlassian.com/git/tutorials
