# 🌤️ Lyra_Météo_Observée

> Génération automatique de bulletins météo localisés à partir d'observations réelles, en Python ou via LangChain.  
> Ce projet démontre un usage raisonné de l’IA pour transformer des données d’observation météorologique en bulletins lisibles et contextualisés, sans aucune fonction de prévision.

---

## 🧭 Objectifs

- Utiliser les observations de WeatherAPI pour générer un bulletin météo localisé.
- Produire un texte en français clair, structuré et professionnel via GPT-3.5.
- Respecter une éthique : **ne pas faire de prévision**, commenter uniquement l’instant observé.
- Démontrer deux approches : une en Python pur, l’autre en LangChain.

---

## 📁 Contenu du dossier `code/`

| Fichier | Description |
|--------|-------------|
| `No_LangChain.ipynb` | Pipeline complet en Python pur (requests + OpenAI) incluant l’envoi d’email via MailJet. |
| `Using_LangChain.ipynb` | Pipeline avec LangChain (`PromptTemplate`, `ChatOpenAI`, `LLMChain`) jusqu’à la génération du message. |

---

## 🔗 Dépendances

```bash
pip install openai requests python-dotenv langchain langchain-community
pip install mailjet-rest  # Pour l'envoi de mail (optionnel)
```

---

## 🔐 Configuration attendue

Créer un fichier `ENV/env.txt` contenant :

```
OPENAI_API_KEY=sk-...
WEATHER_API_KEY=...
MJ_APIKEY_PUBLIC=...
MJ_APIKEY_PRIVATE=...
MJ_FROM_EMAIL=votre@email.com
```

Les variables sont automatiquement chargées dans les notebooks via :

```python
from dotenv import load_dotenv
load_dotenv(dotenv_path="ENV/env.txt")
```

---

## 🧠 Prompt utilisé (version LangChain)

```text
Rédige un bulletin pour Lieu : {location}, Date et heure : {time} avec {temp}°C, vent {wind} km/h, précipitations {precip} mm, couverture nuageuse {cloud} %, indice UV : {uv} UV.
Important : commenter seulement le temps observé mais ne parles pas de ce qui est prévu. Ne précises pas si des précipitations sont attendues. Ajoute un conseil si nécessaire.
```

---

## 🧪 Tests de cohérence

Des **tests par forçage de variables** ont été réalisés pour valider le comportement contextuel du système.  
Exemples :

- `temp = 40` : génération d’un avertissement chaleur.
- `temp = -4`, `wind = 40` : conseil de se couvrir.
- `uv = 0.1` : absence de conseil UV.
- `precip = 0`, `cloud = 0` : pas de prévision générée grâce au prompt contraint.

---

## ✨ Exemple de sortie

```text
Bulletin météo pour Avignon, le 5 août 2025 à 11h06 :

Actuellement, il fait 27.2°C à Avignon avec un vent soufflant à 11.9 km/h. Le ciel est dégagé avec une couverture nuageuse de 0 %. L'indice UV est de 5.2 UV.

Conseil : Avec un indice UV élevé, il est recommandé de bien se protéger du soleil en utilisant de la crème solaire et en portant un chapeau.
```

---

## 📬 Envoi par MailJet (optionnel)

L’email est généré dans `No_LangChain.ipynb` et envoyé à une adresse Gmail personnelle pour test.

- Fonctionne avec les API MailJet.
- L’adresse d’expédition doit être validée dans l’interface.
- L’email peut initialement arriver en SPAM (Gmail) — il suffit de le marquer comme sûr.

---

## 🌍 Portabilité et usage futur

- Intégrable dans Make, Zapier, ou cron local
- Compatible TTS (voix, podcast météo)
- Peut être couplé à un enregistrement Markdown ou .txt

---

## 👤 Auteur

Projet développé par Jérôme Frasson  
GitHub : [Jerome-X1](https://github.com/Jerome-X1)

---