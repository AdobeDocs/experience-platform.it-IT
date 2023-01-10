---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;applicazione;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati dell'applicazione
description: Questo documento fornisce una panoramica del tipo di dati XDM (Application Experience Data Model).
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 2%

---

# [!UICONTROL Applicazione] tipo di dati

[!UICONTROL Applicazione] è un tipo di dati XDM (Experience Data Model) standard che descrive i dettagli relativi alle interazioni generate da un&#39;applicazione. Un&#39;applicazione fa riferimento a un&#39;esperienza software, ad esempio un&#39;applicazione mobile o desktop che può essere installata, eseguita, chiusa o disinstallata da un utente finale. Le proprietà di questo tipo di dati non sono destinate a descrivere agenti quali chatbots, plugin basati su browser o altre esperienze che non si applicano alle applicazioni.

<img src="../images/data-types/application.PNG" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL Misura]](./measure.md) | Descrive i dettagli sulla terminazione di un&#39;applicazione. |
| `crashes` | [[!UICONTROL Misura]](./measure.md) | Questa proprietà viene attivata quando l&#39;applicazione non esce come previsto. |
| `featureUsages` | [[!UICONTROL Misura]](./measure.md) | Descrive tutti i dati provenienti dall&#39;attivazione di una funzionalità dell&#39;applicazione che viene misurata. |
| `firstLaunches` | [[!UICONTROL Misura]](./measure.md) | Contiene dati sul primo avvio. Questa proprietà viene attivata al primo avvio dopo un&#39;installazione. |
| `installs` | [[!UICONTROL Misura]](./measure.md) | Registra l&#39;installazione di un&#39;applicazione su un dispositivo quando è disponibile un evento di installazione specifico. |
| `launches` | [[!UICONTROL Misura]](./measure.md) | Descrive un valore associato all&#39;avvio di un&#39;applicazione. Questo viene attivato a ogni esecuzione, compresi arresti anomali, installazioni e ripresa dal background quando viene superato il timeout della sessione. |
| `upgrades` | [[!UICONTROL Misura]](./measure.md) | Contiene i dati sull&#39;aggiornamento di un&#39;applicazione installata in precedenza. Questo viene attivato al primo avvio dopo un aggiornamento. |
| `id` | Stringa | Identificatore univoco dell&#39;applicazione. |
| `name` | Stringa | Nome dell&#39;applicazione. |
| `userPerspective` | Stringa | La prospettiva o la relazione fisica tra l’utente e l’app o il marchio al momento dell’evento. La comprensione della prospettiva dell’utente in relazione all’app aiuta a generare con precisione le sessioni, in quanto la maggior parte delle volte non desideri includere `background` e `detached` come parte di una sessione &quot;attiva&quot;. Il valore di questa proprietà deve essere uguale a uno dei valori enum elencati di seguito. <li> `foreground`: L’utente e l’app interagiscono direttamente tra loro. </li> <li> `background`: L’app e l’utente interagiscono indirettamente tra di loro. Ad esempio, l’app potrebbe misurare un valore e aggiornare mentre la schermata è bloccata o un’altra app viene utilizzata in primo piano.  </li> <li> `detached`: Detached indica che l’evento era correlato all’app ma non proveniva direttamente dall’app, ad esempio l’invio di un’e-mail o di una notifica push da un sistema esterno. |
| `version` | Stringa | Versione dell&#39;applicazione. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
