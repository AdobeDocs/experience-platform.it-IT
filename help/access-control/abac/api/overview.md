---
keywords: Experience Platform;home;argomenti popolari;api;controllo degli accessi basato su attributi;Controllo degli accessi basato su attributi
solution: Experience Platform
title: Guida dell’API di controllo dell’accesso basato su attributi
description: L’API di controllo dell’accesso basata su attributi consente di gestire in modo programmatico i ruoli e i criteri di accesso all’interno di Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
role: Developer
exl-id: 0fc32354-4869-4392-9501-b1dbea1bc55e
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 8%

---

# Guida API per il controllo degli accessi basato su attributi

Il controllo degli accessi basato sugli attributi è una funzionalità di Adobe Experience Platform che consente agli amministratori di controllare l’accesso a oggetti e/o funzionalità specifici in base agli attributi. Gli attributi possono essere metadati aggiunti a un oggetto, ad esempio un’etichetta aggiunta a un campo o a un segmento dello schema. Un amministratore definisce i criteri di accesso che includono attributi per gestire le autorizzazioni di accesso degli utenti.

L’API di controllo dell’accesso basata su attributi viene utilizzata per accedere a ruoli, prodotti, categorie di autorizzazioni e set di autorizzazioni all’interno di Adobe Experience Platform, fornendo un’interfaccia utente e un’API RESTful da cui tutte le risorse libreria disponibili sono accessibili.

>[!IMPORTANT]
>
>Il controllo dell’accesso basato su attributi non deve essere confuso con le funzionalità di governance dei dati di Experience Platform, che consentono di utilizzare etichette e criteri per controllare il modo in cui i dati vengono utilizzati in Platform, anziché gli utenti dell’organizzazione che vi hanno accesso. Consulta la [Guida API del servizio criteri](../../../data-governance/api/overview.md) per informazioni su come sfruttare queste funzionalità a livello di programmazione.

Questi endpoint sono descritti di seguito. Per informazioni dettagliate, consulta le guide dei singoli endpoint e fai riferimento alla [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, sulla lettura delle chiamate API di esempio e altro ancora.

## Ruoli

I ruoli definiscono l’accesso di un amministratore, uno specialista o un utente finale alle risorse della tua organizzazione. In un ambiente di controllo degli accessi basato su ruoli, il provisioning degli accessi utente è raggruppato in base a responsabilità e esigenze comuni. Un ruolo dispone di un determinato set di autorizzazioni e i membri dell’organizzazione possono essere assegnati a uno o più ruoli, a seconda dell’ambito di visualizzazione o dell’accesso in scrittura di cui hanno bisogno. Per ulteriori informazioni sull&#39;utilizzo dei ruoli nell&#39;API, consulta la guida dell&#39;endpoint [roles](./roles.md).

## Criteri

I criteri sono dichiarazioni che riuniscono alcuni attributi al fine di definire azioni ammissibili e non ammissibili. I criteri possono essere locali o globali e possono ignorare altri criteri. L&#39;endpoint `/policies` consente di gestire in modo programmatico i criteri dell&#39;organizzazione. Per ulteriori informazioni sull&#39;utilizzo dei criteri nell&#39;API, consulta la [guida dell&#39;endpoint &quot;policies&quot;](./policies.md).

## Prodotti

L&#39;endpoint `/products` nell&#39;API di controllo degli accessi basata su attributi consente di gestire in modo programmatico prodotti, categorie di autorizzazioni e set di autorizzazioni associati ai prodotti dell&#39;organizzazione. Per ulteriori informazioni sull&#39;utilizzo dei prodotti e delle categorie di autorizzazioni e dei set di autorizzazioni corrispondenti nell&#39;API, consulta la [guida dell&#39;endpoint &quot;products&quot;](./products.md).

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l&#39;API di controllo degli accessi basata su attributi, leggere la [guida introduttiva](./getting-started.md), quindi selezionare una delle guide degli endpoint per informazioni su come utilizzare endpoint specifici.
