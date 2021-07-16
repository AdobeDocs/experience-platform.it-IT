---
title: Filtrare le risposte nell’API di Reactor
description: Scopri come filtrare i risultati quando inserisci le risorse nell’API di Reactor.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 2%

---

# Filtrare le risposte nell’API di Reactor

Quando si utilizzano gli endpoint di elenco (GET) nell’API di Reactor, potrebbe essere necessario limitare i risultati restituiti a un sottoinsieme di record. A questo scopo, molti degli endpoint dell’elenco API supportano la possibilità di filtrare per attributi specifici. Se invece desideri eseguire query strutturate all&#39;API, consulta la guida alla [ricerca](./search.md).

## Sintassi di filtro

L’esempio seguente spiega come implementare i filtri per le richieste GET.

**Formato API**

Per filtrare la risposta per un determinato endpoint dell’elenco, è necessario fornire un parametro di query `filter` nel percorso della richiesta.

>[!NOTE]
>
>Il modello seguente utilizza le parentesi quadre (`[]`) e gli spazi per la leggibilità. In pratica, questi caratteri devono essere codificati in URI, come descritto in [RFC 3986](https://tools.ietf.org/html/rfc3986). Un esempio di percorso di richiesta correttamente codificato è mostrato più avanti in questa guida.
>
>Se la struttura dei filtri non è corretta, non vengono applicati filtri e viene restituito l’intero set di risultati.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE}
```

| Proprietà | Descrizione |
| --- | --- |
| `{ENDPOINT}` | Un endpoint di elenco nell’API di Reactor che supporta i parametri di filtro. |
| `{ATTRIBUTE_NAME}` | Nome di un attributo specifico per cui filtrare i risultati. Tieni presente che endpoint diversi supportano attributi diversi per il filtraggio. Per un elenco degli attributi di filtro disponibili, consulta la guida di riferimento per l’endpoint con cui stai lavorando. |
| `{OPERATOR}` | Operatore che determina la modalità di valutazione dei risultati rispetto al `{VALUE}` fornito. Gli operatori supportati sono elencati nella sezione [appendice](#supported-operators). |
| `{VALUE}` | Il valore in base al quale confrontare i risultati restituiti. Quando si confronta per l’uguaglianza utilizzando l’operatore `EQ` , per poter essere incluso nella risposta il valore deve essere una corrispondenza esatta e con distinzione tra maiuscole e minuscole. |

{style=&quot;table-layout:auto&quot;}

**Richiesta**

La richiesta di esempio seguente recupera un elenco di librerie pubblicate applicando un filtro che richiede l&#39;attributo `state` della libreria su uguale a `published`.

Prima della codifica URI, la sintassi di questo filtro nel percorso della richiesta sarà simile alla seguente:

`https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter[state]=EQ published`

Una volta che i parametri di percorso e query sono stati codificati in URI, possono essere utilizzati nelle richieste API come quella seguente:

```shell
curl -X GET \
  https://reactor.adobe.io/properties/PR906238a59bbf4262bcedba248f483600/libraries?filter%5Bstate%5D=EQ%20published \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

## Filtro su più valori {#multiple-values}

Per filtrare in base a più valori per un singolo attributo, fornisci i valori come elenco separato da virgole.

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME}]={OPERATOR} {VALUE_1},{VALUE_2}
```

## Utilizzo di più filtri

Per applicare filtri per più attributi, fornisci un parametro `filter` per ciascun attributo. I parametri devono essere separati da caratteri di e commerciale (`&`).

```http
GET {ENDPOINT}?filter[{ATTRIBUTE_NAME_1}]={OPERATOR} {VALUE}&filter[{ATTRIBUTE_NAME_2}]={OPERATOR} {VALUE}
```

>[!NOTE]
>
>Se specifichi lo stesso attributo in più filtri nella stessa richiesta, verrà applicato solo l’ultimo filtro fornito per quell’attributo.

## Appendice

La sezione seguente contiene informazioni aggiuntive sull’utilizzo dei filtri nell’API di Reactor.

### Operatori di filtro supportati {#operators}

Nella tabella seguente sono elencati i valori dell’operatore supportati per i parametri del filtro. Tieni presente che a seconda dell’attributo filtrato, non tutti gli operatori di filtro disponibili saranno applicabili, ad esempio l’utilizzo di operatori &quot;minore di&quot; o &quot;maggiore di&quot; per gli attributi di stringa.

| Operatore | Descrizione |
| --- | --- |
| `EQ` | L&#39;attributo deve corrispondere al valore specificato. |
| `NOT` | L&#39;attributo non deve essere uguale al valore specificato. |
| `LT` | L&#39;attributo deve essere minore del valore specificato. |
| `GT` | L&#39;attributo deve essere maggiore del valore specificato. |
| `BETWEEN` | L&#39;attributo deve rientrare in un intervallo di valori specificato. Quando si utilizza questo operatore, [devono essere forniti due valori](#multiple-values) per indicare i valori minimo e massimo per l&#39;intervallo desiderato. |
| `CONTAINS` | L&#39;attributo deve contenere il valore fornito, ad esempio un set di caratteri all&#39;interno di un attributo di stringa. |
