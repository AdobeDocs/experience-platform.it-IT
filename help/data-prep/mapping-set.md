---
keywords: Experience Platform;home;mappatore;set di mappatura;mappatura;
solution: Experience Platform
title: Panoramica sui set di mappature
topic-legacy: overview
description: Scopri come utilizzare i set di mappatura con Adobe Experience Platform Data Prep.
source-git-commit: 97f803f649b2c42b0449a2f8f0cff370ed1aba93
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---


# Panoramica sui set di mappature

Un set di mappature è un set di mappature che trasforma i dati da uno schema all’altro. Questo documento fornisce informazioni sulla composizione dei set di mappatura, inclusi schema di input, schema di output e mappature.

## Introduzione

Questa panoramica richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [Preparazione](./home.md) dati: Data Prep consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).
- [Flussi di dati](../dataflows/home.md): I flussi di dati sono una rappresentazione dei processi di trasferimento dei dati in Platform. I flussi di dati sono configurati su diversi servizi e consentono di spostare i dati dai connettori di origine ai set di dati di destinazione, a [!DNL Identity] e [!DNL Profile] e a [!DNL Destinations].
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md): I metodi con cui i dati possono essere inviati a  [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.

## Sintassi del set di mappature

Un set di mappatura è composto da un ID, un nome, uno schema di input, uno schema di output e un elenco di mappature associate.

Il seguente JSON è un esempio di set di mappature tipico:

```json
{
    "id" : "cbb0da769faa48fcb29e026a924ba29d",
    "name" : "Demo Mapping Set",
    "inputSchema" : {
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
            "name" : "Id",
            "description" : "Identifier field"
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
| `id` | Identificatore univoco per il set di mappature. |
| `name` | Nome del set di mappature. |
| `inputSchema` | Lo schema XDM per i dati in arrivo. |
| `outputSchema` | Lo schema XDM a cui verranno trasformati i dati di input per conformarsi. |
| `mappings` | Matrice di mappature campo-to-campo dallo schema di origine allo schema di destinazione. |
| `sourceType` | Per ogni mappatura elencata, il relativo attributo `sourceType` indica il tipo di origine da mappare. Può essere tra `ATTRIBUTE`, `STATIC` o `EXPRESSION`: <ul><li> `ATTRIBUTE` viene utilizzato per qualsiasi valore trovato nel percorso di origine. </li><li>`STATIC` viene utilizzato per i valori inseriti nel percorso di destinazione. Questo valore rimane costante e non viene influenzato dallo schema di origine.</li><li> `EXPRESSION` viene utilizzato per un&#39;espressione che verrà risolta durante il runtime. Un elenco di espressioni disponibili si trova nella [guida alle funzioni di mappatura](./functions.md).</li> </ul> |
| `source` | Per ogni mappatura elencata, l&#39;attributo `source` indica il campo da mappare. Ulteriori informazioni su come configurare la sorgente sono disponibili nella sezione [origini](#sources). |
| `destination` | Per ogni mappatura elencata, l&#39;attributo `destination` indica il campo o il percorso del campo, in cui verrà inserito il valore estratto dal campo `source`. Ulteriori informazioni su come configurare le destinazioni sono disponibili nella sezione [destinazione](#destination). |
| `mappings.name` | (*Facoltativo*) Un nome per la mappatura. |
| `mappings.description` | (*Facoltativo*) Una descrizione della mappatura. |

## Configurazione delle origini di mappatura

In una mappatura, il valore `source` può essere un campo, un&#39;espressione o un valore statico. In base al tipo di origine specificato, il valore può essere estratto in vari modi.

### Campo nei dati delle colonne

Quando mappi un campo nei dati delle colonne, ad esempio un file CSV, utilizza il tipo di origine `ATTRIBUTE` . Se il campo contiene `.` all’interno del nome, utilizza `\` per applicare un escape al valore. Di seguito è riportato un esempio di mappatura:

**File CSV di esempio:**

```csv
Full.Name, Email
John Smith, js@example.com
```

**Mappatura del campione**

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

Quando mappi un campo nei dati nidificati, ad esempio un file JSON, utilizza il tipo di origine `ATTRIBUTE` . Se il campo contiene `.` all’interno del nome, utilizza `\` per applicare un escape al valore. Di seguito è riportato un esempio di mappatura:

**File JSON di esempio**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Mappatura del campione**

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

### Campo all’interno di una matrice

Quando mappi un campo all’interno di una matrice, puoi recuperare un valore specifico utilizzando un indice. A questo scopo, utilizza il tipo di origine `ATTRIBUTE` e l&#39;indice del valore da mappare. Di seguito è riportato un esempio di mappatura:

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

**Mappatura del campione**

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

### Array a matrice o oggetto a oggetto

Utilizzando il tipo di origine `ATTRIBUTE`, è inoltre possibile mappare direttamente un array su un array o su un oggetto. Di seguito è riportato un esempio di mappatura:

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

**Mappatura del campione**

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

Utilizzando il tipo di origine `ATTRIBUTE`, è possibile eseguire il ciclo iterativo tra gli array e mapparli su uno schema di destinazione utilizzando un indice di caratteri jolly (`[*]`). Di seguito è riportato un esempio di mappatura:

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

**Mappatura del campione**

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

Se desideri mappare una costante o un valore statico, utilizza il tipo di origine `STATIC` .  Quando si utilizza il tipo di origine `STATIC`, il `source` rappresenta il valore hardcoded che si desidera assegnare al `destination`. Di seguito è riportato un esempio di mappatura:

**File JSON di esempio**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Mappatura del campione**

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

Per mappare un’espressione, utilizza il tipo di origine `EXPRESSION`. Un elenco delle funzioni accettate si trova nella [guida alle funzioni di mappatura](./functions.md). Quando si utilizza il tipo di origine `EXPRESSION`, `source` rappresenta la funzione che si desidera risolvere. Di seguito è riportato un esempio di mappatura:

**File JSON di esempio**

```json
{
    "firstName": "John",
    "lastName": "Smith",
    "email": "js@example.com"
}
```

**Mappatura del campione**

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

In una mappatura, il `destination` è la posizione in cui verrà inserito il valore estratto da `source`.

### Campo a livello principale

Per mappare il valore `source` al livello principale dei dati trasformati, segui l&#39;esempio seguente:

**File JSON di esempio**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Mappatura del campione**

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

Per mappare il valore `source` a un campo nidificato nei dati trasformati, segui l&#39;esempio seguente:

**File JSON di esempio**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Mappatura del campione**

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

### Campo a un indice specifico dell&#39;array

Per mappare il valore `source` a un indice specifico in una matrice nei dati trasformati, segui l&#39;esempio seguente:

**File JSON di esempio**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Mappatura del campione**

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

### Funzionamento dell&#39;array iterativo

Per eseguire un ciclo iterativo tra array e mappare i valori alla destinazione, è possibile utilizzare un indice di caratteri jolly (`[*]`). Di seguito è riportato un esempio:

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

**Mappatura del campione**

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

Leggendo questo documento, è ora necessario comprendere come vengono costruiti i set di mappature, incluso come configurare le singole mappature all’interno di un set di mappature. Per ulteriori informazioni su altre funzioni di preparazione dei dati, consulta la [Panoramica preparazione dei dati](./home.md). Per informazioni su come utilizzare i set di mappatura all&#39;interno dell&#39;API di preparazione dati, consulta la [Guida per gli sviluppatori di preparazione dati](./api/overview.md).