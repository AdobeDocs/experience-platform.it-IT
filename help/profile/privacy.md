---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Elaborazione delle richieste di privacy in Real-time Customer Profile
topic: overview
translation-type: tm+mt
source-git-commit: f7abccb677294e1595fb35c27e03c30eb968082a
workflow-type: tm+mt
source-wordcount: '1013'
ht-degree: 0%

---


# Elaborazione delle richieste di privacy in [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] elabora le richieste dei clienti di accedere, rifiutare la vendita o cancellare i propri dati personali, così come delineati dalle normative sulla privacy, quali il Regolamento generale sulla protezione dei dati (General Data Protection Regulation, GDPR) e [!DNL California Consumer Privacy Act] (CCPA).

Il presente documento illustra i concetti essenziali relativi all’elaborazione delle richieste di privacy per [!DNL Real-time Customer Profile].

## Introduzione

Prima di leggere la presente guida è consigliabile conoscere i seguenti [!DNL Experience Platform] servizi:

* [[!Privacy Service DNL]](home.md): Gestisce le richieste dei clienti relative all&#39;accesso, al rifiuto della vendita o all&#39;eliminazione dei loro dati personali tra le applicazioni Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): Risolve la sfida fondamentale rappresentata dalla frammentazione dei dati relativi all&#39;esperienza dei clienti attraverso il collegamento di identità tra dispositivi e sistemi.
* [[!DNL Profilo cliente in tempo reale]](../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Informazioni sugli spazi dei nomi delle identità {#namespaces}

Adobe Experience Platform [!DNL Identity Service] collega i dati di identità dei clienti tra sistemi e dispositivi. [!DNL Identity Service] utilizza gli spazi dei nomi di **identità** per fornire contesto ai valori di identità collegandoli al loro sistema di origine. Uno spazio dei nomi può rappresentare un concetto generico come un indirizzo e-mail (&quot;E-mail&quot;) o associare l&#39;identità a un&#39;applicazione specifica, ad esempio un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o  Adobe Target ID (&quot;TNTID&quot;).

Servizio identità mantiene un archivio di spazi dei nomi di identità globali (standard) e definiti dall’utente (personalizzati). Gli spazi dei nomi standard sono disponibili per tutte le organizzazioni (ad esempio, &quot;E-mail&quot; e &quot;ECID&quot;), mentre l&#39;organizzazione può anche creare spazi dei nomi personalizzati in base alle proprie esigenze.

Per ulteriori informazioni sugli spazi dei nomi delle identità in [!DNL Experience Platform], vedere la panoramica [dello spazio dei nomi](../identity-service/namespaces.md)delle identità.

## Invio di richieste {#submit}

Le sezioni seguenti descrivono come effettuare richieste di privacy per [!DNL Real-time Customer Profile] l&#39;utilizzo dell&#39; [!DNL Privacy Service] API o dell&#39;interfaccia utente. Prima di leggere queste sezioni, si consiglia vivamente di consultare la documentazione API [](../privacy-service/api/getting-started.md) Privacy Service o interfaccia utente [](../privacy-service/ui/overview.md) Privacy Service per i passaggi completi su come inviare un processo di privacy, inclusa la modalità corretta di formattare i dati di identità utente inviati nei payload di richiesta.

>[!IMPORTANT]
>
>Privacy Service è in grado di elaborare [!DNL Profile] i dati solo utilizzando un criterio di unione che non esegue l&#39;unione delle identità. Se utilizzate l&#39;interfaccia utente per confermare se le richieste di privacy sono in fase di elaborazione, assicuratevi di utilizzare un criterio con il[!DNL None]tipo &quot; [!UICONTROL ID stitching] &quot;. In altre parole, non è possibile utilizzare un criterio di unione in cui [!UICONTROL ID stitching] è impostato su &quot;[!UICONTROL Private graph]&quot;.
>
>![](./images/privacy/no-id-stitch.png)

### Utilizzo dell&#39;API

Quando si creano richieste di processo nell&#39;API, gli ID forniti all&#39;interno `userIDs` devono utilizzare uno specifico `namespace` e `type`. Per il [valore](#namespaces) deve essere fornito uno spazio nomi [!DNL Identity Service] di `namespace` identità valido riconosciuto da, mentre `type` deve essere `standard` o `unregistered` (rispettivamente per gli spazi dei nomi standard e personalizzati).

>[!NOTE]
>
>Potrebbe essere necessario fornire più ID per ciascun cliente, a seconda del grafico dell&#39;identità e della distribuzione dei frammenti di profilo nei set di dati della piattaforma. Per ulteriori informazioni, vedere la sezione successiva [frammenti](#fragments) di profilo.

Inoltre, l&#39; `include` array del payload della richiesta deve includere i valori prodotto per i diversi data store a cui viene effettuata la richiesta. Quando si effettuano richieste al [!DNL Data Lake], l&#39;array deve includere il valore &quot;ProfileService&quot;.

La seguente richiesta crea un nuovo processo per la privacy per i dati di un singolo cliente nello [!DNL Profile] store. Sono forniti due valori di identità per il cliente nell&#39; `userIDs` array; uno che utilizza lo spazio dei nomi `Email` identità standard e l&#39;altro che utilizza uno `Customer_ID` spazio dei nomi personalizzato. Include inoltre il valore del prodotto per [!DNL Profile] (`ProfileService`) nell&#39; `include` array:

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

Quando create richieste di processo nell’interfaccia utente, accertatevi di selezionare **[!UICONTROL AEP Data Lake]** e/o **[!UICONTROL Profile]** in **[!UICONTROL Products]** per elaborare i processi per i dati memorizzati, rispettivamente, nel [!DNL Data Lake] o [!DNL Real-time Customer Profile].

<img src="images/privacy/product-value.png" width="450"><br>

## Frammenti di profilo nelle richieste di privacy {#fragments}

Nell&#39;archivio [!DNL Profile] dati, i dati personali di un singolo cliente saranno spesso composti da più frammenti di profilo, associati alla persona attraverso il grafico dell&#39;identità. Quando si effettuano richieste di privacy allo [!DNL Profile] store, è importante notare che le richieste vengono elaborate solo a livello di frammento di profilo, anziché a livello di intero profilo.

Ad esempio, è consigliabile memorizzare i dati degli attributi cliente in tre set di dati separati, che utilizzano identificatori diversi per associare tali dati ai singoli clienti:

| Nome set di dati | Campo identità principale | Attributi memorizzati |
| --- | --- | --- |
| Set dati 1 | `customer_id` | `address` |
| Set dati 2 | `email_id` | `firstName`, `lastName` |
| Set dati 3 | `email_id` | `mlScore` |

Uno dei set di dati utilizza `customer_id` come identificatore principale, mentre gli altri due utilizzano `email_id`. Se si inviasse una richiesta di privacy (accesso o eliminazione) utilizzando solo `email_id` come valore ID utente, verranno elaborati solo gli `firstName`, `lastName`e `mlScore` gli attributi, senza `address` che ciò influisca.

Per garantire che le richieste di privacy elaborino tutti gli attributi del cliente rilevanti, devi fornire i valori di identità principali per tutti i set di dati applicabili in cui tali attributi possono essere memorizzati (fino a un massimo di nove ID per cliente). Per ulteriori informazioni sui campi generalmente contrassegnati come identità, vedere la sezione sui campi di identità [di base della composizione](../xdm/schema/composition.md#identity) dello schema.

>[!NOTE]
>
>Se utilizzate [sandbox](../sandboxes/home.md) diverse per memorizzare [!DNL Profile] i dati, dovete effettuare una richiesta di privacy separata per ogni sandbox, indicando il nome sandbox appropriato nell&#39; `x-sandbox-name` intestazione.

## Elimina elaborazione richiesta

Quando [!DNL Experience Platform] riceve una richiesta di eliminazione da [!DNL Privacy Service], [!DNL Platform] invia una conferma [!DNL Privacy Service] che la richiesta è stata ricevuta e i dati interessati sono stati contrassegnati per l&#39;eliminazione. I record vengono quindi rimossi dallo [!DNL Data Lake] store o [!DNL Profile] dallo store al termine del processo di privacy. Mentre il processo di eliminazione è ancora in fase di elaborazione, i dati vengono eliminati in modo flessibile e non sono quindi accessibili da alcun [!DNL Platform] servizio. Per ulteriori informazioni sul tracciamento degli stati dei processi, consultate la [[!DNL Privacy Service] documentazione](../privacy-service/home.md#monitor) .

>[!IMPORTANT]
>
>Mentre una richiesta di eliminazione corretta rimuove i dati degli attributi raccolti per un cliente (o per un insieme di clienti), la richiesta non rimuove le associazioni stabilite nel grafico dell&#39;identità.
>
>Ad esempio, una richiesta di eliminazione che utilizza un cliente `email_id` e `customer_id` rimuove tutti i dati attributo memorizzati in tali ID. Tuttavia, tutti i dati successivamente acquisiti in base allo stesso `customer_id` `email_id`continueranno ad essere associati ai dati appropriati, in quanto l&#39;associazione esiste ancora.

Nelle release future, [!DNL Platform] invierà una conferma a [!DNL Privacy Service] seguito dell&#39;eliminazione fisica dei dati.

## Passaggi successivi

Leggendo questo documento, ti sono stati introdotti i concetti importanti relativi all&#39;elaborazione delle richieste di privacy in [!DNL Experience Platform]. Si consiglia di continuare a leggere la documentazione fornita in questa guida per approfondire la conoscenza su come gestire i dati di identità e creare processi di privacy.

Per informazioni sull&#39;elaborazione delle richieste di privacy per [!DNL Platform] le risorse non utilizzate da [!DNL Profile], vedere il documento sull&#39;elaborazione delle richieste di [privacy nel Data Lake](../catalog/privacy.md).