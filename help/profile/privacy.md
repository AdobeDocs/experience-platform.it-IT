---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Elaborazione delle richieste di privacy nel profilo cliente in tempo reale
type: Documentation
description: Adobe Experience Platform Privacy Service elabora le richieste dei clienti di accedere ai propri dati personali, rinunciarvi o cancellarli, come indicato da numerose normative sulla privacy. Questo documento descrive i concetti essenziali relativi all’elaborazione delle richieste di accesso a dati personali per Real-Time Customer Profile.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: f0179bacc55134241bed8de240ee632d0f38e4b6
workflow-type: tm+mt
source-wordcount: '1625'
ht-degree: 0%

---

# Elaborazione della richiesta di accesso a dati personali in [!DNL Real-Time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] tratta le richieste dei clienti di accedere ai propri dati personali, di rinunciarvi o di cancellarli, come definito dalle normative sulla privacy come il Regolamento generale sulla protezione dei dati (RGPD) e [!DNL California Consumer Privacy Act] (CCPA)

Questo documento descrive i concetti essenziali relativi all’elaborazione delle richieste di accesso a dati personali per [!DNL Real-Time Customer Profile] in Adobe Experience Platform.

>[!NOTE]
>
>Questa guida descrive solo come effettuare richieste di accesso ai dati personali per l’archivio dati profilo in Experienci Platform. Se prevedi anche di effettuare richieste di privacy per il data lake di Platform, consulta la guida su [elaborazione della richiesta di accesso a dati personali nel data lake](../catalog/privacy.md) oltre a questa esercitazione.
>
>Per i passaggi su come effettuare richieste di privacy per altre applicazioni Adobe Experience Cloud, consulta [Documentazione di Privacy Service](../privacy-service/experience-cloud-apps.md).

>[!IMPORTANT]
>
>La richiesta di accesso a dati personali in questa guida **non** coprono le entità non personali B2B.

## Introduzione

Questa guida richiede una buona conoscenza di quanto segue [!DNL Platform] componenti:

* [[!DNL Privacy Service]](../privacy-service/home.md): gestisce le richieste dei clienti di accedere ai propri dati personali, rinunciarvi o eliminarli nelle applicazioni Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): risolve la sfida fondamentale posta dalla frammentazione dei dati sull’esperienza del cliente, collegando le identità tra dispositivi e sistemi.
* [[!DNL Real-Time Customer Profile]](home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Informazioni sugli spazi dei nomi delle identità {#namespaces}

Adobe Experience Platform [!DNL Identity Service] collega i dati di identità del cliente tra sistemi e dispositivi. [!DNL Identity Service] utilizza **spazi dei nomi di identità** fornire contesto ai valori di identità collegandoli al loro sistema di origine. Uno spazio dei nomi può rappresentare un concetto generico come un indirizzo e-mail (&quot;E-mail&quot;) o associare l’identità a un’applicazione specifica, come un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o un Adobe Target ID (&quot;TNTID&quot;).

Identity Service gestisce un archivio di spazi dei nomi di identità definiti a livello globale (standard) e definiti dall’utente (personalizzati). Gli spazi dei nomi standard sono disponibili per tutte le organizzazioni (ad esempio, &quot;E-mail&quot; e &quot;ECID&quot;), mentre l’organizzazione può anche creare spazi dei nomi personalizzati in base alle sue esigenze specifiche.

Per ulteriori informazioni sugli spazi dei nomi di identità in [!DNL Experience Platform], vedere [panoramica dello spazio dei nomi delle identità](../identity-service/namespaces.md).

## Invio di richieste {#submit}

Le sezioni seguenti descrivono come effettuare richieste di accesso a dati personali per [!DNL Real-Time Customer Profile] utilizzando [!DNL Privacy Service] API o interfaccia utente. Prima di leggere queste sezioni, è consigliabile rivedere [API PRIVACY SERVICE](../privacy-service/api/getting-started.md) o [Interfaccia utente di Privacy Service](../privacy-service/ui/overview.md) documentazione relativa ai passaggi completi su come inviare un processo di privacy, incluso come formattare correttamente i dati di identità utente inviati nei payload di richiesta.

>[!IMPORTANT]
>
>Privacy Service è in grado di elaborare solo [!DNL Profile] dati utilizzando un criterio di unione che non esegue l’unione di identità. Consulta la sezione su [limitazioni dei criteri di unione](#merge-policy-limitations) per ulteriori informazioni.
>
>Tieni presente che il tempo necessario per completare una richiesta di accesso a dati personali **non può** essere garantita. Se si verificano modifiche nel [!DNL Profile] durante l’elaborazione di una richiesta, non è possibile garantire anche se tali record vengono elaborati o meno.

### Mediante l’API

Durante la creazione di richieste di lavoro nell’API, tutti gli ID forniti in `userIDs` deve utilizzare uno specifico `namespace` e `type`. Un valore valido [spazio dei nomi delle identità](#namespaces) riconosciuto da [!DNL Identity Service] deve essere fornito per `namespace` valore, mentre il `type` deve essere `standard` o `unregistered` (rispettivamente per spazi dei nomi standard e personalizzati).

>[!NOTE]
>
>Potresti dover fornire più di un ID per ogni cliente, a seconda del grafico delle identità e di come i frammenti di profilo sono distribuiti nei set di dati di Platform. Vedere la sezione successiva [frammenti di profilo](#fragments) per ulteriori informazioni.

Inoltre, la `include` l’array del payload della richiesta deve includere i valori del prodotto per i diversi archivi di dati a cui viene effettuata la richiesta. Per eliminare i dati di profilo associati a un’identità, l’array deve includere il valore `ProfileService`. Per eliminare le associazioni del grafico delle identità del cliente, l’array deve includere il valore `identity`.

>[!NOTE]
>
>Consulta la sezione su [richieste di profilo e richieste di identità](#profile-v-identity) più avanti in questo documento per informazioni più dettagliate sugli effetti dell&#39;utilizzo di `ProfileService` e `identity` all&#39;interno del `include` array.

La seguente richiesta crea un nuovo processo di privacy per i dati di un singolo cliente in [!DNL Profile] archiviare. Due valori di identità sono forniti per il cliente nel `userIDs` array; uno che utilizza lo standard `Email` dello spazio dei nomi dell’identità e l’altro utilizzando un `Customer_ID` spazio dei nomi. Include inoltre il valore del prodotto per [!DNL Profile] (`ProfileService`) in `include` array:

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
>Platform elabora le richieste di privacy in tutti [sandbox](../sandboxes/home.md) appartenenti alla tua organizzazione. Di conseguenza, qualsiasi `x-sandbox-name` l’intestazione inclusa nella richiesta viene ignorata dal sistema.

**Risposta del prodotto**

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

Quando crei richieste di lavoro nell’interfaccia utente, assicurati di selezionare **[!UICONTROL Data lake AEP]** e/o **[!UICONTROL Profilo]** in **[!UICONTROL Prodotti]** per elaborare i processi per i dati memorizzati nel data lake o [!DNL Real-Time Customer Profile], rispettivamente.

![È in corso la creazione di una richiesta di processo di accesso nell’interfaccia utente, con l’opzione Profilo selezionata in Prodotti](./images/privacy/product-value.png)

## Frammenti di profilo nelle richieste di accesso a dati personali {#fragments}

In [!DNL Profile] archivio dati, i dati personali di un singolo cliente sono spesso costituiti da più frammenti di profilo, associati alla persona tramite il grafico delle identità. Quando si inviano richieste di accesso a dati personali a [!DNL Profile] store, è importante notare che le richieste vengono elaborate solo a livello di frammento di profilo, anziché all’intero profilo.

Ad esempio, considera una situazione in cui stai memorizzando i dati degli attributi del cliente in tre set di dati separati, che utilizzano identificatori diversi per associare tali dati ai singoli clienti:

| Nome del set di dati | Campo di identità primaria | Attributi memorizzati |
| --- | --- | --- |
| Set di dati 1 | `customer_id` | `address` |
| Set di dati 2 | `email_id` | `firstName`, `lastName` |
| Set di dati 3 | `email_id` | `mlScore` |

Uno dei set di dati utilizza `customer_id` come identificatore primario, mentre gli altri due usano `email_id`. Se invii una richiesta di accesso o cancellazione dei dati personali utilizzando solo `email_id` come valore ID utente, solo il `firstName`, `lastName`, e `mlScore` gli attributi vengono elaborati, mentre `address` non ne risentirebbe.

Per garantire che le richieste di privacy elaborino tutti gli attributi pertinenti del cliente, devi fornire i valori di identità primaria per tutti i set di dati applicabili in cui tali attributi possono essere memorizzati (fino a un massimo di nove ID per cliente). Consulta la sezione sui campi di identità in [nozioni di base sulla composizione dello schema](../xdm/schema/composition.md#identity) per ulteriori informazioni sui campi comunemente contrassegnati come identità.

## Elaborazione richiesta di eliminazione {#delete}

Quando [!DNL Experience Platform] riceve una richiesta di eliminazione da [!DNL Privacy Service], [!DNL Platform] invia una conferma a [!DNL Privacy Service] che la richiesta è stata ricevuta e che i dati interessati sono stati contrassegnati per l’eliminazione. I record vengono quindi rimossi al termine del processo di privacy.

>[!IMPORTANT]
>
>Le richieste di cancellazione della privacy non sono istantanee e possono variare a seconda dei servizi coinvolti e di altri fattori di impatto, come la posizione geografica. I tempi per il completamento dei processi relativi alla privacy possono variare da 15 a 45 giorni, ma non sono garantiti.

A seconda che tu abbia incluso o meno il servizio Identity (`identity`) e il data lake (`aepDataLake`) come prodotti nella richiesta di accesso a dati personali per il profilo (`ProfileService`), diversi set di dati relativi al profilo vengono rimossi dal sistema in momenti potenzialmente diversi:

| Prodotti inclusi | Effetti |
| --- | --- |
| `ProfileService` solo | Il profilo viene eliminato immediatamente dopo l’invio da parte di Platform della conferma della ricezione della richiesta di eliminazione. Tuttavia, il grafico delle identità del profilo rimane ancora, e il profilo può potenzialmente essere ricostruito quando vengono acquisiti nuovi dati con le stesse identità. Anche i dati associati al profilo rimangono nel data lake. |
| `ProfileService` e `identity` | Il profilo e il grafico delle identità associato vengono eliminati immediatamente non appena Platform invia la conferma di ricezione della richiesta di eliminazione. I dati associati al profilo rimangono nel data lake. |
| `ProfileService` e `aepDataLake` | Il profilo viene eliminato immediatamente dopo l’invio da parte di Platform della conferma della ricezione della richiesta di eliminazione. Tuttavia, il grafico delle identità del profilo rimane ancora, e il profilo può potenzialmente essere ricostruito quando vengono acquisiti nuovi dati con le stesse identità.<br><br>Quando il prodotto del data lake risponde che la richiesta è stata ricevuta e che è in fase di elaborazione, i dati associati al profilo vengono eliminati in modo non permanente e non sono quindi accessibili a nessuno [!DNL Platform] servizio. Una volta completato il processo, i dati vengono rimossi completamente dal data lake. |
| `ProfileService`, `identity`, e `aepDataLake` | Il profilo e il grafico delle identità associato vengono eliminati immediatamente non appena Platform invia la conferma di ricezione della richiesta di eliminazione.<br><br>Quando il prodotto del data lake risponde che la richiesta è stata ricevuta e che è in fase di elaborazione, i dati associati al profilo vengono eliminati in modo non permanente e non sono quindi accessibili a nessuno [!DNL Platform] servizio. Una volta completato il processo, i dati vengono rimossi completamente dal data lake. |

Consulta la sezione [[!DNL Privacy Service] documentazione](../privacy-service/home.md#monitor) per ulteriori informazioni sul tracciamento degli stati dei processi.

### Richieste di profilo e richieste di identità {#profile-v-identity}

Se viene effettuata una richiesta di eliminazione per il profilo (`ProfileService`) ma non Identity Service (`identity`), il processo risultante rimuove i dati attributo raccolti per un cliente (o un set di clienti) ma non le associazioni stabilite nel grafico delle identità.

Ad esempio, una richiesta di eliminazione che utilizza `email_id` e `customer_id` rimuove tutti i dati attributo memorizzati sotto tali ID. Tuttavia, i dati successivamente acquisiti con lo stesso `customer_id` sarà ancora associato al `email_id`, poiché l’associazione esiste ancora.

Per rimuovere il profilo e tutte le associazioni di identità per un determinato cliente, assicurati di includere sia Profilo che Identity Service come prodotti di destinazione nelle richieste di eliminazione.

### Limitazioni dei criteri di unione {#merge-policy-limitations}

Privacy Service è in grado di elaborare solo [!DNL Profile] dati utilizzando un criterio di unione che non esegue l’unione di identità. Se utilizzi l’interfaccia utente per confermare se le richieste di accesso a dati personali vengono elaborate, assicurati di utilizzare una policy con **[!DNL None]** come [!UICONTROL Unione ID] tipo. In altre parole, non è possibile utilizzare un criterio di unione in cui [!UICONTROL Unione ID] è impostato su [!UICONTROL Private Graph].

>![L’unione ID del criterio di unione è impostata su Nessuno](./images/privacy/no-id-stitch.png)

## Passaggi successivi

Dopo aver letto questo documento, ti vengono presentati i concetti importanti relativi all’elaborazione delle richieste di accesso a dati personali in [!DNL Experience Platform]. Per comprendere meglio come gestire i dati di identità e creare processi relativi alla privacy, continua a leggere la documentazione fornita in questa guida.

Per informazioni sull’elaborazione delle richieste di accesso a dati personali per [!DNL Platform] risorse non utilizzate da [!DNL Profile], consulta il documento su [elaborazione della richiesta di accesso a dati personali nel data lake](../catalog/privacy.md).
