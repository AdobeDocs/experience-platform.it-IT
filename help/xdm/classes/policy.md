---
title: Classe criterio
description: Scopri la classe Policy in Experience Data Model (XDM).
exl-id: 56cc8c69-84a0-493e-85c5-e0cd994e4bee
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 3%

---

# [!UICONTROL Criterio] classe

In Experience Data Model (XDM), la classe [!UICONTROL Policy] acquisisce il set minimo di proprietà che definiscono una polizza assicurativa.

![](../images/classes/policy.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `assignedBeneficiary` | Array di tipi di dati [[!UICONTROL Person]](../data-types/person.md) | Acquisisce il beneficiario (o i beneficiari) assegnato alla polizza. |
| `benefitAmount` | [[!UICONTROL Valuta]](../data-types/currency.md) | L’importo da pagare secondo i termini della polizza. |
| `location` | [[!UICONTROL Indirizzo postale]](../data-types/postal-address.md) | Il luogo in cui viene emessa la polizza assicurativa. |
| `owner` | [!UICONTROL Oggetto] | Acquisisce le informazioni sul profilo del contraente. |
| `owner.faxPhone` | [[!UICONTROL Numero di telefono]](../data-types/phone-number.md) | Numero di fax del proprietario. |
| `owner.homeAddress` | [[!UICONTROL Indirizzo postale]](../data-types/postal-address.md) | Indirizzo dell&#39;abitazione del proprietario. |
| `owner.homePhone` | [[!UICONTROL Numero di telefono]](../data-types/phone-number.md) | Numero di telefono dell&#39;abitazione del proprietario. |
| `owner.mobilePhone` | [[!UICONTROL Numero di telefono]](../data-types/phone-number.md) | Numero di telefono cellulare del proprietario. |
| `owner.personalEmail` | [[!UICONTROL Indirizzo e-mail]](../data-types/email-address.md) | Indirizzo e-mail personale del proprietario. |
| `ID` | [!UICONTROL Stringa] | Identificatore della polizza assicurativa. |
| `_id` | [!UICONTROL Stringa] | Identificatore di stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell’univocità di un singolo record, evitare la duplicazione dei dati e cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, durante l&#39;inserimento dei dati non verrà fornito un valore esplicito. Tuttavia, se lo desideri, puoi comunque fornire valori ID univoci. |
| `endDate` | [!UICONTROL DataOra] | La data in cui termina (o termina) la copertura assicurativa. |
| `hasAssignedBeneficiary` | [!UICONTROL Booleano] | Indica se al criterio è assegnato un beneficiario. |
| `name` | [!UICONTROL Stringa] | Nome della polizza assicurativa. |
| `startDate` | [!UICONTROL DataOra] | La data di inizio (o inizio) della copertura assicurativa. |
| `type` | [!UICONTROL Stringa] | Il tipo di polizza assicurativa, ad esempio casa, automobile, affittuario o barca. |

{style="table-layout:auto"}
