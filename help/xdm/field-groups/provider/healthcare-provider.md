---
title: Gruppo di campi schema provider di servizi sanitari
description: Scopri il gruppo di campi dello schema per l’operatore sanitario.
exl-id: e39b4082-4b66-47b3-a8e2-951d8a96f742
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 3%

---

# [!UICONTROL Fornitore di servizi sanitari] gruppo di campi schema

[!UICONTROL Fornitore di servizi sanitari] è un gruppo di campi di schema standard per [[!UICONTROL Provider] classe](../../classes/provider.md). Fornisce un singolo campo di tipo oggetto `healthcareProvider` che acquisisce proprietà relative a un singolo professionista sanitario o a un&#39;organizzazione di strutture sanitarie autorizzata a fornire servizi di diagnosi e trattamento di assistenza sanitaria.

![](../../images/field-groups/healthcare-provider.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `addressDetails` | Array di oggetti | Elenca i dettagli dell&#39;indirizzo del provider. Ogni oggetto include le seguenti proprietà: <ul><li>`address`: ([[!UICONTROL Indirizzo postale]](../../data-types/postal-address.md)): l’indirizzo postale del fornitore.</li><li>`addressType`: (Stringa) tipo di indirizzo, che indica dove il provider fornisce servizi.</li></ul> |
| `emailAddress` | [[!UICONTROL Indirizzo e-mail]](../../data-types/email-address.md) | Indirizzo e-mail del provider. |
| `fax` | [[!UICONTROL Numero di telefono]](../../data-types/phone-number.md) | Numero di fax del provider. |
| `phoneNumber` | [[!UICONTROL Numero di telefono]](../../data-types/phone-number.md) | Numero di telefono del provider. |
| `qualifications` | Array di oggetti | Elenca le certificazioni, le licenze o la formazione relative alla fornitura di assistenza. Ogni oggetto include le seguenti proprietà: <ul><li>`issuer`: ([[!UICONTROL Dettagli account]](../../data-types/account-details.md)): l’organizzazione che disciplina e rilascia la qualifica.</li><li>`activePeriod`: (Numero intero) l’anno fino al quale è valida la qualifica.</li><li>`code`: (Stringa) Rappresentazione codificata della qualifica.</li></ul> |
| `classification` | Stringa | La classificazione del fornitore di servizi in base alla classe o alla categoria (ad esempio, assistenza paziente, assistenza non paziente e così via). |
| `isActive` | Booleano | Indica se il provider è attivo. |
| `languages` | Array di stringhe | Elenco di lingue in cui il provider esegue operazioni. |
| `practiceGroupName` | Stringa | Nome del gruppo di esercitazione per il provider di servizi. |
| `practiceGroupType` | Stringa | Tipo di gruppo di esercitazione per il provider di servizi. |
| `practiceType` | Stringa | Tipo di esercitazione per il provider di servizi. |
| `specialties` | Array di stringhe | Elenco delle specialità offerte da questo provider. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json).
