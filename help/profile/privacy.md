---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Elaborazione delle richieste di privacy nel profilo cliente in tempo reale
type: Documentation
description: Adobe Experience Platform Privacy Service elabora le richieste dei clienti di accedere ai propri dati personali, rinunciarvi o cancellarli, come indicato da numerose normative sulla privacy. Questo documento descrive i concetti essenziali relativi all’elaborazione delle richieste di accesso a dati personali per Real-Time Customer Profile.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1743'
ht-degree: 1%

---

# Elaborazione della richiesta di accesso a dati personali in [!DNL Real-Time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] elabora le richieste dei clienti di accedere ai propri dati personali, di rifiutarne la vendita o di eliminarli, in conformità alle normative sulla privacy, come il Regolamento generale sulla protezione dei dati (RGPD) e [!DNL California Consumer Privacy Act] (CCPA).

Questo documento descrive i concetti essenziali relativi all&#39;elaborazione delle richieste di accesso a dati personali per [!DNL Real-Time Customer Profile] in Adobe Experience Platform.

>[!NOTE]
>
>Questa guida descrive solo come effettuare richieste di accesso ai dati personali per l’archivio dati profilo in Experience Platform. Se prevedi anche di effettuare richieste di privacy per il data lake di Platform, oltre a questa esercitazione fai riferimento alla guida sull&#39;[elaborazione delle richieste di privacy nel data lake](../catalog/privacy.md).
>
>Per i passaggi su come effettuare richieste di privacy per altre applicazioni Adobe Experience Cloud, consulta la [documentazione di Privacy Service](../privacy-service/experience-cloud-apps.md).

>[!IMPORTANT]
>
>La richiesta di accesso a dati personali in questa guida **non** riguarda entità non personali B2B.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti [!DNL Platform] componenti:

* [[!DNL Privacy Service]](../privacy-service/home.md): gestisce le richieste dei clienti di accedere, rinunciare alle vendite o eliminare i propri dati personali nelle applicazioni Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): risolve la sfida fondamentale posta dalla frammentazione dei dati sull&#39;esperienza del cliente collegando le identità tra dispositivi e sistemi.
* [[!DNL Real-Time Customer Profile]](home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Comprendere gli spazi dei nomi delle identità {#namespaces}

Adobe Experience Platform [!DNL Identity Service] esegue il bridging dei dati di identità del cliente tra sistemi e dispositivi. [!DNL Identity Service] utilizza **spazi dei nomi di identità** per fornire contesto ai valori di identità tramite la relazione con il proprio sistema di origine. Uno spazio dei nomi può rappresentare un concetto generico come un indirizzo e-mail (&quot;E-mail&quot;) o associare l’identità a un’applicazione specifica, come un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o un Adobe Target ID (&quot;TNTID&quot;).

Identity Service gestisce un archivio di spazi dei nomi di identità definiti a livello globale (standard) e definiti dall’utente (personalizzati). Gli spazi dei nomi standard sono disponibili per tutte le organizzazioni (ad esempio, &quot;E-mail&quot; e &quot;ECID&quot;), mentre l’organizzazione può anche creare spazi dei nomi personalizzati in base alle sue esigenze specifiche.

Per ulteriori informazioni sugli spazi dei nomi delle identità in [!DNL Experience Platform], vedere [panoramica dello spazio dei nomi delle identità](../identity-service/features/namespaces.md).

## Invio di richieste {#submit}

Le sezioni seguenti descrivono come effettuare richieste di accesso a dati personali per [!DNL Real-Time Customer Profile] utilizzando l&#39;API o l&#39;interfaccia utente di [!DNL Privacy Service]. Prima di leggere queste sezioni, è necessario rivedere o tenere presente la documentazione dell&#39;[API Privacy Service](../privacy-service/api/getting-started.md) o dell&#39;[interfaccia utente Privacy Service](../privacy-service/ui/overview.md). Questi documenti forniscono i passaggi completi su come inviare un processo di privacy, incluso come formattare correttamente i dati di identità utente inviati nei payload di richiesta.

>[!IMPORTANT]
>
>Privacy Service è in grado di elaborare solo i dati [!DNL Profile] utilizzando un criterio di unione che non esegue l&#39;unione delle identità. Per ulteriori informazioni, consulta la sezione sulle [limitazioni dei criteri di unione](#merge-policy-limitations).
>
>Tieni presente che le richieste di accesso a dati personali vengono elaborate in modo asincrono in conformità ai requisiti normativi e che il tempo necessario per completarle può variare. Se durante l&#39;elaborazione di una richiesta si verificano modifiche nei dati di [!DNL Profile], non è garantito che anche i record in ingresso verranno elaborati nella richiesta. Solo i profili presenti nel data lake o nell’archivio profili al momento della richiesta del processo di privacy possono essere eliminati. Se acquisisci i dati del profilo relativi all’oggetto di una richiesta di eliminazione durante il processo di eliminazione, non è garantita l’eliminazione di tutti i frammenti di profilo.
>È tua responsabilità essere a conoscenza di eventuali dati in arrivo in Platform o nel servizio profili al momento di una richiesta di cancellazione, in quanto tali dati verranno inseriti negli archivi record. Devi essere prudente nell’acquisire i dati che sono stati eliminati o che sono in corso di eliminazione.

### Mediante l’API

Durante la creazione di richieste di processi nell&#39;API, qualsiasi ID fornito in `userIDs` deve utilizzare un `namespace` e un `type` specifici. È necessario fornire uno spazio dei nomi [identity](#namespaces) valido riconosciuto da [!DNL Identity Service] per il valore `namespace`, mentre `type` deve essere `standard` o `unregistered` (rispettivamente per gli spazi dei nomi standard e personalizzati).

>[!NOTE]
>
>Potresti dover fornire più di un ID per ogni cliente, a seconda del grafico delle identità e di come i frammenti di profilo sono distribuiti nei set di dati di Platform. Per ulteriori informazioni, vedere la sezione successiva [frammenti di profilo](#fragments).

Inoltre, l&#39;array `include` del payload della richiesta deve includere i valori del prodotto per i diversi archivi di dati a cui viene effettuata la richiesta. Per eliminare i dati di profilo associati a un&#39;identità, l&#39;array deve includere il valore `ProfileService`. Per eliminare le associazioni del grafico delle identità del cliente, l&#39;array deve includere il valore `identity`.

>[!NOTE]
>
>Per informazioni più dettagliate sugli effetti dell&#39;utilizzo di `ProfileService` e `identity` nell&#39;array `include`, vedere la sezione relativa alle [richieste di profilo e di identità](#profile-v-identity) più avanti in questo documento.

La richiesta seguente crea un nuovo processo di privacy per i dati di un singolo cliente nell&#39;archivio [!DNL Profile]. Nell&#39;array `userIDs` sono forniti due valori di identità per il cliente: uno utilizza lo spazio dei nomi di identità standard `Email` e l&#39;altro utilizza uno spazio dei nomi personalizzato `Customer_ID`. Include inoltre il valore del prodotto per [!DNL Profile] (`ProfileService`) nell&#39;array `include`:

**Richiesta**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
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
    "include": ["ProfileService","identity"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

>[!IMPORTANT]
>
>Platform elabora le richieste di accesso a dati personali in tutte le [sandbox](../sandboxes/home.md) appartenenti alla tua organizzazione. Di conseguenza, qualsiasi intestazione `x-sandbox-name` inclusa nella richiesta viene ignorata dal sistema.

**Risposta prodotto**

Per Profile Service, una volta completato il processo di accesso a dati personali, viene restituita una risposta in formato JSON con le informazioni relative agli ID utente richiesti.

```json
{
    "privacyResponse": {
        "jobId": "7467850f-9698-11ed-8635-355435552164",
        "response": [
            {
                "sandbox": "prod",
                "mergePolicyId": "none",
                "result": {
                    "person": {
                        "gender": "female"           
                    },
                    "personalEmail": {
                        "address": "ajones@acme.com",
                    },
                    "identityMap": {
                        "crmid": [
                            {
                                "id": "5b7db37a-bc7a-46a2-a63e-2cfe7e1cc068"
                            }
                        ]
                    }
                }
            },
            {
                "sandbox": "prod",
                "mergePolicyId": "none",
                "result": {
                    "person": {
                        "gender": "male"
                    },
                    "id": 12345678,
                    "identityMap": {
                        "crmid": [
                            {
                                "id": "e9d439f2-f5e4-4790-ad67-b13dbd89d52e"
                            }
                        ]
                    }
                }
            }
        ]
    }
}
```

### Utilizzo dell’interfaccia utente

Durante la creazione di richieste di processi nell&#39;interfaccia utente, assicurati di selezionare **[!UICONTROL AEP Data Lake]** e/o **[!UICONTROL Profilo]** in **[!UICONTROL Prodotti]** per elaborare i processi per i dati archiviati nel data lake o [!DNL Real-Time Customer Profile], rispettivamente.

![È in corso la creazione di una richiesta di processo di accesso nell&#39;interfaccia utente, con l&#39;opzione di profilo selezionata in Prodotti](./images/privacy/product-value.png)

## Frammenti di profilo nelle richieste di accesso a dati personali {#fragments}

Nell&#39;archivio dati [!DNL Profile], i dati personali di un singolo cliente sono spesso costituiti da più frammenti di profilo associati alla persona tramite il grafico delle identità. Quando si inviano richieste di accesso a dati personali all&#39;archivio [!DNL Profile], è importante notare che le richieste vengono elaborate solo a livello di frammento di profilo, anziché all&#39;intero profilo.

Ad esempio, considera una situazione in cui stai memorizzando i dati degli attributi del cliente in tre set di dati separati, che utilizzano identificatori diversi per associare tali dati ai singoli clienti:

| Nome del set di dati | Campo dell’identità primaria | Attributi memorizzati |
| --- | --- | --- |
| Set di dati 1 | `customer_id` | `address` |
| Set di dati 2 | `email_id` | `firstName`, `lastName` |
| Set di dati 3 | `email_id` | `mlScore` |

Uno dei set di dati utilizza `customer_id` come identificatore primario, mentre gli altri due utilizzano `email_id`. Se si inviasse una richiesta di privacy (accesso o eliminazione) utilizzando solo `email_id` come valore ID utente, verrebbero elaborati solo gli attributi `firstName`, `lastName` e `mlScore`, mentre `address` non verrebbe influenzato.

Per garantire che le richieste di privacy elaborino tutti gli attributi pertinenti del cliente, devi fornire i valori di identità primaria per tutti i set di dati applicabili in cui tali attributi possono essere memorizzati (fino a un massimo di nove ID per cliente). Per ulteriori informazioni sui campi comunemente contrassegnati come identità, consulta la sezione sui campi di identità nelle [nozioni di base della composizione dello schema](../xdm/schema/composition.md#identity).

## Elaborazione richiesta di eliminazione {#delete}

Quando [!DNL Experience Platform] riceve una richiesta di eliminazione da [!DNL Privacy Service], [!DNL Platform] invia una conferma a [!DNL Privacy Service] che la richiesta è stata ricevuta e che i dati interessati sono stati contrassegnati per l&#39;eliminazione. I record vengono quindi rimossi al termine del processo di privacy.

>[!IMPORTANT]
>
>Le richieste di cancellazione della privacy non sono istantanee e possono variare a seconda dei servizi coinvolti e di altri fattori di impatto, come la posizione geografica. I tempi per il completamento dei processi relativi alla privacy possono variare da 15 a 45 giorni, ma non sono garantiti.

A seconda che il servizio Identity (`identity`) e il data lake (`aepDataLake`) siano stati inclusi o meno come prodotti nella richiesta di accesso a dati personali per il profilo (`ProfileService`), diversi set di dati relativi al profilo vengono rimossi dal sistema in momenti potenzialmente diversi:

| Prodotti inclusi | Effetti |
| --- | --- |
| Solo `ProfileService` | Il profilo viene eliminato immediatamente dopo l’invio da parte di Platform della conferma della ricezione della richiesta di eliminazione. Tuttavia, il grafico delle identità del profilo rimane ancora, e il profilo può potenzialmente essere ricostruito quando vengono acquisiti nuovi dati con le stesse identità. Anche i dati associati al profilo rimangono nel data lake. |
| `ProfileService` e `identity` | Il profilo e il grafico delle identità associato vengono eliminati immediatamente non appena Platform invia la conferma di ricezione della richiesta di eliminazione. I dati associati al profilo rimangono nel data lake. |
| `ProfileService` e `aepDataLake` | Il profilo viene eliminato immediatamente dopo l’invio da parte di Platform della conferma della ricezione della richiesta di eliminazione. Tuttavia, il grafico delle identità del profilo rimane ancora, e il profilo può potenzialmente essere ricostruito quando vengono acquisiti nuovi dati con le stesse identità.<br><br>Quando il prodotto del data lake risponde che la richiesta è stata ricevuta ed è in fase di elaborazione, i dati associati al profilo vengono eliminati in modo non permanente e pertanto non sono accessibili da alcun servizio [!DNL Platform]. Una volta completato il processo, i dati vengono rimossi completamente dal data lake. |
| `ProfileService`, `identity` e `aepDataLake` | Il profilo e il grafico delle identità associato vengono eliminati immediatamente non appena Platform invia la conferma di ricezione della richiesta di eliminazione.<br><br>Quando il prodotto del data lake risponde che la richiesta è stata ricevuta ed è in fase di elaborazione, i dati associati al profilo vengono eliminati in modo non permanente e pertanto non sono accessibili da alcun servizio [!DNL Platform]. Una volta completato il processo, i dati vengono rimossi completamente dal data lake. |

Per ulteriori informazioni sugli stati dei processi di tracciamento, consulta la [[!DNL Privacy Service] documentazione](../privacy-service/home.md#monitor).

### Richieste di profilo e richieste di identità {#profile-v-identity}

Se viene effettuata una richiesta di eliminazione per il profilo (`ProfileService`) ma non per Identity Service (`identity`), il processo risultante rimuove i dati degli attributi raccolti per un cliente (o un set di clienti) ma non le associazioni stabilite nel grafico delle identità.

Ad esempio, una richiesta di eliminazione che utilizza `email_id` e `customer_id` di un cliente rimuove tutti i dati degli attributi memorizzati con tali ID. Tuttavia, i dati successivamente acquisiti con lo stesso `customer_id` continueranno a essere associati a `email_id` appropriato, poiché l&#39;associazione esiste ancora.

Per rimuovere il profilo e tutte le associazioni di identità per un determinato cliente, assicurati di includere sia Profilo che Identity Service come prodotti di destinazione nelle richieste di eliminazione.

### Limitazioni dei criteri di unione {#merge-policy-limitations}

Privacy Service è in grado di elaborare solo i dati [!DNL Profile] utilizzando un criterio di unione che non esegue l&#39;unione delle identità. Se utilizzi l&#39;interfaccia utente per confermare se le richieste di accesso a dati personali vengono elaborate, assicurati di utilizzare un criterio con **[!DNL None]** come tipo [!UICONTROL ID stitching]. In altre parole, non è possibile utilizzare un criterio di unione in cui [!UICONTROL l&#39;unione ID] è impostata su [!UICONTROL Private Graph].

>![L&#39;unione ID del criterio di unione è impostata su Nessuno](./images/privacy/no-id-stitch.png)

## Passaggi successivi

Dopo aver letto questo documento, ti verranno presentati i concetti importanti relativi all&#39;elaborazione delle richieste di accesso a dati personali in [!DNL Experience Platform]. Per comprendere meglio come gestire i dati di identità e creare processi relativi alla privacy, continua a leggere la documentazione fornita in questa guida.

Per informazioni sull&#39;elaborazione delle richieste di accesso a dati personali per le risorse [!DNL Platform] non utilizzate da [!DNL Profile], vedere il documento sull&#39;elaborazione delle richieste di accesso a dati personali [ nel data lake](../catalog/privacy.md).
