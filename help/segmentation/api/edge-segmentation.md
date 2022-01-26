---
keywords: Experience Platform;home;argomenti popolari;segmentazione;Segmentazione;Servizio di segmentazione;segmentazione edge;Segmentazione Edge;Edge Edge Edge;
solution: Experience Platform
title: 'Segmentazione Edge tramite API '
topic-legacy: developer guide
description: Questo documento contiene esempi su come utilizzare la segmentazione edge con l’API di Adobe Experience Platform Segmentation Service.
exl-id: effce253-3d9b-43ab-b330-943fb196180f
source-git-commit: f168566d03485176b16b6d3833c37930b38b0149
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 1%

---

# Segmentazione degli spigoli

>[!NOTE]
>
>Il seguente documento spiega come eseguire la segmentazione edge utilizzando l’API . Per informazioni sull’esecuzione della segmentazione edge tramite l’interfaccia utente, consulta la [guida all’interfaccia utente per la segmentazione dei bordi](../ui/edge-segmentation.md).
>
>La segmentazione dei bordi è ora generalmente disponibile per tutti gli utenti di Platform. Se hai creato segmenti edge durante la versione beta, questi segmenti continueranno a essere operativi.

La segmentazione dei bordi è la capacità di valutare i segmenti in Adobe Experience Platform istantaneamente sul bordo, abilitando casi d’uso di personalizzazione della pagina stessa e di pagina successiva.

>[!IMPORTANT]
>
> I dati edge saranno memorizzati in una posizione server perimetrale più vicina a quella in cui sono stati raccolti e possono essere memorizzati in una posizione diversa da quella designata come centro dati hub (o principal) di Adobe Experience Platform.

## Introduzione

Questa guida per gli sviluppatori richiede una comprensione approfondita dei vari [!DNL Adobe Experience Platform] servizi coinvolti nella segmentazione edge. Prima di iniziare questa esercitazione, consulta la documentazione relativa ai seguenti servizi:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornisce un profilo di consumatore unificato in tempo reale, basato su dati aggregati provenienti da più origini.
- [[!DNL Segmentation]](../home.md): Consente di creare segmenti e tipi di pubblico dal [!DNL Real-time Customer Profile] dati.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il quadro standardizzato [!DNL Platform] organizza i dati sulla customer experience.

Per effettuare correttamente le chiamate a qualsiasi endpoint API di Experience Platform, leggi la guida su [guida introduttiva alle API di Platform](../../landing/api-guide.md) per informazioni sulle intestazioni richieste e su come leggere chiamate API di esempio.

## Tipi di query per segmentazione Edge {#query-types}

Affinché un segmento possa essere valutato utilizzando la segmentazione edge, la query deve essere conforme alle seguenti linee guida:

| Tipo di query | Dettagli | Esempio |
| ---------- | ------- | ------- |
| Evento singolo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo senza restrizioni temporali. | Persone che hanno aggiunto un elemento al carrello. |
| Singolo evento che fa riferimento a un profilo | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a un singolo evento in arrivo senza restrizioni di tempo. | Persone che vivono negli Stati Uniti che hanno visitato la homepage. |
| Singolo evento ignorato con un attributo di profilo | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in entrata negato e a uno o più attributi di profilo | Persone che vivono negli Stati Uniti e che hanno **not** Ho visitato la homepage. |
| Singolo evento in una finestra temporale di 24 ore | Qualsiasi definizione di segmento che fa riferimento a un singolo evento in arrivo entro 24 ore. | Persone che hanno visitato la homepage nelle ultime 24 ore. |
| Singolo evento con un attributo di profilo entro un intervallo di tempo di 24 ore | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a un singolo evento in arrivo negato entro 24 ore. | Persone che vivono negli Stati Uniti che hanno visitato la homepage nelle ultime 24 ore. |
| Singolo evento ignorato con un attributo di profilo entro un intervallo di tempo di 24 ore | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a un singolo evento in arrivo negato entro 24 ore. | Persone che vivono negli Stati Uniti e che hanno **not** Ho visitato la homepage nelle ultime 24 ore. |
| Evento di frequenza entro un intervallo di tempo di 24 ore | Qualsiasi definizione di segmento che fa riferimento a un evento che si verifica un certo numero di volte all’interno di un intervallo di tempo di 24 ore. | Persone che hanno visitato la homepage **almeno** cinque volte nelle ultime 24 ore. |
| Evento di frequenza con un attributo di profilo entro un intervallo di tempo di 24 ore | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a un evento che si verifica un certo numero di volte all’interno di un intervallo di tempo di 24 ore. | Persone dagli Stati Uniti che hanno visitato la homepage **almeno** cinque volte nelle ultime 24 ore. |
| Evento di frequenza ignorato con un profilo entro una finestra temporale di 24 ore | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a un evento negato che si verifica un certo numero di volte all’interno di un intervallo di tempo di 24 ore. | Persone che non hanno visitato la homepage **more** cinque volte nelle ultime 24 ore. |
| Più hit in arrivo in un profilo temporale di 24 ore | Una definizione di segmento che fa riferimento a più eventi che si verificano all’interno di un intervallo di tempo di 24 ore. | Persone che hanno visitato la homepage **o** Ho visitato la pagina di pagamento nelle ultime 24 ore. |
| Eventi multipli con un profilo entro una finestra temporale di 24 ore | Qualsiasi definizione di segmento che fa riferimento a uno o più attributi di profilo e a più eventi che si verificano all’interno di un intervallo di tempo di 24 ore. | Persone dagli Stati Uniti che hanno visitato la homepage **e** Ho visitato la pagina di pagamento nelle ultime 24 ore. |

Inoltre, il segmento **deve** essere associato a un criterio di unione attivo sul bordo. Per ulteriori informazioni sui criteri di unione, consultare il [guida ai criteri di unione](../../profile/api/merge-policies.md).

## Recupera tutti i segmenti abilitati per la segmentazione dei bordi

È possibile recuperare un elenco di tutti i segmenti abilitati per la segmentazione edge all’interno dell’organizzazione IMS effettuando una richiesta di GET al `/segment/definitions` punto finale.

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

Una risposta corretta restituisce un array di segmenti nell’organizzazione IMS abilitati per la segmentazione edge. Informazioni più dettagliate sulla definizione del segmento restituita sono disponibili nella sezione [guida endpoint per le definizioni dei segmenti](./segment-definitions.md).

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

Puoi creare un segmento abilitato per la segmentazione edge effettuando una richiesta di POST al `/segment/definitions` endpoint che corrisponde a uno dei [tipi di query per segmentazione edge elencati sopra](#query-types).

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
    }
}'
```

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

Ora che sai come creare segmenti abilitati per la segmentazione dei bordi, puoi utilizzarli per abilitare i casi di utilizzo per la personalizzazione della pagina stessa e di quella successiva.

Per informazioni su come eseguire azioni simili e lavorare con i segmenti utilizzando l’interfaccia utente di Adobe Experience Platform, visita il [Guida utente di Segment Builder](../ui/segment-builder.md).
