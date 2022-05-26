---
keywords: Experience Platform;home;argomenti comuni;api;controllo degli accessi basato su attributi;controllo degli accessi basato su attributi
solution: Experience Platform
title: Guida all'API per il controllo degli accessi basato su attributi
description: L'API di controllo degli accessi basata su attributi consente di gestire in modo programmatico ruoli e criteri in Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
hide: true
hidefromtoc: true
exl-id: 0fc32354-4869-4392-9501-b1dbea1bc55e
source-git-commit: 19f1e8df8cd8b55ed6b03f80e42810aefd211474
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 5%

---

# Guida API per il controllo degli accessi basato su attributi

>[!IMPORTANT]
>
>Il controllo dell&#39;accesso basato su attributi è attualmente disponibile in una versione limitata per i clienti del settore sanitario negli Stati Uniti. Questa funzionalità sarà disponibile per tutti i clienti Real-time Customer Data Platform una volta rilasciata.

Il controllo dell&#39;accesso basato su attributi è una funzionalità di Adobe Experience Platform che consente agli amministratori di controllare l&#39;accesso a oggetti e/o funzionalità specifici in base agli attributi. Gli attributi possono essere metadati aggiunti a un oggetto, ad esempio un’etichetta aggiunta a un campo o a un segmento dello schema. Un amministratore definisce i criteri di accesso che includono gli attributi per gestire le autorizzazioni di accesso degli utenti.

L’API di controllo accessi basata sugli attributi viene utilizzata per accedere a ruoli, prodotti, categorie di autorizzazioni e set di autorizzazioni in Adobe Experience Platform, fornendo un’interfaccia utente e un’API RESTful da cui sono accessibili tutte le risorse della libreria disponibili.

Questi endpoint sono descritti di seguito. Per informazioni dettagliate, visita le singole guide dell’endpoint e fai riferimento alla sezione [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura di chiamate API di esempio e altro ancora.

## Ruoli

I ruoli definiscono l’accesso che un amministratore, uno specialista o un utente finale ha alle risorse dell’organizzazione. In un ambiente di controllo degli accessi basato su ruoli, il provisioning degli accessi utente viene raggruppato attraverso responsabilità e esigenze comuni. Un ruolo dispone di un determinato set di autorizzazioni e i membri dell’organizzazione possono essere assegnati a uno o più ruoli, a seconda dell’ambito di accesso di visualizzazione o scrittura necessario. Consulta la sezione [guida all’endpoint dei ruoli](./roles.md) per ulteriori informazioni sulle operazioni con i ruoli nell’API.

## Criteri

Le politiche sono dichiarazioni che riuniscono gli attributi per stabilire azioni ammissibili e non ammissibili. I criteri possono essere locali o globali e possono sostituire altri criteri. La `/policies` l’endpoint ti consente di gestire i criteri in modo programmatico all’interno dell’organizzazione. Consulta la sezione [guida all’endpoint dei criteri](./policies.md) per ulteriori informazioni sull’utilizzo dei criteri nell’API.

## Prodotti

La `/products` l’endpoint nell’API di controllo accessi basato su attributi consente di gestire in modo programmatico i prodotti, nonché le categorie di autorizzazioni e i set di autorizzazioni associati ai prodotti dell’organizzazione. Consulta la sezione [guida all’endpoint dei prodotti](./products.md) per ulteriori informazioni sull’utilizzo dei prodotti e delle relative categorie di autorizzazioni e set di autorizzazioni nell’API.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API di controllo accessi basata sugli attributi, leggi la [guida introduttiva](./getting-started.md) quindi seleziona una delle guide dell’endpoint per scoprire come utilizzare endpoint specifici.
