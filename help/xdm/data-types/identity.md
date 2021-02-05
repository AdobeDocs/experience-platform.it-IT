---
keywords: ' Experience Platform;home;argomenti più comuni;schema;schema;XDM;campi;schemi;schemi;identità;tipo di dati;tipo di dati;tipo di dati;'
solution: Experience Platform
title: Tipo dati identità
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM identità.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 3%

---


# [!UICONTROL Identity] tipo di dati

[!UICONTROL Identity] è un tipo di dati XDM standard utilizzato per distinguere chiaramente le persone che interagiscono con le esperienze digitali. L&#39;identità è stabilita da un provider di identità a cui viene fatto riferimento in un attributo `namespace`. All&#39;interno di ogni `namespace`, l&#39;identità è univoca.

<img src="../images/data-types/identity.png" width="550" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `namespace` | Oggetto | Un oggetto che contiene un singolo campo stringa (`code`), che indica lo spazio dei nomi associato all&#39;attributo `id` fornito. |
| `authenticatedState` | Stringa | Lo stato autenticato per questa identità al momento dell’evento esperienza osservato. Vedere l&#39; [appendice](#authenticatedState) per i valori e le definizioni accettati. |
| `id` | Stringa | L&#39;identità del consumatore nello spazio dei nomi correlato. |
| `primary` | Booleano | Indica se si tratta dell&#39;identità principale dell&#39;individuo. Ogni individuo può avere una sola identità primaria. |
| `xid` | Stringa | Se presente, questo valore rappresenta un identificatore internamespace univoco per tutti gli identificatori con ambito dello spazio nomi in tutti gli spazi dei nomi. |

Per ulteriori dettagli sul mixin, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Appendice

La sezione seguente contiene informazioni aggiuntive sul tipo di dati [!UICONTROL Identity].

## Valori accettati per authenticatedState {#authenticatedState}

Nella tabella seguente sono riportati i valori accettati per `authenticatedState` e i significati associati:

| Valore | Descrizione |
| --- | --- |
| `ambiguous` | Lo stato di autenticazione è ambiguo. |
| `authenticated` | L&#39;utente è stato identificato da un login o da un&#39;azione simile valida al momento dell&#39;osservazione dell&#39;evento. |
| `loggedOut` | L&#39;utente è stato identificato da un&#39;azione di login in un momento precedente, ma non ha eseguito l&#39;accesso al momento dell&#39;osservazione dell&#39;evento. |