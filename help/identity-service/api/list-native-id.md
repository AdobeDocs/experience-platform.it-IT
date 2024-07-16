---
keywords: Experience Platform;home;argomenti popolari;identità xid;XID
solution: Experience Platform
title: Ottenere l'ID nativo per un'identità
description: I dati di identità vengono generalmente forniti come valore della stringa ID e spazio dei nomi dell’identità nei dati XDM acquisiti e quando si fornisce un’identità da utilizzare in una chiamata API. Quando le identità vengono rese permanenti in Identity Service, viene generato un ID a cui viene assegnato l’identità, denominato XID nativo. API di Platform che richiedono il supporto dei dati di identità utilizzando questo modulo più compatto per l’ID aggregato e lo spazio dei nomi. XID è una stringa con codifica base64.
role: Developer
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 1%

---

# Ottieni l’ID nativo di un’identità

I dati di identità vengono generalmente forniti come valore della stringa ID e spazio dei nomi dell’identità nei dati XDM acquisiti e quando si fornisce un’identità da utilizzare in una chiamata API. Quando le identità vengono rese permanenti in [!DNL Identity Service], viene generato e assegnato un ID a tale identità, denominato XID nativo. [!DNL Platform] API che richiedono il supporto dei dati di identità utilizzando questo modulo più compatto per l&#39;ID aggregato e lo spazio dei nomi. XID è una stringa con codifica base64.

>[!NOTE]
>
>Questo formato è principalmente per uso Adobe interno. XID nativo come singolo valore è più efficiente in termini di spazio ed è ciò che viene utilizzato internamente nelle soluzioni [!DNL Platform] per l&#39;archiviazione e la serializzazione. Tuttavia, non è leggibile dall’uomo, è opaco e richiede una chiamata separata per ottenerlo per utilizzarlo.

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
