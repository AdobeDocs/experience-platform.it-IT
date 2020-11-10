---
keywords: Experience Platform;home;popular topics;sandbox user guide;sandbox guide
solution: Experience Platform
title: Guida utente sandbox
topic: user guide
description: In questo documento sono descritti i passaggi necessari per eseguire varie operazioni relative alle sandbox nell'interfaccia utente di Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 2d1a9699866bd39de7251731e9f0cd2f753a5083
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# Guida utente sandbox

In questo documento sono descritti i passaggi necessari per eseguire varie operazioni relative alle sandbox nell&#39;interfaccia utente di Adobe Experience Platform.

## Visualizzare le sandbox

Nell’interfaccia utente del Experience Platform , selezionate **[!UICONTROL Sandboxes]** nella navigazione a sinistra per aprire il **[!UICONTROL Sandboxes]** dashboard. Il dashboard elenca tutte le sandbox disponibili per l’organizzazione, incluso il tipo di sandbox (produzione o sviluppo) e lo stato (attivo, creazione, eliminazione o non riuscito).

![](../images/ui/view-sandboxes.png)

## Passaggio tra le sandbox

Il controllo **dello switcher** sandbox in alto a sinistra dello schermo visualizza la sandbox attualmente attiva.

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

Per creare una nuova sandbox nell’interfaccia utente, fate clic sul **[!UICONTROL Create Sandbox]** pulsante in alto a destra della schermata.

![](../images/ui/create-sandbox.png)

Viene **[!UICONTROL Create Sandbox]** visualizzata una finestra di dialogo che richiede di specificare un titolo e un nome da visualizzare per la sandbox. Il titolo **del** display deve essere leggibile dall&#39;uomo e deve essere sufficientemente descrittivo per essere facilmente identificabile. La sandbox **[!UICONTROL Name]** è un identificatore in lettere minuscole da usare nelle chiamate API e deve pertanto essere univoca e concisa. La sandbox **[!UICONTROL Name]** deve contenere solo caratteri alfanumerici e trattini **(-)**, deve iniziare con una lettera e può contenere al massimo 256 caratteri.

Al termine, selezionate **[!UICONTROL Create]**.

![](../images/ui/create-dialog.png)

>[!NOTE]
>
>Poiché vi limitate a creare solo tipi di sandbox non di produzione, l&#39; **[!UICONTROL type]** opzione è bloccata in &quot;Non produzione&quot; e non può essere manipolata.

Dopo aver creato la sandbox, aggiornate la pagina e la nuova sandbox appare nel **[!UICONTROL Sandboxes]** dashboard con lo stato &quot;[!UICONTROL Creating]&quot;. Il provisioning delle nuove sandbox richiede circa 15 minuti, dopo di che il loro stato cambia in &quot;[!UICONTROL Active]&quot;.

![](../images/ui/creating.png)

## Reimpostare una sandbox

>[!NOTE]
>
>Questa funzionalità è disponibile solo per sandbox non di produzione. Impossibile ripristinare le sandbox di produzione.

Reimpostando una sandbox non di produzione, vengono eliminate tutte le risorse associate a tale sandbox (schemi, set di dati e così via), mantenendo il nome della sandbox e le relative autorizzazioni. Questa sandbox &quot;pulita&quot; continua a essere disponibile con lo stesso nome per gli utenti che hanno accesso ad essa.

Per ripristinare una sandbox nell’interfaccia utente, selezionate **[!UICONTROL Sandboxes]** nella navigazione a sinistra, quindi selezionate la sandbox da reimpostare. Nella finestra di dialogo visualizzata sul lato destro dello schermo, selezionate **[!UICONTROL Reset Sandbox]**.

![](../images/ui/reset-sandbox.png)

Viene visualizzata una finestra di dialogo che richiede di confermare la scelta. Selezionare **[!UICONTROL Reset]** per continuare.

![](../images/ui/reset-confirm.png)

Viene visualizzato un messaggio di conferma e lo stato della sandbox diventa &quot;**[!UICONTROL Resetting]&quot;**. Una volta effettuato il provisioning dal sistema, il suo stato si aggiornerà su **&quot;[!UICONTROL Active]&quot;** o **&quot;[!UICONTROL Failed]&quot;**.

![](../images/ui/resetting.png)

## Eliminare una sandbox

>[!NOTE]
>
>Questa funzionalità è disponibile solo per sandbox non di produzione. Impossibile eliminare le sandbox di produzione.

Se eliminate una sandbox non di produzione, vengono rimosse in modo permanente tutte le risorse associate a tale sandbox, comprese le autorizzazioni.

Per eliminare una sandbox nell’interfaccia utente, selezionate **[!UICONTROL Sandboxes]** nella navigazione a sinistra, quindi selezionate la sandbox da eliminare. Nella finestra di dialogo visualizzata sul lato destro dello schermo, selezionate **[!UICONTROL Delete Sandbox]**.

![](../images/ui/delete-sandbox.png)

Viene visualizzata una finestra di dialogo che richiede di confermare la scelta. Selezionare **[!UICONTROL Delete]** per continuare.

![](../images/ui/delete-confirm.png)

Viene visualizzato un messaggio di conferma e la sandbox viene rimossa dall’ **[!UICONTROL Sandboxes]** area di lavoro.

## Passaggi successivi

Questo documento illustra come gestire le sandbox nell&#39;interfaccia utente del Experience Platform . Per informazioni su come gestire le sandbox tramite l&#39;API Sandbox, consultate la guida [per gli sviluppatori di](../api/getting-started.md)sandbox.