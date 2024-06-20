---
solution: Experience Platform
title: Limitazioni note con i playbook
description: Scopri di più sui problemi noti e i problemi comuni dei playbook e come risolverli
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: e24334bb4ac788770abe20ec2324efa1e64bc0e8
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 1%

---


# Limitazioni note {#known-limitations}

Scopri come risolvere gli errori durante l’utilizzo dei playbook basati su casi d’uso e le limitazioni note della versione con disponibilità generale.

## Limitazioni note

Quando crei un’istanza di un playbook e generi risorse, vengono visualizzate alcune limitazioni note.

* Per gli schemi generati, se uno schema viene generato in un’istanza di un playbook e lo si modifica, allora un altro schema *non* viene generato se si abilita un&#39;altra istanza del playbook. Continua invece a utilizzare anche lo schema modificato all’interno dell’istanza.

* Quando si utilizza [funzionalità di riconoscimento dei dati](/help/use-case-playbooks/playbooks/data-awareness.md) per promuovere lo schema dalla sandbox inspirational alla sandbox di sviluppo, potresti visualizzare alcuni errori simili ai seguenti:

![Errori visualizzati nel flusso di lavoro di mappatura schema.](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png){width="1000" zoomable="yes"}

Ciò si verifica perché alcuni dei campi generati dallo schema non sono presenti nello schema nella sandbox di sviluppo in cui si sta copiando. Cercate quali sono questi campi. Quindi, torna alla sandbox di sviluppo dove puoi:

* Creare un nuovo gruppo di campi che includa tali campi oppure
* Includi nello schema un gruppo di campi standard e predefinito che include i campi mancanti.

Dopo aver incluso tali campi nello schema nella sandbox di sviluppo, torna al flusso di lavoro per copiare i campi dello schema dalla sandbox di ispirazione alla sandbox di sviluppo. Gli errori ora non esistono più.

Per ulteriori informazioni, guarda il video seguente per creare gruppi di campi schema.

>[!VIDEO](https://video.tv.adobe.com/v/27013/?learn=on)
