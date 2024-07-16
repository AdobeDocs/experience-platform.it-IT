---
title: Migrazione da Data Lake a Gen2
description: Scopri le nuove funzioni fornite dalla migrazione di Data Lake a Gen2 in Adobe Experience Platform.
exl-id: 56d9c77a-d7eb-498d-994f-b15d150dedb7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Migrazione di Adobe Experience Platform Data Lake a Gen2

Adobe Experience Platform sta eseguendo la migrazione al Data Lake Gen2. Si tratta di una nuova generazione di data lake che offre agli utenti di Platform vantaggi quali la replica geografica, controlli di accesso basati sui ruoli (RBAC) più precisi e una migliore scalabilità.

## Impatto utente

Durante la migrazione del Data Lake da Adobe da Gen1 a Gen 2, gli utenti potranno **leggere** dal Data Lake, ma saranno interessate tutte le funzionalità **scrivere** nel Data Lake. Di seguito è riportato un elenco delle funzionalità interessate:

- **Origini**: i dati provenienti dalle origini e da vari flussi di lavoro di acquisizione dati verranno ritardati. Al termine della migrazione, gli utenti visualizzeranno i propri dati.
- **Servizio query**: gli utenti possono eseguire query ma non saranno in grado di scrivere l&#39;output della query in un set di dati.
- **Profilo cliente in tempo reale**: i dati acquisiti nell&#39;archivio profili tramite l&#39;acquisizione di **batch** non saranno disponibili durante la migrazione. Tuttavia, i dati acquisiti tramite l&#39;acquisizione di **streaming** saranno disponibili durante la migrazione. Inoltre, le esportazioni di profili non saranno disponibili durante la migrazione.
- **Data Science Workspace**: le operazioni di scrittura da Data Science Workspace non riusciranno.
- **Servizio di segmentazione**: impossibile attivare i tipi di pubblico derivati dalla segmentazione **batch** durante la migrazione. I tipi di pubblico derivati dalla segmentazione **streaming** non saranno interessati.
- **Customer Journey Analytics**: i dati dei report di Customer Journey Analytics potrebbero non essere aggiornati e non verranno aggiornati durante la migrazione, poiché i batch non vengono acquisiti nel Data Lake.

## Comunicazione agli utenti di Platform

L’Adobe contatterà gli amministratori di sistema per discutere in dettaglio l’impatto della migrazione e confermare le date e le ore di migrazione per organizzazioni specifiche.
