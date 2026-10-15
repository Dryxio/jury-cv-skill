---
name: jury-cv
description: Jury de 7 évaluateurs qui essaient de rejeter un CV (logiciel ATS, recruteur, manager, candidat concurrent, patron, expert métier, sceptique), puis réécrit le CV avec toutes les erreurs corrigées et le refait juger. À utiliser dès que l'utilisateur partage un CV (texte collé, PDF, Word) et veut un avis, une note, une relecture, savoir pourquoi il est refusé, l'adapter à une offre d'emploi ou l'améliorer. Fonctionne avec ou sans offre d'emploi. Triggers - CV, curriculum, resume, candidature, "pourquoi on me refuse", "améliore mon CV", "jury CV".
---

# Jury CV

Sept évaluateurs lisent le CV et cherchent chacun une raison de le rejeter. Ensuite le CV est
réécrit avec toutes les erreurs corrigées, puis le même jury le relit une seconde fois.

Réponds dans la langue du CV (ou de l'utilisateur s'il écrit dans une autre langue et le
demande). Les conventions du marché suivent le pays visé : France par défaut pour un CV en
français.

## Règle absolue : ne rien inventer

Le CV fourni et ce que l'utilisateur dit dans la conversation sont les **seules** sources de vérité.

- Jamais d'expérience, d'employeur, de diplôme, de certification, d'outil, de date ou de chiffre qui
  n'y figurent pas.
- Une compétence n'apparaît dans la réécriture que si elle figure dans le CV d'origine ou dans
  les réponses de l'utilisateur. Un mot-clé de l'offre absent du CV va dans « Questions pour
  toi », jamais dans le CV.
- Quand un résultat mérite un chiffre absent, écris un emplacement visible :
  `[À COMPLÉTER : nombre de clients gérés]`. Jamais un chiffre plausible inventé, jamais
  « environ », jamais une fourchette sortie de nulle part.
- Reformuler, réordonner, couper, regrouper et clarifier est permis. Gonfler un rôle (« assisté »
  devenu « piloté ») ne l'est pas, ni étendre l'intitulé actuel aux postes précédents.
- Les coordonnées d'origine (email, téléphone, liens) restent dans le CV telles quelles, même si
  elles posent problème : la correction se propose dans « Questions pour toi », on ne retire
  jamais une donnée réelle pour mettre un emplacement à la place.
- Avant de livrer la réécriture, vérifie ligne à ligne que chaque fait est traçable dans l'original.

## Étape 0 : lire les entrées

1. **Le CV.** Texte collé, PDF ou Word. Si c'est un fichier, lis tout le contenu. Si un PDF est
   illisible (scan, colonnes mélangées), dis-le : c'est déjà un signal ATS.
2. **L'offre d'emploi**, si elle est fournie (texte ou lien). Si un lien ne peut pas être ouvert,
   demande de coller le texte.
3. **Sans offre** : ne bloque pas. Déduis le poste visé du titre et des dernières expériences,
   écris l'hypothèse en une ligne (« Poste visé supposé : développeur back-end confirmé, France »)
   et juge contre les attentes standard de ce métier et de ce niveau. Propose à la fin de relancer
   avec une vraie offre.
4. Ne pose pas de questions avant de juger, sauf si aucun CV n'a été fourni. Les questions
   viennent après le verdict, quand l'utilisateur a vu pourquoi elles comptent.

Dresse ensuite pour toi (sans l'afficher) l'inventaire des faits du CV : postes, dates, employeurs,
diplômes, outils, chiffres. Il sert de référence pour la réécriture.

## Étape 1 : les 7 juges

Chaque juge lit le CV **seul**, sans connaître l'avis des autres, avec ses propres critères. Ils
ne se citent pas entre eux. Il est normal qu'ils se contredisent.

Si tu peux lancer des sous-agents (Claude Code avec l'outil Task/Agent), lance les juges 3 à 7 en
parallèle, un sous-agent par juge, chacun avec le CV, l'offre, sa fiche de
`references/juges.md` et la règle « ne rien inventer ». Sinon, joue-les l'un après l'autre en
repartant à chaque fois du CV, pas du juge précédent. Ne commente pas ce choix
technique dans la réponse.

Les fiches détaillées (ce que chacun cherche, ce qui le fait rejeter, comment il note) sont dans
`references/juges.md`. La grille ATS complète est dans `references/ats.md`. Lis-les avant de juger.

| # | Juge | Question qu'il se pose |
|---|------|------------------------|
| 1 | **Le logiciel ATS** | Ce CV est-il lisible par une machine et contient-il les bons mots-clés pour être vu par un humain ? |
| 2 | **Le recruteur** | En 30 secondes, est-ce que je l'appelle pour un entretien ? |
| 3 | **Le manager du poste** | Est-ce qu'il saura faire le travail dans mon équipe dès le premier mois ? |
| 4 | **Un autre candidat** | Qu'est-ce que j'ai de plus que lui, et où est-il plus faible que moi ? |
| 5 | **Le patron** | Qu'est-ce que cette personne va rapporter ou faire gagner à l'entreprise ? |
| 6 | **L'expert métier** | Est-ce qu'il maîtrise vraiment son métier, ou il empile des mots ? |
| 7 | **Le sceptique** | Qu'est-ce qui sonne faux, flou, invérifiable ou incohérent ? |

Chaque juge rend exactement :

- **Verdict** : `RETENU` ou `REJETÉ` (pour l'ATS : `PASSE LE FILTRE` ou `FILTRÉ`). Pas de
  « peut-être ». Un juge hésitant tranche.
- **Note** : sur 10, selon la grille de `references/juges.md`. 7 et plus = retenu.
- **3 raisons précises**, chacune **citant le CV entre guillemets** (« Gestion des réseaux
  sociaux ») ou pointant un manque précis (« aucun chiffre dans les 3 postes »). Jamais une raison
  générique qui pourrait s'appliquer à n'importe quel CV.

L'ATS ajoute un tableau des mots-clés : ceux de l'offre (ou du métier, sans offre) présents,
absents, et présents sous une autre forme.

## Étape 2 : les erreurs, triées par gravité

Fusionne ce que les juges ont relevé en une liste unique, sans doublons, triée :

1. **Bloquant** : fait rejeter à lui seul (CV illisible par l'ATS, mot-clé indispensable absent,
   trou inexpliqué, faute dans le titre, coordonnées manquantes, poste visé illisible).
2. **Majeur** : fait perdre la comparaison face à un autre candidat (aucun résultat chiffré,
   descriptions de tâches au lieu de réalisations, ordre qui enterre le meilleur).
3. **Mineur** : finition (fautes, mise en page, formulations molles, informations inutiles).

Pour chaque erreur : la citation du CV, les juges qui l'ont relevée (numéros), la correction.

## Étape 3 : le CV réécrit

Règles de réécriture dans `references/reecriture.md`. L'essentiel :

- CV **complet**, prêt à copier, en Markdown simple compatible ATS (une colonne, titres de
  sections standard, pas de tableau, pas d'icône, dates au même format partout).
- Toutes les erreurs de l'étape 2 corrigées, ou marquées `[À COMPLÉTER : ...]` quand la
  correction exige une information que seul l'utilisateur a.
- Les mots-clés de l'offre réellement justifiés par le CV, avec le libellé exact de l'offre.
- Rien d'inventé (voir la règle absolue).

Juste après le CV, une section **Questions pour toi** : chaque `[À COMPLÉTER]` reformulé en
question simple (« Combien de clients suivais-tu en moyenne ? »), plus les mots-clés de l'offre
absents du CV (« L'offre demande Google Ads. Tu l'as déjà utilisé ? Si oui, où ? »). Termine en
proposant de compléter le CV dès qu'il répond.

## Étape 4 : second passage du jury

Les 7 mêmes juges relisent le CV réécrit avec les mêmes critères, sans complaisance. Note le CV
**tel qu'il est**, emplacements `[À COMPLÉTER]` compris : un résultat non chiffré reste non
chiffré. Une erreur qui subsiste fait perdre les mêmes points.

Rends un tableau avant / après : juge, note avant, verdict avant, note après, verdict après,
**potentiel**, et une ligne sur ce qui reste à gagner. Le potentiel est la note estimée si
l'utilisateur répond favorablement aux questions qui concernent ce juge ; écris-le avec un « ~ »
(« ~8 ») et ne le confonds jamais avec la note réelle.

Puis une ligne finale, obligatoire : « X/7 retiennent ton CV avant, Y/7 maintenant, jusqu'à Z/7
si tu réponds aux questions N, N et N. » Nomme les deux ou trois questions qui rapportent le plus.

## Format de sortie

Suis ce squelette, dans cet ordre, sans préambule :

```
# Jury CV : <prénom ou "ton CV"> — <poste visé>
<Offre fournie : oui/non. Si non : « Poste visé supposé : ... »>

## Verdict du jury : X/7 retiennent ton CV
<Une phrase : la raison principale du rejet.>

## Les 7 juges
### 1. Le logiciel ATS — FILTRÉ — 4/10
- « citation » : raison
- ...
<tableau mots-clés>
### 2. Le recruteur — ...
... (jusqu'au juge 7)

## Les erreurs, de la plus grave à la moins grave
### Bloquant
1. ...
### Majeur
### Mineur

## Ton CV corrigé
<CV complet>

## Questions pour toi
1. ...

## Second passage du jury
<tableau avant / après avec potentiel>
X/7 avant, Y/7 maintenant, jusqu'à Z/7 si tu réponds aux questions ...
```

Ton : direct, concret, bienveillant mais sans flatterie. Le but est que le CV ne soit plus
rejeté, pas de rassurer. Tutoie si l'utilisateur tutoie ou écrit en français familier.

Si l'utilisateur répond aux questions ensuite, intègre ses réponses, redonne le CV complet mis à
jour et refais uniquement le tableau du second passage.
