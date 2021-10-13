---
keywords: Experience Platform;home;argomenti popolari;guida utente sandbox;guida sandbox
solution: Experience Platform
title: Guida all’interfaccia utente sandbox
topic-legacy: user guide
description: Questo documento fornisce passaggi su come eseguire varie operazioni relative alle sandbox nell’interfaccia utente di Adobe Experience Platform.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: a43dd851a5c7ec722e792a0f43d1bb42777f0c15
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 1%

---

# Guida all’interfaccia utente sandbox

Questo documento fornisce passaggi su come eseguire varie operazioni relative alle sandbox nell’interfaccia utente di Adobe Experience Platform.

## Visualizzare le sandbox

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sandbox]** nel menu di navigazione a sinistra per aprire il dashboard [!UICONTROL Sandbox]. Il dashboard elenca tutte le sandbox disponibili per la tua organizzazione, inclusi il tipo di sandbox (produzione o sviluppo) e lo stato (attivo, creazione, eliminato o non riuscito).

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
>Quando crei una nuova sandbox, devi prima aggiungerla al tuo profilo di prodotto in [Adobe Admin Console](https://adminconsole.adobe.com/) prima di poter iniziare a utilizzare la nuova sandbox. Consulta la documentazione su [gestione delle autorizzazioni per un profilo di prodotto](../../access-control/ui/permissions.md) per informazioni su come eseguire il provisioning di una sandbox a un profilo di prodotto.

Utilizza il seguente video per una rapida panoramica sull’utilizzo delle sandbox in Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Per creare una nuova sandbox, seleziona **[!UICONTROL Crea sandbox]** nell’angolo in alto a destra dello schermo.

![creare](../images/ui/create.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Crea sandbox]** . Se stai creando una sandbox di sviluppo, seleziona **[!UICONTROL Sviluppo]** nel pannello a discesa . Per creare una nuova sandbox di produzione, seleziona **[!UICONTROL Produzione]**.

![type](../images/ui/type.png)

Dopo aver selezionato il tipo, fornisci alla sandbox un nome e un titolo. Il titolo deve essere leggibile dall’uomo e deve essere sufficientemente descrittivo da essere facilmente identificabile. Il nome della sandbox è un identificatore in minuscolo da utilizzare nelle chiamate API e dovrebbe pertanto essere univoco e conciso. Il nome della sandbox deve iniziare con una lettera, contenere un massimo di 256 caratteri e contenere solo caratteri alfanumerici e trattini (-).

Al termine, seleziona **[!UICONTROL Crea]**.

![info](../images/ui/info.png)

Dopo aver completato la creazione della sandbox, aggiorna la pagina e la nuova sandbox viene visualizzata nel dashboard **[!UICONTROL Sandbox]** con lo stato &quot;[!UICONTROL Creazione]&quot;. Il provisioning delle nuove sandbox richiede circa 30 secondi dal sistema, dopodiché il loro stato cambia in &quot;[!UICONTROL Attivo]&quot;.

## Reimpostare una sandbox

>[!IMPORTANT]
>
>Non è possibile ripristinare la sandbox di produzione predefinita se il grafico di identità ospitato al suo interno viene utilizzato anche da Adobe Analytics per la funzione [Cross Device Analytics (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=it) o se il grafico di identità ospitato al suo interno viene utilizzato anche da Adobe Audience Manager per la funzione [People Based Destinations (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html) .

Se si reimposta una sandbox di produzione o sviluppo, vengono eliminate tutte le risorse associate a tale sandbox (schemi, set di dati e così via), mantenendo il nome della sandbox e le relative autorizzazioni. Questa sandbox &quot;pulita&quot; continua a essere disponibile con lo stesso nome per gli utenti che vi hanno accesso.

Seleziona la sandbox da reimpostare dall’elenco delle sandbox. Nel pannello di navigazione a destra visualizzato, seleziona **[!UICONTROL Ripristino sandbox]**.

![reset](../images/ui/reset.png)

Viene visualizzata una finestra di dialogo che richiede di confermare la scelta. Selezionare **[!UICONTROL Continua]** per continuare.

![avviso di reset](../images/ui/reset-warning.png)

Nella finestra di conferma finale, immetti il nome della sandbox nella finestra di dialogo e seleziona **[!UICONTROL Ripristina]**

![reset-confirm](../images/ui/reset-confirm.png)

Dopo alcuni istanti, nella parte inferiore dello schermo viene visualizzata una casella di conferma per confermare il corretto ripristino.

![success](../images/ui/success.png)

### Avvisi

Una sandbox di produzione predefinita contenente dati CDA non può essere reimpostata e restituisce il seguente avviso.

![cda](../images/ui/cda.png)

Anche una sandbox di produzione predefinita contenente dati PBD non può essere reimpostata e restituisce il seguente avviso.

![pbd](../images/ui/pbd.png)

Anche una sandbox di produzione predefinita che contiene dati sia per CDA che per PBD non può essere reimpostata e restituisce il seguente avviso.

![entrambi](../images/ui/both.png)

Puoi ripristinare una sandbox di produzione utilizzata per la condivisione di segmenti bidirezionale con [!DNL Audience Manager] o [!DNL Audience Core Service]. Seleziona [!UICONTROL Continua] per procedere con la reimpostazione.

![entrambi](../images/ui/seg.png)

## Eliminare una sandbox

>[!IMPORTANT]
>
>Impossibile eliminare la sandbox di produzione predefinita.

L’eliminazione di una sandbox di produzione o di sviluppo comporta la rimozione definitiva di tutte le risorse associate a tale sandbox, comprese le autorizzazioni.

Seleziona la sandbox da eliminare dall’elenco delle sandbox. Nel pannello di navigazione a destra visualizzato, seleziona **[!UICONTROL Elimina]**.

![delete](../images/ui/delete.png)

Viene visualizzata una finestra di dialogo che richiede di confermare la scelta. Selezionare **[!UICONTROL Continua]** per continuare.

![avviso di cancellazione](../images/ui/delete-warning.png)

Nella finestra di conferma finale, immetti il nome della sandbox nella finestra di dialogo e seleziona **[!UICONTROL Continua]**

![delete-confirm](../images/ui/delete-confirm.png)

Una sandbox di produzione creata dall’utente utilizzata per la condivisione di segmenti bidirezionali con [!DNL Audience Manager] o [!DNL Audience Core Service] può ancora essere eliminata dopo il seguente avviso.

![cucire](../images/ui/delete-seg.png)

## Passaggi successivi

Questo documento illustra come gestire le sandbox all’interno dell’interfaccia utente di Experience Platform. Per informazioni su come gestire le sandbox utilizzando l’API Sandbox, consulta la [guida per gli sviluppatori di sandbox](../api/getting-started.md).
