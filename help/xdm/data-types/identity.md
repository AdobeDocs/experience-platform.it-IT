---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;identity;datatype;data-type;data type;
solution: Experience Platform
title: Tipo di dati identità
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM identità.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 3%

---


# [!UICONTROL Identity] tipo di dati

[!UICONTROL Identity] è un tipo di dati XDM standard utilizzato per distinguere chiaramente le persone che interagiscono con le esperienze digitali. L&#39;identità è stabilita da un provider di identità a cui viene fatto riferimento in un `namespace` attributo. All&#39;interno `namespace`di ogni identità, l&#39;identità è univoca.

<img src="../images/data-types/identity.png" width="550" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `namespace` | Oggetto | Un oggetto che contiene un singolo campo stringa (`code`), che indica lo spazio dei nomi associato all&#39; `id` attributo fornito. |
| `authenticatedState` | Stringa | Lo stato autenticato per questa identità al momento dell’evento esperienza osservato. Cfr. l&#39; [appendice](#authenticatedState) per i valori e le definizioni accettati. |
| `id` | Stringa | L&#39;identità del consumatore nello spazio dei nomi correlato. |
| `primary` | Booleano | Indica se si tratta dell&#39;identità principale dell&#39;individuo. Ogni individuo può avere una sola identità primaria. |
| `xid` | Stringa | Se presente, questo valore rappresenta un identificatore internamespace univoco per tutti gli identificatori con ambito dello spazio nomi in tutti gli spazi dei nomi. |

Per ulteriori dettagli sul mixin, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Appendice

La sezione seguente contiene informazioni aggiuntive sul tipo di [!UICONTROL Identity] dati.

## Valori accettati per authenticatedState {#authenticatedState}

Nella tabella seguente sono riportati i valori accettati per `authenticatedState` e i significati associati:

| Valore | Descrizione |
| --- | --- |
| `ambiguous` | Lo stato di autenticazione è ambiguo. |
| `authenticated` | L&#39;utente è stato identificato da un login o da un&#39;azione simile valida al momento dell&#39;osservazione dell&#39;evento. |
| `loggedOut` | L&#39;utente è stato identificato da un&#39;azione di login in un momento precedente, ma non ha eseguito l&#39;accesso al momento dell&#39;osservazione dell&#39;evento. |