---
keywords: Experience Platform ;home;argomenti comuni;guida utente sandbox;guida sandbox
solution: Experience Platform
title: Guida all'interfaccia utente sandbox
topic: user guide
description: In questo documento sono descritti i passaggi necessari per eseguire varie operazioni relative alle sandbox nell'interfaccia utente di Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 0%

---


# Guida all&#39;interfaccia utente sandbox

In questo documento sono descritti i passaggi necessari per eseguire varie operazioni relative alle sandbox nell&#39;interfaccia utente di Adobe Experience Platform.

## Visualizzare le sandbox

Nell&#39;interfaccia utente del Experience Platform , selezionare **[!UICONTROL Sandboxes]** nella navigazione a sinistra per aprire il dashboard **[!UICONTROL Sandboxes]**. Il dashboard elenca tutte le sandbox disponibili per l’organizzazione, incluso il tipo di sandbox (produzione o sviluppo) e lo stato (attivo, creazione, eliminazione o non riuscito).

![](../images/ui/view-sandboxes.png)

## Passaggio tra le sandbox

Il controllo **sandbox switcher** in alto a sinistra dello schermo visualizza la sandbox attualmente attiva.

![](../images/ui/sandbox-switcher.png)

Per passare da una sandbox all’altra, selezionate lo switcher sandbox e selezionate la sandbox desiderata dall’elenco a discesa.

![](../images/ui/switcher-menu.png)

Dopo aver selezionato una sandbox, la schermata si aggiorna con la sandbox selezionata ora disponibile nello switcher della sandbox.

![](../images/ui/switched.png)

## Cerca una sandbox

Potete scorrere l&#39;elenco delle sandbox disponibili utilizzando la funzione di ricerca dal menu del commutatore di sandbox. Digitate il nome della sandbox a cui desiderate accedere per filtrare tutte le sandbox disponibili per la vostra organizzazione.

![](../images/ui/sandbox-search.png)

## Creare una nuova sandbox

Usate il seguente video per una panoramica rapida sull’utilizzo delle sandbox in  Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Per creare una nuova sandbox nell&#39;interfaccia utente, fate clic sul pulsante **[!UICONTROL Create Sandbox]** in alto a destra nella schermata.

![](../images/ui/create-sandbox.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Create Sandbox]** in cui si richiede di specificare un titolo e un nome da visualizzare per la sandbox. Il **display title** è concepito per essere leggibile dall&#39;uomo e deve essere sufficientemente descrittivo per essere facilmente identificabile. La sandbox **[!UICONTROL Name]** è un identificatore in lettere minuscole da utilizzare nelle chiamate API e deve pertanto essere univoca e concisa. La sandbox **[!UICONTROL Name]** deve essere composta solo da caratteri alfanumerici e trattini **(-)**, deve iniziare con una lettera e può contenere al massimo 256 caratteri.

Al termine, selezionare **[!UICONTROL Create]**.

![](../images/ui/create-dialog.png)

>[!NOTE]
>
>Poiché siete limitati alla creazione di tipi di sandbox non di produzione, l&#39;opzione **[!UICONTROL type]** è bloccata in &quot;Non produzione&quot; e non può essere manipolata.

Dopo aver creato la sandbox, aggiornate la pagina e la nuova sandbox appare nel dashboard **[!UICONTROL Sandboxes]** con lo stato &quot;[!UICONTROL Creating]&quot;. Il provisioning delle nuove sandbox richiede circa 15 minuti dal sistema, dopo di che il loro stato cambia in &quot;[!UICONTROL Active]&quot;.

![](../images/ui/creating.png)

## Reimpostare una sandbox

>[!NOTE]
>
>Questa funzionalità è disponibile solo per sandbox non di produzione. Impossibile ripristinare le sandbox di produzione.

Reimpostando una sandbox non di produzione, vengono eliminate tutte le risorse associate a tale sandbox (schemi, set di dati e così via), mantenendo il nome della sandbox e le relative autorizzazioni. Questa sandbox &quot;pulita&quot; continua a essere disponibile con lo stesso nome per gli utenti che hanno accesso ad essa.

Per ripristinare una sandbox nell&#39;interfaccia utente, selezionate **[!UICONTROL Sandboxes]** nella navigazione a sinistra, quindi selezionate la sandbox da reimpostare. Nella finestra di dialogo visualizzata sul lato destro dello schermo, selezionare **[!UICONTROL Reset Sandbox]**.

![](../images/ui/reset-sandbox.png)

Viene visualizzata una finestra di dialogo che richiede di confermare la scelta. Selezionare **[!UICONTROL Reset]** per continuare.

![](../images/ui/reset-confirm.png)

Viene visualizzato un messaggio di conferma e lo stato della sandbox diventa &quot;**[!UICONTROL Resetting]&quot;**. Una volta effettuato il provisioning dal sistema, il relativo stato verrà aggiornato a **&quot;[!UICONTROL Active]&quot;** o **&quot;[!UICONTROL Failed]&quot;**.

![](../images/ui/resetting.png)

## Eliminare una sandbox

>[!NOTE]
>
>Questa funzionalità è disponibile solo per sandbox non di produzione. Impossibile eliminare le sandbox di produzione.

Se eliminate una sandbox non di produzione, vengono rimosse in modo permanente tutte le risorse associate a tale sandbox, comprese le autorizzazioni.

Per eliminare una sandbox nell&#39;interfaccia utente, selezionate **[!UICONTROL Sandboxes]** nella barra di navigazione a sinistra, quindi selezionate la sandbox da eliminare. Nella finestra di dialogo visualizzata sul lato destro dello schermo, selezionare **[!UICONTROL Delete Sandbox]**.

![](../images/ui/delete-sandbox.png)

Viene visualizzata una finestra di dialogo che richiede di confermare la scelta. Selezionare **[!UICONTROL Delete]** per continuare.

![](../images/ui/delete-confirm.png)

Viene visualizzato un messaggio di conferma e la sandbox viene rimossa dall&#39;area di lavoro **[!UICONTROL Sandboxes]**.

## Passaggi successivi

Questo documento illustra come gestire le sandbox nell&#39;interfaccia utente del Experience Platform . Per informazioni su come gestire le sandbox tramite l&#39;API Sandbox, consultate la guida per gli sviluppatori [sandbox](../api/getting-started.md).