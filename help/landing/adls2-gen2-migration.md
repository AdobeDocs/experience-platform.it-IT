---
title: Migrazione da Data Lake a Gen2
description: Scopri le nuove funzioni fornite dalla migrazione di Data Lake a Gen2 in Adobe Experience Platform.
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Migrazione di Adobe Experience Platform Data Lake a Gen2

Adobe Experience Platform sta eseguendo la migrazione al Data Lake Gen2. Si tratta di una nuova generazione di data lake che offre agli utenti di Platform vantaggi quali la replica geografica, controlli di accesso basati sui ruoli (RBAC) più precisi e una migliore scalabilità.

## Impatto utente

Durante la migrazione del Data Lake da Adobe a Gen1, gli utenti potranno: **letto** dal Data Lake, ma tutte le funzionalità che **scrivere** nel Data Lake sarà interessato. Di seguito è riportato un elenco delle funzionalità interessate:

- **Sorgenti**: i dati in arrivo dalle sorgenti e dai vari flussi di lavoro di acquisizione dei dati subiranno ritardi. Al termine della migrazione, gli utenti visualizzeranno i propri dati.
- **Servizio query**: gli utenti possono eseguire query ma non saranno in grado di scrivere l’output della query in un set di dati.
- **Profilo cliente in tempo reale**: dati acquisiti nell’archivio dei profili tramite **batch** l’acquisizione non sarà disponibile durante la migrazione. Tuttavia, i dati acquisiti tramite **streaming** l’acquisizione sarà disponibile durante la migrazione. Inoltre, le esportazioni di profili non saranno disponibili durante la migrazione.
- **Data Science Workspace**: le scritture da Data Science Workspace avranno esito negativo.
- **Servizio di segmentazione**: tipi di pubblico derivati da **batch** La segmentazione non può essere attivata durante la migrazione. Tipi di pubblico derivati da **streaming** la segmentazione non verrà influenzata.
- **Customer Journey Analytics**: i dati dei rapporti sul Customer Journey Analytics potrebbero non essere aggiornati e non verranno aggiornati durante la migrazione, in quanto i batch non vengono acquisiti nel Data Lake.

## Comunicazione agli utenti di Platform

L’Adobe contatterà gli amministratori di sistema per discutere in dettaglio l’impatto della migrazione e confermare le date e le ore di migrazione per organizzazioni specifiche.
