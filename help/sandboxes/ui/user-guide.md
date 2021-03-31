---
keywords: Experience Platform;home;argomenti popolari;guida utente sandbox;guida sandbox
solution: Experience Platform
title: Guida all’interfaccia utente sandbox
topic: Guida utente
description: Questo documento fornisce passaggi su come eseguire varie operazioni relative alle sandbox nell’interfaccia utente di Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: ee2fb54ba59f22a1ace56a6afd78277baba5271e
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---


# Guida all’interfaccia utente sandbox

Questo documento fornisce passaggi su come eseguire varie operazioni relative alle sandbox nell’interfaccia utente di Adobe Experience Platform.

## Visualizzare le sandbox

Nell’interfaccia utente di Experience Platform, seleziona **[!UICONTROL Sandboxes]** nel menu di navigazione a sinistra per aprire il dashboard **[!UICONTROL Sandboxes]**. Il dashboard elenca tutte le sandbox disponibili per la tua organizzazione, inclusi il tipo di sandbox (produzione o sviluppo) e lo stato (attivo, creazione, eliminato o non riuscito).

![](../images/ui/view-sandboxes.png)

## Passa da una sandbox all’altra

Il controllo **commutatore sandbox** in alto a sinistra dello schermo visualizza la sandbox attualmente attiva.

![](../images/ui/sandbox-switcher.png)

Per passare da una sandbox all’altra, seleziona il commutatore sandbox e seleziona la sandbox desiderata dall’elenco a discesa.

![](../images/ui/switcher-menu.png)

Una volta selezionata una sandbox, la schermata si aggiorna con la sandbox selezionata ora presente nel commutatore sandbox.

![](../images/ui/switched.png)

## Cercare una sandbox

Puoi navigare nell’elenco delle sandbox disponibili utilizzando la funzione di ricerca dal menu del commutatore sandbox. Digita il nome della sandbox a cui desideri accedere per filtrare tutte le sandbox disponibili per la tua organizzazione.

![](../images/ui/sandbox-search.png)

## Creare una nuova sandbox

>[!NOTE]
>
>La funzione Sandbox di produzione multipla è in versione beta.

Utilizza il seguente video per una rapida panoramica sull’utilizzo delle sandbox in Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Per creare una nuova sandbox, seleziona il pulsante **[!UICONTROL Create Sandbox]** in alto a destra nella schermata .

![](../images/ui/create-sandbox.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Create Sandbox]** in cui viene richiesto di specificare un tipo, un titolo e un nome per la sandbox. Se stai creando una sandbox di sviluppo, seleziona **[!UICONTROL Development]** nel pannello a discesa che viene visualizzato. Se stai creando una sandbox di produzione, seleziona **[!UICONTROL Production]**.

Il titolo deve essere leggibile dall’uomo e deve essere sufficientemente descrittivo da essere facilmente identificabile. Il nome della sandbox è un identificatore in minuscolo da utilizzare nelle chiamate API e dovrebbe pertanto essere univoco e conciso. Il nome della sandbox deve essere composto solo da caratteri alfanumerici e trattini (`-`), deve iniziare con una lettera e deve contenere un massimo di 256 caratteri.

Al termine, seleziona **[!UICONTROL Create]**.

![](../images/ui/create-dialog.png)

Una volta completata la creazione della sandbox, aggiorna la pagina e la nuova sandbox viene visualizzata nel dashboard **[!UICONTROL Sandboxes]** con lo stato &quot;[!UICONTROL Creating]&quot;. Il provisioning delle nuove sandbox richiede circa 15 minuti dal sistema, dopodiché il loro stato cambia in &quot;[!UICONTROL Active]&quot;.

## Reimpostare una sandbox

>[!NOTE]
>
>Puoi ripristinare qualsiasi sandbox di produzione o sviluppo nell’organizzazione, eccetto la sandbox di produzione predefinita.

Se si reimposta una sandbox di produzione o sviluppo, vengono eliminate tutte le risorse associate a tale sandbox (schemi, set di dati e così via), mantenendo il nome della sandbox e le relative autorizzazioni. Questa sandbox &quot;pulita&quot; continua a essere disponibile con lo stesso nome per gli utenti che vi hanno accesso.

Seleziona la sandbox da reimpostare dall’elenco delle sandbox. Nel pannello di navigazione a destra visualizzato, seleziona **[!UICONTROL Sandbox reset]**.

![](../images/ui/reset-sandbox.png)

Viene visualizzata una finestra di dialogo che richiede di confermare la scelta. Selezionare **[!UICONTROL Continue]** per continuare.

![](../images/ui/reset-confirm.png)

Nella finestra di conferma finale, immetti il nome della sandbox nella finestra di dialogo e seleziona **[!UICONTROL Reset]**

![](../images/ui/reset-final-confirm.png)

## Eliminare una sandbox

>[!NOTE]
>
>È possibile eliminare qualsiasi sandbox di produzione o di sviluppo nell’organizzazione, ad eccezione della sandbox di produzione predefinita.

L’eliminazione di una sandbox di produzione o di sviluppo comporta la rimozione definitiva di tutte le risorse associate a tale sandbox, comprese le autorizzazioni.

Seleziona la sandbox da eliminare dall’elenco delle sandbox. Nel pannello di navigazione a destra visualizzato, seleziona **[!UICONTROL Delete]**.

![](../images/ui/delete-sandbox.png)

Viene visualizzata una finestra di dialogo che richiede di confermare la scelta. Selezionare **[!UICONTROL Continue]** per continuare.

![](../images/ui/delete-confirm.png)

Nella finestra di conferma finale, immetti il nome della sandbox nella finestra di dialogo e seleziona **[!UICONTROL Delete]**

![](../images/ui/delete-final-confirm.png)

## Passaggi successivi

Questo documento illustra come gestire le sandbox all’interno dell’interfaccia utente di Experience Platform. Per informazioni su come gestire le sandbox utilizzando l’API Sandbox, consulta la [guida per gli sviluppatori di sandbox](../api/getting-started.md).