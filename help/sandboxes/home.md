---
keywords: Experience Platform;home;argomenti popolari;sandbox;sandbox;test;test
solution: Experience Platform
title: Panoramica delle sandbox
topic-legacy: overview
description: Le sandbox sono partizioni virtuali all’interno di una singola istanza di Experience Platform, che consentono un’integrazione perfetta con il processo di sviluppo delle applicazioni di esperienza digitale.
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 0%

---

# Panoramica delle sandbox

Adobe Experience Platform è progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono provvedere allo sviluppo, al test e alla distribuzione di queste applicazioni, garantendo al contempo la conformità operativa.

Per soddisfare questa esigenza, Experience Platform fornisce sandbox che suddividono una singola istanza di Platform in ambienti virtuali separati per contribuire a sviluppare e sviluppare applicazioni di esperienza digitale.

Questo documento fornisce una panoramica di alto livello delle sandbox in Experience Platform.

## Informazioni sulle sandbox

Le sandbox sono partizioni virtuali all’interno di una singola istanza di Experience Platform, che consentono un’integrazione perfetta con il processo di sviluppo delle applicazioni di esperienza digitale. Un’istanza di Experience Platform supporta una sandbox di produzione e più sandbox non di produzione, con ogni sandbox che mantiene la propria libreria indipendente di risorse Platform (inclusi schemi, set di dati, profili e così via).  Tutti i contenuti e le azioni eseguite all’interno di una sandbox sono limitati a tale sandbox e non hanno alcun effetto su altre sandbox.

Le sandbox non di produzione consentono di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sulla sandbox di produzione. Inoltre, le sandbox non di produzione hanno una funzione di reimpostazione che rimuove tutte le risorse create dal cliente dalla sandbox. Le sandbox non di produzione non possono essere convertite in sandbox di produzione. Una licenza di Experience Platform predefinita concede cinque sandbox (una produzione e quattro non di produzione). Puoi aggiungere pacchetti di dieci sandbox non di produzione fino a un massimo di 75 sandbox in totale. Per ulteriori informazioni, contatta l’amministratore dell’organizzazione IMS o il rappresentante commerciale di Adobe.

>[!NOTE]
>
>Quando viene creata una sandbox, non contiene dati. Poiché ogni sandbox mantiene il proprio archivio dati isolato, deve anche acquisire i propri dati in modo indipendente.

In sintesi, le sandbox offrono i seguenti vantaggi:

* **Gestione** del ciclo di vita dell&#39;applicazione: Creare ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.
* **Gestione** del progetto e del marchio: Consente l’esecuzione parallela di più progetti all’interno della stessa organizzazione IMS, garantendo al contempo l’isolamento e il controllo degli accessi. Le versioni future supporteranno l’implementazione in più aree geografiche.
* **Ecosistema** di sviluppo flessibile: Fornisci sandbox in modo semplice, scalabile e conveniente per scopi di esplorazione, abilitazione e dimostrazione.

## Controllo degli accessi per le sandbox

Per impostazione predefinita, tutti gli utenti di un&#39;organizzazione hanno accesso a una sandbox di produzione. L&#39;accesso alle sandbox non di produzione deve essere concesso da un amministratore di sistema, un amministratore di prodotto o un amministratore di profilo di prodotto tramite [Adobe Admin Console](https://adminconsole.adobe.com).

Per visualizzare, creare, aggiornare o eliminare sandbox non di produzione, è necessario concedere agli utenti anche le autorizzazioni di amministrazione sandbox.

Per ulteriori informazioni sulla gestione di ruoli e autorizzazioni per le sandbox, consulta la [panoramica sul controllo degli accessi](../access-control/home.md).

## Sandbox nell’interfaccia utente di Experience Platform

Nell’ [interfaccia utente di Experience Platform](https://platform.adobe.com), gli utenti possono passare dalle sandbox a cui hanno accesso utilizzando il controllo **commutatore sandbox** in alto a sinistra dello schermo.  Gli utenti con privilegi di amministrazione della sandbox possono inoltre accedere alla scheda **[!UICONTROL Sandboxes]** nella navigazione a sinistra, dove possono visualizzare e gestire le sandbox per la propria organizzazione. Per ulteriori informazioni su come utilizzare le sandbox nell&#39;interfaccia utente, consulta la [guida utente della sandbox](ui/overview.md).

## Sandbox nelle API di Experience Platform

Quando si effettuano chiamate alle API di Experience Platform, un nome sandbox deve essere fornito sotto l’intestazione `x-sandbox-name`. Ad esempio, quando effettui una chiamata a [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) per visualizzare tutti i set di dati all’interno della sandbox Produzione, il nome della sandbox (&quot;prod&quot;) viene fornito come intestazione nella richiesta API:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: prod'
```

Se `x-sandbox-name` non è incluso in una chiamata API, il sistema utilizza invece una sandbox predefinita. Tuttavia, la best practice consiste nell’includere sempre questa intestazione in tutte le chiamate API, anche quando si utilizza la sandbox predefinita. Per questo motivo, la documentazione API per Experience Platform tratta `x-sandbox-name` come un’intestazione obbligatoria.

### API sandbox

L’API Sandbox consente di gestire le sandbox utilizzando le operazioni API RESTful. Per informazioni dettagliate su come utilizzare l&#39;API, incluse le richieste formattate correttamente e le risposte di esempio, consulta la [guida per gli sviluppatori di sandbox](api/getting-started.md) .

## Passaggi successivi

Leggendo questo documento, ti sono stati presentati i concetti essenziali sulle sandbox in Experience Platform. Per passaggi dettagliati su come gestire le sandbox, consulta la [guida utente](ui/overview.md) per l’interfaccia utente o la [guida per gli sviluppatori](./api/getting-started.md) per l’API.

Mentre le sandbox fungono da strumento utile per isolare gli ambienti Platform per il team di sviluppo, puoi anche gestire un controllo degli accessi più granulare utilizzando Adobe Admin Console. Per ulteriori informazioni, consulta la [panoramica sul controllo degli accessi](../access-control/home.md) .
