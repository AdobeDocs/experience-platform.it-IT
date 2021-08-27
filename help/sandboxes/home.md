---
keywords: Experience Platform;home;argomenti popolari;sandbox;sandbox;test;test
solution: Experience Platform
title: Panoramica delle sandbox
topic-legacy: overview
description: Le sandbox sono partizioni virtuali all’interno di una singola istanza di Experience Platform, che consentono un’integrazione perfetta con il processo di sviluppo delle applicazioni di esperienza digitale.
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 0%

---

# Panoramica delle sandbox

Adobe Experience Platform è progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono provvedere allo sviluppo, al test e alla distribuzione di queste applicazioni, garantendo al contempo la conformità operativa.

Per soddisfare questa esigenza, Experience Platform fornisce sandbox che suddividono una singola istanza di Platform in ambienti virtuali separati per contribuire a sviluppare e sviluppare applicazioni di esperienza digitale.

Questo documento fornisce una panoramica di alto livello delle sandbox in Experience Platform.

## Informazioni sulle sandbox

Le sandbox sono partizioni virtuali all’interno di una singola istanza di Experience Platform, che consentono un’integrazione perfetta con il processo di sviluppo delle applicazioni di esperienza digitale. Tutti i contenuti e le azioni eseguite all’interno di una sandbox sono limitati a tale sandbox e non hanno alcun effetto su altre sandbox. Ad Experience Platform, sono supportati due tipi di sandbox:

* **Sandbox** di produzione: Una sandbox di produzione deve essere utilizzata con i profili nell’ambiente di produzione. Platform consente di creare più sandbox di produzione per fornire la funzionalità giusta per i dati mantenendo al tempo stesso l’isolamento operativo. Questa funzione consente di dedicare sandbox di produzione specifiche a linee di business, marchi, progetti o aree geografiche diverse. Le sandbox di produzione supportano un volume di profili di produzione fino all’impegno [!DNL Profile] concesso in licenza (misurato cumulativamente in tutte le sandbox di produzione autorizzate). Hai il diritto di utilizzare un profilo medio concesso in licenza per [!DNL Profile] autorizzato (misurato cumulativamente in tutte le sandbox di produzione autorizzate).
* **Sandbox** di sviluppo: Una sandbox di sviluppo è una sandbox che può essere utilizzata esclusivamente per lo sviluppo e il test con profili non di produzione. Le sandbox di sviluppo supportano un volume di profili non di produzione fino al 10% dell’impegno concesso in licenza [!DNL Profile] (misurato cumulativamente in tutte le sandbox di sviluppo autorizzate). Hai diritto fino a:
   * una ricchezza media di profilo non di produzione di 75 kilobyte per profilo non di produzione autorizzato (misurata cumulativamente in tutte le sandbox di sviluppo autorizzate);
   * Un processo di segmentazione batch al giorno, per sandbox di sviluppo;
   * Una media di 120 chiamate API [!DNL Profile] all&#39;anno, per [!DNL Profile] (misurate cumulativamente tra tutte le sandbox di sviluppo autorizzate.

Un’istanza di Experience Platform supporta più sandbox di produzione e sviluppo, con ogni sandbox che mantiene la propria libreria indipendente di risorse di Platform (inclusi schemi, set di dati, profili e così via). Inoltre, sia le sandbox di produzione che di sviluppo dispongono di una funzione di ripristino che rimuove tutte le risorse create dal cliente dalla sandbox. Non è possibile convertire le sandbox di sviluppo in sandbox di produzione.

Una licenza di Experience Platform predefinita ti concede un totale di cinque sandbox, che puoi classificare come produzione o sviluppo. È possibile concedere in licenza pacchetti aggiuntivi di 10 sandbox fino a un massimo di 75 sandbox in totale. Queste sandbox aggiuntive possono essere utilizzate per creare sandbox di produzione e di sviluppo. Per ulteriori informazioni, contatta l’amministratore dell’organizzazione IMS o il rappresentante commerciale di Adobe.

Infine, la sandbox di produzione predefinita è la prima sandbox di produzione che viene creata quando viene creata un’organizzazione IMS per la prima volta. La sandbox di produzione predefinita consente di acquisire o utilizzare dati da Platform, nonché di accettare richieste che non includono valori per un nome sandbox o un ID sandbox.

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

Nell’ [interfaccia utente di Experience Platform](https://platform.adobe.com), gli utenti possono passare dalle sandbox a cui hanno accesso utilizzando il controllo **commutatore sandbox** in alto a sinistra dello schermo.  Gli utenti con privilegi di amministrazione della sandbox possono inoltre accedere alla scheda **[!UICONTROL Sandbox]** nella navigazione a sinistra, dove possono visualizzare e gestire le sandbox per la loro organizzazione. Per ulteriori informazioni su come utilizzare le sandbox nell&#39;interfaccia utente, consulta la [guida utente della sandbox](ui/overview.md).

## Sandbox nelle API di Experience Platform

Quando si effettuano chiamate alle API di Experience Platform, un nome sandbox deve essere fornito sotto l’intestazione `x-sandbox-name`. Ad esempio, quando effettui una chiamata a [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) per visualizzare tutti i set di dati all’interno della sandbox Produzione, il nome della sandbox (&quot;prod&quot;) viene fornito come intestazione nella richiesta API:

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

L’API Sandbox consente di gestire le sandbox utilizzando le operazioni API RESTful. Per informazioni dettagliate su come utilizzare l&#39;API, incluse le richieste formattate correttamente e le risposte di esempio, consulta la [guida per gli sviluppatori di sandbox](api/overview.md) .

## Passaggi successivi

Leggendo questo documento, ti sono stati presentati i concetti essenziali sulle sandbox in Experience Platform. Per passaggi dettagliati su come gestire le sandbox, consulta la [guida utente](ui/overview.md) per l’interfaccia utente o la [guida per gli sviluppatori](./api/getting-started.md) per l’API.

Mentre le sandbox fungono da strumento utile per isolare gli ambienti Platform per il team di sviluppo, puoi anche gestire un controllo degli accessi più granulare utilizzando Adobe Admin Console. Per ulteriori informazioni, consulta la [panoramica sul controllo degli accessi](../access-control/home.md) .
