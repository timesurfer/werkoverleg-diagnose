# Werkoverleg Diagnose - GitHub + Obsidian Integratie

## GitHub gebruiken met Obsidian

Er zijn drie gangbare manieren om GitHub te koppelen aan Obsidian:

---

### 1. Obsidian Git Plugin (aanbevolen)

De community plugin **Obsidian Git** maakt het mogelijk om je vault direct vanuit Obsidian te synchroniseren met GitHub.

**Installatie:**

1. Open Obsidian > Instellingen > Community plugins > Bladeren
2. Zoek naar **"Obsidian Git"** en installeer
3. Schakel de plugin in

**Eerste keer instellen:**

1. Maak een repository aan op GitHub (bijv. `werkoverleg-diagnose`)
2. Open een terminal in je Obsidian vault-map:
   ```bash
   cd /pad/naar/je/vault
   git init
   git remote add origin https://github.com/GEBRUIKER/werkoverleg-diagnose.git
   git add .
   git commit -m "Eerste commit"
   git push -u origin main
   ```
3. Herstart Obsidian

**Dagelijks gebruik:**

- De plugin maakt automatisch commits en pusht op een instelbaar interval (bijv. elke 10 minuten)
- Handmatig: gebruik `Ctrl+P` > "Obsidian Git: Commit and push"
- Pull: `Ctrl+P` > "Obsidian Git: Pull"

**Aanbevolen instellingen:**

| Instelling | Waarde |
|---|---|
| Auto pull on startup | Aan |
| Auto commit interval | 10 minuten |
| Auto push after commit | Aan |

---

### 2. Handmatig met Git via de terminal

Als je geen plugin wilt gebruiken, kun je Git direct gebruiken:

```bash
# Navigeer naar je vault
cd /pad/naar/je/vault

# Wijzigingen opslaan
git add .
git commit -m "Notities bijgewerkt"
git push
```

Tip: maak een `.gitignore` aan in je vault:

```
.obsidian/workspace.json
.obsidian/workspace-mobile.json
.trash/
```

Dit voorkomt dat persoonlijke layout-instellingen conflicten veroorzaken.

---

### 3. GitHub Desktop

Voor wie liever een grafische interface gebruikt:

1. Installeer [GitHub Desktop](https://desktop.github.com)
2. Clone je repository of voeg je bestaande vault-map toe
3. Gebruik de interface om te committen en pushen

---

## Tips voor samenwerking

- **Branching:** Gebruik branches als meerdere mensen aan dezelfde vault werken
- **Conflicten:** Markdown-bestanden zijn tekst, dus merge-conflicten zijn makkelijk op te lossen
- **Privé houden:** Maak de repository **private** als het gevoelige informatie bevat
- **.gitignore:** Sluit bestanden uit die per gebruiker verschillen (zie voorbeeld hierboven)

## Veelvoorkomende problemen

| Probleem | Oplossing |
|---|---|
| Merge-conflicten | Open het bestand, kies de juiste versie, commit opnieuw |
| Grote bestanden (afbeeldingen) | Gebruik Git LFS of bewaar afbeeldingen extern |
| Plugin-sync conflicten | Voeg `.obsidian/workspace.json` toe aan `.gitignore` |
| Authenticatie mislukt | Gebruik een Personal Access Token (PAT) in plaats van wachtwoord |

## Authenticatie instellen (PAT)

GitHub accepteert geen wachtwoorden meer. Gebruik een **Personal Access Token**:

1. Ga naar GitHub > Settings > Developer settings > Personal access tokens > Tokens (classic)
2. Genereer een nieuw token met `repo`-rechten
3. Gebruik dit token als wachtwoord bij het pushen
