---
keywords: ' Experience Platform;home;argomenti più comuni;schema;schema;XDM;campi;schemi;emailAddress;xdm:emailAddress;email;email;email address;dattype;data-type;data type;'
solution: Experience Platform
title: Tipo dati indirizzo e-mail
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM Indirizzo e-mail.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 1%

---


# [!UICONTROL Email address] tipo di dati

[!UICONTROL Email address] è un tipo di dati XDM standard che descrive i dettagli di un indirizzo e-mail.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Proprietà | Descrizione |
| --- | --- |
| `address` | L&#39;indirizzo tecnico dell&#39;e-mail comunemente definito in RFC2822 e negli standard successivi (ad esempio, `name@domain.com`). |
| `label` | Ulteriori informazioni di visualizzazione che potrebbero essere disponibili. Ad esempio, se un&#39;e-mail con un indirizzo RTF di Microsoft Outlook è `John Smith smithjr@company.uk`, `John Smith` viene inserito in questo campo. |
| `primary` | Indica se si tratta dell&#39;indirizzo e-mail principale dell&#39;utente. Un profilo può avere un solo indirizzo `primary` di posta elettronica in un dato momento. |
| `status` | Indica se l&#39;indirizzo e-mail può essere utilizzato al momento |
| `statusReason` | Una descrizione della `status` corrente. |
| `type` | Il modo in cui l&#39;account si riferisce alla persona (ad esempio `work` o `personal`). |


Per ulteriori dettagli sul tipo di dati dell&#39;indirizzo e-mail, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.schema.json)