---
keywords: Experience Platform;home;argomenti popolari;identità xid;XID
solution: Experience Platform
title: Ottenere l'ID nativo per un'identità
description: I dati di identità vengono generalmente forniti come valore della stringa ID e spazio dei nomi dell’identità nei dati XDM acquisiti e quando si fornisce un’identità da utilizzare in una chiamata API. Quando le identità vengono rese permanenti in Identity Service, viene generato un ID a cui viene assegnato l’identità, denominato XID nativo. API di Platform che richiedono il supporto dei dati di identità utilizzando questo modulo più compatto per l’ID aggregato e lo spazio dei nomi. XID è una stringa con codifica base64.
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 1%

---

# Ottieni l’ID nativo di un’identità

I dati di identità vengono generalmente forniti come valore della stringa ID e spazio dei nomi dell’identità nei dati XDM acquisiti e quando si fornisce un’identità da utilizzare in una chiamata API. Quando le identità vengono rese permanenti in [!DNL Identity Service], viene generato un ID a cui viene assegnata l’identità, denominata XID nativo. [!DNL Platform] API che richiedono il supporto dei dati di identità utilizzando questo modulo più compatto per l’ID aggregato e lo spazio dei nomi. XID è una stringa con codifica base64.

>[!NOTE]
>
>Questo formato è principalmente per uso Adobe interno. XID nativo come singolo valore è più efficiente in termini di spazio ed è ciò che viene utilizzato internamente in [!DNL Platform] soluzioni di storage e serializzazione. Tuttavia, non è leggibile dall’uomo, è opaco e richiede una chiamata separata per ottenerlo per utilizzarlo.

Acquisisci l’XID per un determinato valore ID e spazio dei nomi utilizzando il servizio descritto in questa sezione.

**Formato API**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/identity?namespace={NAMESPACE}&id={ID_VALUE}
```

**Richiesta**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/identity?namespace=email&id=test@adobetest.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```json
{
    "xid":"BVrqzwVuzbXrLfmnaG3rXrLf3KJg"
}
```
