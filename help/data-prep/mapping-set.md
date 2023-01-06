---
keywords: Experience Platform;home;mappatore;set di mappatura;mappatura;
solution: Experience Platform
title: Panoramica sui set di mappature
description: Scopri come utilizzare i set di mappatura con Adobe Experience Platform Data Prep.
exl-id: b45545b7-3ae7-400d-b6fd-b2cb76061093
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---

# Panoramica sui set di mappature

Un set di mappature è un set di mappature che trasforma i dati da uno schema all’altro. Questo documento fornisce informazioni sulla composizione dei set di mappatura, inclusi schema di input, schema di output e mappature.

## Introduzione

Questa panoramica richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [Preparazione dei dati](./home.md): Data Prep consente ai data engineer di mappare, trasformare e convalidare i dati da e verso Experience Data Model (XDM).
- [Flussi di dati](../dataflows/home.md): I flussi di dati sono una rappresentazione dei processi di trasferimento dei dati in Platform. I flussi di dati sono configurati su diversi servizi e consentono di spostare i dati dai connettori di origine ai set di dati di destinazione, fino a [!DNL Identity] e [!DNL Profile]e a [!DNL Destinations].
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md): I metodi con cui i dati possono essere inviati a [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.

## Sintassi del set di mappature

Un set di mappatura è composto da un ID, un nome, uno schema di input, uno schema di output e un elenco di mappature associate.

Il seguente JSON è un esempio di set di mappature tipico:

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
| `id` | Identificatore univoco per il set di mappature. |
| `name` | Nome del set di mappature. |
| `inputSchema` | Lo schema XDM per i dati in arrivo. |
| `outputSchema` | Lo schema XDM a cui verranno trasformati i dati di input per conformarsi. |
| `mappings` | Matrice di mappature campo-to-campo dallo schema di origine allo schema di destinazione. |
| `sourceType` | Per ogni mappatura elencata, la `sourceType` attributo indica il tipo di origine da mappare. Può essere uno dei `ATTRIBUTE`, `STATIC`oppure `EXPRESSION`: <ul><li> `ATTRIBUTE` viene utilizzato per qualsiasi valore trovato nel percorso di origine. </li><li>`STATIC` viene utilizzato per i valori inseriti nel percorso di destinazione. Questo valore rimane costante e non viene influenzato dallo schema di origine.</li><li> `EXPRESSION` viene utilizzato per un&#39;espressione che verrà risolta durante il runtime. Un elenco di espressioni disponibili è disponibile nella sezione [guida alle funzioni di mappatura](./functions.md).</li> </ul> |
| `source` | Per ogni mappatura elencata, la variabile `source` attributo indica il campo da mappare. Per ulteriori informazioni su come configurare la sorgente, consulta la sezione [sezione origini](#sources). |
| `destination` | Per ogni mappatura elencata, la variabile `destination` attributo indica il campo, o il percorso del campo, in cui il valore estratto dal `source` verrà posizionato il campo . Per ulteriori informazioni su come configurare le destinazioni, consulta la sezione [sezione di destinazione](#destination). |
| `mappings.name` | (*Facoltativo*) Un nome per la mappatura. |
| `mappings.description` | (*Facoltativo*) Una descrizione della mappatura. |

## Configurazione delle origini di mappatura

In una mappatura, il `source` può essere un campo, un&#39;espressione o un valore statico. In base al tipo di origine specificato, il valore può essere estratto in vari modi.

### Campo nei dati delle colonne

Quando mappi un campo nei dati delle colonne, ad esempio un file CSV, utilizza la variabile `ATTRIBUTE` tipo di origine. Se il campo contiene `.` all&#39;interno del nome, utilizza `\` per evitare il valore. Di seguito è riportato un esempio di mappatura:

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

Quando mappi un campo nei dati nidificati, ad esempio un file JSON, utilizza la variabile `ATTRIBUTE` tipo di origine. Se il campo contiene `.` all&#39;interno del nome, utilizza `\` per evitare il valore. Di seguito è riportato un esempio di mappatura:

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

Quando mappi un campo all’interno di una matrice, puoi recuperare un valore specifico utilizzando un indice. Per eseguire questa operazione, utilizza la variabile `ATTRIBUTE` tipo di origine e indice del valore da mappare. Di seguito è riportato un esempio di mappatura:

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

Utilizzo della `ATTRIBUTE` tipo di origine, è inoltre possibile mappare direttamente una matrice a una matrice o a un oggetto a un oggetto. Di seguito è riportato un esempio di mappatura:

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

Utilizzo della `ATTRIBUTE` tipo di origine, è possibile eseguire un ciclo iterativo tra gli array e mapparli su uno schema di destinazione utilizzando un indice con caratteri jolly (`[*]`). Di seguito è riportato un esempio di mappatura:

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

Se desideri mappare una costante o un valore statico, utilizza la variabile `STATIC` tipo di origine.  Quando utilizzi `STATIC` tipo di origine, `source` rappresenta il valore hardcoded che si desidera assegnare al `destination`. Di seguito è riportato un esempio di mappatura:

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

Se desideri mappare un’espressione, utilizza la variabile `EXPRESSION` tipo di origine. Un elenco delle funzioni accettate è disponibile nella [guida alle funzioni di mappatura](./functions.md). Quando utilizzi `EXPRESSION` tipo di origine, `source` rappresenta la funzione che si desidera risolvere. Di seguito è riportato un esempio di mappatura:

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

In una mappatura, il `destination` è la posizione in cui il valore estratto dalla `source` saranno inseriti.

### Campo a livello principale

Quando desideri mappare il `source` al livello principale dei dati trasformati, segui l’esempio seguente:

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

Quando desideri mappare il `source` in un campo nidificato nei dati trasformati, segui l’esempio seguente:

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

Quando desideri mappare il `source` a un indice specifico in una matrice nei dati trasformati, seguire l&#39;esempio seguente:

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

Per eseguire un ciclo iterativo tra array e mappare i valori sulla destinazione, è possibile utilizzare un indice con caratteri jolly (`[*]`). Di seguito è riportato un esempio:

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

Leggendo questo documento, è ora necessario comprendere come vengono costruiti i set di mappature, incluso come configurare le singole mappature all’interno di un set di mappature. Per ulteriori informazioni su altre funzioni di preparazione dei dati, consulta la sezione [Panoramica sulla preparazione dei dati](./home.md). Per informazioni su come utilizzare i set di mappatura all’interno dell’API di preparazione dati, consulta la sezione [Guida per gli sviluppatori di Data Prep](./api/overview.md).
