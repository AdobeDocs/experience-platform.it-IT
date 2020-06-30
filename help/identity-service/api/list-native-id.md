---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ottenere l'ID nativo per un'identità
topic: API guide
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 1%

---


# Ottenere l&#39;XID per un&#39;identità

I dati di identità vengono generalmente forniti come valore stringa ID e spazio dei nomi di identità nei dati XDM acquisiti e quando viene fornita un&#39;identità da utilizzare in una chiamata API. Quando le identità sono persistenti in [!DNL Identity Service], viene generato un ID che viene assegnato a tale identità, detto XID nativo. [!DNL Platform] API che richiedono il supporto dei dati di identità utilizzando questo modulo più compatto per l&#39;ID aggregato e lo spazio dei nomi. XID è una stringa codificata base64.

>[!NOTE] Questo formato è destinato principalmente all&#39;uso interno di Adobe. L&#39;XID nativo come valore singolo è più efficiente in termini di spazio ed è ciò che viene utilizzato internamente nelle [!DNL Platform] soluzioni per l&#39;archiviazione e la serializzazione. Tuttavia non è leggibile dall&#39;uomo, è opaco e richiede una chiamata separata per ottenerlo da utilizzare.

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
