---
solution: Experience Platform
title: Segmentazione di Edge tramite l’API
description: Questo documento contiene esempi su come utilizzare la segmentazione Edge con l’API del servizio di segmentazione di Adobe Experience Platform.
role: Developer
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: a1c9003a1b219325daf8fa38cda8bb1a019a55c6
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 2%

---

# Segmentazione Edge

>[!NOTE]
>
>Il documento seguente illustra come eseguire la segmentazione Edge utilizzando l’API. Per informazioni sull&#39;esecuzione della segmentazione Edge tramite l&#39;interfaccia utente, leggere la [guida dell&#39;interfaccia utente per la segmentazione Edge](../ui/edge-segmentation.md).
>
>La segmentazione di Edge è ora generalmente disponibile per tutti gli utenti di Platform. Se hai creato definizioni di segmenti edge durante la versione beta, queste definizioni di segmenti continueranno a essere operative.

La segmentazione di Edge è la capacità di valutare le definizioni dei segmenti in Adobe Experience Platform istantaneamente al limite, abilitando casi di utilizzo di personalizzazione della stessa pagina e della pagina successiva.

>[!IMPORTANT]
>
> I dati edge verranno memorizzati in una posizione del server perimetrale più vicina al punto in cui sono stati raccolti e possono essere memorizzati in una posizione diversa da quella designata come centro dati Adobe Experience Platform hub (o principale).
>
> Inoltre, il motore di segmentazione Edge rispetterà solo le richieste sul server Edge in cui è presente **una** identità primaria contrassegnata, il che è coerente con le identità primarie non basate su Edge.

## Introduzione

Questa guida per gli sviluppatori richiede una buona conoscenza dei vari servizi [!DNL Adobe Experience Platform] coinvolti nella segmentazione Edge. Prima di iniziare questo tutorial, consulta la documentazione dei seguenti servizi:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornisce un profilo consumer unificato in tempo reale, basato su dati aggregati provenienti da più origini.
- [[!DNL Adobe Experience Platform Segmentation Service]](../home.md): consente di creare tipi di pubblico dai dati di [!DNL Real-Time Customer Profile].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): framework standardizzato tramite il quale [!DNL Platform] organizza i dati sull&#39;esperienza del cliente.

Per effettuare correttamente le chiamate a qualsiasi endpoint API Experience Platform, leggi la guida [guida introduttiva alle API Platform](../../landing/api-guide.md) per scoprire le intestazioni richieste e come leggere le chiamate API di esempio.

## Tipi di query di segmentazione di Edge {#query-types}

Affinché un segmento possa essere valutato utilizzando la segmentazione Edge, la query deve essere conforme alle seguenti linee guida:

| Tipo di query | Dettagli |
| ---------- | ------- |
| Singolo evento entro un intervallo di tempo inferiore a 24 ore | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo entro un intervallo di tempo inferiore a 24 ore. |
| Solo profilo | Qualsiasi definizione di segmento che fa riferimento solo a un attributo di profilo. |
| Singolo evento con un attributo di profilo entro un intervallo di tempo relativo inferiore a 24 ore | Qualsiasi definizione di segmento che si riferisce a un singolo evento in arrivo, con uno o più attributi di profilo, e si verifica entro un intervallo di tempo relativo inferiore a 24 ore. |
| Segmento di segmenti | Qualsiasi definizione di segmento che contiene uno o più segmenti batch o in streaming. **Nota:** se si utilizza un segmento di segmenti, l&#39;annullamento del profilo avverrà **ogni 24 ore**. |
| Più eventi con un attributo di profilo | Qualsiasi definizione di segmento che fa riferimento a più eventi **nelle ultime 24 ore** e (facoltativamente) ha uno o più attributi di profilo. |

Inoltre, il segmento **must** deve essere associato a un criterio di unione attivo su Edge. Per ulteriori informazioni sui criteri di unione, leggere la [guida ai criteri di unione](../../profile/api/merge-policies.md).

Una definizione di segmento **non** verrà abilitata per la segmentazione Edge nei seguenti scenari:

- La definizione del segmento include una combinazione di un singolo evento e un evento `inSegment`.
   - Tuttavia, se il segmento contenuto nell&#39;evento `inSegment` è solo di profilo, la definizione del segmento **sarà** abilitata per la segmentazione Edge.
- La definizione del segmento utilizza &quot;Ignora anno&quot; come parte dei vincoli di tempo.

## Recupera tutti i segmenti abilitati per la segmentazione Edge

Per recuperare un elenco di tutti i segmenti abilitati per la segmentazione Edge nell&#39;organizzazione, effettua una richiesta di GET all&#39;endpoint `/segment/definitions`.

**Formato API**

Per recuperare i segmenti abilitati per la segmentazione Edge, è necessario includere il parametro di query `evaluationInfo.synchronous.enabled=true` nel percorso della richiesta.

```http
GET /segment/definitions?evaluationInfo.synchronous.enabled=true
```

**Richiesta**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.synchronous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce un array di segmenti dell’organizzazione abilitati per la segmentazione Edge. Informazioni più dettagliate sulla definizione del segmento restituita sono disponibili nella [guida dell&#39;endpoint per le definizioni dei segmenti](./segment-definitions.md).

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

## Creare un segmento abilitato per la segmentazione Edge

Per creare un segmento abilitato per la segmentazione Edge, devi eseguire una richiesta POST all&#39;endpoint `/segment/definitions` che corrisponda a uno dei [tipi di query di segmentazione Edge elencati sopra](#query-types).

**Formato API**

```http
POST /segment/definitions
```

**Richiesta**

>[!NOTE]
>
>L’esempio seguente è una richiesta standard per creare un segmento. Per ulteriori informazioni sulla creazione di una definizione di segmento, consulta l&#39;esercitazione su [creazione di un segmento](../tutorials/create-a-segment.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
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
    }
}'
```

**Risposta**

In caso di esito positivo, la risposta restituisce i dettagli della definizione del segmento appena creata, abilitata per la segmentazione Edge.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "imsOrgId": "{ORG_ID}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "chain(xEvent, timestamp, [X: WHAT(var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = "true")])"
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
```

## Passaggi successivi

Ora che sai come creare segmenti abilitati per la segmentazione edge, puoi utilizzarli per abilitare casi d’uso di personalizzazione della stessa pagina e della pagina successiva.

Per informazioni su come eseguire azioni simili e lavorare con i segmenti utilizzando l&#39;interfaccia utente di Adobe Experience Platform, visita la [guida utente di Segment Builder](../ui/segment-builder.md).

## Appendice

Nella sezione seguente sono elencate le domande frequenti relative alla segmentazione Edge:

### Quanto tempo ci vuole affinché un segmento sia disponibile nell’Edge Network?

È necessaria fino a un’ora perché un segmento sia disponibile nell’Edge Network.
