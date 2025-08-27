---
title: Guida alla segmentazione di Edge
description: Scopri come utilizzare la segmentazione Edge per valutare i tipi di pubblico in Experience Platform istantaneamente al limite, abilitando casi di utilizzo di personalizzazione della pagina stessa e successiva.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 5de8597dd1d5249297a09976c804d1c1f3d822c5
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 2%

---

# Guida alla segmentazione Edge

La segmentazione di Edge consente di valutare istantaneamente le definizioni dei segmenti in Adobe Experience Platform [sul server Edge](../../landing/edge-and-hub-comparison.md), abilitando casi di utilizzo di personalizzazione della pagina corrente e successiva.

>[!IMPORTANT]
>
> I dati edge verranno memorizzati in una posizione del server perimetrale più vicina al punto in cui sono stati raccolti. Questi dati possono anche essere archiviati in una posizione diversa da quella designata come centro dati Adobe Experience Platform hub (o principale).
>
> Inoltre, il motore di segmentazione Edge rispetterà solo le richieste sul server Edge in cui è presente **una** identità primaria contrassegnata, il che è coerente con le identità primarie non basate su Edge.

## Tipi di query di segmentazione di Edge {#query-types}

Una query può essere valutata con segmentazione Edge se soddisfa uno qualsiasi dei criteri descritti nella tabella seguente.

>[!NOTE]
>
>Se la query corrisponde a uno dei tipi di query della tabella seguente, verrà valutata automaticamente utilizzando la segmentazione Edge. Il sistema determina automaticamente questa capacità in base all&#39;espressione della query.
>
>Inoltre, se il pubblico **only** contiene attributi di profilo, verrà valutato ogni giorno. Se desideri che il pubblico venga valutato in tempo reale, devi aggiungere i dati dell&#39;evento al pubblico.

| Tipo di query | Dettagli | Query | Esempio |
| ---------- | ------- | ----- | ------- |
| Singolo evento entro un intervallo di tempo inferiore a 24 ore | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo entro un intervallo di tempo inferiore a 24 ore. | `CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![Viene visualizzato un esempio di un singolo evento all&#39;interno di un intervallo di tempo relativo.](../images/methods/edge/single-event.png) |
| Solo profilo | Qualsiasi definizione di segmento che fa riferimento solo a un attributo di profilo. | `homeAddress.country.equals("US", false)` | ![Viene visualizzato un esempio di un attributo di profilo.](../images/methods/edge/profile-attribute.png) |
| Singolo evento con un attributo di profilo entro un intervallo di tempo relativo inferiore a 24 ore | Qualsiasi definizione di segmento che si riferisce a un singolo evento in arrivo, con uno o più attributi di profilo, e si verifica entro un intervallo di tempo relativo inferiore a 24 ore. | `workAddress.country.equals("US", false) and CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) WHEN(today)])` | ![Viene visualizzato un esempio di un singolo evento con un attributo di profilo all&#39;interno di un intervallo di tempo relativo.](../images/methods/edge/single-event-with-profile-attribute.png) |
| Segmento di segmenti | Qualsiasi definizione di segmento che contiene uno o più segmenti batch o edge. **Nota:** se si utilizza un segmento di segmenti, l&#39;annullamento del profilo avverrà **ogni 24 ore**. | `inSegment("a730ed3f-119c-415b-a4ac-27c396ae2dff") and inSegment("8fbbe169-2da6-4c9d-a332-b6a6ecf559b9")` | ![Viene visualizzato un esempio di segmento di segmenti.](../images/methods/edge/segment-of-segments.png) |

Inoltre, la definizione del segmento **deve** essere associata a un criterio di unione attivo sul server Edge. Per ulteriori informazioni sui criteri di unione, leggere la [guida ai criteri di unione](../../profile/api/merge-policies.md).

Una definizione di segmento **non** sarà idonea per la segmentazione Edge nel seguente scenario:

- La definizione del segmento include una combinazione di un singolo evento e un evento `inSegment`.
   - Tuttavia, se la definizione del segmento contenuta nell&#39;evento `inSegment` è solo di profilo, la definizione del segmento **sarà** abilitata per la segmentazione Edge.
- La definizione del segmento utilizza &quot;Ignora anno&quot; come parte dei vincoli di tempo.

## Crea pubblico {#create-audience}

Puoi creare un pubblico valutato utilizzando la segmentazione Edge di utilizzando l’API del servizio di segmentazione o tramite Audience Portal nell’interfaccia utente.

Una definizione di segmento può essere abilitata per Edge se corrisponde a uno dei [tipi di query idonei](#eligible-query-types).

>[!BEGINTABS]

>[!TAB API servizio di segmentazione]

**Formato API**

```http
POST /segment/definitions
```

**Richiesta**

+++ Richiesta di esempio per creare una definizione di segmento abilitata per la segmentazione Edge

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "People in the USA",
        "description: "An audience that looks for people who live in the USA",
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "homeAddress.country = \"US\""
        },
        "evaluationInfo": {
            "batch": {
                "enabled": false
            },
            "continuous": {
                "enabled": false
            },
            "synchronous": {
                "enabled": true
            }
        },
        "schema": {
            "name": "_xdm.context.profile"
        }
     }'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con i dettagli della definizione del segmento appena creata.

+++Una risposta di esempio durante la creazione di una definizione di segmento.

```json
{
    "id": "4afe34ae-8c98-4513-8a1d-67ccaa54bc05",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "profileInstanceId": "ups",
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "People in the USA",
    "description": "An audience that looks for people who live in the USA",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "homeAddress.country = \"US\""
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": true
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 0,
    "updateEpoch": 1579292094,
    "updateTime": 1579292094000
}
```

+++

Ulteriori informazioni sull&#39;utilizzo di questo endpoint sono disponibili nella [guida dell&#39;endpoint di definizione del segmento](../api/segment-definitions.md).

>[!TAB Audience Portal]

In Audience Portal, seleziona **[!UICONTROL Crea pubblico]**.

![Il pulsante Crea pubblico è evidenziato in Audience Portal.](../images/methods/edge/select-create-audience.png)

Viene visualizzata una finestra a comparsa. Seleziona **[!UICONTROL Genera regole]** per accedere al Generatore di segmenti.

![Il pulsante Genera regole è evidenziato nel popover Crea pubblico.](../images/methods/edge/select-build-rules.png)

In Segment Builder (Generatore di segmenti), crea una definizione di segmento che corrisponda a uno dei [tipi di query idonei](#eligible-query-types). Se la definizione del segmento è idonea per la segmentazione Edge, potrai selezionare **[!UICONTROL Edge]** come **[!UICONTROL metodo di valutazione]**.

![Viene visualizzata la definizione del segmento. Il tipo di valutazione è evidenziato e mostra che la definizione del segmento può essere valutata utilizzando la segmentazione Edge.](../images/methods/edge/edge-evaluation-method.png)

Per ulteriori informazioni sulla creazione delle definizioni dei segmenti, consulta la [guida del Generatore di segmenti](../ui/segment-builder.md)

>[!ENDTABS]

## Recuperare i tipi di pubblico valutati utilizzando la segmentazione Edge {#retrieve-audiences}

Puoi recuperare tutti i tipi di pubblico valutati utilizzando la segmentazione Edge tramite l’API del servizio di segmentazione o tramite Audience Portal nell’interfaccia utente.

>[!BEGINTABS]

>[!TAB API servizio di segmentazione]

Recupera un elenco di tutte le definizioni di segmenti valutate utilizzando la segmentazione Edge nell&#39;organizzazione effettuando una richiesta GET all&#39;endpoint `/segment/definitions`.

**Formato API**

È necessario includere il parametro query `evaluationInfo.synchronous.enabled=true` nel percorso della richiesta per recuperare le definizioni dei segmenti valutate utilizzando la segmentazione Edge.

```http
GET /segment/definitions?evaluationInfo.synchronous.enabled=true
```

**Richiesta**

+++ Una richiesta di esempio per elencare tutte le definizioni di segmenti abilitati per Edge

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.synchronous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**Risposta**

In caso di esito positivo, la risposta restituisce lo stato HTTP 200 con un array di definizioni di segmenti nell’organizzazione abilitate per la segmentazione Edge.

+++ Una risposta di esempio contenente un elenco di tutte le definizioni di segmenti abilitati per la segmentazione edge nell’organizzazione

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": " People who are NOT on their homepage ",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = false"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": true
                }
            },
            "creationTime": 1572029711000,
            "updateEpoch": 1572029712000,
            "updateTime": 1572029712000
        },
        {
            "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "imsOrgId": "{ORG_ID}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "Homepage_continuous",
            "description": "People who are on their homepage - continuous",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
            },
            "evaluationInfo": {
                "batch": {
                    "enabled": false
                },
                "continuous": {
                    "enabled": false
                },
                "synchronous": {
                    "enabled": true
                }
            },
            "creationTime": 1572021085000,
            "updateEpoch": 1572021086000,
            "updateTime": 1572021086000
        }
    ],
    "page": {
        "totalCount": 2,
        "totalPages": 1,
        "sortField": "creationTime",
        "sort": "desc",
        "pageSize": 2,
        "limit": 100
    },
    "link": {}
}
```

Informazioni più dettagliate sulla definizione del segmento restituita sono disponibili nella [guida dell&#39;endpoint per le definizioni dei segmenti](../api/segment-definitions.md).

+++

>[!TAB Audience Portal]

Puoi recuperare tutti i tipi di pubblico abilitati per la segmentazione Edge nell’organizzazione utilizzando i filtri in Audience Portal. Seleziona l&#39;icona ![icona filtro](../../images/icons/filter.png) per visualizzare l&#39;elenco dei filtri.

![L&#39;icona del filtro è evidenziata in Audience Portal.](../images/methods/filter-audiences.png)

All&#39;interno dei filtri disponibili, vai a **Frequenza di aggiornamento** e seleziona &quot;Edge&quot;. Utilizzando questo filtro vengono visualizzati tutti i tipi di pubblico dell’organizzazione valutati mediante la segmentazione Edge.

![È selezionata la frequenza di aggiornamento di Edge, con tutti i tipi di pubblico dell&#39;organizzazione valutati tramite la segmentazione Edge.](../images/methods/edge/filter-edge.png)

Per ulteriori informazioni sulla visualizzazione dei tipi di pubblico in Experience Platform, consulta la [guida di Audience Portal](../ui/audience-portal.md).

>[!ENDTABS]

## Dettagli del pubblico {#audience-details}

Puoi visualizzare i dettagli di un pubblico specifico valutato utilizzando la segmentazione Edge selezionandola all’interno di Audience Portal.

Dopo aver selezionato un pubblico su Audience Portal, viene visualizzata la pagina dei dettagli del pubblico. Visualizza informazioni sul pubblico, tra cui un riepilogo dei dettagli del pubblico, la quantità di profili qualificati nel tempo, nonché le destinazioni in cui il pubblico è stato attivato.

![Viene visualizzata la pagina dei dettagli del pubblico per un pubblico valutato mediante la segmentazione Edge.](../images/methods/edge/audience-details.png)

Per i tipi di pubblico abilitati per Edge, viene visualizzata la scheda **[!UICONTROL Profili nel tempo]**, che mostra il totale delle metriche qualificate e le nuove metriche di aggiornamento del pubblico.

La metrica **[!UICONTROL Totale qualificato]** rappresenta il numero totale di tipi di pubblico qualificati, in base alle valutazioni edge per questo pubblico.

La metrica **[!UICONTROL Nuovo pubblico aggiornato]** è rappresentata da un grafico a linee che mostra la modifica della dimensione del pubblico tramite la segmentazione Edge. Puoi regolare il menu a discesa per visualizzare le ultime 24 ore, l’ultima settimana o gli ultimi 30 giorni.

![La scheda Profili nel tempo è evidenziata.](../images/methods/edge/profiles-over-time.png)

Per ulteriori dettagli sui dettagli del pubblico, consulta la [Panoramica di Audience Portal](../ui/audience-portal.md#audience-details).

## Passaggi successivi

Questa guida spiega cos’è la segmentazione Edge e come creare una definizione di segmento che può essere valutata utilizzando la segmentazione Edge in Adobe Experience Platform.

Per ulteriori informazioni sull&#39;utilizzo dell&#39;interfaccia utente di Experience Platform, leggere la [Guida utente per la segmentazione](./overview.md).

Per le domande frequenti sulla segmentazione Edge, leggi la sezione [segmentazione Edge delle domande frequenti](../faq.md#edge-segmentation).

