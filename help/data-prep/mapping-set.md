---
keywords: Experience Platform;home;mappatore;set di mappatura;mappatura;
solution: Experience Platform
title: Panoramica sui set di mappatura
description: Scopri come utilizzare i set di mappatura con la preparazione dati di Adobe Experience Platform.
exl-id: b45545b7-3ae7-400d-b6fd-b2cb76061093
source-git-commit: 660948b7a43ed3c18feb74cccf8f9c607470759c
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---

# Panoramica sui set di mappatura

Un set di mappatura è un set di mappature che trasforma i dati da uno schema a un altro. Questo documento fornisce informazioni sulla composizione dei set di mappatura, inclusi schema di input, schema di output e mappature.

## Introduzione

Questa panoramica richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [Preparazione dati](./home.md): la preparazione dati consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).
- [Flussi dati](../dataflows/home.md): i flussi dati sono una rappresentazione dei processi di dati che spostano i dati in Platform. I flussi di dati sono configurati tra servizi diversi, consentendo di spostare i dati dai connettori di origine ai set di dati di destinazione, a [!DNL Identity] e [!DNL Profile] e a [!DNL Destinations].
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md): i metodi tramite i quali i dati possono essere inviati a [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.

## Sintassi del set di mappatura

Un set di mappatura è composto da un ID, un nome, uno schema di input, uno schema di output e un elenco di mappature associate.

Il seguente codice JSON è un esempio di un set di mappatura tipico:

```json
{
    "id": "cbb0da769faa48fcb29e026a924ba29d",
    "name": "Demo Mapping Set",
    "inputSchema": {
        "id": "a167ff2947ff447ebd8bcf7ef6756232",
        "version": 0
    },
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/6dd1768be928c36d58ad4897219bb52d491671f966084bc0",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "Id",
            "destination": "_id",
            "name": "Id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "FirstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "LastName",
            "destination": "person.name.lastName"
        }
    ]
}
```

| Proprietà | Descrizione |
| -------- | ----------- |
| `id` | Identificatore univoco per il set di mappatura. |
| `name` | Nome del set di mappatura. |
| `inputSchema` | Schema XDM per i dati in arrivo. |
| `outputSchema` | Lo schema XDM a cui i dati di input verranno trasformati per essere conformi. |
| `mappings` | Matrice di mappature campo-campo dallo schema di origine allo schema di destinazione. |
| `sourceType` | Per ogni mappatura elencata, il relativo attributo `sourceType` indica il tipo di origine da mappare. Può essere uno di `ATTRIBUTE`, `STATIC` o `EXPRESSION`: <ul><li> `ATTRIBUTE` viene utilizzato per qualsiasi valore trovato nel percorso di origine. </li><li>`STATIC` viene utilizzato per i valori inseriti nel percorso di destinazione. Questo valore rimane costante e non è influenzato dallo schema di origine.</li><li> `EXPRESSION` viene utilizzato per un&#39;espressione che verrà risolta durante il runtime. Un elenco delle espressioni disponibili è disponibile nella [guida alle funzioni di mappatura](./functions.md).</li> </ul> |
| `source` | Per ogni mappatura elencata, l&#39;attributo `source` indica il campo da mappare. Ulteriori informazioni sulla configurazione dell&#39;origine sono disponibili nella [panoramica delle origini](../sources/home.md). |
| `destination` | Per ogni mappatura elencata, l&#39;attributo `destination` indica il campo o il percorso del campo in cui verrà inserito il valore estratto dal campo `source`. Ulteriori informazioni su come configurare le destinazioni sono disponibili nella [panoramica sulla destinazione](../destinations/home.md). |
| `mappings.name` | (*Facoltativo*) Nome per il mapping. |
| `mappings.description` | (*Facoltativo*) Descrizione del mapping. |

## Configurazione delle origini di mappatura

In una mappatura, `source` può essere un campo, un&#39;espressione o un valore statico. In base al tipo di origine fornito, il valore può essere estratto in vari modi.

### Campo nei dati a colonne

Quando si esegue il mapping di un campo in dati a colonne, ad esempio un file CSV, utilizzare il tipo di origine `ATTRIBUTE`. Se il campo contiene `.` nel nome, utilizzare `\` per eseguire l&#39;escape del valore. Di seguito è riportato un esempio di questa mappatura:

**File CSV di esempio:**

```csv
Full.Name, Email
John Smith, js@example.com
```

**Mappatura di esempio**

```json
{
    "source": "Full.Name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**Dati trasformati**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### Campo nei dati nidificati

Quando si esegue il mapping di un campo in dati nidificati, ad esempio un file JSON, utilizzare il tipo di origine `ATTRIBUTE`. Se il campo contiene `.` nel nome, utilizzare `\` per eseguire l&#39;escape del valore. Di seguito è riportato un esempio di questa mappatura:

**File JSON di esempio**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Mappatura di esempio**

```json
{
    "source": "customerInfo.name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**Dati trasformati**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### Campo all’interno di un array

Quando mappi un campo all’interno di un array, puoi recuperare un valore specifico utilizzando un indice. A tale scopo, utilizzare il tipo di origine `ATTRIBUTE` e l&#39;indice del valore da mappare. Di seguito è riportato un esempio di questa mappatura:

**File JSON di esempio**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Mappatura di esempio**

```json
{
    "source": "customerInfo.emails[0].email",
    "destination": "pi.email",
    "sourceType": "ATTRIBUTE"
}
```

**Dati trasformati**

```json
{
    "pi": {
        "email": "js@example.com"
    }
}
```

### Matrice per matrice o oggetto per oggetto

Utilizzando il tipo di origine `ATTRIBUTE`, è inoltre possibile mappare direttamente un array a un array o un oggetto a un oggetto. Di seguito è riportato un esempio di questa mappatura:

**File JSON di esempio**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Mappatura di esempio**

```json
{
    "source": "customerInfo.emails",
    "destination": "pi.emailList",
    "sourceType": "ATTRIBUTE"
}
```

**Dati trasformati**

```json
{
    "pi": {
        "emailList": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

### Operazioni iterative sugli array

Utilizzando il tipo di origine `ATTRIBUTE`, è possibile eseguire un ciclo iterativo tra le matrici e mapparle su uno schema di destinazione utilizzando un indice con caratteri jolly (`[*]`). Di seguito è riportato un esempio di questa mappatura:

**File JSON di esempio**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Mappatura di esempio**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**Dati trasformati**

```json
{
    "pi": [
        {
            "names": {
                "name": "John Smith"
            } 
        },
        {
            "names": {
                "name": "Jane Smith"
            }
        }
    ]
}
```

### Valore costante

Se si desidera mappare una costante o un valore statico, utilizzare il tipo di origine `STATIC`.  Quando si utilizza il tipo di origine `STATIC`, `source` rappresenta il valore hardcoded da assegnare a `destination`. Di seguito è riportato un esempio di questa mappatura:

**File JSON di esempio**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Mappatura di esempio**

```json
{
    "source": "CUSTOMER",
    "destination": "userType",
    "sourceType": "STATIC"
}
```

**Dati trasformati**

```json
{
    "userType:": "CUSTOMER"
}
```

### Espressioni

Se si desidera mappare un&#39;espressione, utilizzare il tipo di origine `EXPRESSION`. Un elenco delle funzioni accettate è disponibile nella [guida delle funzioni di mappatura](./functions.md). Quando si utilizza il tipo di origine `EXPRESSION`, `source` rappresenta la funzione da risolvere. Di seguito è riportato un esempio di questa mappatura:

**File JSON di esempio**

```json
{
    "firstName": "John",
    "lastName": "Smith",
    "email": "js@example.com"
}
```

**Mappatura di esempio**

```json
{
    "source": "concat(upper(lastName), upper(firstName), now())",
    "destination": "pi.created",
    "sourceType": "EXPRESSION"
}
```

**Dati trasformati**

```json
{
    "pi": {
        "created": "SMITHJOHNFri Sep 25 15:17:31 PDT 2020"
    }
}
```

## Configurazione delle destinazioni di mappatura

In una mappatura, `destination` è la posizione in cui verrà inserito il valore estratto da `source`.

### Campo a livello di radice

Per mappare il valore `source` al livello principale dei dati trasformati, attenersi all&#39;esempio seguente:

**File JSON di esempio**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Mappatura di esempio**

```json
{
    "source": "customerInfo.name",
    "destination": "name",
    "sourceType": "ATTRIBUTE"
}
```

**Dati trasformati**

```json
{
    "name": "John Smith"
}
```

### Campo nidificato

Per mappare il valore `source` a un campo nidificato nei dati trasformati, attenersi all&#39;esempio seguente:

**File JSON di esempio**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Mappatura di esempio**

```json
{
    "source": "name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**Dati trasformati**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### Campo in un indice di array specifico

Per mappare il valore `source` a un indice specifico di un array nei dati trasformati, attenersi all&#39;esempio seguente:

**File JSON di esempio**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Mappatura di esempio**

```json
{
    "source": "customerInfo.name",
    "destination": "piList[0]",
    "sourceType": "ATTRIBUTE"
}
```

**Dati trasformati**

```json
{
    "piList": ["John Smith"]
}
```

### Funzionamento iterativo dell&#39;array

Se si desidera eseguire un ciclo iterativo tra matrici e mappare i valori alla destinazione, è possibile utilizzare un indice con caratteri jolly (`[*]`). Di seguito è riportato un esempio:

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Mappatura di esempio**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**Dati trasformati**

```json
{
    "pi": [
        {
            "names": {
                "name": "John Smith"
            } 
        },
        {
            "names": {
                "name": "Jane Smith"
            }
        }
    ]
}
```

## Passaggi successivi

Una volta letto questo documento, sarai in grado di comprendere come vengono costruiti i set di mappatura, e come configurare le singole mappature all’interno di un set di mappatura. Per ulteriori informazioni su altre funzioni di preparazione dati, leggere la [panoramica sulla preparazione dati](./home.md). Per informazioni su come utilizzare i set di mappatura nell&#39;API della preparazione dati, consulta la [Guida per gli sviluppatori della preparazione dati](./api/overview.md).
