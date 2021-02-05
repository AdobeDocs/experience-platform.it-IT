---
keywords: ' Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;area di lavoro;obbligatorio;campo;'
solution: Experience Platform
title: Definire i campi obbligatori nell'interfaccia utente
description: Scoprite come definire un campo XDM richiesto nell'interfaccia utente del Experience Platform .
topic: user guide
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---


# Definire i campi obbligatori nell&#39;interfaccia utente

In Experience Data Model (XDM), un campo obbligatorio indica che è necessario fornire un valore valido per consentire l&#39;accettazione di un determinato record o evento della serie temporale durante l&#39;assimilazione dei dati. I casi d’uso comuni per i campi obbligatori includono informazioni sull’identità dell’utente e marche temporali.

Quando [definisci un nuovo campo](./overview.md#define) nell&#39;interfaccia utente di Adobe Experience Platform, puoi impostarlo come campo obbligatorio selezionando la casella di controllo **[!UICONTROL Required]** nella barra a destra. Selezionare **[!UICONTROL Apply]** per applicare la modifica allo schema.

![](../../images/ui/fields/special/required.png)

Una volta applicato il campo, il relativo percorso viene visualizzato sotto **[!UICONTROL Required fields]** nella barra a sinistra. Se il campo è nidificato, tutti i campi principali verranno visualizzati come necessario.

![](../../images/ui/fields/special/required-applied.png)

## Passaggi successivi

Questa guida descrive come definire un campo obbligatorio nell’interfaccia utente. Per informazioni su come definire altri tipi di campi XDM nell&#39; [!DNL Schema Editor], vedere la panoramica relativa alla [definizione dei campi nell&#39;interfaccia utente](./overview.md#special).