---
source-git-commit: b9816767556b9d50cf2ff5268816d1de6b85fc63
workflow-type: tm+mt
translation-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---
# Migrazione Adobe Experience Platform Data Lake a Gen2

Adobe Experience Platform sta effettuando la migrazione al Gen2 Data Lake. Si tratta di una nuova generazione di data Lake che offre agli utenti della piattaforma vantaggi quali replica di aree geografiche, controlli di accesso basati su ruoli più precisi (RBAC) e scalabilità migliore.

## Impatto dell&#39;utente

Mentre  Adobe sta migrando il Data Lake da Gen1 a Gen 2, gli utenti saranno in grado di **leggere** dal Data Lake, ma tutte le capacità che **scrivono** nel Data Lake saranno influenzate. Di seguito è riportato un elenco delle funzionalità interessate:

- **Origini**: I dati provenienti dalle origini e dai vari flussi di lavoro di acquisizione dei dati saranno ritardati. Al termine della migrazione, gli utenti visualizzeranno i propri dati.
- **Servizio** query: Gli utenti possono eseguire query ma non saranno in grado di scrivere l&#39;output della query in un dataset.
- **Profilo** cliente in tempo reale: I dati trasferiti allo store Profilo tramite l’assimilazione **batch** non saranno disponibili durante la migrazione. Tuttavia, durante la migrazione saranno disponibili i dati acquisiti tramite l’assimilazione **in streaming** . Inoltre, le esportazioni di profili non saranno disponibili durante la migrazione.
- **Area di lavoro** dati: Le scritture da Data Science Workspace non riusciranno.
- **Servizio** segmentazione: Durante la migrazione non è possibile attivare audience derivate dalla segmentazione **batch** . Le audience derivate dalla segmentazione **dello streaming** non verranno interessate.
- **Customer Journey Analytics**: I dati dei rapporti sugli Customer Journey Analytics potrebbero non essere aggiornati e non verranno aggiornati durante la migrazione, in quanto i batch non vengono trasferiti in Data Lake.

## Comunicazione agli utenti della piattaforma

 Adobe contatterà gli amministratori di sistema per discutere in dettaglio l&#39;impatto della migrazione e per confermare le date e le ore di migrazione per specifiche organizzazioni IMS.