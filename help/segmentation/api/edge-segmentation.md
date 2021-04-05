---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;segmentazione edge;Segmentazione Edge;Edge Edge Edge;
solution: Experience Platform
title: 'Segmentazione Edge tramite API '
topic: guida per sviluppatori
description: Questo documento contiene esempi su come utilizzare la segmentazione edge con l’API di Adobe Experience Platform Segmentation Service.
exl-id: effce253-3d9b-43ab-b330-943fb196180f
translation-type: tm+mt
source-git-commit: 692bfca8d14ac247527f956bbcba8b4eb37516e3
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 1%

---

# Segmentazione degli spigoli

>[!NOTE]
>
>Il seguente documento spiega come eseguire la segmentazione edge utilizzando l’API . Per informazioni su come eseguire la segmentazione dei bordi tramite l’interfaccia utente, consulta la [guida all’interfaccia utente per la segmentazione dei bordi](../ui/edge-segmentation.md) .

La segmentazione dei bordi è la capacità di valutare i segmenti in Adobe Experience Platform istantaneamente sul bordo, abilitando casi d’uso di personalizzazione della pagina stessa e di pagina successiva.

## Introduzione

Questa guida per gli sviluppatori richiede una buona comprensione dei vari servizi [!DNL Adobe Experience Platform] coinvolti nella segmentazione edge. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumatore unificato in tempo reale, basato su dati aggregati provenienti da più origini.
- [[!DNL Segmentation]](../home.md): Consente di creare segmenti e tipi di pubblico dai  [!DNL Real-time Customer Profile] dati.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Platform] vengono organizzati i dati sulla customer experience.

Per effettuare correttamente le chiamate agli endpoint API [!DNL Data Prep], leggi la guida introduttiva [alle API Platform](../../landing/api-guide.md) per informazioni sulle intestazioni richieste e su come leggere chiamate API di esempio.

## Tipi di query per segmentazione Edge {#query-types}

Affinché un segmento possa essere valutato utilizzando la segmentazione edge, la query deve essere conforme alle seguenti linee guida:

| Tipo di query | Dettagli |
| ---------- | ------- |
| Hit in entrata | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo senza restrizioni temporali. |
| Hit in entrata che fa riferimento a un profilo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo, senza restrizioni di tempo, e a uno o più attributi di profilo. |
| Query di frequenza | Qualsiasi definizione di segmento che fa riferimento a un evento che si verifica almeno un certo numero di volte. |
| Query di frequenza che fa riferimento a un profilo | Qualsiasi definizione di segmento che fa riferimento a un evento che si verifica almeno un determinato numero di volte e presenta uno o più attributi di profilo. |

{style=&quot;table-layout:auto&quot;}

I seguenti tipi di query sono **non** attualmente supportati dalla segmentazione edge:

| Tipo di query | Dettagli |
| ---------- | ------- |
| Intervallo di tempo relativo | Se una query fa riferimento a una finestra temporale, non può essere valutata utilizzando la segmentazione edge. |
| Negazione | Se una query contiene una negazione o un evento `not`, non può essere valutata utilizzando la segmentazione edge. |
| Eventi multipli | Se una query contiene più di un evento, non può essere valutata utilizzando la segmentazione edge. |

{style=&quot;table-layout:auto&quot;}

## Recupera tutti i segmenti abilitati per la segmentazione dei bordi

È possibile recuperare un elenco di tutti i segmenti abilitati per la segmentazione edge all’interno dell’organizzazione IMS effettuando una richiesta di GET all’endpoint `/segment/definitions`.

**Formato API**

Per recuperare i segmenti abilitati per la segmentazione edge, è necessario includere il parametro query `evaluationInfo.synchronous.enabled=true` nel percorso della richiesta.

```http
GET /segment/definitions?evaluationInfo.synchronous.enabled=true
```

**Richiesta**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/segment/definitions?evaluationInfo.synchronous.enabled=true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

Una risposta corretta restituisce un array di segmenti nell’organizzazione IMS abilitati per la segmentazione edge. Informazioni più dettagliate sulla definizione del segmento restituita sono disponibili nella [guida all&#39;endpoint per le definizioni dei segmenti](./segment-definitions.md).

```json
{
    "segments": [
        {
            "id": "15063cb-2da8-4851-a2e2-bf59ddd2f004",
            "schema": {
                "name": "_xdm.context.profile"
            },
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
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
            "ttlInDays": 30,
            "imsOrgId": "{IMS_ORG_ID}",
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

## Creare un segmento abilitato per la segmentazione dei bordi

Puoi creare un segmento abilitato per la segmentazione edge effettuando una richiesta POST all’endpoint `/segment/definitions` . Oltre a corrispondere a uno dei tipi di query di segmentazione edge elencati sopra](#query-types), è necessario impostare il flag `evaluationInfo.synchronous.enabled` nel payload su true.[

**Formato API**

```http
POST /segment/definitions
```

**Richiesta**

>[!NOTE]
>
>L’esempio seguente è una richiesta standard per creare un segmento. Per ulteriori informazioni sulla creazione di una definizione di segmento, consulta l’esercitazione su [creazione di un segmento](../tutorials/create-a-segment.md).

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/definitions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'  \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "name": "Homepage_continuous",
    "description": "People who are on their homepage - continuous",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "select var1 from xEvent where var1._experience.analytics.endUser.firstWeb.webPageDetails.isHomePage = true"
    },
    "evaluationInfo": {
        "synchronous": {
            "enabled": true
        }
    }
}'
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `evaluationInfo.synchronous.enabled` | L’oggetto `evaluationInfo` determina il tipo di valutazione a cui verrà sottoposta la definizione del segmento. Per utilizzare la segmentazione dei bordi, impostate `evaluationInfo.synchronous.enabled` con un valore di `true`. |

**Risposta**

Una risposta corretta restituisce i dettagli della nuova definizione di segmento creata che è abilitata per la segmentazione edge.

```json
{
    "id": "f15063cb-2da8-4851-a2e2-bf59ddd2f004",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 30,
    "imsOrgId": "{IMS_ORG}",
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
```

## Passaggi successivi

Ora che sai come creare segmenti abilitati per la segmentazione dei bordi, puoi utilizzarli per abilitare i casi di utilizzo per la personalizzazione della pagina stessa e di quella successiva.

Per informazioni su come eseguire azioni simili e lavorare con segmenti utilizzando l’interfaccia utente di Adobe Experience Platform, visita la [Guida utente di Generatore di segmenti](../ui/segment-builder.md).
