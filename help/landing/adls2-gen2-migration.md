---
title: Migrazione Data Lake a Gen2
description: Scopri le nuove funzionalità fornite dalla migrazione del Data Lake a Gen2 in Adobe Experience Platform.
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 97f803f649b2c42b0449a2f8f0cff370ed1aba93
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Migrazione Adobe Experience Platform Data Lake a Gen2

È in corso la migrazione di Adobe Experience Platform a Gen2 Data Lake. Si tratta di una nuova generazione di data lake che offre agli utenti Platform vantaggi quali la replica in area geografica, controlli di accesso basati su ruoli più precisi (RBAC) e una migliore scalabilità.

## Impatto utente

Durante la migrazione di Adobe dal Data Lake da Gen1 a Gen 2, gli utenti saranno in grado di **leggere** dal Data Lake, ma saranno interessate tutte le funzionalità che **scrivono** nel Data Lake. Di seguito è riportato un elenco delle funzionalità interessate:

- **Origini**: I dati provenienti dalle sorgenti e dai vari flussi di lavoro di acquisizione dei dati verranno ritardati. Al termine della migrazione, gli utenti visualizzeranno i propri dati.
- **Servizio** query: Gli utenti possono eseguire query ma non possono scrivere l’output della query in un set di dati.
- **Profilo** cliente in tempo reale: I dati acquisiti nell’archivio profili tramite  **** batch non saranno disponibili durante la migrazione. Tuttavia, i dati acquisiti tramite **streaming** acquisizione saranno disponibili durante la migrazione. Inoltre, le esportazioni del profilo non saranno disponibili durante la migrazione.
- **Data Science Workspace**: Le scritture da Data Science Workspace avranno esito negativo.
- **Servizio** di segmentazione: I tipi di pubblico derivati dalla segmentazione  **** in batch non possono essere attivati durante la migrazione. I tipi di pubblico derivati dalla segmentazione **streaming** non saranno interessati.
- **Customer Journey Analytics**: I dati dei rapporti di Customer Journey Analytics potrebbero non essere aggiornati e non verranno aggiornati durante la migrazione, in quanto i batch non vengono acquisiti in Data Lake.

## Comunicazione agli utenti di Platform

Ad Adobe, gli amministratori di sistema contatteranno per discutere in dettaglio l’impatto della migrazione e per confermare le date e le ore di migrazione per specifiche organizzazioni IMS.
