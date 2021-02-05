---
keywords: ' Experience Platform;home;argomenti più comuni;schema;schema;XDM;campi;schemi;phoneNumber;xdm:phoneNumber;dataType;data-type;data type;'
solution: Experience Platform
title: Tipo dati numero di telefono
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM Numero di telefono.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---


# [!UICONTROL Phone number] tipo di dati

[!UICONTROL Phone number] è un tipo di dati XDM standard che descrive i dettagli di un numero di telefono.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| Proprietà | Descrizione |
| --- | --- |
| `extension` | Il numero di composizione interno utilizzato per chiamare da una borsa valori privata, un operatore o un quadro di comando. |
| `number` | Il numero di telefono. Si noti che il numero di telefono è una stringa e può includere caratteri significativi come parentesi `()`, trattini `-` o caratteri per indicare identificatori di sub-composizione come le estensioni `x`, ad esempio `1-353(0)18391111` o `+613 9403600x1234`. |
| `primary` | Un valore booleano che indica se si tratta del numero di telefono principale dell&#39;utente. A differenza dell&#39;indirizzo o dell&#39;indirizzo e-mail, possono essere presenti più numeri di telefono primari; uno per canale di comunicazione. Il canale di comunicazione è definito dal tipo (indicato dal nome della proprietà parent): `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown` e `fax`. |
| `status` | Indica se è possibile utilizzare il numero di telefono. |
| `statusReason` | Una descrizione dello stato corrente. |
| `validity` | Livello di correttezza tecnica del numero di telefono. |

Per ulteriori dettagli sul tipo di dati del numero di telefono, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.schema.json)