---
title: Classe criteri
description: Questo documento fornisce una panoramica della classe Policy in Experience Data Model (XDM).
source-git-commit: c0437b8f9d93c46dbec991a33a893a5b9e0cdf2c
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 5%

---

# [!UICONTROL Criterio] Classe

In Experience Data Model (XDM), l’ [!UICONTROL Criterio] acquisisce l&#39;insieme minimo di proprietà che definiscono una polizza assicurativa.

![](../images/classes/policy.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `assignedBeneficiary` | Array di [[!UICONTROL Persona]](../data-types/person.md) tipi di dati | Acquisisce il beneficiario (o i beneficiari) assegnato alla politica. |
| `benefitAmount` | [[!UICONTROL Valuta]](../data-types/currency.md) | Importo da pagare in base alle condizioni della polizza. |
| `location` | [[!UICONTROL Indirizzo postale]](../data-types/postal-address.md) | Luogo in cui è emessa la polizza assicurativa. |
| `owner` | [!UICONTROL Oggetto] | Acquisisce le informazioni di profilo del contraente. |
| `owner.faxPhone` | [[!UICONTROL Numero di telefono]](../data-types/phone-number.md) | Numero di fax del proprietario. |
| `owner.homeAddress` | [[!UICONTROL Indirizzo postale]](../data-types/postal-address.md) | L&#39;indirizzo di casa del proprietario. |
| `owner.homePhone` | [[!UICONTROL Numero di telefono]](../data-types/phone-number.md) | Il numero di telefono di casa del proprietario. |
| `owner.mobilePhone` | [[!UICONTROL Numero di telefono]](../data-types/phone-number.md) | Il numero di cellulare del proprietario. |
| `owner.personalEmail` | [[!UICONTROL Indirizzo e-mail]](../data-types/email-address.md) | Indirizzo e-mail personale del proprietario. |
| `ID` | [!UICONTROL Stringa] | Identificatore della polizza assicurativa. |
| `_id` | [!UICONTROL Stringa] | Identificatore stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell&#39;univocità di un singolo record, evitare la duplicazione dei dati e per cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, non viene fornito un valore esplicito durante l’inserimento dei dati. Tuttavia, se lo desideri, puoi comunque scegliere di fornire i tuoi valori ID univoci. |
| `endDate` | [!UICONTROL DateTime] | Data in cui termina (o termina) la copertura assicurativa. |
| `hasAssignedBeneficiary` | [!UICONTROL Booleano] | Indica se al criterio è assegnato un beneficiario. |
| `name` | [!UICONTROL Stringa] | Nome della polizza assicurativa. |
| `startDate` | [!UICONTROL DateTime] | Data di inizio (o di inizio) della copertura assicurativa. |
| `type` | [!UICONTROL Stringa] | Tipo di polizza assicurativa, ad esempio casa, automobile, affittatore o barca. |

{style=&quot;table-layout:auto&quot;}
