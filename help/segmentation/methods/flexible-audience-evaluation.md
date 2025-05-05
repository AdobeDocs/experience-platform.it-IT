---
title: Guida flessibile alla valutazione del pubblico
description: Scopri come utilizzare la valutazione flessibile del pubblico per eseguire processi batch Segmentazione on-demand.
role: Developer, User
exl-id: b85bf735-be02-4bf7-bd63-8d74ae905e58
source-git-commit: 7084b05d1ae142016cb2158fd22d07a240385190
workflow-type: tm+mt
source-wordcount: '1063'
ht-degree: 5%

---

# Guida flessibile alla valutazione del pubblico

>[!AVAILABILITY]
>
>La valutazione flessibile del pubblico è **disponibile solo** sulle istanze di Experience Platform in esecuzione su [!DNL Microsoft Azure]. Per ulteriori informazioni sull&#39;infrastruttura Experience Platform supportata, vedere la [panoramica Experience Platform multi cloud](../../landing/multi-cloud.md).
>
>Inoltre, la valutazione flessibile del pubblico è **disponibile solo** per l&#39;uso con CDP in tempo reale B2C Edition.

La valutazione flessibile dell&#39;audience consente di eseguire un batch Segmentazione job on-demand. Grazie alla valutazione flessibile del pubblico, puoi eseguire lanci di campagne annuncio-hoc, comunicazioni just-in-time o altre attività urgenti.

## Guardrail {#guardrails}

>[!CONTEXTUALHELP]
>id="platform_segmentation_browse_flexibleaudienceevaluation"
>title="Limiti flessibili per la valutazione del pubblico"
>abstract="È possibile valutare fino a 20 tipi di pubblico in un’unica esecuzione di valutazione del pubblico flessibile.<br/><br/>Inoltre, mentre il processo di valutazione viene eseguito il prima possibile, potrebbero verificarsi ritardi di sistema poiché le valutazioni su richiesta <b>non possono</b> essere eseguite contemporaneamente a un’altra valutazione su richiesta o in batch."

Quando esegui una valutazione flessibile del pubblico, tieni presenti le seguenti condizioni:

- Puoi utilizzare la valutazione **flessibile del pubblico solo due volte** al giorno per sandbox. Questo limite viene reimpostato a mezzanotte (UTC).
- Hai un **massimo** di 50 esecuzioni flessibili di valutazione del pubblico all&#39;anno per sandbox **di produzione** .
- Hai un **massimo** di 100 esecuzioni flessibili di valutazione del pubblico all&#39;anno per ogni **sandbox di sviluppo** .
- Tutti i tipi di **pubblico devono** avere un&#39;origine di &quot;Servizio di segmentazione&quot;.
- Tutti i tipi di pubblico devono **essere valutati** utilizzando Segmentazione batch.
- Tutti i tipi di **pubblico devono** essere basati sulle persone.
- Puoi selezionare solo un massimo di 20 tipi di pubblico per ogni esecuzione flessibile di valutazione.

>[!NOTE]
>
>Puoi acquistare ulteriori esecuzioni di valutazione flessibili del pubblico all&#39;anno. Per ulteriori informazioni, contatta Adobe Systems l&#39;Assistenza clienti.

## Accesso {#access}

Per utilizzare la valutazione flessibile del pubblico, devi disporre dei seguenti autorizzazione:

- **[!UICONTROL Valuta il segmento a un pubblico]** sotto la **[!DNL Profile Management]** sezione.

Per ulteriori informazioni sul controllo accesso basato sui ruoli, leggere la panoramica[&#128279;](../../access-control/home.md) del controllo accesso.

## Esecuzione di una valutazione flessibile del pubblico

Puoi eseguire una valutazione flessibile dell&#39;audience utilizzando le API Experience Platform o interfaccia.

>[!BEGINTABS]

>[!TAB API Experience Platform]

Per eseguire una valutazione flessibile dell&#39;audience all&#39;interno delle API Experience Platform, devi creare un processo di segmento che contenga gli ID di tutte le definizioni di segmento (audience) che desideri valutare.

>[!NOTE]
>
>Puoi aggiungere solo un **massimo** di 20 ID di definizione di segmento per ogni chiamata API del processo di segmento.

È possibile creare un nuovo processo di segmento effettuando una richiesta POST all&#39;endpoint `/segment/jobs` e includendo gli ID delle definizioni del segmento nel corpo del richiesta.

+++Un richiesta di esempio per la creazione di un nuovo processo segmento

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/jobs \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '[
    {
        "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e"
    },
    {
        "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85"
    }
 ]'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `segmentId` | ID della definizione del segmento che si desidera valutare. Queste definizioni di segmento possono appartenere a criteri di unione diversi. |

+++

Una risposta corretta restituisce lo stato HTTP 200 con le informazioni sul processo di segmento appena creato.

+++ Risposta di esempio durante la creazione di un nuovo processo segmento.

```json
{
    "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "PROCESSING",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e",
            "segment": {
                "id": "7863c010-e092-41c8-ae5e-9e533186752e",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85",
            "segment": {
                "id": "07d39471-05d1-4083-a310-d96978fd7c85",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1573203617195,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 778460
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1573204266727,
            "endTimeInMs": 1573204395655,
            "totalTimeInMs": 128928
        },
        "segmentedProfileCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":1033
        },
        "segmentedProfileByNamespaceCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "tenantiduserobjid":1033,
                "campaign_profile_mscom_mkt_prod2":1033
            }
        },
        "segmentedProfileByStatusCounter":{
            "7863c010-e092-41c8-ae5e-9e533186752e":{
                "exited":144646,
                "realized":2056
            }
        },
        "totalProfiles":13146432,
        "totalProfilesByMergePolicy":{
            "25c548a0-ca7f-4dcd-81d5-997642f178b9":13146432
        }
    },
    "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "properties": {
        "scheduleId": "4e538382-dbd8-449e-988a-4ac639ebe72b",
        "runId": "e6c1308d-0d4b-4246-b2eb-43697b50a149"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
            "method": "GET"
        }
    },
    "updateTime": 1573204395000,
    "creationTime": 1573203600535,
    "updateEpoch": 1573204395
}
```

+++

Dopo aver creato il processo di segmento, puoi verificarne lo stato effettuando una richiesta GET all&#39;endpoint `/segment/jobs` , fornendo l&#39;ID del processo di segmento appena creato nel percorso richiesta.

+++richiesta di esempio per recuperare un processo di segmento

```shell
curl -X GET https://platform.adobe.io/data/core/ups/segment/jobs/b31aed3d-b3b1-4613-98c6-7d3846e8d48f \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

Una risposta corretta restituisce lo stato HTTP 200 con informazioni dettagliate sul processo di segmento specificato.


+++ Risposta di esempio per il recupero di un processo di segmento.

```json
{
    "id": "b31aed3d-b3b1-4613-98c6-7d3846e8d48f",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "profileInstanceId": "ups",
    "source": "api",
    "status": "SUCCEEDED",
    "batchId": "678f53bc-e21d-4c47-a7ec-5ad0064f8e4c",
    "computeJobId": 8811,
    "computeGatewayJobId": "9ea97b25-a0f5-410e-ae87-b2d85e58f399",
    "segments": [
        {
            "segmentId": "7863c010-e092-41c8-ae5e-9e533186752e",
            "segment": {
                "id": "7863c010-e092-41c8-ae5e-9e533186752e",
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "07d39471-05d1-4083-a310-d96978fd7c85",
            "segment": {
                "id": "07d39471-05d1-4083-a310-d96978fd7c85",
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "workAddress.country = \"US\""
                },
                "mergePolicyId": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                "mergePolicy": {
                    "id": "25c548a0-ca7f-4dcd-81d5-997642f178b9",
                    "version": 1
                }
            }
        }
    ],
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1579304313411
        },
        "profileSegmentationTime": {}
    },
    "requestId": "4e538382-dbd8-449e-988a-4ac639ebe72b-1573203600264",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "_links": {
        "cancel": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/d3b4a50d-dfea-43eb-9fca-557ea53771fd",
            "method": "GET"
        }
    },
    "updateTime": 1579304339000,
    "creationTime": 1579304260897,
    "updateEpoch": 1579304339
}
```

+++

>[!TAB Experience Platform interfaccia]

Per eseguire una valutazione flessibile dell&#39;audience all&#39;interno del interfaccia Experience Platform, seleziona **[!UICONTROL Audiences]** nella **[!UICONTROL sezione Clienti]** .

![Vengono evidenziate le pulsante Audiences all&#39;interno della sezione Clienti. Viene visualizzato il Audience Portal per i profili dei clienti.](../images/methods/fae/audience-portal.png)

Viene visualizzato il portale del pubblico con un elenco di tutti i tipi di pubblico dell&#39;organizzazione. In Audience Portal, puoi scegliere i tipi di pubblico da valutare e selezionare **[!UICONTROL Valuta pubblico]**.

![Vengono selezionati i tipi di pubblico per i quali desideri utilizzare la valutazione flessibile del pubblico.](../images/methods/fae/evaluate-audiences.png)

Viene visualizzato il **[!UICONTROL popover Valuta pubblico on-demand]** , con l&#39;elenco dei tipi di pubblico che verranno valutati con il processo di segmento su richiesta. Se un pubblico non è idoneo a essere valutato on-demand, verrà automaticamente rimosso dal lavoro di valutazione. Verifica che i tipi di pubblico elencati siano quelli che desideri valutare.

![Vengono visualizzati i tipi di pubblico che possono essere valutati utilizzando una valutazione flessibile.](../images/methods/fae/evaluate-audiences-modal.png)

Dopo aver confermato che sono elencati i tipi di pubblico corretti, puoi procedere con l&#39;richiesta e inizierà la valutazione flessibile del pubblico. Puoi visualizzare lo stato di questa valutazione del pubblico nella vista[&#128279;](../../dataflows/ui/monitor-audiences.md#evaluation-job-details) Monitoraggio del processo di valutazione.

>[!NOTE]
>
>Lo stato del processo di segmento può essere riportato come nello stato &quot;In coda&quot; all&#39;interno del dashboard di monitoraggio. È possibile visualizzare lo stato più aggiornato del processo di segmento effettuando una richiesta GET all&#39;endpoint `/segment/jobs` , fornendo l&#39;ID del processo di segmento nel percorso richiesta. Ulteriori informazioni sull&#39;utilizzo di questo endpoint sono disponibili in API scheda.
>
>Se esegui una valutazione flessibile del pubblico e desideri che la valutazione attivi il pubblico verso una destinazione, devi assicurarti che la frequenza sia impostata su **[!UICONTROL Dopo la valutazione]** del segmento. L&#39;esecuzione di una valutazione flessibile del pubblico sui tipi di pubblico che sono già impostati per essere attivati [dopo la valutazione](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files) del segmento, attiverà i tipi di pubblico non appena termina il processo di valutazione del pubblico flessibile, indipendentemente da eventuali precedenti processi di attivazione giornaliera.

>[!ENDTABS]

## Video {#video}

Il video seguente illustra come accesso e utilizzare la valutazione flessibile del pubblico in Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/3453648?&captions=ita)

## Domande frequenti {#faq}

Nella sezione seguente sono elencate le domande frequenti relative alla valutazione flessibile del pubblico.

### Quando posso attivare un pubblico utilizzando una valutazione flessibile del pubblico?

+++ Risposta

È possibile attivare un pubblico utilizzando una valutazione flessibile del pubblico subito dopo la creazione.

+++

### Posso eseguire la pianificazione con una valutazione flessibile del pubblico?

+++ Risposta

No, la programmazione non è disponibile per la valutazione flessibile del pubblico.

+++

### Devo eseguire un ulteriore processo di esportazione quando uso la valutazione flessibile del pubblico?

+++ Risposta

No, il processo di esportazione viene eseguito automaticamente dopo aver completato il processo di segmento corrispondente.

+++

### Quali servizi posso utilizzare per i tipi di pubblico valutati con una valutazione flessibile?

+++ Risposta

Puoi usare i tipi di pubblico in tutti i servizi a valle, incluse le destinazioni e i percorsi Adobe Systems Ottimizzatore percorso.

+++

### Quando vengono ripristinati i limiti flessibili di valutazione del pubblico?

+++ Risposta

Il limite giornaliero viene reimpostato a mezzanotte (UTC). Il limite annuale viene reimpostato alla data di scadenza del contratto.

+++

### Quali tipi di pubblico sono supportati con una valutazione flessibile del pubblico?

+++ Risposta

Solo i tipi di pubblico con l&#39;origine del servizio di segmentazione sono supportati per una valutazione flessibile del pubblico. Altri tipi di pubblico, come composizioni, caricamento personalizzato o Distiller dati, non sono supportati per una valutazione flessibile del pubblico.

+++

### Quali corse contribuiscono al conteggio flessibile delle corse di valutazione del pubblico?

+++ Risposta

Le esecuzioni di valutazione flessibili del pubblico create utilizzando l&#39;API o il interfaccia vengono conteggiate ai fini del limite massimo. Tuttavia, l&#39;esecuzione giornaliera di batch Segmentazione processi che viene eseguita su base **notturna non** contribuisce a questo limite.

+++

