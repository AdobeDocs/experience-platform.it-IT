---
keywords: Experience Platform;home;argomenti popolari;sandbox;sandbox;test;test
solution: Experience Platform
title: Panoramica delle sandbox
description: Le sandbox sono partizioni virtuali all’interno di una singola istanza di Experience Platform, che consentono un’integrazione perfetta con il processo di sviluppo delle applicazioni di esperienza digitale.
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 0%

---

# Panoramica delle sandbox

Adobe Experience Platform è progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono provvedere allo sviluppo, al test e alla distribuzione di queste applicazioni, garantendo al contempo la conformità operativa.

Per soddisfare questa esigenza, Experience Platform fornisce sandbox che suddividono una singola istanza di Platform in ambienti virtuali separati per contribuire a sviluppare e sviluppare applicazioni di esperienza digitale.

Questo documento fornisce una panoramica di alto livello delle sandbox in Experience Platform.

## Informazioni sulle sandbox

Le sandbox sono partizioni virtuali all’interno di una singola istanza di Experience Platform, che consentono un’integrazione perfetta con il processo di sviluppo delle applicazioni di esperienza digitale. Tutti i contenuti e le azioni eseguite all’interno di una sandbox sono limitati a tale sandbox e non hanno alcun effetto su altre sandbox. Ad Experience Platform, sono supportati due tipi di sandbox:

* **Sandbox di produzione**: Una sandbox di produzione deve essere utilizzata con i profili nell’ambiente di produzione. Platform consente di creare più sandbox di produzione per fornire la funzionalità giusta per i dati mantenendo al tempo stesso l’isolamento operativo. Questa funzione consente di dedicare sandbox di produzione specifiche a linee di business, marchi, progetti o aree geografiche diverse. Le sandbox di produzione supportano un volume di profili di produzione fino al vostro sotto licenza [!DNL Profile] impegno (misurato cumulativamente in tutte le sandbox di produzione autorizzate). Hai il diritto di utilizzare il profilo medio concesso in licenza per ogni autorizzato [!DNL Profile] (misurato cumulativamente in tutte le sandbox di produzione autorizzate).
* **Sandbox di sviluppo**: Una sandbox di sviluppo è una sandbox che può essere utilizzata esclusivamente per lo sviluppo e il test con profili non di produzione. Le sandbox di sviluppo supportano un volume di profili non di produzione fino al 10% della licenza [!DNL Profile] impegno (misurato cumulativamente in tutte le sandbox di sviluppo autorizzate). Hai diritto fino a:
   * una ricchezza media di profilo non di produzione di 75 kilobyte per profilo non di produzione autorizzato (misurata cumulativamente in tutte le sandbox di sviluppo autorizzate);
   * Un processo di segmentazione batch al giorno, per sandbox di sviluppo;
   * Una media di 120 [!DNL Profile] Chiamate API, per [!DNL Profile], per anno (misurato cumulativamente in tutte le sandbox di sviluppo autorizzate.

Un’istanza di Experience Platform supporta più sandbox di produzione e sviluppo, con ogni sandbox che mantiene la propria libreria indipendente di risorse di Platform (inclusi schemi, set di dati, profili e così via). Inoltre, sia le sandbox di produzione che di sviluppo dispongono di una funzione di ripristino che rimuove tutte le risorse create dal cliente dalla sandbox. Non è possibile convertire le sandbox di sviluppo in sandbox di produzione.

Una licenza di Experience Platform predefinita ti concede un totale di cinque sandbox, che puoi classificare come produzione o sviluppo. È possibile concedere in licenza pacchetti aggiuntivi di 10 sandbox fino a un massimo di 75 sandbox in totale. Queste sandbox aggiuntive possono essere utilizzate per creare sandbox di produzione e di sviluppo. Per ulteriori informazioni, contatta l’amministratore dell’organizzazione o il rappresentante commerciale di Adobe.

Infine, la sandbox di produzione predefinita è la prima sandbox di produzione che viene creata quando un&#39;organizzazione viene creata per la prima volta. La sandbox di produzione predefinita consente di acquisire o utilizzare dati da Platform, nonché di accettare richieste che non includono valori per un nome sandbox o un ID sandbox.

>[!NOTE]
>
>Quando viene creata una sandbox, non contiene dati. Poiché ogni sandbox mantiene il proprio archivio dati isolato, deve anche acquisire i propri dati in modo indipendente.

In sintesi, le sandbox offrono i seguenti vantaggi:

* **Gestione del ciclo di vita delle applicazioni**: Creare ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.
* **Gestione di progetti e marchi**: Consente l’esecuzione parallela di più progetti all’interno della stessa organizzazione, garantendo al contempo l’isolamento e il controllo degli accessi. Le versioni future supporteranno l’implementazione in più aree geografiche.
* **Ecosistema di sviluppo flessibile**: Fornisci sandbox in modo semplice, scalabile e conveniente per scopi di esplorazione, abilitazione e dimostrazione.

## Controllo degli accessi per le sandbox

Per impostazione predefinita, tutti gli utenti di un&#39;organizzazione hanno accesso a una sandbox di produzione. L’accesso alle sandbox non di produzione deve essere concesso da un amministratore di sistema, un amministratore di prodotto o un amministratore di profilo di prodotto tramite [Adobe Admin Console](https://adminconsole.adobe.com).

Per visualizzare, creare, aggiornare o eliminare sandbox non di produzione, è necessario concedere agli utenti anche le autorizzazioni di amministrazione sandbox.

Per ulteriori informazioni sulla gestione di ruoli e autorizzazioni per le sandbox, consulta la sezione [panoramica sul controllo degli accessi](../access-control/home.md).

## Sandbox nell’interfaccia utente di Experience Platform

In [Interfaccia utente di Experience Platform](https://platform.adobe.com), gli utenti possono passare dalle sandbox a cui hanno accesso utilizzando il **commutatore sandbox** in alto a sinistra sullo schermo.  Gli utenti con privilegi di amministrazione della sandbox hanno anche accesso alla **[!UICONTROL Sandbox]** nella navigazione a sinistra, dove possono visualizzare e gestire le sandbox per la loro organizzazione. Per ulteriori informazioni su come utilizzare le sandbox nell’interfaccia utente, consulta la sezione [guida utente sandbox](ui/overview.md).

## Sandbox nelle API di Experience Platform

Quando si effettuano chiamate alle API di Experience Platform, un nome sandbox deve essere fornito sotto l’intestazione `x-sandbox-name`. Ad esempio, quando effettui una chiamata al [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) per visualizzare tutti i set di dati all’interno della sandbox di produzione, il nome della sandbox (&quot;prod&quot;) viene fornito come intestazione nella richiesta API:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: prod'
```

Se `x-sandbox-name` non è incluso in una chiamata API, il sistema utilizza invece una sandbox predefinita. Tuttavia, la best practice consiste nell’includere sempre questa intestazione in tutte le chiamate API, anche quando si utilizza la sandbox predefinita. Per questo motivo, la documentazione API per Experience Platform tratta `x-sandbox-name` come intestazione obbligatoria.

### API sandbox

L’API Sandbox consente di gestire le sandbox utilizzando le operazioni API RESTful. Consulta la sezione [guida per sviluppatori di sandbox](api/overview.md) per informazioni dettagliate su come utilizzare l’API, incluse richieste formattate correttamente e risposte di esempio.

## Passaggi successivi

Leggendo questo documento, ti sono stati presentati i concetti essenziali sulle sandbox in Experience Platform. Per i passaggi dettagliati su come gestire le sandbox, consulta la sezione [guida utente](ui/overview.md) per l’interfaccia utente o [guida per sviluppatori](./api/getting-started.md) per l’API .

Mentre le sandbox fungono da strumento utile per isolare gli ambienti Platform per il team di sviluppo, puoi anche gestire un controllo degli accessi più granulare utilizzando Adobe Admin Console. Consulta la sezione [panoramica sul controllo degli accessi](../access-control/home.md) per ulteriori informazioni.
