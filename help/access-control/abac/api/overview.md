---
keywords: Experience Platform;home;argomenti popolari;api;controllo degli accessi basato su attributi;Controllo degli accessi basato su attributi
solution: Experience Platform
title: Guida dell’API di controllo dell’accesso basato su attributi
description: L’API di controllo dell’accesso basata su attributi consente di gestire in modo programmatico i ruoli e i criteri di accesso all’interno di Adobe Experience Platform. Segui questa guida per scoprire come eseguire operazioni chiave utilizzando l’API.
exl-id: 0fc32354-4869-4392-9501-b1dbea1bc55e
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 5%

---

# Guida API per il controllo degli accessi basato su attributi

Il controllo degli accessi basato sugli attributi è una funzionalità di Adobe Experience Platform che consente agli amministratori di controllare l’accesso a oggetti e/o funzionalità specifici in base agli attributi. Gli attributi possono essere metadati aggiunti a un oggetto, ad esempio un’etichetta aggiunta a un campo o a un segmento dello schema. Un amministratore definisce i criteri di accesso che includono attributi per gestire le autorizzazioni di accesso degli utenti.

L’API di controllo dell’accesso basata su attributi viene utilizzata per accedere a ruoli, prodotti, categorie di autorizzazioni e set di autorizzazioni all’interno di Adobe Experience Platform, fornendo un’interfaccia utente e un’API RESTful da cui tutte le risorse libreria disponibili sono accessibili.

>[!IMPORTANT]
>
>Il controllo dell’accesso basato su attributi non deve essere confuso con le funzionalità di governance dei dati di Experience Platform, che consentono di utilizzare etichette e criteri per controllare il modo in cui i dati vengono utilizzati in Platform, anziché gli utenti dell’organizzazione che vi hanno accesso. Consulta la [Guida API del servizio criteri](../../../data-governance/api/overview.md) per i passaggi su come sfruttare in modo programmatico queste funzionalità.

Questi endpoint sono descritti di seguito. Per informazioni dettagliate, consulta le guide dei singoli endpoint e fai riferimento a [guida introduttiva](./getting-started.md) per informazioni importanti sulle intestazioni richieste, leggi le chiamate API di esempio e altro ancora.

## Ruoli

I ruoli definiscono l’accesso di un amministratore, uno specialista o un utente finale alle risorse della tua organizzazione. In un ambiente di controllo degli accessi basato su ruoli, il provisioning degli accessi utente è raggruppato in base a responsabilità e esigenze comuni. Un ruolo dispone di un determinato set di autorizzazioni e i membri dell’organizzazione possono essere assegnati a uno o più ruoli, a seconda dell’ambito di visualizzazione o dell’accesso in scrittura di cui hanno bisogno. Consulta la [guida dell’endpoint &quot;roles&quot;](./roles.md) per ulteriori informazioni sull’utilizzo dei ruoli nell’API.

## Criteri

Le politiche sono dichiarazioni che riuniscono attributi per stabilire azioni ammissibili e inammissibili. I criteri possono essere locali o globali e possono ignorare altri criteri. Il `/policies` l’endpoint ti consente di gestire in modo programmatico i criteri dell’organizzazione. Consulta la [guida dell’endpoint &quot;policies&quot;](./policies.md) per ulteriori informazioni sull’utilizzo dei criteri nell’API.

## Prodotti

Il `/products` L’endpoint nell’API di controllo degli accessi basata su attributi consente di gestire in modo programmatico prodotti, categorie di autorizzazioni e set di autorizzazioni associati ai prodotti dell’organizzazione. Consulta la [guida dell’endpoint &quot;products&quot;](./products.md) per ulteriori informazioni sull’utilizzo dei prodotti e delle categorie e dei set di autorizzazioni corrispondenti nell’API.

## Passaggi successivi

Per iniziare a effettuare chiamate utilizzando l’API di controllo degli accessi basata su attributi, leggi [guida introduttiva](./getting-started.md) quindi seleziona una delle guide degli endpoint per scoprire come utilizzare endpoint specifici.
