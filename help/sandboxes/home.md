---
keywords: Experience Platform;home;argomenti popolari;sandbox;sandbox;test;Testing
solution: Experience Platform
title: Panoramica sulle sandbox
description: Le sandbox sono partizioni virtuali all’interno di un’unica istanza di Experienci Platform, che consentono un’integrazione fluida con il processo di sviluppo delle applicazioni di esperienza digitale.
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: 06f1b64d5c4dfa6e0ca1f6da171ece8e9db9e693
workflow-type: tm+mt
source-wordcount: '991'
ht-degree: 0%

---

# Panoramica sulle sandbox

Adobe Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa.

Per soddisfare questa esigenza, Experienci Platform fornisce sandbox che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Questo documento fornisce una panoramica di alto livello delle sandbox in Experienci Platform.

## Informazioni sulle sandbox

Le sandbox sono partizioni virtuali all’interno di un’unica istanza di Experienci Platform, che consentono un’integrazione fluida con il processo di sviluppo delle applicazioni di esperienza digitale. Tutti i contenuti e le azioni eseguite all’interno di una sandbox sono limitati a tale sandbox e non influiscono su altre sandbox. Ad Experience Platform, sono supportati due tipi di sandbox:

* **Sandbox di produzione**: una sandbox di produzione deve essere utilizzata con i profili nell’ambiente di produzione. Platform consente di creare più sandbox di produzione per fornire la funzionalità giusta per i dati, mantenendo al contempo l’isolamento operativo. Questa funzione consente di dedicare specifiche sandbox di produzione a linee di business, marchi, progetti o aree geografiche distinte. Le sandbox di produzione supportano un volume di profili di produzione fino alla licenza [!DNL Profile] impegno (misurato cumulativamente in tutte le sandbox di produzione autorizzate). Hai diritto a utilizzare il profilo medio concesso in licenza per ogni [!DNL Profile] (misurato cumulativamente in tutte le sandbox di produzione autorizzate).
* **Sandbox di sviluppo**: una sandbox di sviluppo è una sandbox che può essere utilizzata esclusivamente per lo sviluppo e il test con profili non di produzione. Le sandbox di sviluppo supportano un volume di profili non di produzione fino al 10% del [!DNL Profile] impegno (misurato cumulativamente in tutte le sandbox di sviluppo autorizzate). Hai diritto a:
   * Una ricchezza media di profilo non di produzione di 75 kilobyte per profilo non di produzione autorizzato (misurata cumulativamente in tutte le sandbox di sviluppo autorizzate);
   * Un processo di segmentazione batch al giorno, per sandbox di sviluppo;
   * Una media di 120 [!DNL Profile] Chiamate API, per [!DNL Profile], all’anno (misurato cumulativamente in tutte le sandbox di sviluppo autorizzate.

Un’istanza di Experience Platform supporta più sandbox di produzione e sviluppo, ognuna delle quali mantiene la propria libreria indipendente di risorse Platform (inclusi schemi, set di dati, profili e così via). Inoltre, sia le sandbox di produzione che quelle di sviluppo dispongono di una funzione di ripristino che rimuove tutte le risorse create dal cliente dalla sandbox. Le sandbox di sviluppo non possono essere convertite in sandbox di produzione.

Una licenza di Experience Platform predefinita ti concede un totale di cinque sandbox, che puoi classificare come produzione o sviluppo. Puoi concedere in licenza pacchetti aggiuntivi di 10 sandbox per un massimo di 75 sandbox in totale. Queste sandbox aggiuntive possono essere utilizzate per creare sandbox di produzione e di sviluppo. Per ulteriori informazioni, contatta l’amministratore dell’organizzazione o il rappresentante commerciale Adobe.

Infine, la sandbox di produzione predefinita è la prima sandbox di produzione creata al momento della creazione di un’organizzazione. La sandbox di produzione predefinita consente di acquisire o utilizzare dati da Platform, nonché di accettare richieste che non includono valori per il nome di una sandbox o l’ID di una sandbox.

>[!NOTE]
>
>La prima volta che viene creata una sandbox, non contiene dati. Poiché ogni sandbox mantiene il proprio archivio dati isolato, deve acquisire i dati in modo indipendente.

In sintesi, le sandbox offrono i seguenti vantaggi:

* **Gestione del ciclo di vita delle applicazioni**: crea ambienti virtuali separati per sviluppare ed evolvere applicazioni di esperienza digitale.
* **Gestione di progetti e marchi**: consente l’esecuzione in parallelo di più progetti all’interno della stessa organizzazione, garantendo al contempo l’isolamento e il controllo degli accessi.
* **Ecosistema di sviluppo flessibile**: fornisce ambienti sandbox in modo semplice, scalabile e conveniente a scopo di esplorazione, abilitazione e dimostrazione.

## Controllo degli accessi per le sandbox

Per impostazione predefinita, tutti gli utenti di un’organizzazione hanno accesso a una sandbox di produzione. L’accesso alle sandbox non di produzione deve essere concesso da un amministratore di sistema, un amministratore di prodotto o un amministratore del profilo di prodotto tramite [Adobe Admin Console](https://adminconsole.adobe.com).

Per visualizzare, creare, aggiornare o eliminare sandbox non di produzione, è necessario concedere agli utenti anche le autorizzazioni di amministrazione delle sandbox.

Per ulteriori informazioni sulla gestione di ruoli e autorizzazioni per le sandbox, consulta [panoramica sul controllo degli accessi](../access-control/home.md).

## Sandbox nell’interfaccia utente di Experienci Platform

In [Interfaccia utente di Experienci Platform](https://platform.adobe.com), gli utenti possono passare dalle sandbox a cui hanno accesso utilizzando **commutatore sandbox** in alto a sinistra sullo schermo.  Gli utenti con privilegi di amministrazione Sandbox possono inoltre accedere a **[!UICONTROL Sandbox]** nella barra di navigazione a sinistra, per visualizzare e gestire le sandbox per la propria organizzazione. Per ulteriori informazioni su come utilizzare le sandbox nell’interfaccia utente, consulta la sezione [guida utente sulle sandbox](ui/overview.md).

## Sandbox nelle API di Experienci Platform

Quando si effettuano chiamate alle API Experienci Platform, è necessario fornire un nome sandbox sotto l’intestazione `x-sandbox-name`. Ad esempio, quando effettui una chiamata al [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) per visualizzare tutti i set di dati all’interno della sandbox di produzione, il nome della sandbox (&quot;prod&quot;) viene fornito come intestazione nella richiesta API:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: prod'
```

Se `x-sandbox-name` non è incluso in una chiamata API, il sistema utilizzerà invece una sandbox predefinita. Tuttavia, la best practice prevede di includere sempre questa intestazione in tutte le chiamate API, anche quando si utilizza la sandbox predefinita. Per questo motivo, ad Experience Platform, nella documentazione dell’API vengono trattati i seguenti aspetti: `x-sandbox-name` come intestazione obbligatoria.

### API sandbox

L’API Sandbox consente di gestire le sandbox utilizzando le operazioni API RESTful. Consulta la [guida per gli sviluppatori sulle sandbox](api/overview.md) per informazioni dettagliate su come utilizzare l’API, incluse richieste formattate correttamente e risposte di esempio.

## Passaggi successivi

Una volta letto questo documento, avrai introdotto i concetti essenziali relativi alle sandbox in questo Experience Platform. Per i passaggi dettagliati su come gestire le sandbox, consulta la [guida utente](ui/overview.md) per l’interfaccia o [guida per sviluppatori](./api/getting-started.md) per l’API.

Anche se le sandbox sono uno strumento utile per isolare gli ambienti Platform per il team di sviluppo, puoi anche gestire un controllo degli accessi più granulare utilizzando Adobe Admin Console. Consulta la [panoramica sul controllo degli accessi](../access-control/home.md) per ulteriori informazioni.
