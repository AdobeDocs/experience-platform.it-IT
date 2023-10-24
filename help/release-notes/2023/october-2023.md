---
title: Note sulla versione di Adobe Experience Platform
description: Note sulla versione di ottobre 2023 per Adobe Experience Platform.
source-git-commit: d024596c7d85139721ef370f9e081911a217d9ba
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 43%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 25 ottobre 2023**

Aggiornamenti alle funzioni esistenti in Experience Platform:

- [Origini](#sources)

## Origini {#sources}

Experience Platform fornisce un’API RESTful e un’interfaccia utente interattiva per impostare facilmente le connessioni di origine per vari provider di dati. Queste connessioni di origine consentono di autenticarti e connetterti a sistemi di archiviazione esterni e servizi di gestione delle relazioni con i clienti, impostare i tempi per le esecuzioni dell’acquisizione e gestire la velocità effettiva di acquisizione dei dati.

**Funzioni nuove o aggiornate**

| Funzione | Descrizione |
| --- | --- |
| Autenticazione aggiornata per Data Landing Zone | Visualizzando le credenziali, ora puoi vedere la data di scadenza designata per la Data Landing Zone. Per continuare a utilizzare il token nell’applicazione, è necessario aggiornarlo prima della data di scadenza. Se non aggiorni manualmente il token prima della data di scadenza dichiarata, al successivo recupero delle credenziali verrà automaticamente aggiornato e verrà fornito un nuovo token. Per ulteriori informazioni, consulta la documentazione su [utilizzo della Data Landing Zone](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

Per ulteriori informazioni sulle origini, leggere la [panoramica sulle origini](../../sources/home.md).
