---
title: Migrazione Data Lake a Gen2
description: Scopri le nuove funzionalità fornite dalla migrazione del Data Lake a Gen2 in Adobe Experience Platform.
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Migrazione Adobe Experience Platform Data Lake a Gen2

È in corso la migrazione di Adobe Experience Platform a Gen2 Data Lake. Si tratta di una nuova generazione di data lake che offre agli utenti Platform vantaggi quali la replica in area geografica, controlli di accesso basati su ruoli più precisi (RBAC) e una migliore scalabilità.

## Impatto utente

Mentre Adobe sta eseguendo la migrazione del Data Lake da Gen1 a Gen 2, gli utenti potranno **read** dal Data Lake, ma tutte le funzionalità che **scrivere** Influenza sul Data Lake. Di seguito è riportato un elenco delle funzionalità interessate:

- **Origini**: I dati provenienti dalle sorgenti e dai vari flussi di lavoro di acquisizione dei dati verranno ritardati. Al termine della migrazione, gli utenti visualizzeranno i propri dati.
- **Servizio query**: Gli utenti possono eseguire query ma non possono scrivere l’output della query in un set di dati.
- **Profilo cliente in tempo reale**: Dati acquisiti nell’archivio profili tramite **batch** L’acquisizione non sarà disponibile durante la migrazione. Tuttavia, i dati acquisiti tramite **streaming** Durante la migrazione sarà disponibile l’acquisizione. Inoltre, le esportazioni del profilo non saranno disponibili durante la migrazione.
- **Data Science Workspace**: Le scritture da Data Science Workspace avranno esito negativo.
- **Servizio di segmentazione**: Tipi di pubblico derivati da **batch** la segmentazione non può essere attivata durante la migrazione. Tipi di pubblico derivati da **streaming** la segmentazione non verrà modificata.
- **Customer Journey Analytics**: I dati dei rapporti di Customer Journey Analytics potrebbero non essere aggiornati e non verranno aggiornati durante la migrazione, in quanto i batch non vengono acquisiti in Data Lake.

## Comunicazione agli utenti di Platform

Ad Adobe, gli amministratori di sistema contatteranno per discutere in dettaglio l’impatto della migrazione e per confermare le date e le ore di migrazione per organizzazioni specifiche.
