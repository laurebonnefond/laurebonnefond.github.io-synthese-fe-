# 📊 Synthèse Radar — Fiche d'Entreprise

> Outil autonome de génération de **diagrammes de synthèse des risques** à partir d'une fiche d'entreprise (FE) en santé au travail, avec **anonymisation obligatoire** et **export Word**.

[![GitHub Pages](https://img.shields.io/badge/demo-en%20ligne-1F4E79)](https://laurebonnefond.github.io/synthese-fe/)
[![Licence](https://img.shields.io/badge/licence-MIT-green)](LICENSE)
[![SPSTI](https://img.shields.io/badge/SPSTI-23%2F87-C55A11)](https://spsti2387.fr/)

---

## 🎯 À quoi ça sert

Transformer une fiche d'entreprise (FE) en un **diagramme radar synthétique** lisible en 30 secondes par un employeur, accompagné d'une **lecture rapide rédigée** (point fort, zones à renforcer, point critique, message à l'employeur).

**Cas d'usage typiques :**
- Annexe visuelle à joindre à la FE remise à l'entreprise
- Support de restitution lors de la visite médico-professionnelle
- Document de cadrage pour la rédaction du PAPRIPACT
- Comparaison année N vs N-1 (évolution de la maîtrise des risques)

---

## ✨ Fonctionnalités

- 📤 **Upload** : `.docx` · `.pdf` · `.txt`
- 🔒 **Anonymisation obligatoire** avant tout traitement
  - Détection automatique : noms, téléphones, emails, SIRET, adresses, codes postaux
  - Édition manuelle + masquage de sélection
  - Outil « couper l'entête » (avant la section *Facteurs de risques*)
  - Case de certification RGPD obligatoire pour passer à l'étape suivante
- ✏️ **Édition libre** : 8 axes par défaut, scoring 0-4 par boutons, autocomplete sur le référentiel des 22 familles de risque
- 📊 **Radar interactif** : mise à jour en temps réel (Chart.js)
- 📄 **Export Word natif** : document `.doc` prêt à l'emploi avec radar embarqué, tableau détaillé, lecture rapide formatée
- 🖼️ **Export PNG** haute résolution (2× DPI)
- 📋 **Export JSON** pour archivage / réutilisation
- 🔌 **100% navigateur** : aucune donnée transmise à un serveur

---

## 🚀 Démo en ligne

👉 **[laurebonnefond.github.io/synthese-fe](https://laurebonnefond.github.io/synthese-fe/)**

Un bouton **« Lancer une démo »** est disponible sur la page d'accueil pour tester l'outil avec un cas anonymisé (FE Transport sous-traitance livraison) — sans avoir à uploader de fichier.

---

## 📖 Utilisation

### Workflow en 3 étapes

```
┌─────────────┐    ┌──────────────────┐    ┌─────────────────────┐
│  1. Upload  │ →  │ 2. Anonymisation │ →  │ 3. Synthèse & Export│
│   FE .docx  │    │   (obligatoire)  │    │  Word · PNG · JSON  │
└─────────────┘    └──────────────────┘    └─────────────────────┘
```

### Étape 1 — Upload
Glissez-déposez la FE ou cliquez pour parcourir. L'extraction texte se fait localement via Mammoth (`.docx`) ou PDF.js (`.pdf`).

### Étape 2 — Anonymisation
Le texte est pré-anonymisé automatiquement. Vérifiez visuellement, complétez manuellement si besoin, puis cochez la case de certification pour continuer.

> ⚠️ **Cette étape n'est jamais contournable** : le bouton « Continuer » reste désactivé tant que la certification n'est pas validée.

### Étape 3 — Édition & export
- Modifiez les axes (ajout/suppression, scoring, justifications)
- Rédigez la lecture rapide (4 paragraphes)
- Exportez en **Word** pour annexer à la FE

---

## 🏗️ Architecture & fichiers

```
synthese-fe/
├── index.html          # Application complète (HTML/CSS/JS)
├── SKILL.md            # Méthodologie de scoring et de rédaction
├── README.md           # Ce fichier
└── LICENSE             # MIT
```

**Aucune build, aucun bundler, aucune dépendance npm.** Le fichier `index.html` est autoportant : il charge ses dépendances (Chart.js, Mammoth, PDF.js) depuis le CDN Cloudflare.

---

## 🛠️ Stack technique

| Couche | Outil | Source |
|---|---|---|
| Graphique radar | Chart.js 4.4 | cdnjs.cloudflare.com |
| Extraction `.docx` | Mammoth.js 1.6 | cdnjs.cloudflare.com |
| Extraction `.pdf` | PDF.js 3.11 | cdnjs.cloudflare.com |
| Export Word | HTML → .doc (natif Microsoft Office) | aucune dépendance |
| Polices | DM Serif Display + DM Sans | Google Fonts |
| Style | CSS Custom Properties | natif |

**Compatibilité navigateurs :** Chrome / Edge / Firefox / Safari (versions des 2 dernières années).

---

## 🔒 Confidentialité & RGPD

Cet outil est conçu pour le **secret médical** et la **conformité RGPD** :

- ✅ **Aucun envoi serveur** : tout traitement se fait dans votre navigateur
- ✅ **Pas de tracking** : aucun analytics, aucun cookie
- ✅ **Anonymisation obligatoire** avant toute manipulation ultérieure
- ✅ **Hébergement statique** GitHub Pages (HTTPS, pas de backend)

**Bonnes pratiques recommandées :**
- Préférez l'usage local du fichier `index.html` (téléchargé) pour les FE les plus sensibles
- Anonymisez aussi les **noms d'entreprise** si vous prévoyez de partager ou d'archiver le document Word final
- Le contrôle reste à votre charge : l'outil détecte les motifs courants mais ne peut garantir une anonymisation exhaustive

---

## 📐 Méthodologie

La méthodologie complète de scoring et de rédaction est documentée dans **[SKILL.md](SKILL.md)**.

### Échelle de notation 0-4

| Note | Libellé | Critère |
|---|---|---|
| **4** | Maîtrisé | Tous les moyens INRS/Code du travail en place |
| **3** | Globalement en place | Cadre principal OK, recommandations marginales |
| **2** | Partiel / à renforcer | Moyens présents, gaps significatifs (formation, EPI, procédure) |
| **1** | À traiter | Très peu de moyens, gaps majeurs multiples |
| **0** | Non concerné | Non affiché sur le radar |

### Règle de déduplication

Si un moyen apparaît dans *« observés »* ET *« conseillés »* (formulation équivalente), il est compté **une seule fois**.

### Référentiel — 22 familles de risque

Risque routier · Addictions / sécurité · Manutention manuelle · Travail répétitif / TMS · Postures contraignantes · Vibrations mécaniques · Chute de plain-pied · Chute de hauteur · Chute d'objet · Coactivité · Risque machine · Risque électrique · Risque chimique · Risque biologique · Bruit · Ambiance thermique · Éclairage / rayonnements · Incendie / explosion · RPS / contact public · Travail isolé · Travail sur écran · Horaires atypiques.

---

## 🤝 Pour les services SST qui souhaitent l'adopter

Cet outil est **libre et adaptable** à votre charte graphique :

1. **Forkez** le repo
2. Ouvrez `index.html` et modifiez les variables CSS dans la section `:root` :
   ```css
   --navy: #VOTRE_COULEUR_PRIMAIRE;
   --orange: #VOTRE_COULEUR_ACCENT;
   ```
3. Remplacez les mentions `SPSTI 23/87` par votre service
4. Activez GitHub Pages dans les paramètres du repo

**Vous adaptez l'outil ?** N'hésitez pas à ouvrir une *issue* pour partager vos retours d'usage ou suggérer des évolutions.

---

## 🛣️ Roadmap

- [ ] Export PDF direct (en plus du Word)
- [ ] Mode comparaison N vs N-1
- [ ] Variante « DUERP simplifié » à partir du même socle
- [ ] Intégration optionnelle d'un webhook IA (Make.com → Claude) pour pré-remplissage automatique
- [ ] Module d'anonymisation enrichi (entités nommées via modèle local Hugging Face Transformers.js)
- [ ] Internationalisation (interface EN/ES)

---

## 👤 Auteure

**Laure Bonnefond**
Infirmière en Santé au Travail (IDE-ST) · IPRP · SPSTI 23/87 (Creuse / Haute-Vienne)

- 🌐 Portfolio : [PréventIA-LaB](https://laurebonnefond.github.io/PreventIA-LaB/)
- 💼 LinkedIn : [Laure Bonnefond](https://www.linkedin.com/in/laure-bonnefond/)
- 🎓 En formation Master IA, Big Data & Développement — IPSSI Bordeaux (alternance, 2026)

---

## 📜 Licence

[MIT](LICENSE) — libre d'usage, de modification et de redistribution, y compris à des fins professionnelles.

Si vous utilisez cet outil dans le cadre de votre activité, **une mention de la source est appréciée** mais non obligatoire.

---

## 🙏 Remerciements

- Équipe médico-professionnelle du **SPSTI 23/87** pour le cadrage métier et les retours terrain
- INRS pour les référentiels de prévention et la documentation publique
- Communauté open-source des bibliothèques utilisées (Chart.js, Mammoth, PDF.js)

---

*Dernière mise à jour : 2026 · Version 1.0*
