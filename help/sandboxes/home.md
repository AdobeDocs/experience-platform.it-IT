---
keywords: Experience Platform;home;argomenti popolari;sandbox;sandbox;test;Test;;home;popular topic;sandbox;Sandbox;testing;Testing
solution: Experience Platform
title: Panoramica sulle sandbox
description: Le sandbox sono partizioni virtuali all’interno di una singola istanza di Experience Platform, che consentono un’integrazione perfetta con il processo di sviluppo delle applicazioni di esperienza digitale.
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 2%

---

# Panoramica sulle sandbox

Adobe Experience Platform è stato progettato per arricchire le applicazioni di esperienza digitale su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono occuparsi di sviluppo, test e distribuzione di tali applicazioni, garantendo al contempo la conformità operativa.

Per soddisfare questa esigenza, Experience Platform fornisce ambienti sandbox che permettono di suddividere una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

Questo documento fornisce una panoramica di alto livello delle sandbox in Experience Platform.

## Informazioni sulle sandbox

Le sandbox sono partizioni virtuali all’interno di una singola istanza di Experience Platform, che consentono un’integrazione perfetta con il processo di sviluppo delle applicazioni di esperienza digitale. Tutti i contenuti e le azioni eseguite all’interno di una sandbox sono limitati a tale sandbox e non influiscono su altre sandbox. In Experience Platform sono supportati due tipi di sandbox:

* **Sandbox di produzione**: una sandbox di produzione deve essere utilizzata con i profili nell&#39;ambiente di produzione. Experience Platform consente di creare più sandbox di produzione per fornire la funzionalità giusta per i dati, mantenendo al contempo l’isolamento operativo. Questa funzione consente di dedicare specifiche sandbox di produzione a linee di business, marchi, progetti o aree geografiche distinte. Le sandbox di produzione supportano un volume di profili di produzione fino all&#39;impegno [!DNL Profile] concesso in licenza (misurato cumulativamente in tutte le sandbox di produzione autorizzate). Hai diritto a utilizzare l’intero volume totale di dati concesso in licenza (misurato cumulativamente in tutte le sandbox di produzione autorizzate).

* **Sandbox di sviluppo**: una sandbox di sviluppo è una sandbox che può essere utilizzata esclusivamente per lo sviluppo e il test con profili non di produzione. Le sandbox di sviluppo supportano un volume di profili non di produzione fino al 10% dell&#39;impegno [!DNL Profile] concesso in licenza (misurato cumulativamente in tutte le sandbox di sviluppo autorizzate). Hai diritto a:
   * Un processo di segmentazione batch al giorno, per sandbox di sviluppo;
   * Una media di 120 chiamate API [!DNL Profile], per [!DNL Profile], all&#39;anno (misurata cumulativamente in tutte le sandbox di sviluppo autorizzate.

Un’istanza di Experience Platform supporta più sandbox di produzione e sviluppo; ogni sandbox mantiene la propria libreria indipendente di risorse di Experience Platform (inclusi schemi, set di dati, profili e così via). Inoltre, sia le sandbox di produzione che quelle di sviluppo dispongono di una funzione di ripristino che rimuove tutte le risorse create dal cliente dalla sandbox. Le sandbox di sviluppo non possono essere convertite in sandbox di produzione.

Una licenza Experience Platform predefinita ti consente di ottenere un totale di cinque sandbox, che puoi classificare come produzione o sviluppo. Puoi concedere in licenza pacchetti aggiuntivi di 10 sandbox per un massimo di 75 sandbox in totale. Queste sandbox aggiuntive possono essere utilizzate per creare sandbox di produzione e di sviluppo. Per ulteriori informazioni, contatta l’amministratore dell’organizzazione o il rappresentante commerciale Adobe.

Infine, la sandbox di produzione predefinita è la prima sandbox di produzione creata al momento della creazione di un’organizzazione. La sandbox di produzione predefinita consente di acquisire o utilizzare dati da Experience Platform, nonché di accettare richieste che non includono valori per il nome di una sandbox o per un ID di sandbox.

>[!NOTE]
>
>La prima volta che viene creata una sandbox, non contiene dati. Poiché ogni sandbox mantiene il proprio archivio dati isolato, deve acquisire i dati in modo indipendente.

In sintesi, le sandbox offrono i seguenti vantaggi:

* **Gestione del ciclo di vita delle applicazioni**: creare ambienti virtuali separati per sviluppare ed evolvere le applicazioni di esperienza digitale.
* **Gestione di progetti e marchi**: consente l&#39;esecuzione in parallelo di più progetti all&#39;interno della stessa organizzazione, garantendo al contempo l&#39;isolamento e il controllo degli accessi.
* **Ecosistema di sviluppo flessibile**: fornisce sandbox in modo semplice, scalabile e conveniente a scopo di esplorazione, abilitazione e dimostrazione.

## Controllo degli accessi per le sandbox

Per impostazione predefinita, tutti gli utenti di un’organizzazione hanno accesso a una sandbox di produzione. L&#39;accesso alle sandbox non di produzione deve essere concesso da un amministratore di sistema, un amministratore di prodotto o un amministratore del profilo di prodotto tramite [Adobe Admin Console](https://adminconsole.adobe.com).

Per visualizzare, creare, aggiornare o eliminare sandbox non di produzione, è necessario concedere agli utenti anche le autorizzazioni di amministrazione delle sandbox.

Per ulteriori informazioni sulla gestione di ruoli e autorizzazioni per le sandbox, vedere [panoramica sul controllo degli accessi](../access-control/home.md).

## Sandbox nell’interfaccia utente di Experience Platform

Nell&#39;interfaccia utente di [Experience Platform](https://platform.adobe.com), gli utenti possono passare dalle sandbox a cui hanno accesso utilizzando il controllo **commutatore sandbox** in alto a sinistra dello schermo.  Gli utenti con privilegi di amministrazione della sandbox possono inoltre accedere alla scheda **[!UICONTROL Sandbox]** nella navigazione a sinistra, dove possono visualizzare e gestire le sandbox per la propria organizzazione. Per ulteriori informazioni su come utilizzare le sandbox nell&#39;interfaccia utente, consulta la [guida utente sulle sandbox](ui/overview.md).

## Sandbox nelle API di Experience Platform

Quando si effettuano chiamate alle API di Experience Platform, è necessario fornire un nome di sandbox sotto l&#39;intestazione `x-sandbox-name`. Ad esempio, quando si effettua una chiamata a [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) per visualizzare tutti i set di dati all&#39;interno della sandbox di produzione, il nome della sandbox (&quot;prod&quot;) viene fornito come intestazione nella richiesta API:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: prod'
```

Se `x-sandbox-name` non è incluso in una chiamata API, il sistema utilizzerà una sandbox predefinita. Tuttavia, la best practice prevede di includere sempre questa intestazione in tutte le chiamate API, anche quando si utilizza la sandbox predefinita. Per questo motivo, la documentazione API per Experience Platform considera `x-sandbox-name` come intestazione obbligatoria.

### API sandbox

L’API Sandbox consente di gestire le sandbox utilizzando le operazioni API RESTful. Consulta la [guida per gli sviluppatori di sandbox](api/overview.md) per informazioni dettagliate su come utilizzare l&#39;API, incluse richieste formattate correttamente e risposte di esempio.

## Passaggi successivi

Una volta letto questo documento, avrai introdotto i concetti essenziali relativi alle sandbox in Experience Platform. Per i passaggi dettagliati su come gestire le sandbox, consulta la [guida utente](ui/overview.md) per l&#39;interfaccia utente o la [guida per sviluppatori](./api/getting-started.md) per l&#39;API.

Le sandbox sono uno strumento utile per isolare gli ambienti Experience Platform per il team di sviluppo, ma puoi anche gestire un controllo degli accessi più granulare utilizzando Adobe Admin Console. Per ulteriori informazioni, vedere [panoramica sul controllo degli accessi](../access-control/home.md).
