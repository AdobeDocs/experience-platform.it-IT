---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;emailAddress;xdm:emailAddress;email;indirizzo e-mail;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati indirizzo e-mail
description: Questo documento fornisce una panoramica del tipo di dati XDM Indirizzo e-mail.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 2%

---

# [!UICONTROL Indirizzo e-mail] tipo di dati

[!UICONTROL Indirizzo e-mail] è un tipo di dati XDM (Experience Data Model) standard che descrive i dettagli di un indirizzo e-mail.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Proprietà | Descrizione |
| --- | --- |
| `address` | L’indirizzo tecnico dell’e-mail come comunemente definito nella RFC2822 e negli standard successivi (ad esempio, `name@domain.com`).<br><br>In XDM, gli indirizzi e-mail devono contenere un dominio di primo livello valido per superare la convalida. Consulta quanto segue [documento](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) per un elenco completo dei domini di primo livello validi, come definito dall’Autorità di numerazione con assegnazione Internet (IANA). |
| `label` | Informazioni aggiuntive disponibili. Ad esempio, se un&#39;e-mail dispone di un indirizzo RTF di Microsoft Outlook, viene visualizzato `John Smith smithjr@company.uk`, `John Smith` in questo campo. |
| `primary` | Indica se si tratta dell&#39;indirizzo e-mail principale dell&#39;utente. Un profilo può avere solo un `primary` indirizzo e-mail in un determinato momento. |
| `status` | Indica se l’indirizzo e-mail può essere attualmente utilizzato |
| `statusReason` | Descrizione dell&#39;attuale `status`. |
| `type` | Il modo in cui l&#39;account si riferisce alla persona (ad esempio `work` o `personal`). |

{style=&quot;table-layout:auto&quot;}


Per ulteriori dettagli sul tipo di dati dell’indirizzo e-mail, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
