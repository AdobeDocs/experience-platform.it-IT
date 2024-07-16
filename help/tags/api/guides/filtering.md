---
title: Filtrare le risposte nell’API di Reactor
description: Scopri come filtrare i risultati quando elenchi le risorse nell’API di Reactor.
exl-id: 8a91f3dd-4ead-4a10-abb1-e71acb0d73b6
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 100%

---

# Filtrare le risposte nell’API di Reactor

Quando nell’API di Reactor si utilizzano gli endpoint di elenco (GET), potrebbe essere necessario limitare i risultati restituiti a un sottoinsieme dei record. A questo scopo, molti degli endpoint di elenco dell’API supportano la possibilità di filtrare per specifici attributi. Se invece desideri eseguire query strutturate, consulta la guida alla [ricerca](./search.md).

## Sintassi per i filtri

L’esempio seguente spiega come implementare i filtri per le richieste GET.

**Formato API**

Per filtrare la risposta per un determinato endpoint di elenco, è necessario fornire un parametro di query `filter` nel percorso della richiesta.

>[!NOTE]
>
>Nel modello seguente vengono utilizzate parentesi quadre (`[]`) e spazi per migliorarne la leggibilità. Nella pratica, invece, questi caratteri devono essere codificati in URI, come descritto in [RFC 3986](https://tools.ietf.org/html/rfc3986). Più avanti in questa guida viene fornito un esempio del codice corretto per un percorso di richiesta.
>
>Se la struttura dei filtri non è corretta, non vengono applicati filtri e viene restituito l’intero set di risultati.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE}
```

| Proprietà | Descrizione |
| --- | --- |
| `{ENDPOINT}` | Endpoint di elenco nell’API di Reactor che supporta i parametri per filtri. |
| `{ATTRIBUTE_NAME}` | Nome di un attributo specifico in base al quale filtrare i risultati. Tieni presente che endpoint diversi supportano attributi diversi per il filtraggio. Per un elenco degli attributi di filtro disponibili, consulta la guida di riferimento per l’endpoint con cui stai lavorando. |
| `{OPERATOR}` | Operatore che determina come devono essere valutati i risultati rispetto al `{VALUE}` fornito. Gli operatori supportati sono elencati nell’[appendice](#supported-operators). |
| `{VALUE}` | Valore in base al quale vengono confrontati i risultati restituiti. Quando si confronta per l’uguaglianza utilizzando l’operatore `EQ`, per poter essere incluso nella risposta il valore deve corrispondere esattamente, rispettando maiuscole e minuscole. |

{style="table-layout:auto"}

**Richiesta**

L’esempio di richiesta seguente recupera un elenco di librerie pubblicate applicando un filtro che richiede che l’attributo `state` della libreria sia uguale a `published`.

Prima della codifica URI, la sintassi di questo filtro nel percorso della richiesta sarà simile alla seguente:

`https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter[state]=EQ published`

Una volta che i parametri di percorso e query sono stati codificati in URI, possono essere utilizzati in richieste API simili alla seguente:

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter%5Bstate%5D=EQ%20published \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

## Filtro per più valori {#multiple-values}

Per filtrare in base a più valori per un singolo attributo, fornisci i valori come elenco separato da virgole.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE_1},{VALUE_2}
```

## Utilizzo di più filtri

Per applicare filtri per più attributi, fornisci un parametro `filter` per ciascun attributo. I parametri devono essere separati da caratteri di E commerciale (`&`).

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME_1}]={OPERATOR} {VALUE}&filter[{ATTRIBUTE_NAME_2}]={OPERATOR} {VALUE}
```

>[!NOTE]
>
>Se specifichi lo stesso attributo in più filtri nella stessa richiesta, verrà applicato solo l’ultimo filtro fornito per quell’attributo.

## Appendice

La sezione seguente contiene informazioni aggiuntive sull’utilizzo dei filtri nell’API di Reactor.

### Operatori di filtro supportati {#operators}

Nella tabella seguente sono elencati gli operatori supportati nei parametri di filtro. A seconda dell’attributo filtrato, non tutti gli operatori di filtro disponibili saranno applicabili, ad esempio l’utilizzo di operatori “minore di” o “maggiore di” per gli attributi di stringa.

| Operatore | Descrizione |
| --- | --- |
| `EQ` | L’attributo deve corrispondere al valore specificato. |
| `NOT` | L’attributo non deve essere uguale al valore specificato. |
| `LT` | L’attributo deve essere minore del valore specificato. |
| `GT` | L’attributo deve essere maggiore del valore specificato. |
| `BETWEEN` | L’attributo deve rientrare in un intervallo di valori specificato. Quando si utilizza questo operatore, devono essere forniti [due valori](#multiple-values) per indicare i valori minimo e massimo per l’intervallo desiderato. |
| `CONTAINS` | L’attributo deve contenere il valore fornito, ad esempio una serie di caratteri all’interno di un attributo di stringa. |
