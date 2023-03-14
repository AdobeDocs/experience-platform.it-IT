---
title: Classe criterio
description: Questo documento fornisce una panoramica della classe Policy in Experience Data Model (XDM).
exl-id: 56cc8c69-84a0-493e-85c5-e0cd994e4bee
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 5%

---

# [!UICONTROL Policy] classe

In Experience Data Model (XDM), la [!UICONTROL Policy] la classe acquisisce l’insieme minimo di proprietà che definiscono una polizza assicurativa.

![](../images/classes/policy.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `assignedBeneficiary` | Array di [[!UICONTROL Persona]](../data-types/person.md) tipi di dati | Acquisisce il beneficiario (o i beneficiari) assegnato alla polizza. |
| `benefitAmount` | [[!UICONTROL Valuta]](../data-types/currency.md) | L’importo da pagare secondo i termini della polizza. |
| `location` | [[!UICONTROL Indirizzo postale]](../data-types/postal-address.md) | Il luogo in cui viene emessa la polizza assicurativa. |
| `owner` | [!UICONTROL Oggetto] | Acquisisce le informazioni sul profilo del contraente. |
| `owner.faxPhone` | [[!UICONTROL Numero di telefono]](../data-types/phone-number.md) | Numero di fax del proprietario. |
| `owner.homeAddress` | [[!UICONTROL Indirizzo postale]](../data-types/postal-address.md) | Indirizzo dell&#39;abitazione del proprietario. |
| `owner.homePhone` | [[!UICONTROL Numero di telefono]](../data-types/phone-number.md) | Numero di telefono dell&#39;abitazione del proprietario. |
| `owner.mobilePhone` | [[!UICONTROL Numero di telefono]](../data-types/phone-number.md) | Numero di telefono cellulare del proprietario. |
| `owner.personalEmail` | [[!UICONTROL Indirizzo e-mail]](../data-types/email-address.md) | Indirizzo e-mail personale del proprietario. |
| `ID` | [!UICONTROL Stringa] | Identificatore della polizza assicurativa. |
| `_id` | [!UICONTROL Stringa] | Identificatore di stringa univoco generato dal sistema per il record. Questo campo viene utilizzato per tenere traccia dell’univocità di un singolo record, evitare la duplicazione dei dati e cercare tale record nei servizi a valle.<br><br>Poiché questo campo è generato dal sistema, durante l’inserimento dei dati non viene fornito un valore esplicito. Tuttavia, se lo desideri, puoi comunque fornire valori ID univoci. |
| `endDate` | [!UICONTROL DateTime] | La data in cui termina (o termina) la copertura assicurativa. |
| `hasAssignedBeneficiary` | [!UICONTROL Booleano] | Indica se al criterio è assegnato un beneficiario. |
| `name` | [!UICONTROL Stringa] | Nome della polizza assicurativa. |
| `startDate` | [!UICONTROL DateTime] | La data di inizio (o inizio) della copertura assicurativa. |
| `type` | [!UICONTROL Stringa] | Il tipo di polizza assicurativa, ad esempio casa, automobile, affittuario o barca. |

{style="table-layout:auto"}
