---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;data model;ui;workspace;required;field;
solution: Experience Platform
title: Definire un campo obbligatorio nell'interfaccia utente
description: Scoprite come definire un campo XDM richiesto nell'interfaccia utente del Experience Platform .
topic: user guide
translation-type: tm+mt
source-git-commit: 48025fc11558bf6773ce5c48054483758c7e993f
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---


# Definire un campo obbligatorio nell&#39;interfaccia utente

In Experience Data Model (XDM), un campo obbligatorio indica che è necessario fornire un valore valido per consentire l&#39;accettazione di un determinato record o evento della serie temporale durante l&#39;assimilazione dei dati. I casi d’uso comuni per i campi obbligatori includono informazioni sull’identità dell’utente e marche temporali.

Quando [definisci un nuovo campo](./overview.md#define) nell&#39;interfaccia utente di Adobe Experience Platform, puoi impostarlo come campo obbligatorio selezionando la casella di controllo **[!UICONTROL Required]** nella barra a destra. Selezionare **[!UICONTROL Apply]** per applicare la modifica allo schema.

![](../../images/ui/fields/special/required.png)

Una volta applicato il campo, il relativo percorso viene visualizzato sotto **[!UICONTROL Required fields]** nella barra a sinistra. Se il campo è nidificato, tutti i campi principali verranno visualizzati come necessario.

![](../../images/ui/fields/special/required-applied.png)

## Passaggi successivi

Questa guida descrive come definire un campo obbligatorio nell’interfaccia utente. Per informazioni su come definire altri tipi di campi XDM nell&#39; [!DNL Schema Editor], vedere la panoramica relativa alla [definizione dei campi nell&#39;interfaccia utente](./overview.md#special).