---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;identità;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati identità
description: Scopri il tipo di dati XDM per l’identità.
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 11%

---

# Tipo di dati [!UICONTROL Identity]

[!UICONTROL Identity] è un tipo di dati XDM standard utilizzato per distinguere chiaramente le persone che interagiscono con le esperienze digitali. L&#39;identità è stabilita da un provider di identità, a cui si fa riferimento in un attributo `namespace`. In ogni `namespace`, l&#39;identità è univoca.

<img src="../images/data-types/identity.png" width="550" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `namespace` | Oggetto | Oggetto contenente un singolo campo stringa (`code`), che indica lo spazio dei nomi associato all&#39;attributo `id` fornito. |
| `authenticatedState` | Stringa | Lo stato di autenticazione per questa identità al momento dell’evento esperienza osservato. Per informazioni sui valori e le definizioni accettati, vedere [appendice](#authenticatedState). |
| `id` | Stringa | L’identità del consumatore nel relativo spazio dei nomi. |
| `primary` | Booleano | Indica se si tratta dell’identità primaria dell’individuo. Ogni individuo può avere una sola identità primaria. |
| `xid` | Stringa | Se presente, questo valore rappresenta un identificatore per più spazi dei nomi che è univoco tra tutti gli identificatori relativi allo spazio dei nomi in tutti gli spazi dei nomi. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## Appendice

La sezione seguente contiene informazioni aggiuntive sul tipo di dati [!UICONTROL Identity].

## Valori accettati per authenticatedState {#authenticatedState}

Nella tabella seguente vengono illustrati i valori accettati per `authenticatedState` e i relativi significati associati:

| Valore | Descrizione |
| --- | --- |
| `ambiguous` | Lo stato di autenticazione è ambiguo. |
| `authenticated` | L’utente è stato identificato da un login o da un’azione simile valida al momento dell’osservazione dell’evento. |
| `loggedOut` | L’utente è stato identificato da un’azione di accesso in un momento precedente, ma non ha eseguito l’accesso al momento dell’osservazione dell’evento. |
