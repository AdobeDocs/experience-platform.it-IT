---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;identità;tipo di dati;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati identità
topic-legacy: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM di identità.
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 3%

---

#  Tipo di dati di identità

 Identity è un tipo di dati XDM standard utilizzato per distinguere chiaramente le persone che interagiscono con le esperienze digitali. L&#39;identità è stabilita da un provider di identità, a cui si fa riferimento in un attributo `namespace` . All&#39;interno di ogni `namespace`, l&#39;identità è univoca.

<img src="../images/data-types/identity.png" width="550" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `namespace` | Oggetto | Un oggetto che contiene un singolo campo stringa (`code`), che indica lo spazio dei nomi associato all&#39;attributo `id` fornito. |
| `authenticatedState` | Stringa | Lo stato autenticato per questa identità al momento dell’evento esperienza osservato. Per i valori e le definizioni accettati, consultare l&#39; [appendice](#authenticatedState) . |
| `id` | Stringa | L’identità del consumatore nello spazio dei nomi correlato. |
| `primary` | Booleano | Indica se si tratta dell&#39;identità principale dell&#39;individuo. Ogni individuo può avere una sola identità primaria. |
| `xid` | Stringa | Se presente, questo valore rappresenta un identificatore dello spazio dei nomi incrociato univoco per tutti gli identificatori con ambito dello spazio dei nomi in tutti i namespace. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Appendice

La sezione seguente contiene informazioni aggiuntive sul tipo di dati [!UICONTROL Identity] .

## Valori accettati per authenticatedState {#authenticatedState}

La tabella seguente illustra i valori accettati per `authenticatedState` e i relativi significati associati:

| Valore | Descrizione |
| --- | --- |
| `ambiguous` | Lo stato autenticato è ambiguo. |
| `authenticated` | L&#39;utente è stato identificato da un login o da un&#39;azione simile valida al momento dell&#39;osservazione dell&#39;evento. |
| `loggedOut` | L&#39;utente è stato identificato da un&#39;azione di accesso in un momento precedente, ma non è stato effettuato l&#39;accesso al momento dell&#39;osservazione dell&#39;evento. |
