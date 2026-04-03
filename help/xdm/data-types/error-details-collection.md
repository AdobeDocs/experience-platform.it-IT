---
title: Tipo di dati raccolta dettagli errore
description: Scopri il tipo di dati Experience Data Model (XDM) della raccolta dei dettagli degli errori.
exl-id: 54b03147-9bca-46af-86c8-90e42b4de26b
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 10%

---

# Tipo di dati della raccolta [!UICONTROL Error Details]

La raccolta [!UICONTROL Error Details] è un tipo di dati XDM (Experience Data Model) standard che descrive i dettagli dell&#39;errore. Utilizzare il tipo di dati della raccolta [!UICONTROL Error Details] per acquisire i dettagli per l&#39;origine dell&#39;errore e l&#39;identificazione. L’ID errore identifica l’errore e la sorgente dell’errore specifica se proviene dal lettore o da una sorgente esterna.

![Diagramma del tipo di dati Informazioni dettagli errore.](../images/data-types/error-details-collection.png)

| Nome visualizzato | Proprietà | Tipo di dati | Obbligatorio | Descrizione |
|----------------------------|--------------|-----------|----------|-----------------------------------------------|
| [!UICONTROL Error ID] | `name` | stringa | No | ID dell’errore. |
| [!UICONTROL Error Source] | `source` | stringa | No | Origine dell’errore. Enumerato: &quot;player&quot;, &quot;external&quot; con i rispettivi significati. |

{style="table-layout:auto"}
