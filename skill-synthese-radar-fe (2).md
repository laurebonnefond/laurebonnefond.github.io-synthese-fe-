# SKILL — Synthèse Radar Fiche d'Entreprise

> Méthodologie de génération d'un diagramme radar de synthèse des risques (0-4) à partir d'une fiche d'entreprise SPSTI, avec lecture rapide rédigée.

**Version :** 1.0
**Auteure :** Laure Bonnefond — IDE-ST / IPRP — SPSTI 23/87
**Outil d'application :** `index.html` du présent repo
**Démo en ligne :** [laurebonnefond.github.io/synthese-fe](https://laurebonnefond.github.io/synthese-fe/)

---

## 1. Quand utiliser ce skill

✅ **À utiliser quand :**
- On dispose d'une FE rédigée avec tableau des risques rempli
- L'objectif est une synthèse visuelle pour l'employeur (annexe FE, support de restitution, cadrage PAPRIPACT)
- On veut un livrable cohérent avec la charte SPSTI 23/87

❌ **À ne pas utiliser pour :**
- DUERP complet (le radar n'est pas un substitut à l'évaluation détaillée par poste)
- Évaluation individuelle (EvRP, fiche de suivi médical)
- Audit ergonomique ou PICB seul (utiliser les SKILLs dédiés)

---

## 2. Référentiel — 22 familles de risque

Alignement sur `CONCLUSION_FE_2026.docx`. Toutes ne sont pas affichées sur le radar — voir §5 pour la sélection.

```
1.  Risque routier              12. Risque électrique
2.  Addictions / sécurité       13. Risque chimique (incl. radon, CMR)
3.  Manutention manuelle        14. Risque biologique
4.  Travail répétitif / TMS     15. Bruit
5.  Postures contraignantes     16. Ambiance thermique
6.  Vibrations mécaniques       17. Éclairage / rayonnements
7.  Chute de plain-pied         18. Incendie / explosion
8.  Chute de hauteur            19. RPS / contact public
9.  Chute d'objet               20. Travail isolé
10. Coactivité                  21. Travail sur écran
11. Risque machine              22. Horaires atypiques / nuit
```

---

## 3. Rubrique de notation 0-4

| Note | Libellé | Critère opérationnel | Couleur |
|---|---|---|---|
| **4** | Maîtrisé | Tous les moyens INRS/Code du travail attendus en place. Aucune recommandation significative. | `#2D7A4F` |
| **3** | Globalement en place | Cadre principal en place. Recommandations marginales (sensibilisation, formalisation). | `#6BAE5C` |
| **2** | Partiel / à renforcer | Moyens présents mais **gaps significatifs** : formation, EPI, procédure, équipement manquants. | `#E89B3E` |
| **1** | À traiter | Très peu de moyens. **Gaps majeurs** sur plusieurs dimensions. | `#C44545` |
| **0** | Non concerné | Risque absent ou non applicable au GHE. **N'apparaît pas sur le radar.** | — |

### Règle de déduplication (essentielle)

> Si un moyen apparaît dans **« observés »** ET dans **« conseillés »** (formulation équivalente, ex. *« sensibilisation »* dans les deux colonnes), il est compté **une seule fois** côté observés.

### Heuristiques de pondération

- Recommandation = **renforcement de l'existant** → gap mineur, n'abaisse pas la note
- Recommandation = **nouvel élément** (formation PRAP, EPI, procédure, équipement) → **−1**
- Recommandation = **obligation réglementaire non respectée** (DUERP, SST, mesure radon zone 3, RI ≥50 salariés) → **−2 minimum**
- Cases observés **ET** conseillés vides alors que le risque est noté présent → note plafonnée à **1**

---

## 4. Workflow

```
1. Lecture FE → identifier entreprise, activité, GHE principal
2. Anonymisation OBLIGATOIRE de l'entête (coordonnées, noms, SIRET…)
3. Mapping des risques observés → référentiel §2
4. Scoring 0-4 (rubrique §3 + déduplication + heuristiques)
5. Sélection de 8 axes (§5)
6. Rédaction Lecture rapide (§6)
7. Génération diagramme + export Word (§7)
```

---

## 5. Sélection des 8 axes du radar

**Objectif :** image lisible et informative, pas un inventaire exhaustif.

### Critères (ordre décroissant de priorité)

1. **Pertinence GHE principal** — risque effectivement coté pour le métier dominant
2. **Contraste informatif** — privilégier un mélange de scores (un radar 8 axes tous à 2 n'apprend rien)
3. **Enjeux réglementaires** — inclure systématiquement les risques avec obligation légale non respectée
4. **Demande employeur / médecin** — axes explicitement souhaités

### Cible

- **8 axes** = sweet spot (lisibilité × richesse)
- **6 minimum** (en dessous, préférer un tableau)
- **12 maximum** (au-delà, labels illisibles)

### Convention de tri

Disposer les axes du plus haut score (en haut) vers le plus bas (en bas) en sens horaire, pour que le « creux » du radar soit immédiatement visible.

---

## 6. Lecture rapide — gabarit

**Format : 4 paragraphes courts (30-50 mots chacun).**

```
Point fort :         [axe(s) à 3-4/4]    → moyens INRS/CdT en place, mots-clés concrets
Zones à renforcer :  [N axes à 2/4]      → pattern transversal (formation / EPI / procédure)
Point critique :     [axe(s) à 0-1/4]    → conséquences réglementaires, ce qui manque
Message employeur :  [3 chantiers prioritaires propres, numérotés]
```

**Style obligatoire :**
- Concis, action-oriented
- Vocabulaire INRS / Code du travail
- **Pas de framing DUERP** dans la Lecture rapide (limite posée par les médecins)
- Pas de redite avec le détail risque par risque de la FE

---

## 7. Rendu visuel

### Palette SPSTI (variables CSS)

```css
:root {
  --navy:        #1F4E79;   /* trame radar, titres */
  --navy-soft:   rgba(31, 78, 121, 0.18);   /* fill radar */
  --orange:      #C55A11;   /* accents "zones à renforcer" */
  --green-dark:  #2D7A4F;   /* score 4 */
  --green:       #6BAE5C;   /* score 3 */
  --orange-warn: #E89B3E;   /* score 2 */
  --red:         #C44545;   /* score 1 */
}
```

**Typographie :** DM Serif Display (titres) · DM Sans (corps) · Calibri (export Word)

### Trois formats de sortie

| Format | Usage | Implémentation |
|---|---|---|
| **HTML interactif** | Présentation écran, démo restitution | `index.html` du repo (Chart.js radar) |
| **Word (.doc)** | Annexe FE remise à l'entreprise | Export natif depuis l'outil (chart embarqué en base64) |
| **PNG haute résolution** | Insertion mail, rapport, slide | `chart.toBase64Image(2.0)` |

### Cartouche de pied de page (obligatoire)

```
SPSTI 23/87 — Source : Fiche d'entreprise — [Nom anonymisé]
```

---

## 8. Confidentialité (RGPD / secret médical)

L'anonymisation est une étape **obligatoire et non contournable** :

- Toujours masquer la **première partie de la FE** : entreprise, adresse, dirigeant, médecin du travail, IPRP, référent sécurité, contacts, SIRET, NAF, emails, téléphones
- Préférer un descriptif d'activité au nom propre (`Transport sous-traitance livraison` plutôt que `O Transport`)
- Vérifier visuellement la pré-anonymisation auto avant validation
- Aucune FE brute ne doit transiter en dehors du poste de travail (cf. `.gitignore` du repo : `*.docx` et `*.pdf` exclus)

---

## 9. Checklist qualité avant livraison

- [ ] Anonymisation vérifiée et confirmée
- [ ] Tous les axes affichés correspondent à des risques réellement présents dans la FE
- [ ] Aucun axe à 0 ne figure sur le radar
- [ ] Déduplication appliquée (vérification ligne à ligne)
- [ ] Obligations réglementaires non respectées prises en compte dans le scoring
- [ ] Lecture rapide ne fait pas double-emploi avec le détail FE
- [ ] Pas de framing DUERP dans la Lecture rapide
- [ ] Cartouche SPSTI 23/87 présente
- [ ] Couleurs conformes palette
- [ ] Répartition (N/8) cohérente avec les scores affichés

---

## 10. Exemple d'application — FE Transport sous-traitance

**GHE :** Chauffeurs livreurs (10 salariés)

| Axe | Note | Justification synthétique |
|---|---|---|
| Ambiance thermique | 4 | Clim + boissons + pauses tempérées + vêtements adaptés |
| Risque routier | 3 | Maintenance Bernis + DPAE + DREAL + contrôle permis — manque formation pratique |
| Chute de plain-pied | 3 | Sensibilisation + chaussures sécurité — manque balisage |
| Manutention manuelle | 2 | Aides matérielles OK — PRAP, gants, aménagement véhicules manquants |
| Vibrations mécaniques | 2 | Entretien Bernis OK — siège anti-vibratile manquant |
| Coactivité | 2 | Gérée chez EU — plan circulation propre site absent |
| RPS / contact public | 2 | Organisation OK — alarme + sensibilisation manquantes |
| Addictions / sécurité | 1 | Sensibilisation ponctuelle uniquement — RI, éthylotests, protocole absents |

**Répartition :** 1/8 maîtrisé · 2/8 en place · 4/8 à renforcer · 1/8 à traiter

---

*Skill maintenu par Laure Bonnefond — SPSTI 23/87 — v1.0 (2026)*
