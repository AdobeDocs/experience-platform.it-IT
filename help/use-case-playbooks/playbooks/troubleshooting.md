---
solution: Experience Platform
title: Limitazioni note e risoluzione dei problemi relativi ai playbook
description: Scopri di più sui problemi noti e i problemi comuni dei playbook e come risolverli
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: d6be5d3e21ea924ff98c400b972709b1f60c25eb
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 2%

---


# Risoluzione dei problemi e limitazioni note {#troubleshooting-known-limitations}

## Risoluzione dei problemi {#troubleshooting}

### Adobe Journey Optimizer Surfaces non configurato

Durante la creazione di un&#39;istanza di un playbook, è possibile che venga visualizzato il messaggio seguente.

![Risoluzione dei problemi](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

Questo perché i playbook Journey Optimizer creano messaggi per i canali e-mail, push e SMS. Leggi le [introduzione](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer) per configurare le diverse superfici.

### Stato *non riuscito* durante la creazione di una nuova istanza

Se durante il tentativo di creazione di un&#39;istanza viene visualizzato un messaggio di errore, è possibile che l&#39;amministratore non abbia concesso le autorizzazioni utente necessarie. Un playbook contiene molte risorse diverse e l’utente ha bisogno delle autorizzazioni per crearle per poter creare correttamente l’istanza del playbook. Consulta la [autorizzazioni](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) sezione di questa guida sulla configurazione delle autorizzazioni.

## Limitazioni note

Quando crei un’istanza di un playbook e generi risorse, vengono visualizzate alcune limitazioni note.

* Per gli schemi generati, se uno schema viene generato in un’istanza di un playbook e lo si modifica, allora un altro schema *non* viene generato se si abilita un&#39;altra istanza del playbook. Continua invece a utilizzare anche lo schema modificato all’interno dell’istanza.

* Quando si utilizza [funzionalità di riconoscimento dei dati](/help/use-case-playbooks/playbooks/data-awareness.md) per promuovere lo schema dalla sandbox inspirational alla sandbox di sviluppo, potresti visualizzare alcuni errori simili ai seguenti:

![schema-errors](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png)

Ciò si verifica perché alcuni dei campi generati dallo schema non sono presenti nello schema nella sandbox di sviluppo in cui si sta copiando. Cercate quali sono questi campi. Quindi, torna alla sandbox di sviluppo dove puoi:

* Creare un nuovo gruppo di campi che includa tali campi oppure
* Includi nello schema un gruppo di campi standard e predefinito che include i campi mancanti.

Dopo aver incluso tali campi nello schema nella sandbox di sviluppo, torna al flusso di lavoro per copiare i campi dello schema dalla sandbox di ispirazione alla sandbox di sviluppo. Gli errori ora non esistono più.

Per ulteriori informazioni, guarda il video seguente per creare gruppi di campi schema.

>[!VIDEO](https://video.tv.adobe.com/v/27013/?learn=on)
