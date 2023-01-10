---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;numeroTelefono;xdm:phoneNumber;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati numero di telefono
description: Questo documento fornisce una panoramica del tipo di dati XDM Numero di telefono.
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 2%

---

# [!UICONTROL Numero di telefono] tipo di dati

[!UICONTROL Numero di telefono] è un tipo di dati XDM standard che descrive i dettagli di un numero di telefono.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| Proprietà | Descrizione |
| --- | --- |
| `extension` | Il numero di composizione interno utilizzato per chiamare da uno scambio privato, un operatore o un quadro comandi. |
| `number` | Il numero di telefono. Il numero di telefono è una stringa e può includere caratteri significativi come le parentesi `()`, trattini `-`o caratteri per indicare identificatori di composizione secondaria, come le estensioni `x` ad esempio, `1-353(0)18391111` o `+613 9403600x1234`. |
| `primary` | Un valore booleano che indica se si tratta del numero di telefono principale dell&#39;utente. A differenza dell&#39;indirizzo o dell&#39;indirizzo e-mail, possono essere presenti più numeri di telefono primari; uno per canale di comunicazione. Il canale di comunicazione è definito dal tipo (indicato dal nome della proprietà principale): `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`e `fax`. |
| `status` | Indica se il numero di telefono può essere attualmente utilizzato. |
| `statusReason` | Una descrizione dello stato corrente. |
| `validity` | Livello di correttezza tecnica del numero di telefono. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati del numero di telefono, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.schema.json)
