---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Elaborazione delle richieste di privacy in Real-time Customer Profile
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---


# Elaborazione delle richieste di privacy in Real-time Customer Profile

 Adobe Experience Platform Privacy Service elabora le richieste dei clienti di accedere, rifiutare la vendita o cancellare i loro dati personali, come delineato dalle normative sulla privacy, come il General Data Protection Regulation (GDPR) e il California Consumer Privacy Act (CCPA).

Questo documento tratta i concetti essenziali relativi all&#39;elaborazione delle richieste di privacy per il profilo cliente in tempo reale.

## Introduzione

Prima di leggere questa guida, è consigliabile avere una conoscenza approfondita dei seguenti servizi  Experience Platform:

* [Privacy Service](home.md): Gestisce le richieste dei clienti relative all&#39;accesso, al rifiuto della vendita o all&#39;eliminazione dei loro dati personali tra le applicazioni Adobe Experience Cloud.
* [Servizio](../identity-service/home.md)identità: Risolve la sfida fondamentale rappresentata dalla frammentazione dei dati relativi all&#39;esperienza dei clienti attraverso il collegamento di identità tra dispositivi e sistemi.
* [Profilo](../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Informazioni sugli spazi dei nomi delle identità {#namespaces}

 Adobe Experience Platform Identity Service collega i dati di identità dei clienti tra sistemi e dispositivi. Identity Service utilizza gli spazi dei nomi **di identità** per fornire contesto ai valori di identità collegandoli al proprio sistema di origine. Uno spazio dei nomi può rappresentare un concetto generico come un indirizzo e-mail (&quot;E-mail&quot;) o associare l&#39;identità a un&#39;applicazione specifica, ad esempio un Adobe  Advertising Cloud ID (&quot;AdCloud&quot;) o un  Adobe Target ID (&quot;TNTID&quot;).

Servizio identità mantiene un archivio di spazi dei nomi di identità globali (standard) e definiti dall’utente (personalizzati). Gli spazi dei nomi standard sono disponibili per tutte le organizzazioni (ad esempio, &quot;E-mail&quot; e &quot;ECID&quot;), mentre l&#39;organizzazione può anche creare spazi dei nomi personalizzati in base alle proprie esigenze.

Per ulteriori informazioni sugli spazi dei nomi di identità in  Experience Platform, consultate la panoramica [dello spazio dei nomi](../identity-service/namespaces.md)identità.

## Invio di richieste {#submit}

>[!NOTE]
>
>Questa sezione descrive come creare richieste di privacy per l’archivio dati del profilo. È vivamente consigliato di consultare la documentazione API [](../privacy-service/api/getting-started.md) Privacy Service o dell’interfaccia utente [](../privacy-service/ui/overview.md) Privacy Service per i passaggi completi relativi all’invio di un processo per la privacy, incluso il modo in cui formattare correttamente i dati di identità dell’utente inviati nei payload di richieste.

Nella sezione seguente viene illustrato come effettuare richieste di privacy per Real-time Customer Profile (Profilo cliente in tempo reale) e Data Lake mediante l&#39;API o l&#39;interfaccia utente di Privacy Service.

### Utilizzo dell&#39;API

Quando si creano richieste di processo nell&#39;API, tutte le `userIDs` richieste fornite devono utilizzare un archivio dati specifico `namespace` e `type` a seconda dell&#39;archivio dati a cui si riferiscono. Gli ID per l&#39;archivio profili devono utilizzare &quot;standard&quot; o &quot;personalizzati&quot; per il loro `type` valore, e uno spazio dei nomi [di](#namespaces) identità valido riconosciuto dal servizio identità per il loro `namespace` valore.


Inoltre, l&#39; `include` array del payload della richiesta deve includere i valori prodotto per i diversi data store a cui viene effettuata la richiesta. Quando si effettuano richieste al Data Lake, l&#39;array deve includere il valore &quot;ProfileService&quot;.

La richiesta seguente crea un nuovo processo per la privacy sia per il profilo cliente in tempo reale, utilizzando lo spazio dei nomi di identità &quot;E-mail&quot; standard. Include inoltre il valore prodotto per Profile nell&#39; `include` array:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "Email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService", "aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

### Utilizzo dell’interfaccia

Durante la creazione di richieste di lavoro nell’interfaccia utente, accertatevi di selezionare **AEP Data Lake** e/o **Profile** in _Products_ , rispettivamente, per elaborare i processi per i dati memorizzati nel Data Lake o nel Real-time Customer Profile.

<img src="images/privacy/product-value.png" width="450"><br>

## Elimina elaborazione richiesta

Quando  Experience Platform riceve una richiesta di eliminazione da Privacy Service, Platform invia ad Privacy Service la conferma che la richiesta è stata ricevuta e che i dati interessati sono stati contrassegnati per l’eliminazione. I record vengono quindi rimossi dal Data Lake o dall&#39;archivio dei profili entro sette giorni. Durante la finestra di sette giorni, i dati vengono eliminati in modo morbido e pertanto non sono accessibili da alcun servizio Platform.

Nelle release future, Platform invierà una conferma ad Privacy Service dopo che i dati saranno stati fisicamente eliminati.

## Passaggi successivi

Leggendo questo documento, è stato introdotto l&#39;importante concetto relativo all&#39;elaborazione delle richieste di privacy in  Experience Platform. Si consiglia di continuare a leggere la documentazione fornita in questa guida per approfondire la conoscenza su come gestire i dati di identità e creare processi di privacy.

Per informazioni sull&#39;elaborazione delle richieste di privacy per le risorse Platform non utilizzate da Profile, consultare il documento relativo all&#39;elaborazione delle richieste di [privacy nel Data Lake](../catalog/privacy.md).