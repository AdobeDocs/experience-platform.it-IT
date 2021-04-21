---
keywords: Experience Platform;home;argomenti popolari;identity xid;XID
solution: Experience Platform
title: Ottenere l'ID nativo per un'identità
topic-legacy: API guide
description: I dati di identità vengono generalmente forniti come valore di stringa ID e namespace di identità nei dati XDM acquisiti e quando si fornisce un’identità da utilizzare in una chiamata API. Quando le identità vengono mantenute nel servizio Identity, viene generato un ID che viene assegnato a tale identità, denominato XID nativo. API di Platform che richiedono il supporto dei dati di identità utilizzando questo modulo più compatto per l’ID aggregato e lo spazio dei nomi. XID è una stringa codificata base64.
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Ottieni l&#39;ID nativo per un&#39;identità

I dati di identità vengono generalmente forniti come valore di stringa ID e namespace di identità nei dati XDM acquisiti e quando si fornisce un’identità da utilizzare in una chiamata API. Quando le identità vengono mantenute in [!DNL Identity Service], viene generato un ID e assegnato a tale identità, denominato XID nativo. [!DNL Platform] API che richiedono il supporto dei dati di identità utilizzando questo modulo più compatto per l’ID aggregato e lo spazio dei nomi. XID è una stringa codificata base64.

>[!NOTE]
>
>Questo formato è principalmente per uso interno Adobe. L&#39;XID nativo come valore unico è più efficiente in termini di spazio ed è ciò che viene utilizzato internamente nelle soluzioni [!DNL Platform] per lo storage e la serializzazione. Tuttavia non è leggibile dall&#39;uomo, è opaco e richiede una chiamata separata per ottenerlo da utilizzare.

Acquisisci l&#39;XID per un determinato valore ID e spazio dei nomi utilizzando il servizio descritto in questa sezione.

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Risposta**

```json
{
    "xid":"BVrqzwVuzbXrLfmnaG3rXrLf3KJg"
}
```
