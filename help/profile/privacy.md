---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Elaborazione delle richieste di privacy in Profilo cliente in tempo reale
topic-legacy: overview
type: Documentation
description: Adobe Experience Platform Privacy Service elabora le richieste dei clienti relative all’accesso, alla rinuncia alla vendita o alla cancellazione dei propri dati personali come delineato da numerose normative sulla privacy. Questo documento tratta i concetti essenziali relativi all’elaborazione delle richieste di privacy per Profilo cliente in tempo reale.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 0%

---

# Elaborazione della richiesta di privacy in [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] elabora le richieste dei clienti per accedere, rinunciare alla vendita o cancellare i propri dati personali come delineato dalle normative sulla privacy, come il Regolamento generale sulla protezione dei dati (RGPD) e [!DNL California Consumer Privacy Act] (CCPA).

Questo documento tratta i concetti essenziali relativi all’elaborazione delle richieste di privacy per [!DNL Real-time Customer Profile].

## Introduzione

Prima di leggere questa guida, è consigliabile avere familiarità con i seguenti servizi [!DNL Experience Platform] :

* [[!DNL Privacy Service]](home.md): Gestisce le richieste dei clienti relative all’accesso, alla rinuncia alla vendita o all’eliminazione dei loro dati personali tra le applicazioni Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): Risolve la sfida fondamentale rappresentata dalla frammentazione dei dati sulla customer experience attraverso il collegamento di identità tra dispositivi e sistemi.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Informazioni sugli spazi dei nomi delle identità {#namespaces}

Adobe Experience Platform [!DNL Identity Service] collega i dati di identità dei clienti tra sistemi e dispositivi. [!DNL Identity Service] utilizza  **i** namespace di identità per fornire contesto ai valori di identità collegandoli al loro sistema di origine. Uno spazio dei nomi può rappresentare un concetto generico, ad esempio un indirizzo e-mail (&quot;E-mail&quot;) o associare l’identità a un’applicazione specifica, ad esempio un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o un Adobe Target ID (&quot;TNTID&quot;).

Identity Service conserva un archivio di namespace di identità definiti a livello globale (standard) e definiti dall’utente (personalizzati). Gli spazi dei nomi standard sono disponibili per tutte le organizzazioni (ad esempio, &quot;E-mail&quot; ed &quot;ECID&quot;), mentre l’organizzazione può anche creare spazi dei nomi personalizzati in base alle proprie esigenze.

Per ulteriori informazioni sugli spazi dei nomi di identità in [!DNL Experience Platform], consulta la [panoramica dello spazio dei nomi di identità](../identity-service/namespaces.md).

## Invio di richieste {#submit}

Le sezioni seguenti descrivono come effettuare richieste di privacy per [!DNL Real-time Customer Profile] utilizzando l’ API o l’interfaccia utente [!DNL Privacy Service] . Prima di leggere queste sezioni, si consiglia vivamente di consultare la documentazione [API Privacy Service](../privacy-service/api/getting-started.md) o [Interfaccia Privacy Service](../privacy-service/ui/overview.md) per i passaggi completi su come inviare un processo relativo alla privacy, incluso come formattare correttamente i dati di identità utente inviati nei payload della richiesta.

>[!IMPORTANT]
>
>Privacy Service è in grado di elaborare solo i dati [!DNL Profile] utilizzando un criterio di unione che non esegue l’unione delle identità. Se utilizzi l’interfaccia utente per confermare se le richieste di privacy sono in fase di elaborazione, assicurati di utilizzare un criterio con &quot;[!DNL None]&quot; come tipo [!UICONTROL ID stitching]. In altre parole, non è possibile utilizzare un criterio di unione in cui [!UICONTROL ID stitching] è impostato su &quot;[!UICONTROL Private graph]&quot;.
>
>![](./images/privacy/no-id-stitch.png)
>
>È inoltre importante notare che il tempo necessario per completare una richiesta di accesso a dati personali non può essere garantito. Se si verificano modifiche nei dati [!DNL Profile] durante l&#39;elaborazione di una richiesta, non è possibile garantire l&#39;elaborazione di tali record.

### Utilizzo dell’API

Quando crei richieste di lavoro nell&#39;API, qualsiasi ID fornito in `userIDs` deve utilizzare un `namespace` e `type` specifici. Per il valore `namespace` deve essere fornito un [namespace di identità](#namespaces) valido riconosciuto da [!DNL Identity Service], mentre il valore `type` deve essere `standard` o `unregistered` (rispettivamente per i namespace standard e personalizzati).

>[!NOTE]
>
>Potrebbe essere necessario fornire più di un ID per ciascun cliente, a seconda del grafico delle identità e della distribuzione dei frammenti di profilo nei set di dati di Platform. Per ulteriori informazioni, consulta la sezione successiva [frammenti di profilo](#fragments) .

Inoltre, la matrice `include` del payload della richiesta deve includere i valori del prodotto per i diversi archivi di dati in cui viene effettuata la richiesta. Quando si effettuano richieste a [!DNL Data Lake], l&#39;array deve includere il valore &quot;ProfileService&quot;.

La seguente richiesta crea un nuovo processo di privacy per i dati di un singolo cliente nell&#39;archivio [!DNL Profile]. Nell&#39;array `userIDs` vengono forniti due valori di identità per il cliente. uno che utilizza lo spazio dei nomi `Email` Identity standard e l’altro che utilizza uno spazio dei nomi `Customer_ID` personalizzato. Include inoltre il valore del prodotto per [!DNL Profile] (`ProfileService`) nell&#39;array `include`:

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

Durante la creazione di richieste di lavoro nell&#39;interfaccia utente, assicurati di selezionare **[!UICONTROL AEP Data Lake]** e/o **[!UICONTROL Profile]** in **[!UICONTROL Products]** per elaborare i processi per i dati memorizzati rispettivamente in [!DNL Data Lake] o [!DNL Real-time Customer Profile].

<img src="images/privacy/product-value.png" width="450"><br>

## Frammenti di profilo nelle richieste di privacy {#fragments}

Nell’archivio dati [!DNL Profile] i dati personali di un singolo cliente sono spesso costituiti da più frammenti di profilo, che sono associati alla persona tramite il grafico dell’identità. Quando esegui richieste di privacy nell&#39;archivio [!DNL Profile] , è importante notare che le richieste vengono elaborate solo a livello di frammento di profilo, anziché nell&#39;intero profilo.

Ad esempio, considera una situazione in cui memorizzare i dati degli attributi del cliente in tre set di dati separati, che utilizzano identificatori diversi per associare tali dati ai singoli clienti:

| Nome set di dati | Campo di identità principale | Attributi memorizzati |
| --- | --- | --- |
| Set di dati 1 | `customer_id` | `address` |
| Set di dati 2 | `email_id` | `firstName`, `lastName` |
| Set di dati 3 | `email_id` | `mlScore` |

Uno dei set di dati utilizza `customer_id` come identificatore principale, mentre gli altri due utilizzano `email_id`. Se invii una richiesta di accesso a dati personali (accesso o eliminazione) utilizzando solo `email_id` come valore ID utente, verranno elaborati solo gli attributi `firstName`, `lastName` e `mlScore`, mentre `address` non ne risentirà.

Per garantire che le richieste di privacy elaborino tutti gli attributi del cliente rilevanti, devi fornire i valori di identità principali per tutti i set di dati applicabili in cui tali attributi possono essere memorizzati (fino a un massimo di nove ID per cliente). Per ulteriori informazioni sui campi comunemente contrassegnati come identità, consulta la sezione sui campi di identità in [nozioni di base sulla composizione dello schema](../xdm/schema/composition.md#identity) .

>[!NOTE]
>
>Se utilizzi [sandbox](../sandboxes/home.md) diverse per memorizzare i dati [!DNL Profile], devi effettuare una richiesta di privacy separata per ogni sandbox, indicando il nome della sandbox appropriato nell’intestazione `x-sandbox-name` .

## Elimina elaborazione richiesta

Quando [!DNL Experience Platform] riceve una richiesta di cancellazione da [!DNL Privacy Service], [!DNL Platform] invia una conferma a [!DNL Privacy Service] che la richiesta è stata ricevuta e i dati interessati sono stati contrassegnati per l’eliminazione. I record vengono quindi rimossi dall&#39;archivio [!DNL Data Lake] o [!DNL Profile] una volta completato il processo di privacy. Mentre il processo di eliminazione è ancora in elaborazione, i dati vengono eliminati in modo morbido e non sono quindi accessibili da nessun servizio [!DNL Platform]. Per ulteriori informazioni sul tracciamento degli stati dei processi, consulta la [[!DNL Privacy Service] documentazione](../privacy-service/home.md#monitor) .

>[!IMPORTANT]
>
>Mentre una richiesta di cancellazione corretta rimuove i dati degli attributi raccolti per un cliente (o per un set di clienti), la richiesta non rimuove le associazioni stabilite nel grafico delle identità.
>
>Ad esempio, una richiesta di cancellazione che utilizza i valori `email_id` e `customer_id` di un cliente rimuove tutti i dati degli attributi memorizzati in tali ID. Tuttavia, tutti i dati successivamente acquisiti sotto lo stesso `customer_id` saranno ancora associati all’ `email_id` appropriato, in quanto l’associazione esiste ancora.

Nelle versioni future, [!DNL Platform] invierà una conferma a [!DNL Privacy Service] dopo che i dati sono stati fisicamente eliminati.

## Passaggi successivi

Leggendo questo documento, ti sono stati introdotti i concetti importanti relativi all’elaborazione delle richieste di privacy in [!DNL Experience Platform]. Si consiglia di continuare a leggere la documentazione fornita in questa guida per approfondire la comprensione su come gestire i dati di identità e creare processi di privacy.

Per informazioni sull&#39;elaborazione delle richieste di privacy per le risorse [!DNL Platform] non utilizzate da [!DNL Profile], consulta il documento sull&#39; [elaborazione della richiesta di privacy in Data Lake](../catalog/privacy.md).
