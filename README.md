# rappels-echeances

Note tes échéances (carte d'identité, assurance, facture, impôts) et **exporte-les vers l'agenda de ton téléphone** pour recevoir une alerte à l'avance.

**Démo : https://agberesahir.github.io/rappels-echeances/**

- Un seul fichier HTML, aucune installation, aucun compte.
- Les rappels restent **dans ton navigateur** : rien n'est envoyé à un serveur.
- L'export `.ics` s'ouvre dans Google Agenda, Apple Calendrier, Outlook et la plupart des agendas.

## Comment l'utiliser

1. Écris **quoi** (par exemple « Renouvellement de la carte d'identité »), la date d'**échéance** et le nombre de jours pour être **prévenu avant** (14 par défaut).
2. Clique sur **Ajouter le rappel**. La liste est triée par date.
3. Clique sur **Exporter vers l'agenda (.ics)**. Un fichier `echeances.ics` est téléchargé.
4. Ouvre ce fichier : ton agenda propose d'ajouter les événements, chacun avec son alerte.

## Ce que montre la liste

| Couleur | Signification |
|---|---|
| Bordure rouge | **En retard** : l'échéance est passée (« En retard de 3 jours »). |
| Bordure jaune | **Bientôt** : tu es dans la fenêtre de prévenance, ou c'est aujourd'hui. |
| Bordure neutre | Pas encore urgent (« Dans 120 jours »). |

Chaque ligne a un bouton **Supprimer**.

## Le fichier exporté

Chaque rappel devient un événement « journée entière » à la date d'échéance, avec une alerte `-P<n>D` (n jours avant). Le titre sert aussi de texte de l'alerte.

```text
BEGIN:VEVENT
UID:rappel-0-20261231@petits-outils
DTSTART;VALUE=DATE:20261231
SUMMARY:Renouvellement de la carte d'identité
BEGIN:VALARM
ACTION:DISPLAY
TRIGGER:-P14D
END:VALARM
END:VEVENT
```

Les caractères spéciaux du titre (virgules, points-virgules, retours à la ligne) sont échappés pour que le fichier reste valide.

## Limites à connaître

- **La page ne t'envoie aucune notification.** Elle prépare des événements ; ce sont Google Agenda, Apple Calendrier ou Outlook qui émettent l'alerte. Sans export, aucune alerte n'est envoyée.
- **Les données sont propres à un navigateur sur un appareil.** Ton téléphone et ton ordinateur ont chacun leur liste. Vider les données du navigateur (ou la navigation privée) efface tout. Il n'y a pas de sauvegarde ni d'import : si une liste est précieuse, exporte-la en `.ics`.
- **Un export contient toute la liste.** Importer le fichier une seconde fois peut créer des doublons selon ton agenda. Supprime les anciens événements avant de réimporter, ou n'exporte qu'une fois la liste stabilisée.
- Pas de récurrence (une assurance annuelle doit être ajoutée chaque année) ni d'heure précise : les événements durent toute la journée.
- L'heure exacte à laquelle l'alerte sonne pour un événement « journée entière » dépend de l'application d'agenda.
- Les jours restants sont calculés avec la date et le fuseau de ton appareil.

## Utiliser en local

```bash
git clone https://github.com/AGBERESahir/rappels-echeances.git
cd rappels-echeances
# puis ouvre index.html dans ton navigateur
```

Seule la police Atkinson Hyperlegible est chargée depuis Google Fonts ; sans connexion, la police système la remplace.

## Fichiers

| Fichier | Rôle |
|---|---|
| `index.html` | Formulaire, liste, export `.ics`. |
| `shared.css` | Styles communs avec [frais-transfert](https://github.com/AGBERESahir/frais-transfert) et [documents-types](https://github.com/AGBERESahir/documents-types). |

## Licence

MIT, voir [LICENSE](LICENSE).
