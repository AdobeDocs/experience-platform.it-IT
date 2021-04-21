---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;emailAddress;xdm:emailAddress;email;indirizzo e-mail;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati indirizzo e-mail
topic-legacy: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM Indirizzo e-mail.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 1%

---

# [!UICONTROL Email address] tipo di dati

[!UICONTROL Email address] è un tipo di dati XDM standard che descrive i dettagli di un indirizzo e-mail.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Proprietà | Descrizione |
| --- | --- |
| `address` | L’indirizzo tecnico dell’e-mail come comunemente definito nella RFC2822 e negli standard successivi (ad esempio, `name@domain.com`). |
| `label` | Informazioni aggiuntive disponibili. Ad esempio, se un&#39;e-mail presenta un indirizzo RTF di Microsoft Outlook pari a `John Smith smithjr@company.uk`, `John Smith` viene posizionato in questo campo. |
| `primary` | Indica se si tratta dell&#39;indirizzo e-mail principale dell&#39;utente. Un profilo può avere un solo indirizzo e-mail `primary` in un dato momento. |
| `status` | Indica se l’indirizzo e-mail può essere attualmente utilizzato |
| `statusReason` | Una descrizione del `status` corrente. |
| `type` | Il modo in cui l’account si riferisce alla persona (ad esempio `work` o `personal`). |


Per ulteriori dettagli sul tipo di dati dell’indirizzo e-mail, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/emailaddress.schema.json)
