---
id: notif-configuration
title: Configurer les notifications
---

Par défaut, aucune notification n'est envoyée par Centreon Cloud. Pour activer les emails de notification pour des ressources spécifiques, vous devez créer des règles de notification.

## Dans quels cas des notifications peuvent-elles être envoyées ?

Pour chaque règle de notification, vous définissez dans quel cas les notifications doivent être envoyées :

* Quand une ressource passe dans un statut non-ok (**Alerte**, **Critique** ou inconnu pour un service, **Indisponible** ou **Injoignable** pour un hôte).
* Quand une ressource revient dans un statut OK (notifications de type **Recovery**).

## Comment sont contrôlées les ressources?

Les ressources sont contrôlées selon les paramètres suivants :

* Par défaut, les contrôles ont lieu 24x7 tant que l'hôte ou le service sont dans un état OK, toutes les 5 minutes.
   * La période de contrôle peut être personnalisée via [le champ **Période de contrôle** de la ressource](../monitoring/basic-objects/hosts.md#paramètres-de-supervision).
   * La fréquence de contrôle peut être personnalisée via [le champ **Intervalle normal de contrôle** de la ressource](../monitoring/basic-objects/hosts.md#options-dordonnancement).
* Lorsqu'un hôte ou un service entre dans un statut non-ok (type de statut SOFT, par exemple Injoignable SOFT pour un hôte), par défaut Centreon vérifie 3 fois que l'hôte ou le service est toujours dans un état non-ok. Vous pouvez définir un nombre personnalisé de contrôles via [le champ **Nombre de contrôles avant validation de l'état**de la ressource](../monitoring/basic-objects/hosts.md#options-dordonnancement). Par défaut, les 3 contrôles sont chacun espacés d'une minute (vous pouvez personnaliser cette valeur via [le champ **Intervalle non-régulier de contrôle** de la ressource](../monitoring/basic-objects/hosts.md#options-dordonnancement)).
* Si, après ces contrôles, la ressource est toujours dans un statut non-ok, son type de statut devient HARD. Si les notifications sont activées pour ce statut et la [période de temps](../monitoring/basic-objects/timeperiods.md) correspond, un email de notification est envoyé.
* Quand la ressource revient à un état OK, un email de notification est envoyé si vous avez activé les notifications en cas de **Recovery**.
* Les contacts ne reçoivent qu'un seul email de notification lorsque le statut de la ressource change (suivant les statuts que vous avez définis). Exemple : si vous avez seulement sélectionné **Critique**, aucun email ne sera envoyé lorsque le service passera à un statut **Alerte**. Un seul email sera envoyé quand le service passera à **Critique**.
* Si un service avait déjà un statut **Critique** avant la création d'une règle activant les notifications pour le statut **Critique**, alors aucun email de notification ne sera envoyé.

## Créer une règle de notification

1. Allez à la page **Configuration > Notifications > Notifications**.
2. Cliquez sur le bouton **Ajouter** au-dessus de la liste, à gauche. Le panneau de détails de la nouvelle notification s'ouvre.
3. Configurez la règle de notification :

   - Donnez un nom à la règle dans le champ **Name** en haut du panneau.
   - Sélectionnez les groupes d'hôtes et/ou les groupes de services et/ou les vues métier (Édition Business seulement) pour lesquels vous voulez que des notifications soient envoyées. Pour chaque type de ressource, sélectionnez les évènements qui déclencheront l'envoi d'une notification.
   - Sélectionnez la [période temporelle](../monitoring/basic-objects/timeperiods.md) durant laquelle les notifications seront autorisées pour cette ressource.
     > Les exceptions dans les périodes temporelles sont ignorées pour les notifications. Les notifications seront envoyées même pendant les périodes exclues. 
   - Sélectionnez les utilisateurs (contacts) qui recevront une notification en cas d'évènement.
   - Définissez un modèle d'email. Un modèle par défaut vous est fourni. Vous pouvez le modifier et utiliser des macros (variables). Pour insérer une macro dans votre modèle, utilisez le bouton **Macros** en bas à droite de l'encadré d'aperçu.
	
    | Macro | Description | Exemple |
    | ----- | ----------- |-------- |
	|\{\{NOTIFICATIONTYPE\}\}| **Recovery**, **Warning**, **Critical** or **Unknown** pour un service; **Recovery**, **Down** ou **Unreachable** pour un hôte. | CRITICAL |
	\{\{NAME\}\}| Le nom du service ou de l'hôte. Pour un service, le nom de l'hôte auquel celui-ci est rattaché est également indiqué. | central/proc-ntpd |
	\{\{ID\}\}| Un ID interne pour cette ressource. Cet ID peut être utilisé pour des appels API. | 41:209 |
	\{\{STATE\}\}| Le [statut](./concepts.md) dans lequel la ressource vient de passer. | CRITICAL |
	\{\{SHORTDATETIME\}\}| Date et heure au format suivant : MM/JJ/AA hh:mm:ss | 10/18/23 12:20:42 |
    \{\{LONGDATETIME\}\}| Date et heure, avec le jour de la semaine.  | Wednesday October 18, 2023, 12:20:42 |
	\{\{OUTPUT\}\}| La sortie de la commande de contrôle, c'est-à-dire le texte affiché dans la colonne **Information** de la page **Statut des ressources**. | CRITICAL: Number of current processes running: 0 |

3. Cliquez sur le bouton **Save** en haut à droite du panneau. La nouvelle règle de notification apparaît dans la liste. Elle peut mettre jusqu'à 5 minutes pour commencer à s'appliquer.
