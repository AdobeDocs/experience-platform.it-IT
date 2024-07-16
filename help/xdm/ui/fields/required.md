---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;XDM system;experience data model;data model;ui;workspace;required;field;
title: Definire i campi obbligatori nell’interfaccia utente
description: Scopri come definire un campo XDM richiesto nell’interfaccia utente di Experience Platform.
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# Definire i campi obbligatori nell’interfaccia utente

In Experience Data Model (XDM), un campo obbligatorio indica che è necessario fornire un valore valido affinché un record o un evento di serie temporale particolare possa essere accettato durante l’acquisizione dei dati. I casi d’uso comuni per i campi obbligatori includono informazioni sull’identità dell’utente e marche temporali.

>[!IMPORTANT]
>
>A prescindere dal fatto che un campo schema sia obbligatorio o meno, Platform non accetta `null` o valori vuoti per nessun campo acquisito. Se non è presente alcun valore per un particolare campo in un record o in un evento, la chiave per tale campo deve essere esclusa dal payload di acquisizione.

Quando [definisci un nuovo campo](./overview.md#define) nell&#39;interfaccia utente di Adobe Experience Platform, puoi impostarlo come campo obbligatorio selezionando la casella di controllo **[!UICONTROL Obbligatorio]** nella barra a destra. Seleziona **[!UICONTROL Applica]** per applicare la modifica allo schema.

![Casella di controllo obbligatoria](../../images/ui/fields/required/root.png)

Se il campo è un attributo a livello di radice sotto l&#39;oggetto ID tenant, il relativo percorso viene visualizzato immediatamente in **[!UICONTROL Campi obbligatori]** nella barra a sinistra.

![Campo obbligatorio a livello di radice](../../images/ui/fields/required/applied.png)

Tuttavia, se un campo obbligatorio è nidificato all&#39;interno di un oggetto che non è contrassegnato come obbligatorio, il campo nidificato non viene visualizzato in **[!UICONTROL Campi obbligatori]** nella barra a sinistra.

Nell&#39;esempio seguente, il campo `internalSKU` è impostato come obbligatorio, ma l&#39;oggetto padre `SKUs` non lo è. In questo caso, non si verificherebbero errori di convalida se `SKUs` venisse escluso durante l&#39;acquisizione dei dati, anche se il campo secondario `internalSKU` è contrassegnato come obbligatorio. In altre parole, mentre `SKUs` è facoltativo, deve contenere un campo `internalSKU` nel caso in cui sia incluso.

![Campo obbligatorio nidificato](../../images/ui/fields/required/nested.png)

Se desideri che un campo nidificato sia sempre obbligatorio in uno schema, devi impostare anche tutti i campi principali come richiesto (ad eccezione dell’oggetto ID tenant).

![Campi obbligatori padre e figlio](../../images/ui/fields/required/parent-and-child.png)

## Passaggi successivi

Questa guida illustra come definire un campo obbligatorio nell’interfaccia utente. Per informazioni su come definire altri tipi di campi XDM in [!DNL Schema Editor], consulta la panoramica su [definizione dei campi nell&#39;interfaccia utente](./overview.md#special).
