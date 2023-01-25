---
keywords: Experience Platform;home;argomenti popolari
solution: Experience Platform
title: Elaborazione delle richieste di privacy nel profilo cliente in tempo reale
type: Documentation
description: Adobe Experience Platform Privacy Service elabora le richieste dei clienti relative all’accesso, alla rinuncia alla vendita o alla cancellazione dei propri dati personali come delineato da numerose normative sulla privacy. Questo documento tratta i concetti essenziali relativi all’elaborazione delle richieste di privacy per il profilo cliente in tempo reale.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: d41606e4df297d11b4e0e755363d362e075e862c
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 0%

---

# Elaborazione della richiesta di privacy in [!DNL Real-Time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] elabora le richieste dei clienti per accedere, rinunciare alla vendita o cancellare i propri dati personali come delineato dalle normative sulla privacy, come il Regolamento generale sulla protezione dei dati (RGPD) e [!DNL California Consumer Privacy Act] (CCPA).

Questo documento tratta i concetti essenziali relativi all’elaborazione delle richieste di privacy per [!DNL Real-Time Customer Profile] in Adobe Experience Platform.

>[!NOTE]
>
>Questa guida descrive solo come effettuare richieste sulla privacy per i dati del profilo archiviati in Experience Platform. Se prevedi anche di effettuare richieste di privacy per il data lake di Platform, consulta la guida su [elaborazione della richiesta di accesso a dati nel lago dati](../catalog/privacy.md) oltre a questa esercitazione.
>
>Per i passaggi su come effettuare richieste di privacy per altre applicazioni Adobe Experience Cloud, consulta [Documentazione di Privacy Service](../privacy-service/experience-cloud-apps.md).

## Introduzione

Questa guida richiede una buona comprensione dei seguenti elementi [!DNL Platform] componenti:

* [[!DNL Privacy Service]](../privacy-service/home.md): Gestisce le richieste dei clienti relative all’accesso, alla rinuncia alla vendita o all’eliminazione dei loro dati personali tra le applicazioni Adobe Experience Cloud.
* [[!DNL Identity Service]](../identity-service/home.md): Risolve la sfida fondamentale rappresentata dalla frammentazione dei dati sulla customer experience attraverso il collegamento di identità tra dispositivi e sistemi.
* [[!DNL Real-Time Customer Profile]](home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

## Informazioni sugli spazi dei nomi delle identità {#namespaces}

Adobe Experience Platform [!DNL Identity Service] collega i dati di identità dei clienti tra sistemi e dispositivi. [!DNL Identity Service] utilizza **spazi dei nomi delle identità** fornire un contesto ai valori d&#39;identità collegandoli al loro sistema d&#39;origine. Uno spazio dei nomi può rappresentare un concetto generico, ad esempio un indirizzo e-mail (&quot;E-mail&quot;) o associare l’identità a un’applicazione specifica, ad esempio un Adobe Advertising Cloud ID (&quot;AdCloud&quot;) o un Adobe Target ID (&quot;TNTID&quot;).

Identity Service conserva un archivio di namespace di identità definiti a livello globale (standard) e definiti dall’utente (personalizzati). Gli spazi dei nomi standard sono disponibili per tutte le organizzazioni (ad esempio, &quot;E-mail&quot; ed &quot;ECID&quot;), mentre l’organizzazione può anche creare spazi dei nomi personalizzati in base alle proprie esigenze.

Per ulteriori informazioni sugli spazi dei nomi delle identità in [!DNL Experience Platform], vedi [panoramica dello spazio dei nomi identità](../identity-service/namespaces.md).

## Invio di richieste {#submit}

Le sezioni seguenti illustrano come effettuare richieste di accesso a dati personali per [!DNL Real-Time Customer Profile] utilizzando [!DNL Privacy Service] API o interfaccia utente. Prima di leggere queste sezioni, si consiglia vivamente di rivedere il [API Privacy Service](../privacy-service/api/getting-started.md) o [Interfaccia utente di Privacy Service](../privacy-service/ui/overview.md) documentazione completa sui passaggi per l’invio di un processo relativo alla privacy, inclusa la modalità di formattazione corretta dei dati di identità utente inviati nei payload della richiesta.

>[!IMPORTANT]
>
>Privacy Service è in grado di elaborare solo [!DNL Profile] i dati che utilizzano un criterio di unione che non esegue la combinazione di identità. Vedi la sezione su [limitazioni dei criteri di unione](#merge-policy-limitations) per ulteriori informazioni.
>
>Tieni presente che il tempo necessario per completare una richiesta di accesso a dati personali può richiedere **impossibile** essere garantiti. Se si verificano modifiche nel [!DNL Profile] i dati durante l&#39;elaborazione di una richiesta, indipendentemente dal fatto che tali record siano o meno elaborati, non possono essere garantiti.

### Mediante l’API

Quando crei richieste di lavoro nell&#39;API, qualsiasi ID fornito in `userIDs` deve utilizzare un `namespace` e `type`. Una valida [spazio dei nomi identità](#namespaces) riconosciuti [!DNL Identity Service] devono essere previste `namespace` , mentre `type` deve `standard` o `unregistered` (per namespace standard e personalizzati, rispettivamente).

>[!NOTE]
>
>Potrebbe essere necessario fornire più di un ID per ciascun cliente, a seconda del grafico delle identità e della distribuzione dei frammenti di profilo nei set di dati di Platform. Vedi la sezione successiva [frammenti di profilo](#fragments) per ulteriori informazioni.

Inoltre, il `include` la matrice del payload della richiesta deve includere i valori di prodotto per i diversi archivi di dati in cui viene effettuata la richiesta. Per eliminare i dati del profilo associati a un&#39;identità, la matrice deve includere il valore `ProfileService`. Per eliminare le associazioni del grafico delle identità del cliente, l&#39;array deve includere il valore `identity`.

>[!NOTE]
>
>Vedi la sezione su [richieste di profilo e richieste di identità](#profile-v-identity) più avanti in questo documento per informazioni più dettagliate sugli effetti dell&#39;uso `ProfileService` e `identity` all&#39;interno del `include` array.

La seguente richiesta crea un nuovo processo di privacy per i dati di un singolo cliente nel [!DNL Profile] archiviare. Per il cliente vengono forniti due valori di identità nel `userIDs` array; uno che utilizza lo standard `Email` spazio dei nomi di identità e l&#39;altro utilizzando un `Customer_ID` spazio dei nomi. Include inoltre il valore del prodotto per [!DNL Profile] (`ProfileService`) nel `include` array:

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
>Platform elabora le richieste di privacy in tutti [sandbox](../sandboxes/home.md) appartenente alla tua organizzazione. Di conseguenza, qualsiasi `x-sandbox-name` l’intestazione inclusa nella richiesta viene ignorata dal sistema.

**Risposta del prodotto**

Per il Servizio profili, una volta completato il processo di privacy, viene restituita una risposta in formato JSON con le informazioni relative agli ID utente richiesti.

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

### Utilizzo dell’interfaccia

Quando crei richieste di lavoro nell’interfaccia utente, assicurati di selezionare **[!UICONTROL AEP Data Lake]** e/o **[!UICONTROL Profilo]** sotto **[!UICONTROL Prodotti]** al fine di elaborare lavori per i dati memorizzati nel lago di dati o [!DNL Real-Time Customer Profile], rispettivamente.

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

## Elimina elaborazione richiesta {#delete}

Quando [!DNL Experience Platform] riceve una richiesta di cancellazione da [!DNL Privacy Service], [!DNL Platform] invia conferma a [!DNL Privacy Service] che la richiesta è stata ricevuta e i dati interessati sono stati contrassegnati per l’eliminazione. I record vengono quindi rimossi al termine del processo di privacy.

A seconda che tu abbia incluso o meno il servizio Identity (`identity`) e il lago dati (`aepDataLake`) come prodotti nella richiesta di accesso a dati personali per il profilo (`ProfileService`), diversi set di dati relativi al profilo vengono rimossi dal sistema in momenti potenzialmente diversi:

| Prodotti inclusi | Effetti |
| --- | --- |
| `ProfileService` only | Il profilo viene eliminato immediatamente non appena Platform invia la conferma della ricezione della richiesta di eliminazione. Tuttavia, il grafico dell’identità del profilo rimane ancora e il profilo può potenzialmente essere ricostruito in seguito all’acquisizione di nuovi dati con le stesse identità. Anche i dati associati al profilo rimangono nel lago dati. |
| `ProfileService` e `identity` | Il profilo e il relativo grafico di identità vengono eliminati immediatamente non appena Platform invia la conferma della ricezione della richiesta di eliminazione. I dati associati al profilo rimangono nel data lake. |
| `ProfileService` e `aepDataLake` | Il profilo viene eliminato immediatamente non appena Platform invia la conferma della ricezione della richiesta di eliminazione. Tuttavia, il grafico dell’identità del profilo rimane ancora e il profilo può potenzialmente essere ricostruito in seguito all’acquisizione di nuovi dati con le stesse identità.<br><br>Quando il prodotto data lake risponde che la richiesta è stata ricevuta e sta attualmente elaborando, i dati associati al profilo vengono eliminati in modo morbido e non sono quindi accessibili da alcun [!DNL Platform] servizio. Una volta completato il lavoro, i dati vengono rimossi completamente dal data lake. |
| `ProfileService`, `identity`, e `aepDataLake` | Il profilo e il relativo grafico di identità vengono eliminati immediatamente non appena Platform invia la conferma della ricezione della richiesta di eliminazione.<br><br>Quando il prodotto data lake risponde che la richiesta è stata ricevuta e sta attualmente elaborando, i dati associati al profilo vengono eliminati in modo morbido e non sono quindi accessibili da alcun [!DNL Platform] servizio. Una volta completato il lavoro, i dati vengono rimossi completamente dal data lake. |

Fai riferimento a [[!DNL Privacy Service] documentazione](../privacy-service/home.md#monitor) per ulteriori informazioni sul tracciamento degli stati dei processi.

### Richieste di profilo e richieste di identità {#profile-v-identity}

Se viene effettuata una richiesta di cancellazione per Profilo (`ProfileService`) ma non il servizio Identity (`identity`), il processo risultante rimuove i dati degli attributi raccolti per un cliente (o set di clienti) ma non rimuove le associazioni stabilite nel grafico delle identità.

Ad esempio, una richiesta di cancellazione che utilizza un `email_id` e `customer_id` rimuove tutti i dati attributo memorizzati in tali ID. Tuttavia, qualsiasi dato successivamente acquisito in base agli stessi `customer_id` saranno ancora associati al `email_id`, poiché l&#39;associazione esiste ancora.

Per rimuovere il profilo e tutte le associazioni di identità per un dato cliente, assicurati di includere sia il servizio Profilo che il servizio Identity come prodotti di destinazione nelle richieste di eliminazione.

### Limiti dei criteri di unione {#merge-policy-limitations}

Privacy Service è in grado di elaborare solo [!DNL Profile] i dati che utilizzano un criterio di unione che non esegue la combinazione di identità. Se utilizzi l’interfaccia utente per confermare se le richieste di privacy sono in fase di elaborazione, assicurati di utilizzare un criterio con **[!DNL None]** come [!UICONTROL unione degli ID] digitare. In altre parole, non è possibile utilizzare un criterio di unione in cui [!UICONTROL unione degli ID] è impostato su [!UICONTROL Grafico privato].
>![L&#39;unione ID del criterio di unione è impostata su Nessuno](./images/privacy/no-id-stitch.png)
>
## Passaggi successivi

Leggendo questo documento, ti sono stati introdotti i concetti importanti relativi all’elaborazione delle richieste di privacy in [!DNL Experience Platform]. Per comprendere meglio come gestire i dati di identità e creare processi per la privacy, continua a leggere la documentazione fornita in questa guida.

Per informazioni sull’elaborazione delle richieste di accesso a dati personali per [!DNL Platform] risorse non utilizzate da [!DNL Profile], consulta il documento in [elaborazione della richiesta di accesso a dati nel lago dati](../catalog/privacy.md).
