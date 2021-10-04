---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;workspace;obbligatorio;campo;
title: Definire i campi obbligatori nell’interfaccia utente
description: Scopri come definire un campo XDM obbligatorio nell’interfaccia utente di Experience Platform.
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: 1d04bf56c51506f84c5156e6d2ed6c9f58f15235
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Definire i campi obbligatori nell’interfaccia utente

In Experience Data Model (XDM), un campo obbligatorio indica che è necessario fornire un valore valido affinché un particolare record o evento della serie temporale sia accettato durante l’inserimento dei dati. I casi d’uso comuni per i campi obbligatori includono informazioni sull’identità dell’utente e marche temporali.

Quando [definisci un nuovo campo](./overview.md#define) nell’interfaccia utente di Adobe Experience Platform, puoi impostarlo come campo obbligatorio selezionando la casella di controllo **[!UICONTROL Obbligatorio]** nella barra a destra. Selezionare **[!UICONTROL Applica]** per applicare la modifica allo schema.

![Casella di controllo obbligatoria](../../images/ui/fields/required/root.png)

Se il campo è un attributo a livello principale sotto l’oggetto ID tenant, il relativo percorso viene immediatamente visualizzato sotto **[!UICONTROL Campi obbligatori]** nella barra a sinistra.

![Campo obbligatorio a livello di radice](../../images/ui/fields/required/applied.png)

Se un campo obbligatorio è nidificato all’interno di un oggetto non contrassegnato come obbligatorio, tuttavia, il campo nidificato non viene visualizzato sotto **[!UICONTROL Campi obbligatori]** nella barra a sinistra.

Nell’esempio seguente, il campo `loyaltyId` è impostato come obbligatorio, ma l’oggetto principale `loyalty` non lo è. In questo caso, non si verificano errori di convalida se `loyalty` è stato escluso durante l’acquisizione dei dati, anche se il campo secondario `loyaltyId` è contrassegnato come obbligatorio. In altre parole, mentre `loyalty` è facoltativo, deve contenere un campo `loyaltyId` nell’evento in cui è incluso.

![Campo obbligatorio nidificato](../../images/ui/fields/required/nested.png)

Se si desidera che un campo nidificato sia sempre obbligatorio in uno schema, è inoltre necessario impostare tutti i campi principali come richiesto (ad eccezione dell’oggetto ID tenant).

![Campi obbligatori padre e figlio](../../images/ui/fields/required/parent-and-child.png)

## Passaggi successivi

Questa guida illustra come definire un campo obbligatorio nell’interfaccia utente di . Per informazioni su come definire altri tipi di campi XDM nell’ [!DNL Schema Editor], consulta la panoramica relativa alla [definizione dei campi nell’interfaccia utente](./overview.md#special) .
