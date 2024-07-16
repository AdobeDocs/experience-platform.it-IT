---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;applicazione;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati applicazione
description: Scopri il tipo di dati Application Experience Data Model (XDM).
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---

# Tipo di dati [!UICONTROL Applicazione]

[!UICONTROL Applicazione] è un tipo di dati XDM (Experience Data Model) standard che descrive i dettagli relativi alle interazioni generate da un&#39;applicazione. Un’applicazione si riferisce a un’esperienza software, ad esempio un’applicazione mobile o desktop che può essere installata, eseguita, chiusa o disinstallata da un utente finale. Le proprietà di questo tipo di dati non sono intese a descrivere agenti come chatbot, plug-in basati su browser o altre esperienze che non si applicano alle applicazioni.

<img src="../images/data-types/application.PNG" width="500" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL Misura]](./measure.md) | Descrive i dettagli sulla chiusura di un&#39;applicazione. |
| `crashes` | [[!UICONTROL Misura]](./measure.md) | Questa proprietà viene attivata quando l’applicazione non si chiude come previsto. |
| `featureUsages` | [[!UICONTROL Misura]](./measure.md) | Descrive tutti i dati relativi all&#39;attivazione di una funzionalità dell&#39;applicazione misurata. |
| `firstLaunches` | [[!UICONTROL Misura]](./measure.md) | Contiene dati sul primo avvio. Questa proprietà viene attivata al primo avvio dopo un’installazione. |
| `installs` | [[!UICONTROL Misura]](./measure.md) | Registra l&#39;installazione di un&#39;applicazione su un dispositivo quando è disponibile un evento di installazione specifico. |
| `launches` | [[!UICONTROL Misura]](./measure.md) | Descrive un valore associato all’avvio di un’applicazione. Viene attivato a ogni esecuzione, inclusi arresti anomali, installazioni e ripresa dal background quando viene superato il timeout della sessione. |
| `upgrades` | [[!UICONTROL Misura]](./measure.md) | Contiene dati sull&#39;aggiornamento di un&#39;applicazione installata in precedenza. Viene attivato al primo avvio dopo un aggiornamento. |
| `id` | Stringa | Identificatore univoco dell’applicazione. |
| `name` | Stringa | Nome dell&#39;applicazione. |
| `userPerspective` | Stringa | Il rapporto prospettico o fisico tra l’utente e l’app o il brand nel momento in cui si è verificato un evento. Comprendere la prospettiva dell&#39;utente in relazione all&#39;app aiuta a generare accuratamente le sessioni, in quanto la maggior parte delle volte non è necessario includere `background` e `detached` eventi come parte di una sessione &quot;attiva&quot;. Il valore di questa proprietà deve essere uguale a uno dei valori enum elencati di seguito. <li> `foreground`: l&#39;utente e l&#39;app interagiscono direttamente tra loro. </li> <li> `background`: l&#39;app e l&#39;utente interagiscono indirettamente l&#39;uno con l&#39;altro. Ad esempio, l’app può misurare un valore e aggiornarlo mentre lo schermo è bloccato o un’altra app viene utilizzata in primo piano.  </li> <li> `detached`: scollegato significa che l&#39;evento era correlato all&#39;app ma non proveniva direttamente dall&#39;app, ad esempio l&#39;invio di un&#39;e-mail o di una notifica push da un sistema esterno. |
| `version` | Stringa | Versione dell’applicazione. |

{style="table-layout:auto"}

Per ulteriori dettagli sul tipo di dati, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
