---
keywords: ' Experience Platform;home;argomenti popolari'
solution: Experience Platform
title: Privacy Request Processing in Real-time Customer Profile
topic: overview
type: Documentation
description: ' Adobe Experience Platform Privacy Service elabora le richieste dei clienti di accedere, rifiutare la vendita o cancellare i propri dati personali, come indicato da numerose normative sulla privacy. Questo documento tratta i concetti essenziali relativi all''elaborazione delle richieste di privacy per il profilo cliente in tempo reale.'
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 0%

---


# Elaborazione delle richieste di privacy in [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] elabora le richieste dei clienti di accedere, rifiutare la vendita o cancellare i propri dati personali, come delineato dalle normative sulla privacy, quali il Regolamento generale sulla protezione dei dati (General Data Protection Regulation, GDPR) e [!DNL California Consumer Privacy Act] (CCPA).

Questo documento tratta i concetti essenziali relativi all&#39;elaborazione delle richieste di privacy per [!DNL Real-time Customer Profile].

## Introduzione

Prima di leggere la presente guida è consigliabile conoscere correttamente i seguenti servizi [!DNL Experience Platform]:

* [[!DNL Privacy Service]](home.md): Gestisce le richieste dei clienti relative all&#39;accesso, al rifiuto della vendita o all&#39;eliminazione dei loro dati personali tra le applicazioni Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): Risolve la sfida fondamentale rappresentata dalla frammentazione dei dati relativi all&#39;esperienza dei clienti attraverso il collegamento di identità tra dispositivi e sistemi.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Informazioni sugli spazi dei nomi delle identità {#namespaces}

Adobe Experience Platform [!DNL Identity Service] collega i dati di identità dei clienti tra sistemi e dispositivi. [!DNL Identity Service] utilizza  **i** namespace di identità per fornire contesto ai valori di identità collegandoli al loro sistema di origine. Uno spazio dei nomi può rappresentare un concetto generico come un indirizzo e-mail (&quot;E-mail&quot;) o associare l&#39;identità a un&#39;applicazione specifica, ad esempio un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o  Adobe Target ID (&quot;TNTID&quot;).

Servizio identità mantiene un archivio di spazi dei nomi di identità globali (standard) e definiti dall’utente (personalizzati). Gli spazi dei nomi standard sono disponibili per tutte le organizzazioni (ad esempio, &quot;E-mail&quot; e &quot;ECID&quot;), mentre l&#39;organizzazione può anche creare spazi dei nomi personalizzati in base alle proprie esigenze.

Per ulteriori informazioni sugli spazi dei nomi delle identità in [!DNL Experience Platform], vedere la [panoramica dello spazio dei nomi delle identità](../identity-service/namespaces.md).

## Invio di richieste {#submit}

Le sezioni seguenti descrivono come effettuare richieste di privacy per [!DNL Real-time Customer Profile] utilizzando l&#39;API o l&#39;interfaccia utente [!DNL Privacy Service]. Prima di leggere queste sezioni, si consiglia vivamente di consultare la documentazione [Privacy Service API](../privacy-service/api/getting-started.md) o [Privacy Service UI](../privacy-service/ui/overview.md) per i passaggi completi su come inviare un processo per la privacy, incluso come formattare correttamente i dati di identità dell&#39;utente inviati nei payload di richiesta.

>[!IMPORTANT]
>
>Il Privacy Service è in grado di elaborare solo i dati [!DNL Profile] utilizzando un criterio di unione che non esegue la cucitura dell&#39;identità. Se utilizzate l&#39;interfaccia utente per confermare se le richieste di privacy sono in fase di elaborazione, assicuratevi di utilizzare un criterio con &quot;[!DNL None]&quot; come tipo [!UICONTROL ID stitching]. In altre parole, non è possibile utilizzare un criterio di unione in cui [!UICONTROL ID stitching] è impostato su &quot;[!UICONTROL Private graph]&quot;.
>
>![](./images/privacy/no-id-stitch.png)
>
>È inoltre importante notare che il tempo necessario per completare una richiesta di privacy non può essere garantito. Se si verificano modifiche nei dati [!DNL Profile] durante l&#39;elaborazione di una richiesta, non è possibile garantire l&#39;elaborazione di tali record.

### Utilizzo dell&#39;API

Durante la creazione di richieste di processo nell&#39;API, gli ID forniti in `userIDs` devono utilizzare `namespace` e `type` specifici. Per il valore `namespace` è necessario fornire uno spazio dei nomi [identità](#namespaces) valido riconosciuto da [!DNL Identity Service], mentre `type` deve essere `standard` o `unregistered` (rispettivamente per spazi dei nomi standard e personalizzati).

>[!NOTE]
>
>Potrebbe essere necessario fornire più ID per ciascun cliente, a seconda del grafico dell&#39;identità e della distribuzione dei frammenti di profilo nei set di dati della piattaforma. Per ulteriori informazioni, vedere la sezione successiva [frammenti di profilo](#fragments).

Inoltre, l&#39;array `include` del payload della richiesta deve includere i valori del prodotto per i diversi data store a cui viene effettuata la richiesta. Quando si effettuano richieste a [!DNL Data Lake], l&#39;array deve includere il valore &quot;ProfileService&quot;.

La richiesta seguente crea un nuovo processo per la privacy per i dati di un singolo cliente nello store [!DNL Profile]. Per il cliente vengono forniti due valori di identità nell&#39;array `userIDs`; uno che utilizza lo spazio dei nomi di identità standard `Email` e l&#39;altro che utilizza uno spazio dei nomi `Customer_ID` personalizzato. Include inoltre il valore del prodotto per [!DNL Profile] (`ProfileService`) nell&#39;array `include`:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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
            "namespace": "Customer_ID",
            "value": "12345678",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

### Utilizzo dell’interfaccia

Durante la creazione di richieste di processo nell&#39;interfaccia utente, assicurarsi di selezionare **[!UICONTROL AEP Data Lake]** e/o **[!UICONTROL Profile]** in **[!UICONTROL Products]** al fine di elaborare i processi per i dati memorizzati rispettivamente in [!DNL Data Lake] o [!DNL Real-time Customer Profile].

<img src="images/privacy/product-value.png" width="450"><br>

## Frammenti di profilo nelle richieste di privacy {#fragments}

Nell&#39;archivio [!DNL Profile] i dati personali di un singolo cliente saranno spesso composti da più frammenti di profilo, associati alla persona attraverso il grafico dell&#39;identità. Quando si effettuano richieste di privacy nello store [!DNL Profile], è importante notare che le richieste vengono elaborate solo a livello di frammento di profilo, anziché nell&#39;intero profilo.

Ad esempio, è consigliabile memorizzare i dati degli attributi cliente in tre set di dati separati, che utilizzano identificatori diversi per associare tali dati ai singoli clienti:

| Nome set di dati | Campo identità principale | Attributi memorizzati |
| --- | --- | --- |
| Set dati 1 | `customer_id` | `address` |
| Set dati 2 | `email_id` | `firstName`, `lastName` |
| Set dati 3 | `email_id` | `mlScore` |

Uno dei set di dati utilizza `customer_id` come identificatore principale, mentre gli altri due utilizzano `email_id`. Se doveste inviare una richiesta di privacy (accesso o eliminazione) utilizzando solo `email_id` come valore ID utente, verrebbero elaborati solo gli attributi `firstName`, `lastName` e `mlScore`, mentre `address` non verrebbero interessati.

Per garantire che le richieste di privacy elaborino tutti gli attributi del cliente rilevanti, devi fornire i valori di identità principali per tutti i set di dati applicabili in cui tali attributi possono essere memorizzati (fino a un massimo di nove ID per cliente). Per ulteriori informazioni sui campi di identità generalmente contrassegnati come identità, vedere la sezione relativa ai campi di identità in [Nozioni di base sulla composizione dello schema](../xdm/schema/composition.md#identity).

>[!NOTE]
>
>Se utilizzate [sandbox](../sandboxes/home.md) diverse per memorizzare i dati [!DNL Profile], dovete effettuare una richiesta di privacy separata per ogni sandbox, indicando il nome sandbox appropriato nell&#39;intestazione `x-sandbox-name`.

## Elimina elaborazione richiesta

Quando [!DNL Experience Platform] riceve una richiesta di eliminazione da [!DNL Privacy Service], [!DNL Platform] invia una conferma a [!DNL Privacy Service] che la richiesta è stata ricevuta e i dati interessati sono stati contrassegnati per l&#39;eliminazione. I record vengono quindi rimossi dallo store [!DNL Data Lake] o [!DNL Profile] al termine del processo di privacy. Mentre il processo di eliminazione è ancora in fase di elaborazione, i dati vengono eliminati in modo flessibile e non sono quindi accessibili da alcun servizio [!DNL Platform]. Per ulteriori informazioni sul tracciamento degli stati dei processi, fare riferimento alla [[!DNL Privacy Service] documentazione](../privacy-service/home.md#monitor).

>[!IMPORTANT]
>
>Mentre una richiesta di eliminazione corretta rimuove i dati degli attributi raccolti per un cliente (o per un insieme di clienti), la richiesta non rimuove le associazioni stabilite nel grafico dell&#39;identità.
>
>Ad esempio, una richiesta di eliminazione che utilizza le `email_id` e `customer_id` di un cliente rimuove tutti i dati attributo memorizzati in tali ID. Tuttavia, tutti i dati che vengono successivamente trasferiti sotto lo stesso `customer_id` saranno ancora associati al `email_id` appropriato, in quanto l&#39;associazione esiste ancora.

Nelle release future, [!DNL Platform] invierà una conferma a [!DNL Privacy Service] dopo che i dati saranno stati fisicamente eliminati.

## Passaggi successivi

Leggendo questo documento, ti sono stati introdotti i concetti importanti relativi all&#39;elaborazione delle richieste di privacy in [!DNL Experience Platform]. Si consiglia di continuare a leggere la documentazione fornita in questa guida per approfondire la conoscenza su come gestire i dati di identità e creare processi di privacy.

Per informazioni sull&#39;elaborazione delle richieste di privacy per le risorse [!DNL Platform] non utilizzate da [!DNL Profile], consultare il documento relativo all&#39;elaborazione delle richieste di privacy in Data Lake](../catalog/privacy.md).[