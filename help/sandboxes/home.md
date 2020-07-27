---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica sulle sandbox
topic: overview
translation-type: tm+mt
source-git-commit: c52d8cdbc5a4ee6fab8c2b1b284efea5f735d424
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 0%

---


# Panoramica sulle sandbox

 Adobe Experience Platform è stato creato per arricchire le applicazioni per esperienze digitali su scala globale. Le aziende spesso eseguono più applicazioni di esperienza digitale in parallelo e devono provvedere allo sviluppo, al test e all&#39;implementazione di tali applicazioni, garantendo al contempo la conformità operativa.

Per rispondere a questa esigenza,  Experience Platform fornisce **sandbox** che dividono una singola istanza di Platform in ambienti virtuali separati per contribuire allo sviluppo e all&#39;evoluzione di applicazioni per esperienze digitali.

Questo documento fornisce una panoramica di alto livello delle sandbox in  Experience Platform.

## Informazioni sulle sandbox

Le sandbox sono partizioni virtuali all&#39;interno di un&#39;unica istanza di  Experience Platform, che consentono un&#39;integrazione perfetta con il processo di sviluppo delle applicazioni di esperienza digitale. Un&#39;istanza di Experience Platform  supporta una sandbox di produzione e più sandbox non di produzione, con ciascuna sandbox che mantiene una propria libreria indipendente di risorse Platform (inclusi schemi, set di dati, profili e così via).  Tutti i contenuti e le azioni effettuate all’interno di una sandbox sono limitati a tale sandbox e non hanno effetto su altre sandbox.

Le sandbox non di produzione consentono di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sulla sandbox di produzione. Inoltre, le sandbox non di produzione dispongono di una funzione di ripristino che rimuove tutte le risorse create dal cliente dalla sandbox. I sandbox non di produzione non possono essere convertiti in sandbox di produzione.

>[!NOTE]
>
>Quando viene creata per la prima volta una sandbox non contiene dati. Poiché ogni sandbox mantiene un proprio archivio dati isolato, deve anche acquisire i dati in modo indipendente.

In sintesi, le sandbox offrono i seguenti vantaggi:

* **Gestione** del ciclo di vita dell’applicazione: Creare ambienti virtuali separati per sviluppare e sviluppare applicazioni per esperienze digitali.
* **Gestione** del progetto e del marchio: Consentire l&#39;esecuzione parallela di più progetti all&#39;interno della stessa organizzazione IMS, fornendo al contempo l&#39;isolamento e il controllo dell&#39;accesso. Le release future offriranno supporto per l&#39;implementazione in più aree.
* **Ecosistema** di sviluppo flessibile: Fornite sandbox in modo semplice, scalabile e conveniente per scopi di esplorazione, abilitazione e dimostrazione.

## Controllo di accesso per le sandbox

Per impostazione predefinita, tutti gli utenti di un&#39;organizzazione hanno accesso a una sandbox di produzione. L&#39;accesso alle sandbox non di produzione deve essere concesso da un amministratore di sistema, un amministratore di prodotto o un amministratore di profilo di prodotto tramite [Adobe Admin Console](https://adminconsole.adobe.com).

Per visualizzare, creare, aggiornare o eliminare sandbox non di produzione, agli utenti devono anche essere concesse autorizzazioni di amministrazione sandbox.

Per ulteriori informazioni sulla gestione di ruoli e autorizzazioni per le sandbox, consultate la panoramica [del controllo di](../access-control/home.md)accesso.

## Sandbox nell’interfaccia  di Experience Platform

Nell&#39;interfaccia [utente](https://platform.adobe.com)Experience Platform, gli utenti possono passare dalle sandbox a cui hanno accesso utilizzando il controllo **sandbox switcher** in alto a sinistra dello schermo.  Gli utenti con privilegi di amministrazione sandbox possono accedere anche alla **[!UICONTROL Sandboxes]** scheda nella navigazione a sinistra, dove possono visualizzare e gestire le sandbox per la propria organizzazione. Per ulteriori informazioni sull’utilizzo delle sandbox nell’interfaccia utente, consultate la guida [utente alla](ui/overview.md)sandbox.

## Sandbox in  API Experience Platform

Quando si effettuano chiamate a  API Experience Platform, è necessario fornire un nome sandbox sotto l&#39;intestazione `x-sandbox-name`. Ad esempio, quando si effettua una chiamata [!DNL Catalog Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) per visualizzare tutti i set di dati nella sandbox Produzione, il nome della sandbox (&quot;prod&quot;) viene fornito come intestazione nella richiesta API:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: prod'
```

Se non `x-sandbox-name` è inclusa in una chiamata API, il sistema utilizzerà una sandbox predefinita. Tuttavia, la procedura consigliata consiste nell’includere sempre questa intestazione in tutte le chiamate API, anche quando si utilizza la sandbox predefinita. Per questo motivo, la documentazione API per  Experience Platform viene trattata `x-sandbox-name` come un&#39;intestazione obbligatoria.

### API sandbox

L&#39;API Sandbox consente di gestire le sandbox utilizzando le operazioni RESTful API. Per informazioni dettagliate sull&#39;utilizzo dell&#39;API, comprese le richieste formattate correttamente e le risposte di esempio, consultate la guida [per gli sviluppatori](api/getting-started.md) sandbox.

## Passaggi successivi

Leggendo questo documento, avete introdotto i concetti fondamentali sulle sandbox in  Experience Platform. Per i passaggi dettagliati su come gestire le sandbox, consultate la guida [](ui/overview.md) utente per l&#39;interfaccia utente o la guida [](./api/getting-started.md) per gli sviluppatori per l&#39;API.

Le sandbox fungono da strumento prezioso per isolare gli ambienti Platform per il team di sviluppo, ma è anche possibile gestire un controllo degli accessi più dettagliato utilizzando Adobe Admin Console. Per ulteriori informazioni, consulta la panoramica [sul controllo](../access-control/home.md) degli accessi.