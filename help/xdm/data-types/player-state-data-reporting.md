---
title: Tipo di dati per reporting dati stato lettore
description: Scopri il tipo di dati Experience Data Model (XDM) per il reporting dei dati sullo stato del lettore.
exl-id: b01e126d-2467-46b3-8da7-8ec4580595b3
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 21%

---

# [!UICONTROL Tipo di dati Reporting dati stato lettore]

[!UICONTROL Segnalazione dati stato lettore] è un tipo di dati Experience Data Model (XDM) standard che descrive i vari stati e le relative occorrenze all&#39;interno di un lettore multimediale. Utilizza il tipo di dati [!UICONTROL Segnalazione dati stato lettore] per acquisire diversi stati del lettore, ad esempio a schermo intero, disattivato, sottotitoli, immagine nell&#39;immagine e stato attivo. Per ogni stato, registra se è impostato lo stato, il conteggio delle occorrenze e la durata totale in cui rimane attivo durante la riproduzione multimediale.

![Diagramma del tipo di dati del report dei dati sullo stato del lettore.](../images/data-types/player-state-data-information.png)

| Nome visualizzato | Proprietà | Tipo di dati | Descrizione |
|-------------------|----------------|-----------|----------------------------------------------|
| [!UICONTROL Nome stato lettore] | `name` | stringa | Nome dello stato del lettore. Enumerato: &quot;fullscreen&quot;, &quot;mute&quot;, &quot;closedCaptioning&quot;, &quot;pictureInPicture&quot;, &quot;inFocus&quot; con i rispettivi significati. |
| [!UICONTROL Stato del lettore impostato] | `isSet` | booleano | Indica se lo stato del lettore è impostato o meno su quello stato. |
| [!UICONTROL Conteggio stato lettore] | `count` | intero | Il numero di volte in cui lo stato del lettore è stato impostato sul flusso. |
| [!UICONTROL Ora stato lettore] | `time` | intero | La durata totale di quello stato del lettore. |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l&#39;[archivio XDM pubblico](https://github.com/adobe/xdm/blob/master/components/datatypes/playerstatedata.schema.json)
