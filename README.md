# 🏗️ MOB-IA - Système de Qualification de Leads par IA

Système hybride de qualification automatique de leads pour l'auto-construction en Normandie.

## 🎯 Fonctionnalités

- **Scoring automatique** des leads avec IA (Ollama + Llama 3.1)
- **Qualification intelligente** : HOT (≥75/100), WARM (50-74), COLD (<50)
- **Emails personnalisés** automatiques via Brevo
- **0€/mois** de coûts récurrents

## 🚀 Démarrage du Système

### Prérequis
- Python 3.9+
- Ollama installé avec Llama 3.1
- Compte Brevo (gratuit)
- Compte ngrok (gratuit)

### Terminal 1 : API Python
```bash
cd ~/mob-ia-hybrid
source venv/bin/activate
python api_direct.py
```

Vous devriez voir :
```
🤖 Ollama : ✅
API MOB-IA
* Running on http://192.168.1.39:5001
```

### Terminal 2 : Ngrok
```bash
ngrok http 5001
```

**Important** : Copiez l'URL ngrok affichée (ex: `https://xxxxx.ngrok-free.dev`)

### Mise à jour de l'URL (si ngrok a changé)
```bash
cd ~/MehdiBatExpert
nano index.html
```

Cherchez avec `Ctrl + W` → tapez `fetch`

Remplacez l'URL par la nouvelle URL ngrok :
```javascript
const response = await fetch('https://NOUVELLE-URL.ngrok-free.dev/webhook/lead', {
```

Sauvegardez et poussez :
```bash
git add index.html
git commit -m "Update ngrok URL"
git push
```

## 🧪 Tests

### Test local
```bash
cd ~/mob-ia-hybrid
open formulaire_test.html
```

### Test production
Visitez : https://mehdibatexpert.github.io/MehdiBatExpert/

## 📊 Algorithme de Scoring

Le système évalue chaque lead sur 100 points :

- **Budget** (30 pts) : >200k€ = 30pts, 150-200k€ = 25pts, etc.
- **Terrain** (25 pts) : Acquis = 25pts, Promesse = 15pts, Recherche = 5pts
- **Délai** (20 pts) : <6 mois = 20pts, 6-12 mois = 15pts, >12 mois = 5pts
- **Localisation** (15 pts) : Normandie (76,27,14,50,61) = 15pts, Hors région = 5pts
- **Projet défini** (10 pts) : Précis = 10pts, Vague = 5pts

### Catégories

- 🔥 **HOT** (≥75/100) : Lead qualifié, appel immédiat
- 🟠 **WARM** (50-74/100) : Lead à nurture
- 🔵 **COLD** (<50/100) : Ressources gratuites uniquement

## 📁 Structure
```
mob-ia-hybrid/
├── api_direct.py          # API Flask principale
├── config.py              # Configuration Brevo
├── mob_ia_hybrid.py       # Logique de scoring IA
├── formulaire_test.html   # Formulaire de test
└── venv/                  # Environnement Python

MehdiBatExpert/
└── index.html             # Landing page avec formulaire
```

## 🔧 Commandes Utiles

### Vérifier Ollama
```bash
ollama list
```

### Test API manuel
```bash
curl -X POST http://localhost:5001/webhook/lead \
  -H "Content-Type: application/json" \
  -d '{
    "prenom": "Test",
    "email": "test@example.com",
    "budget": "180000",
    "terrain": "acquis",
    "delai": "4 mois"
  }'
```

### Vérifier la clé Brevo
```bash
echo $BREVO_API_KEY
```

## 🔐 Configuration

### Clé API Brevo
Configurée dans `~/.zshrc` :
```bash
export BREVO_API_KEY="xkeysib-..."
```

### Email expéditeur
`mehdi@avantispartner.fr` (validé dans Brevo)

## ⚠️ Troubleshooting

### L'API ne démarre pas
```bash
cd ~/mob-ia-hybrid
source venv/bin/activate
pip install --break-system-packages -r requirements.txt
```

### Ollama ne répond pas
```bash
ollama serve
```

### Erreur CORS
Vérifiez que `flask-cors` est installé dans `api_direct.py`

### Emails non reçus
1. Vérifiez que la clé Brevo est configurée
2. Vérifiez que l'email expéditeur est validé dans Brevo
3. Consultez les logs dans le Terminal de l'API

## 🚧 Prochaines Améliorations

- [ ] URL ngrok fixe ou VPS
- [ ] Dashboard de suivi des leads
- [ ] Séquences email automatiques
- [ ] Enrichissement du scoring (téléphone, projet détaillé)
- [ ] Intégration CRM

## 📞 Contact

**Mehdi Derradji - MOB-IA**  
Auto-construction écologique en Normandie  
https://mob-ia.fr

---

*Système développé avec Claude (Anthropic)*## Hi there 👋

<!--
**MehdiBatExpert/MehdiBatExpert** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
