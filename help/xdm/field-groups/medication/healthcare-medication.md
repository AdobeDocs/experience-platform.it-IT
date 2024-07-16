---
title: Gruppo di campi Schema per il medicinale sanitario
description: Scopri il gruppo di campi Schema del medicinale per l’assistenza sanitaria.
exl-id: 3423d067-fe8c-44e5-a6f9-ce0458d26ebc
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 7%

---

# [!UICONTROL Medicinale sanitario] gruppo di campi schema

[!UICONTROL Medicinale sanitario] è un gruppo di campi di schema standard per la [[!UICONTROL classe di farmaci]](../../classes/medication.md). Fornisce un singolo campo di tipo oggetto `medication` che acquisisce dettagli quali nome del marchio, numero di lotto e quantità.

![](../../images/field-groups/healthcare-medication.png)

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `ingredients` | Array di oggetti | Elenca gli ingredienti presenti nel medicinale. Ogni oggetto include le seguenti proprietà: <ul><li>`isActive`: (booleano) indica se questo ingrediente è ancora utilizzato attivamente in questo medicinale.</li><li>`name`: (stringa) il nome del componente.</li><li>`quantity`: (Stringa) La quantità dell&#39;ingrediente presente nel medicinale.</li></ul> |
| `brandName` | Stringa | Il nome commerciale del farmaco. |
| `codes` | Array di stringhe | Un elenco di codici che identificano questo medicinale. |
| `dosageUnitNumber` | Doppio | Numero dell’unità di dosaggio del medicinale. |
| `dosageUnitOfMeasurement` | Stringa | Unità di misura per il numero del dosaggio. |
| `expiryDate` | Data e ora | Data di scadenza del medicinale. |
| `genericName` | Stringa | Il nome generico del farmaco. |
| `lotNumber` | Stringa | L’identificatore univoco del batch del farmaco. |
| `manufacturerName` | Stringa | Il nome del produttore del farmaco. |
| `quantity` | Doppio | La quantità di farmaco nella confezione. |
| `status` | Stringa | Uno stato generale che indica se il farmaco/farmaco è attivo o meno. |
| `volume` | Doppio | Il volume del farmaco. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l&#39;[archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json).
