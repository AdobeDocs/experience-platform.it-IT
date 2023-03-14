---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;XDM system;experience data model;data model;ui;workspace;required;field;
title: Definire i campi obbligatori nell’interfaccia utente
description: Scopri come definire un campo XDM richiesto nell’interfaccia utente di Experience Platform.
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: fe3d9a3fc473e7ca13f0e0c2f222bcc1b1a991c4
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Definire i campi obbligatori nell’interfaccia utente

In Experience Data Model (XDM), un campo obbligatorio indica che è necessario fornire un valore valido affinché un record o un evento di serie temporale particolare possa essere accettato durante l’acquisizione dei dati. I casi d’uso comuni per i campi obbligatori includono informazioni sull’identità dell’utente e marche temporali.

>[!IMPORTANT]
>
>A prescindere dal fatto che un campo schema sia obbligatorio o meno, Platform non accetta `null` o valori vuoti per qualsiasi campo acquisito. Se non è presente alcun valore per un particolare campo in un record o in un evento, la chiave per tale campo deve essere esclusa dal payload di acquisizione.

Quando [definizione di un nuovo campo](./overview.md#define) nell’interfaccia utente di Adobe Experience Platform, puoi impostarla come campo obbligatorio selezionando il **[!UICONTROL Obbligatorio]** nella barra a destra. Seleziona **[!UICONTROL Applica]** per applicare la modifica allo schema.

![Casella di controllo obbligatoria](../../images/ui/fields/required/root.png)

Se il campo è un attributo a livello di radice sotto l’oggetto ID tenant, il relativo percorso viene visualizzato immediatamente in **[!UICONTROL Campi obbligatori]** nella barra a sinistra.

![Campo obbligatorio a livello di radice](../../images/ui/fields/required/applied.png)

Se un campo obbligatorio è nidificato all’interno di un oggetto che non è contrassegnato come obbligatorio, tuttavia, il campo nidificato non viene visualizzato in **[!UICONTROL Campi obbligatori]** nella barra a sinistra.

Nell’esempio seguente, il `internalSKU` il campo viene impostato come richiesto, ma il relativo oggetto padre `SKUs` non lo è. In questo caso, non si verificherebbero errori di convalida se `SKUs` è escluso durante l’acquisizione dei dati, anche se il campo secondario `internalSKU` è contrassegnato come obbligatorio. In altre parole, mentre `SKUs` è facoltativo, deve contenere `internalSKU` nel caso in cui sia incluso.

![Campo obbligatorio nidificato](../../images/ui/fields/required/nested.png)

Se desideri che un campo nidificato sia sempre obbligatorio in uno schema, devi impostare anche tutti i campi principali come richiesto (ad eccezione dell’oggetto ID tenant).

![Campi obbligatori padre e figlio](../../images/ui/fields/required/parent-and-child.png)

## Passaggi successivi

Questa guida illustra come definire un campo obbligatorio nell’interfaccia utente di. Consulta la panoramica su [definizione dei campi nell’interfaccia utente](./overview.md#special) per scoprire come definire altri tipi di campi XDM in [!DNL Schema Editor].
