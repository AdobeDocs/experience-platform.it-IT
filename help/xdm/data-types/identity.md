---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;identità;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati identità
description: Questo documento fornisce una panoramica del tipo di dati XDM per l’identità.
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 4%

---

# [!UICONTROL Identità] tipo di dati

[!UICONTROL Identità] è un tipo di dati XDM standard utilizzato per distinguere chiaramente le persone che interagiscono con le esperienze digitali. L’identità è stabilita da un provider di identità, a cui a sua volta si fa riferimento in una `namespace` attributo. All’interno di ogni `namespace`, l’identità è univoca.

<img src="../images/data-types/identity.png" width="550" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `namespace` | Oggetto | Oggetto contenente un singolo campo stringa (`code`), che indica lo spazio dei nomi associato al `id` attributo. |
| `authenticatedState` | Stringa | Lo stato di autenticazione per questa identità al momento dell’evento esperienza osservato. Consulta la [appendice](#authenticatedState) per i valori e le definizioni accettati. |
| `id` | Stringa | L’identità del consumatore nel relativo spazio dei nomi. |
| `primary` | Booleano | Indica se si tratta dell’identità primaria dell’individuo. Ogni individuo può avere una sola identità primaria. |
| `xid` | Stringa | Se presente, questo valore rappresenta un identificatore per più spazi dei nomi che è univoco tra tutti gli identificatori relativi allo spazio dei nomi in tutti gli spazi dei nomi. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Appendice

La sezione seguente contiene informazioni aggiuntive sulle [!UICONTROL Identità] tipo di dati.

## Valori accettati per authenticatedState {#authenticatedState}

La tabella seguente illustra i valori accettati per `authenticatedState` e il significato associato:

| Valore | Descrizione |
| --- | --- |
| `ambiguous` | Lo stato di autenticazione è ambiguo. |
| `authenticated` | L’utente è stato identificato da un login o da un’azione simile valida al momento dell’osservazione dell’evento. |
| `loggedOut` | L’utente è stato identificato da un’azione di accesso in un momento precedente, ma non ha eseguito l’accesso al momento dell’osservazione dell’evento. |
