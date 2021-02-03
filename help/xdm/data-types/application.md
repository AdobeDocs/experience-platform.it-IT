---
keywords: ' Experience Platform;home;argomenti comuni;schema;schema;XDM;campi;schemi;applicazione;tipo di dati;tipo di dati;tipo di dati;'
solution: Experience Platform
title: Tipo dati applicazione
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM (Application Experience Data Model).
translation-type: tm+mt
source-git-commit: d282ea5526a05b28c6a82470eabf23e44d1fb420
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 1%

---


# [!UICONTROL Application] tipo di dati

[!UICONTROL Application] è un tipo di dati XDM (Experience Data Model) standard che descrive i dettagli relativi alle interazioni generate dall&#39;applicazione. Un&#39;applicazione fa riferimento a un&#39;esperienza software, ad esempio un&#39;applicazione mobile o desktop che può essere installata, eseguita, chiusa o disinstallata da un utente finale. Le proprietà per questo tipo di dati non sono destinate a descrivere agenti quali chatbots, plug-in basati su browser o altre esperienze che non si applicano alle applicazioni.

<img src="../images/data-types/application.PNG" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL Measure]](./measure.md) | Descrive i dettagli sulla terminazione di un&#39;applicazione. |
| `crashes` | [[!UICONTROL Measure]](./measure.md) | Questa proprietà viene attivata quando l&#39;applicazione non si chiude come previsto. |
| `featureUsages` | [[!UICONTROL Measure]](./measure.md) | Descrive tutti i dati derivanti dall&#39;attivazione di una funzionalità dell&#39;applicazione che viene misurata. |
| `firstLaunches` | [[!UICONTROL Measure]](./measure.md) | Contiene i dati relativi al primo avvio. Questa proprietà viene attivata al primo avvio dopo un&#39;installazione. |
| `installs` | [[!UICONTROL Measure]](./measure.md) | Registra l&#39;installazione di un&#39;applicazione su un dispositivo quando è disponibile un evento di installazione specifico. |
| `launches` | [[!UICONTROL Measure]](./measure.md) | Descrive un valore associato all&#39;avvio di un&#39;applicazione. Questo viene attivato a ogni esecuzione, compresi arresti anomali, installazioni e ripresa in background quando viene superato il timeout della sessione. |
| `upgrades` | [[!UICONTROL Measure]](./measure.md) | Contiene i dati sull&#39;aggiornamento di un&#39;applicazione precedentemente installata. Questo viene attivato al primo avvio dopo un aggiornamento. |
| `id` | Stringa | Un identificatore univoco per l’applicazione. |
| `name` | Stringa | Nome dell’applicazione. |
| `userPerspective` | Stringa | Prospettiva o relazione fisica tra l&#39;utente e l&#39;app o il marchio al momento dell&#39;evento. La comprensione della prospettiva dell&#39;utente in relazione all&#39;app aiuta a generare con precisione le sessioni, poiché la maggior parte delle volte non desiderate includere gli eventi `background` e `detached` come parte di una sessione &quot;attiva&quot;. Il valore di questa proprietà deve essere uguale a uno dei valori enum elencati di seguito. <li> `foreground`: L&#39;utente e l&#39;app interagiscono direttamente tra loro. </li> <li> `background`: L&#39;app e l&#39;utente interagiscono indirettamente tra loro. Ad esempio, l&#39;app potrebbe misurare un valore e aggiornare mentre lo schermo è bloccato o un&#39;altra app viene utilizzata in primo piano.  </li> <li> `detached`: Scollegato indica che l’evento era correlato all’app ma non proveniva direttamente dall’app, ad esempio l’invio di una notifica e-mail o push da un sistema esterno. |
| `version` | Stringa | Versione dell’applicazione. |

Per ulteriori dettagli sul tipo di dati, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)