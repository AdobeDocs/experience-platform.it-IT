---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;phoneNumber;xdm:phoneNumber;datatype;data-type;data type;
solution: Experience Platform
title: Tipo di dati numero di telefono
description: Scopri il tipo di dati XDM Numero di telefono.
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 16%

---

# [!UICONTROL Tipo di dati numero di telefono]

[!UICONTROL Phone number] è un tipo di dati XDM standard che descrive i dettagli di un numero di telefono.

![](../images/data-types/phone-number.png){width=600}

| Proprietà | Descrizione |
| --- | --- |
| `extension` | Il numero interno utilizzato per chiamare da un centralino, centralino privato o operatore. |
| `number` | Il numero di telefono. Nota: il numero di telefono è una stringa e può includere caratteri significativi come parentesi quadre `()`, trattini `-` o caratteri per indicare identificatori di sotto-composizione come le estensioni `x`, ad esempio `1-353(0)18391111` o `+613 9403600x1234`. |
| `primary` | Un valore booleano che indica se si tratta del numero di telefono principale dell’individuo. A differenza dell’indirizzo o dell’indirizzo e-mail, ci possono essere più numeri di telefono primari; uno per canale di comunicazione. Il canale di comunicazione è definito dal tipo (indicato dal nome della proprietà padre): `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown` e `fax`. |
| `status` | Indica se il numero di telefono può essere attualmente utilizzato. |
| `statusReason` | Descrizione dello stato corrente. |
| `validity` | Un livello di correttezza tecnica del numero di telefono. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati del numero di telefono, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.schema.json)
