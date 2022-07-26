---
title: Gruppo di campi dello schema dei fornitori sanitari
description: Questo documento fornisce una panoramica del gruppo di campi dello schema del fornitore sanitario.
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 4%

---

# [!UICONTROL Fornitore sanitario] gruppo di campi schema

[!UICONTROL Fornitore sanitario] è un gruppo di campi di schema standard per [[!UICONTROL Provider] Classe](../../classes/provider.md). Fornisce un singolo campo di tipo oggetto `healthcareProvider` che acquisisce proprietà relative a un singolo professionista sanitario o a un&#39;organizzazione di strutture sanitarie autorizzata a fornire servizi di diagnosi e trattamento delle cure sanitarie.

![](../../images/field-groups/healthcare-provider.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `addressDetails` | Array di oggetti | Elenca i dettagli dell&#39;indirizzo del provider. Ogni oggetto include le seguenti proprietà: <ul><li>`address`: ([[!UICONTROL Indirizzo postale]](../../data-types/postal-address.md)): Indirizzo postale del provider.</li><li>`addressType`: (Stringa) Il tipo di indirizzo, che indica la posizione in cui il fornitore fornisce i servizi.</li></ul> |
| `emailAddress` | [[!UICONTROL Indirizzo e-mail]](../../data-types/email-address.md) | Indirizzo e-mail del provider. |
| `fax` | [[!UICONTROL Numero di telefono]](../../data-types/phone-number.md) | Numero di fax del provider. |
| `phoneNumber` | [[!UICONTROL Numero di telefono]](../../data-types/phone-number.md) | Numero di telefono del provider. |
| `qualifications` | Array di oggetti | Elenca le certificazioni, le licenze o la formazione relative alla prestazione di cure. Ogni oggetto include le seguenti proprietà: <ul><li>`issuer`: ([[!UICONTROL Dettagli account]](../../data-types/account-details.md)): L&#39;organizzazione che regola e rilascia la qualifica.</li><li>`activePeriod`: (Intero) L&#39;anno fino al quale la qualifica è valida.</li><li>`code`: (Stringa) Una rappresentazione codificata della qualifica.</li></ul> |
| `classification` | Stringa | Classificazione del fornitore di servizi in base alla classe o alla categoria (ad esempio assistenza ai pazienti, cure non ai pazienti e così via). |
| `isActive` | Booleano | Indica se il provider è attivo. |
| `languages` | Matrice di stringhe | Elenco delle lingue in cui il provider esegue le operazioni. |
| `practiceGroupName` | Stringa | Nome del gruppo di pratiche per il provider di servizi. |
| `practiceGroupType` | Stringa | Tipo di gruppo di procedure per il provider di servizi. |
| `practiceType` | Stringa | Tipo di pratica per il provider di servizi. |
| `specialties` | Matrice di stringhe | Elenco delle specialità offerte da questo fornitore. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta la [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json).
