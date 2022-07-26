---
title: Gruppo di campi dello schema medico
description: Questo documento fornisce una panoramica del gruppo di campi dello schema del farmaco sanitario.
source-git-commit: 3b0c85eb5184dd116b1013e617cf528080fa0656
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 6%

---

# [!UICONTROL Medicina sanitaria] gruppo di campi schema

[!UICONTROL Medicina sanitaria] è un gruppo di campi di schema standard per [[!UICONTROL Medicina] Classe](../../classes/medication.md). Fornisce un singolo campo di tipo oggetto `medication` che acquisisce dettagli quali nome del marchio, numero di lotto e quantità.

![](../../images/field-groups/healthcare-medication.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `ingredients` | Array di oggetti | Elenca gli ingredienti presenti nel farmaco. Ogni oggetto include le seguenti proprietà: <ul><li>`isActive`: (Booleano) Indica se questo ingrediente è ancora utilizzato attivamente in questo farmaco.</li><li>`name`: (Stringa) Il nome dell&#39;ingrediente.</li><li>`quantity`: (Stringa) La quantità dell&#39;ingrediente presente nel farmaco.</li></ul> |
| `brandName` | Stringa | Il marchio del farmaco. |
| `codes` | Matrice di stringhe | Un elenco di codici che identificano questo farmaco. |
| `dosageUnitNumber` | Doppio | Numero dell&#39;unità di dosaggio per il farmaco. |
| `dosageUnitOfMeasurement` | Stringa | Unità di misura per il numero di dosaggio. |
| `expiryDate` | DateTime | Data di scadenza del farmaco. |
| `genericName` | Stringa | Il nome generico del farmaco. |
| `lotNumber` | Stringa | Identificatore univoco per il batch del farmaco. |
| `manufacturerName` | Stringa | Il nome del produttore del farmaco. |
| `quantity` | Doppio | La quantità di droga nel pacchetto. |
| `status` | Stringa | Uno stato generale che indica se il farmaco/farmaco è attivo o meno. |
| `volume` | Doppio | Il volume del farmaco. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta la [archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json).
