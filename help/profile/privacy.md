---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Elaborazione delle richieste di privacy in Real-time Customer Profile
topic: overview
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 0%

---


# Elaborazione delle richieste di privacy in [!DNL Real-time Customer Profile]

 Adobe Experience Platform [!DNL Privacy Service] elabora le richieste dei clienti di accedere, rifiutare la vendita o cancellare i propri dati personali, come delineato dalle normative sulla privacy, quali il Regolamento generale sulla protezione dei dati (General Data Protection Regulation, GDPR) e [!DNL California Consumer Privacy Act] (CCPA).

Il presente documento illustra i concetti essenziali relativi all’elaborazione delle richieste di privacy per [!DNL Real-time Customer Profile].

## Introduzione

Prima di leggere la presente guida è consigliabile conoscere i seguenti [!DNL Experience Platform] servizi:

* [!DNL Privacy Service](home.md): Gestisce le richieste dei clienti relative all&#39;accesso, al rifiuto della vendita o all&#39;eliminazione dei loro dati personali tra le applicazioni Adobe Experience Cloud.
* [!DNL Identity Service](../identity-service/home.md): Risolve la sfida fondamentale rappresentata dalla frammentazione dei dati relativi all&#39;esperienza dei clienti attraverso il collegamento di identità tra dispositivi e sistemi.
* [!DNL Real-time Customer Profile](../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Informazioni sugli spazi dei nomi delle identità {#namespaces}

 Adobe Experience Platform [!DNL Identity Service] collega i dati di identità dei clienti tra sistemi e dispositivi. [!DNL Identity Service] utilizza gli spazi dei nomi di **identità** per fornire contesto ai valori di identità collegandoli al loro sistema di origine. Uno spazio dei nomi può rappresentare un concetto generico come un indirizzo e-mail (&quot;E-mail&quot;) o associare l&#39;identità a un&#39;applicazione specifica, ad esempio un Adobe  Advertising Cloud ID (&quot;AdCloud&quot;) o un  Adobe Target ID (&quot;TNTID&quot;).

Servizio identità mantiene un archivio di spazi dei nomi di identità globali (standard) e definiti dall’utente (personalizzati). Gli spazi dei nomi standard sono disponibili per tutte le organizzazioni (ad esempio, &quot;E-mail&quot; e &quot;ECID&quot;), mentre l&#39;organizzazione può anche creare spazi dei nomi personalizzati in base alle proprie esigenze.

Per ulteriori informazioni sugli spazi dei nomi delle identità in [!DNL Experience Platform], vedere la panoramica [dello spazio dei nomi](../identity-service/namespaces.md)delle identità.

## Invio di richieste {#submit}

>[!NOTE]
>
>In questa sezione viene illustrato come creare richieste di privacy per l&#39;archivio [!DNL Profile] dati. È vivamente consigliato di consultare la documentazione API [](../privacy-service/api/getting-started.md) Privacy Service o dell’interfaccia utente [](../privacy-service/ui/overview.md) Privacy Service per i passaggi completi relativi all’invio di un processo per la privacy, incluso il modo in cui formattare correttamente i dati di identità dell’utente inviati nei payload di richieste.

Nella sezione seguente viene illustrato come effettuare richieste di privacy per [!DNL Real-time Customer Profile] e [!DNL Data Lake] tramite l&#39; [!DNL Privacy Service] API o l&#39;interfaccia utente.

### Utilizzo dell&#39;API

Quando si creano richieste di processo nell&#39;API, tutte le `userIDs` richieste fornite devono utilizzare un archivio dati specifico `namespace` e `type` a seconda dell&#39;archivio dati a cui si riferiscono. Gli ID per lo [!DNL Profile] store devono utilizzare &quot;standard&quot; o &quot;custom&quot; per il loro `type` valore, e uno spazio dei nomi [di](#namespaces) identità valido riconosciuto [!DNL Identity Service] per il loro `namespace` valore.


Inoltre, l&#39; `include` array del payload della richiesta deve includere i valori prodotto per i diversi data store a cui viene effettuata la richiesta. Quando si effettuano richieste al [!DNL Data Lake], l&#39;array deve includere il valore &quot;ProfileService&quot;.

La richiesta seguente crea un nuovo processo di privacy per entrambi [!DNL Real-time Customer Profile], utilizzando lo spazio dei nomi di identità &quot;Email&quot; standard. Include inoltre il valore prodotto per [!DNL Profile] nell&#39; `include` array:

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

Quando create richieste di processo nell’interfaccia utente, accertatevi di selezionare **[!UICONTROL AEP Data Lake]** e/o **[!UICONTROL Profile]** in _[!UICONTROL Products]_per elaborare i processi per i dati memorizzati, rispettivamente, nel[!DNL Data Lake]o[!DNL Real-time Customer Profile].

<img src="images/privacy/product-value.png" width="450"><br>

## Elimina elaborazione richiesta

Quando [!DNL Experience Platform] riceve una richiesta di eliminazione da [!DNL Privacy Service], [!DNL Platform] invia una conferma [!DNL Privacy Service] che la richiesta è stata ricevuta e i dati interessati sono stati contrassegnati per l&#39;eliminazione. I record vengono quindi rimossi dal [!DNL Data Lake] [!DNL Profile] negozio entro sette giorni. Durante quella finestra di sette giorni, i dati vengono eliminati in modo morbido e quindi non sono accessibili da alcun [!DNL Platform] servizio.

Nelle release future, [!DNL Platform] invierà una conferma a [!DNL Privacy Service] seguito dell&#39;eliminazione fisica dei dati.

## Passaggi successivi

Leggendo questo documento, ti sono stati introdotti i concetti importanti relativi all&#39;elaborazione delle richieste di privacy in [!DNL Experience Platform]. Si consiglia di continuare a leggere la documentazione fornita in questa guida per approfondire la conoscenza su come gestire i dati di identità e creare processi di privacy.

Per informazioni sull&#39;elaborazione delle richieste di privacy per [!DNL Platform] le risorse non utilizzate da [!DNL Profile], vedere il documento sull&#39;elaborazione delle richieste di [privacy nel Data Lake](../catalog/privacy.md).