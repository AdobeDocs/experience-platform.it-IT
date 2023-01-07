---
keywords: Experience Platform;home;argomenti popolari;api;API;XDM;sistema XDM;modello dati esperienza;modello dati;ui;workspace;obbligatorio;campo;
title: Definire i campi obbligatori nell’interfaccia utente
description: Scopri come definire un campo XDM obbligatorio nell’interfaccia utente di Experience Platform.
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: fe3d9a3fc473e7ca13f0e0c2f222bcc1b1a991c4
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# Definire i campi obbligatori nell’interfaccia utente

In Experience Data Model (XDM), un campo obbligatorio indica che è necessario fornire un valore valido affinché un particolare record o evento della serie temporale sia accettato durante l’inserimento dei dati. I casi d’uso comuni per i campi obbligatori includono informazioni sull’identità dell’utente e marche temporali.

>[!IMPORTANT]
>
>Indipendentemente dal fatto che un campo dello schema sia obbligatorio o meno, Platform non accetta `null` o valori vuoti per qualsiasi campo acquisito. Se in un record o in un evento non è presente alcun valore per un particolare campo, la chiave per tale campo deve essere esclusa dal payload di acquisizione.

Quando [definizione di un nuovo campo](./overview.md#define) nell’interfaccia utente di Adobe Experience Platform, puoi impostarla come campo obbligatorio selezionando la **[!UICONTROL Obbligatorio]** nella barra a destra. Seleziona **[!UICONTROL Applica]** per applicare la modifica allo schema.

![Casella di controllo obbligatoria](../../images/ui/fields/required/root.png)

Se il campo è un attributo di livello principale sotto l&#39;oggetto ID tenant, il relativo percorso viene immediatamente visualizzato sotto **[!UICONTROL Campi obbligatori]** nella barra a sinistra.

![Campo obbligatorio a livello di radice](../../images/ui/fields/required/applied.png)

Tuttavia, se un campo obbligatorio è nidificato all’interno di un oggetto non contrassegnato come obbligatorio, il campo nidificato non viene visualizzato sotto **[!UICONTROL Campi obbligatori]** nella barra a sinistra.

Nell’esempio seguente, la `internalSKU` il campo è impostato come obbligatorio, ma l&#39;oggetto principale è `SKUs` non lo è. In questo caso, se non si verificano errori di convalida `SKUs` viene escluso durante l’acquisizione dei dati, anche se il campo figlio `internalSKU` è contrassegnato come necessario. In altre parole, mentre `SKUs` è facoltativo e deve contenere un `internalSKU` nel caso in cui sia incluso.

![Campo obbligatorio nidificato](../../images/ui/fields/required/nested.png)

Se si desidera che un campo nidificato sia sempre obbligatorio in uno schema, è inoltre necessario impostare tutti i campi principali come richiesto (ad eccezione dell’oggetto ID tenant).

![Campi obbligatori padre e figlio](../../images/ui/fields/required/parent-and-child.png)

## Passaggi successivi

Questa guida illustra come definire un campo obbligatorio nell’interfaccia utente di . Vedi la panoramica su [definizione dei campi nell’interfaccia utente](./overview.md#special) per scoprire come definire altri tipi di campi XDM nel [!DNL Schema Editor].
