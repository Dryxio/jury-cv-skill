# Jury CV

> **Note pour Claude** : si un utilisateur t'a donné le lien de ce dépôt, lis
> `jury-cv/SKILL.md` puis les trois fichiers de `jury-cv/references/` (`juges.md`, `ats.md`,
> `reecriture.md`), et applique ces instructions à la lettre. Demande ensuite son CV
> (texte collé, PDF ou Word) et, s'il en a une, l'offre d'emploi visée. Ne résume pas ce dépôt :
> exécute-le.

Un jury de 7 Claude qui essaient de rejeter ton CV. Puis il te le réécrit avec toutes les erreurs
corrigées, et le jury le relit une seconde fois.

Gratuit, sans compte en plus, sans rien à installer si tu passes par le lien.

## Les 7 juges

1. **Le logiciel ATS** : le logiciel automatique qui décide si ton CV sera même vu par un humain.
   Lisibilité, sections, mots-clés de l'offre, critères éliminatoires.
2. **Le recruteur** : décide en 30 secondes si tu passes l'entretien.
3. **Le manager du poste** : est-ce que tu sauras faire le travail dès le premier mois ?
4. **Un autre candidat** : ton concurrent sur la même offre, qui cherche où il te bat.
5. **Le patron** : qu'est-ce que tu vas rapporter à l'entreprise ?
6. **L'expert métier** : est-ce que tu maîtrises vraiment ton métier ou tu empiles des mots ?
7. **Le sceptique** : ce qui sonne faux, flou, invérifiable ou incohérent.

Chaque juge rend un verdict (retenu ou rejeté), une note sur 10 et trois raisons qui citent ton CV.

## Ce que tu obtiens

1. Le verdict des 7 juges.
2. La liste de tes erreurs, de la plus grave à la moins grave.
3. Ton CV réécrit en entier, prêt à copier dans Word ou Google Docs.
4. Les questions à te poser pour finir de le blinder (les chiffres que toi seul connais).
5. Le second passage du jury : tes notes avant / après.

Il n'invente rien. Aucune expérience, aucun diplôme, aucun chiffre ajouté. Quand un chiffre
manque, il laisse un emplacement `[À COMPLÉTER : ...]` et te pose la question.

## Installer

### Le plus simple : coller le lien

Colle le lien de ce dépôt dans une conversation Claude (claude.ai, appli mobile ou desktop) avec
ton CV, et écris : « Utilise ce jury sur mon CV ». Claude lit les instructions depuis le lien et
lance le jury. La recherche web doit être activée dans Claude pour qu'il puisse ouvrir le lien.

### Claude.ai : l'installer pour de bon

1. Télécharge `jury-cv.zip`.
2. Dans **Paramètres > Fonctionnalités** (Capabilities), vérifie que l'exécution de code est
   activée.
3. Va dans **Personnaliser > Skills** (claude.ai/customize/skills), clique sur **+**, puis
   **Créer une skill > Importer une skill**, et choisis le zip.
4. Ensuite, dans n'importe quelle conversation, envoie ton CV : la skill se déclenche toute
   seule.

Marche aussi avec un compte gratuit.

### Claude Code

```bash
cp -R jury-cv ~/.claude/skills/
```

Puis donne ton CV à Claude Code (« juge mon CV : cv.pdf »). Dans Claude Code, les juges 3 à 7
tournent en parallèle, chacun dans son propre agent.

## Utiliser

- **CV + offre d'emploi** (le mieux) : colle les deux. L'ATS prend les mots-clés dans l'offre.
- **CV seul** : le jury déduit le poste visé de ton CV et juge contre les attentes standard du
  métier. Tu pourras relancer ensuite avec une offre.
- Formats : texte collé, PDF ou Word.
- Après le verdict, réponds aux questions : Claude complète ton CV et refait le second passage.

## Contenu

```
jury-cv/
  SKILL.md                 le déroulé du jury
  references/juges.md      les 7 juges en détail et la grille de notation
  references/ats.md        la grille du logiciel de tri
  references/reecriture.md les règles de réécriture (et ce qui est interdit)
tests/                     deux CV fictifs et les résultats du jury
```
