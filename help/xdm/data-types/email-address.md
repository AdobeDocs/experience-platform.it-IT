---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;emailAddress;xdm:emailAddress;email;email;email;email address;datatype;data-type;data type;
solution: Experience Platform
title: Tipo di dati indirizzo e-mail
description: Scopri il tipo di dati XDM Indirizzo e-mail.
exl-id: 1364df42-f89f-4f48-bcda-5332f3828326
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# [!UICONTROL Indirizzo e-mail] tipo di dati

[!UICONTROL Indirizzo e-mail] è un tipo di dati Experience Data Model (XDM) standard che descrive i dettagli di un indirizzo e-mail.

<img src="../images/data-types/email-address.png" width="450" /><br />

| Proprietà | Descrizione |
| --- | --- |
| `address` | L’indirizzo tecnico dell’e-mail come comunemente definito in RFC2822 e standard successivi (ad esempio, `name@domain.com`).<br><br>In XDM, gli indirizzi e-mail devono contenere un dominio di primo livello valido per superare la convalida. Fai riferimento a quanto segue [documento](https://data.iana.org/TLD/tlds-alpha-by-domain.txt) per un elenco completo dei domini di primo livello validi definiti dall&#39;autorità IANA (Internet Assigned Numbers Authority). |
| `label` | Informazioni aggiuntive sulla visualizzazione che potrebbero essere disponibili. Ad esempio, se un’e-mail ha una visualizzazione dell’indirizzo RTF di Microsoft Outlook `John Smith smithjr@company.uk`, `John Smith` verrebbe inserito in questo campo. |
| `primary` | Indica se si tratta dell’indirizzo e-mail principale dell’individuo. Un profilo può averne solo uno `primary` indirizzo e-mail in un determinato momento. |
| `status` | Indica se l’indirizzo e-mail può essere attualmente utilizzato |
| `statusReason` | Una descrizione dell&#39;attuale `status`. |
| `type` | Il modo in cui l’account si riferisce alla persona (ad esempio `work` o `personal`). |

{style="table-layout:auto"}


Per ulteriori dettagli sul tipo di dati dell’indirizzo e-mail, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/emailaddress.schema.json)
