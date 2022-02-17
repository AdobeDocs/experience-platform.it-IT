---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Elaborazione delle richieste di privacy in Profilo cliente in tempo reale
type: Documentation
description: Adobe Experience Platform Privacy Service elabora le richieste dei clienti relative all’accesso, alla rinuncia alla vendita o alla cancellazione dei propri dati personali come delineato da numerose normative sulla privacy. Questo documento tratta i concetti essenziali relativi all’elaborazione delle richieste di privacy per Profilo cliente in tempo reale.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: 6cb30dc9e7e76ff9ca060f83405196fa09ed0ebb
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 0%

---

# Elaborazione della richiesta di privacy in [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] elabora le richieste dei clienti per accedere, rinunciare alla vendita o cancellare i propri dati personali come delineato dalle normative sulla privacy, come il Regolamento generale sulla protezione dei dati (RGPD) e [!DNL California Consumer Privacy Act] (CCPA).

Questo documento tratta i concetti essenziali relativi all’elaborazione delle richieste di privacy per [!DNL Real-time Customer Profile] in Adobe Experience Platform.

>[!NOTE]
>
>Questa guida descrive solo come effettuare richieste sulla privacy per i dati del profilo archiviati in Experience Platform. Se prevedi anche di effettuare richieste di privacy per Platform Data Lake, consulta la guida su [elaborazione delle richieste di privacy in Data Lake](../catalog/privacy.md) oltre a questa esercitazione.
>
>Per i passaggi su come effettuare richieste di privacy per altre applicazioni Adobe Experience Cloud, consulta [Documentazione di Privacy Service](../privacy-service/experience-cloud-apps.md).

## Introduzione

Si consiglia di avere una comprensione operativa dei seguenti elementi [!DNL Experience Platform] servizi prima di leggere questa guida:

* [[!DNL Privacy Service]](../privacy-service/home.md): Gestisce le richieste dei clienti relative all’accesso, alla rinuncia alla vendita o all’eliminazione dei loro dati personali tra le applicazioni Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): Risolve la sfida fondamentale rappresentata dalla frammentazione dei dati sulla customer experience attraverso il collegamento di identità tra dispositivi e sistemi.
* [[!DNL Real-time Customer Profile]](home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Informazioni sugli spazi dei nomi delle identità {#namespaces}

Adobe Experience Platform [!DNL Identity Service] collega i dati di identità dei clienti tra sistemi e dispositivi. [!DNL Identity Service] utilizza **spazi dei nomi delle identità** fornire un contesto ai valori d&#39;identità collegandoli al loro sistema d&#39;origine. Uno spazio dei nomi può rappresentare un concetto generico, ad esempio un indirizzo e-mail (&quot;E-mail&quot;) o associare l’identità a un’applicazione specifica, ad esempio un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o un Adobe Target ID (&quot;TNTID&quot;).

Identity Service conserva un archivio di namespace di identità definiti a livello globale (standard) e definiti dall’utente (personalizzati). Gli spazi dei nomi standard sono disponibili per tutte le organizzazioni (ad esempio, &quot;E-mail&quot; ed &quot;ECID&quot;), mentre l’organizzazione può anche creare spazi dei nomi personalizzati in base alle proprie esigenze.

Per ulteriori informazioni sugli spazi dei nomi delle identità in [!DNL Experience Platform], vedi [panoramica dello spazio dei nomi identità](../identity-service/namespaces.md).

## Invio di richieste {#submit}

Le sezioni seguenti illustrano come effettuare richieste di accesso a dati personali per [!DNL Real-time Customer Profile] utilizzando [!DNL Privacy Service] API o interfaccia utente. Prima di leggere queste sezioni, si consiglia vivamente di rivedere il [API Privacy Service](../privacy-service/api/getting-started.md) o [Interfaccia utente di Privacy Service](../privacy-service/ui/overview.md) documentazione completa sui passaggi per l’invio di un processo relativo alla privacy, inclusa la modalità di formattazione corretta dei dati di identità utente inviati nei payload della richiesta.

>[!IMPORTANT]
>
>Privacy Service è in grado di elaborare solo [!DNL Profile] i dati che utilizzano un criterio di unione che non esegue la combinazione di identità. Se utilizzi l’interfaccia utente per confermare se le richieste di privacy sono in fase di elaborazione, assicurati di utilizzare un criterio con &quot;[!DNL None]&quot; [!UICONTROL unione degli ID] digitare. In altre parole, non è possibile utilizzare un criterio di unione in cui [!UICONTROL unione degli ID] è impostato su &quot;[!UICONTROL Grafico privato]&quot;.
>
>![L&#39;unione ID del criterio di unione è impostata su Nessuno](./images/privacy/no-id-stitch.png)
>
>È inoltre importante notare che il tempo necessario per completare una richiesta di accesso a dati personali non può essere garantito. Se si verificano modifiche nel [!DNL Profile] i dati durante l&#39;elaborazione di una richiesta, indipendentemente dal fatto che tali record siano o meno elaborati, non possono essere garantiti.

### Mediante l’API

Quando crei richieste di lavoro nell&#39;API, qualsiasi ID fornito in `userIDs` deve utilizzare un `namespace` e `type`. Una valida [spazio dei nomi identità](#namespaces) riconosciuti [!DNL Identity Service] devono essere previste `namespace` , mentre `type` deve `standard` o `unregistered` (per namespace standard e personalizzati, rispettivamente).

>[!NOTE]
>
>Potrebbe essere necessario fornire più di un ID per ciascun cliente, a seconda del grafico delle identità e della distribuzione dei frammenti di profilo nei set di dati di Platform. Vedi la sezione successiva [frammenti di profilo](#fragments) per ulteriori informazioni.

Inoltre, il `include` la matrice del payload della richiesta deve includere i valori di prodotto per i diversi archivi di dati in cui viene effettuata la richiesta. Quando si effettuano richieste a [!DNL Data Lake], la matrice deve includere il valore &quot;ProfileService&quot;.

La seguente richiesta crea un nuovo processo di privacy per i dati di un singolo cliente nel [!DNL Profile] archiviare. Per il cliente vengono forniti due valori di identità nel `userIDs` array; uno che utilizza lo standard `Email` spazio dei nomi di identità e l&#39;altro utilizzando un `Customer_ID` spazio dei nomi. Include inoltre il valore del prodotto per [!DNL Profile] (`ProfileService`) nel `include` array:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
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
    "regulation": "ccpa"
}'
```

>[!IMPORTANT]
>
>Platform elabora le richieste di privacy in tutti [sandbox](../sandboxes/home.md) appartenente alla tua organizzazione. Di conseguenza, qualsiasi `x-sandbox-name` l’intestazione inclusa nella richiesta viene ignorata dal sistema.

### Utilizzo dell’interfaccia

Quando crei richieste di lavoro nell’interfaccia utente, assicurati di selezionare **[!UICONTROL AEP Data Lake]** e/o **[!UICONTROL Profilo]** sotto **[!UICONTROL Prodotti]** al fine di elaborare i processi per i dati memorizzati nel [!DNL Data Lake] o [!DNL Real-time Customer Profile], rispettivamente.

![Viene creata una richiesta di processo di accesso nell’interfaccia utente, con l’opzione Profilo selezionata in Prodotti](./images/privacy/product-value.png)

## Frammenti di profilo nelle richieste di privacy {#fragments}

In [!DNL Profile] archivio dati, i dati personali di un singolo cliente saranno spesso costituiti da più frammenti di profilo, che sono associati alla persona attraverso il grafico dell’identità. Quando si effettuano richieste di privacy a [!DNL Profile] memorizza, è importante notare che le richieste vengono elaborate solo a livello di frammento di profilo, anziché nell’intero profilo.

Ad esempio, considera una situazione in cui memorizzare i dati degli attributi del cliente in tre set di dati separati, che utilizzano identificatori diversi per associare tali dati ai singoli clienti:

| Nome set di dati | Campo di identità principale | Attributi memorizzati |
| --- | --- | --- |
| Set di dati 1 | `customer_id` | `address` |
| Set di dati 2 | `email_id` | `firstName`, `lastName` |
| Set di dati 3 | `email_id` | `mlScore` |

Uno dei set di dati utilizza `customer_id` come identificatore principale, mentre gli altri due usano `email_id`. Se invii una richiesta di accesso a dati personali (accesso o cancellazione) utilizzando solo `email_id` come valore ID utente, solo il `firstName`, `lastName`e `mlScore` gli attributi vengono elaborati mentre `address` non sono interessati.

Per garantire che le richieste di privacy elaborino tutti gli attributi del cliente rilevanti, devi fornire i valori di identità principali per tutti i set di dati applicabili in cui tali attributi possono essere memorizzati (fino a un massimo di nove ID per cliente). Consulta la sezione sui campi di identità nella sezione [nozioni di base sulla composizione dello schema](../xdm/schema/composition.md#identity) per ulteriori informazioni sui campi generalmente contrassegnati come identità.

## Elimina elaborazione richiesta

Quando [!DNL Experience Platform] riceve una richiesta di cancellazione da [!DNL Privacy Service], [!DNL Platform] invia conferma a [!DNL Privacy Service] che la richiesta è stata ricevuta e i dati interessati sono stati contrassegnati per l’eliminazione. I record vengono quindi rimossi dal [!DNL Data Lake] o [!DNL Profile] una volta che il processo di privacy è stato completato. Mentre il processo di eliminazione è ancora in elaborazione, i dati vengono eliminati tramite software e non sono quindi accessibili da nessuno [!DNL Platform] servizio. Fai riferimento a [[!DNL Privacy Service] documentazione](../privacy-service/home.md#monitor) per ulteriori informazioni sul tracciamento degli stati dei processi.

>[!IMPORTANT]
>
>Mentre una richiesta di cancellazione corretta rimuove i dati degli attributi raccolti per un cliente (o per un set di clienti), la richiesta non rimuove le associazioni stabilite nel grafico delle identità.
>
>Ad esempio, una richiesta di cancellazione che utilizza un `email_id` e `customer_id` rimuove tutti i dati attributo memorizzati in tali ID. Tuttavia, qualsiasi dato successivamente acquisito in base agli stessi `customer_id` saranno ancora associati al `email_id`, poiché l&#39;associazione esiste ancora.
>
>Inoltre, Privacy Service è in grado di elaborare solo [!DNL Profile] i dati che utilizzano un criterio di unione che non esegue la combinazione di identità. Se utilizzi l’interfaccia utente per confermare se le richieste di privacy sono in fase di elaborazione, assicurati di utilizzare un criterio con &quot;[!DNL None]&quot; [!UICONTROL unione degli ID] digitare. In altre parole, non è possibile utilizzare un criterio di unione in cui [!UICONTROL unione degli ID] è impostato su &quot;[!UICONTROL Grafico privato]&quot;.
>
>![L&#39;unione ID del criterio di unione è impostata su Nessuno](./images/privacy/no-id-stitch.png)

Nelle versioni future, [!DNL Platform] invierà conferma a [!DNL Privacy Service] dopo che i dati sono stati fisicamente cancellati.

## Passaggi successivi

Leggendo questo documento, ti sono stati introdotti i concetti importanti relativi all’elaborazione delle richieste di privacy in [!DNL Experience Platform]. Si consiglia di continuare a leggere la documentazione fornita in questa guida per approfondire la comprensione su come gestire i dati di identità e creare processi di privacy.

Per informazioni sull’elaborazione delle richieste di accesso a dati personali per [!DNL Platform] risorse non utilizzate da [!DNL Profile], consulta il documento in [elaborazione delle richieste di privacy in Data Lake](../catalog/privacy.md).
