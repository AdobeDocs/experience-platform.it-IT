---
keywords: Experience Platform;home;argomenti popolari;guida utente sandbox;guida sandbox
solution: Experience Platform
title: Guida all’interfaccia utente Sandbox
description: In questo documento sono descritti i passaggi necessari per eseguire varie operazioni relative alle sandbox nell’interfaccia utente di Adobe Experience Platform.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 4%

---

# Guida all’interfaccia utente Sandbox

In questo documento sono descritti i passaggi necessari per eseguire varie operazioni relative alle sandbox nell’interfaccia utente di Adobe Experience Platform.

## Visualizza sandbox

Nell&#39;interfaccia utente di Experience Platform, selezionare **[!UICONTROL Sandboxes]** nel menu di navigazione a sinistra, quindi selezionare la scheda **[!UICONTROL Browse]** per aprire il dashboard [!UICONTROL Sandboxes]. Il dashboard elenca tutte le sandbox disponibili per la tua organizzazione, compresi i rispettivi tipi (produzione o sviluppo).

![Dashboard delle sandbox con la scheda Sfoglia selezionata che visualizza un elenco delle sandbox disponibili.](../images/ui/view-sandboxes.png)

## Passare da una sandbox all’altra

L’indicatore della sandbox si trova nell’intestazione superiore dell’interfaccia utente di Experience Platform e mostra il titolo, l’area e il tipo della sandbox in cui ti trovi attualmente.

![Dashboard delle sandbox con l&#39;indicatore della sandbox evidenziato.](../images/ui/sandbox-indicator.png)

Per passare da una sandbox all’altra, seleziona l’indicatore sandbox e quindi seleziona la sandbox desiderata dall’elenco a discesa. In alternativa, puoi cercare la sandbox desiderata utilizzando la funzione di ricerca nel menu a discesa.

![Viene visualizzato il menu a discesa dell&#39;indicatore della sandbox, che mostra un elenco di sandbox a cui hai accesso.](../images/ui/switcher-interface.png)

Una volta selezionata una sandbox, la schermata si aggiorna e si aggiorna alla sandbox selezionata.

![Dashboard della sandbox con l&#39;indicatore della sandbox modificato evidenziato.](../images/ui/sandbox-switched.png)

## Creare una nuova sandbox {#create}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxname"
>title="Nome sandbox"
>abstract="Il nome della sandbox è il testo utilizzato nel back-end per creare un ID univoco per questa sandbox."

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtitle"
>title="Titolo sandbox"
>abstract="Il titolo della sandbox è il nome visualizzato che rappresenta la sandbox nei menu e nei menu a discesa nell’interfaccia di Experience Platform."

>[!WARNING]
>
>Per creare una nuova sandbox è necessario aggiungerla a un ruolo in [[!UICONTROL Permissions]](../../access-control/abac/ui/permissions.md) prima di poter iniziare a utilizzarla. Per informazioni su come eseguire il provisioning di una sandbox per un ruolo, consulta la documentazione [gestione delle sandbox per un ruolo](../../access-control/abac/ui/permissions.md#managing-sandboxes-for-role).

Il video seguente offre una rapida panoramica sull’utilizzo delle Sandbox in Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/3430300/?captions=ita&quality=12&learn=on)

Per creare una nuova sandbox, seleziona **[!UICONTROL Create sandbox]** nell&#39;angolo in alto a destra dello schermo.

![create-sandbox](../images/ui/create-sandbox.png)

Verrà visualizzata la finestra di dialogo **[!UICONTROL Create sandbox]**. Seleziona il menu a discesa **[!UICONTROL Type]** e scegli il tipo di sandbox [!UICONTROL Development] o [!UICONTROL Production].

![Finestra di dialogo Crea sandbox con il selettore del tipo di sandbox evidenziato.](../images/ui/sandbox-type.png)

Dopo aver selezionato il tipo, fornisci un nome per la sandbox nel campo **[!UICONTROL Name]**. Il nome della sandbox è un identificatore tutto minuscolo da utilizzare nelle chiamate API e deve quindi essere univoco e conciso. Il nome della sandbox deve iniziare con una lettera, contenere un massimo di 256 caratteri e contenere solo caratteri alfanumerici e trattini (-). Quindi, fornisci un titolo per la sandbox nel campo **[!UICONTROL Title]**. Il titolo deve essere leggibile e sufficientemente descrittivo da essere facilmente identificabile.

Al termine, selezionare **[!UICONTROL Create]**.

![La finestra di dialogo Crea sandbox con i campi Nome e Titolo è stata compilata ed è stata evidenziata l&#39;opzione Crea.](../images/ui/sandbox-info.png)

Dopo aver completato la creazione della sandbox, aggiorna la pagina e la nuova sandbox viene visualizzata nel dashboard **[!UICONTROL Sandboxes]** con lo stato &quot;[!UICONTROL Creating]&quot;. Il provisioning di nuove sandbox richiede circa 30 secondi dal sistema, dopo di che il loro stato cambia in &quot;[!UICONTROL Active]&quot;.

![Dashboard delle sandbox con la sandbox appena creata evidenziata.](../images/ui/new-sandbox.png)

## Ripristinare una sandbox

>[!WARNING]
>
>Di seguito è riportato un elenco di eccezioni che possono impedire la reimpostazione della sandbox di produzione predefinita o di una sandbox di produzione creata dall&#39;utente:
>
>* Una sandbox di produzione creata dall’utente e utilizzata per la condivisione bidirezionale dei segmenti con Adobe Audience Manager o Audience Core Service può essere reimpostata dopo un messaggio di avviso.
>* Prima di avviare il ripristino di una sandbox, ti verrà richiesto di eliminare manualmente le composizioni per assicurarti che i dati del pubblico associato siano puliti correttamente.
>* Al termine del ripristino, l’ID della sandbox cambia.
>* Per [Journey Optimizer B2B edition](https://experienceleague.adobe.com/it/docs/journey-optimizer-b2b/user/guide-overview), il ripristino della sandbox **non è attualmente supportato**. Il ripristino o l’eliminazione di una sandbox mappata su Journey Optimizer B2B edition può causare la perdita permanente di dati in Journey Optimizer B2B edition e richiedere il provisioning di una nuova istanza di Journey Optimizer B2B edition.

### Eliminare le composizioni del pubblico

La composizione del pubblico non è attualmente integrata con la funzionalità di ripristino della sandbox, pertanto i tipi di pubblico dovranno essere eliminati manualmente prima di eseguire il ripristino della sandbox.

Selezionare **[!UICONTROL Audiences]** dalla sezione **[!UICONTROL Customers]** nel menu di navigazione a sinistra, quindi selezionare la scheda **[!UICONTROL Compositions]**.

![Dashboard dei tipi di pubblico con la scheda Composizioni selezionata ed evidenziata.](../images/ui/audiences.png)

Quindi, seleziona i puntini di sospensione (`...`) accanto al primo pubblico, quindi seleziona **[!UICONTROL Delete]**.

![Il menu del pubblico evidenzia l&#39;opzione [!UICONTROL Delete].](../images/ui/delete-composition.png)

Viene visualizzata una conferma dell&#39;eliminazione e si ritorna alla scheda **[!UICONTROL Compositions]**.

Ripeti i passaggi precedenti con tutte le tue composizioni. Questo eliminerà tutti i tipi di pubblico dall’inventario dei tipi di pubblico. Una volta rimossi tutti i tipi di pubblico, puoi continuare a reimpostare la sandbox.

### Reimpostazione di una sandbox

Se si ripristina una sandbox di produzione o di sviluppo, vengono eliminate anche tutte le risorse associate a tale sandbox (schemi, set di dati e così via), mantenendo il nome della sandbox e le autorizzazioni associate. Questa sandbox &quot;pulita&quot; continua a essere disponibile con lo stesso nome per gli utenti che vi hanno accesso.

Seleziona la sandbox da reimpostare dall’elenco delle sandbox. Nel pannello di navigazione a destra visualizzato, selezionare **[!UICONTROL Sandbox reset]**.

![Dashboard della sandbox con la sandbox selezionata ed evidenziata l&#39;opzione di ripristino sandbox.](../images/ui/reset.png)

Viene visualizzata una finestra di dialogo in cui viene richiesto di confermare la scelta. Selezionare **[!UICONTROL Continue]** per continuare.

![Viene visualizzata la finestra di dialogo di reimpostazione con l&#39;opzione Continua evidenziata.](../images/ui/reset-warning.png)

Nella finestra di conferma finale, immettere il nome della sandbox nella finestra di dialogo e selezionare **[!UICONTROL Reset]**.

![La finestra di dialogo di reimpostazione con il campo del nome di conferma e l&#39;opzione di reimpostazione evidenziata.](../images/ui/reset-confirm.png)

## Eliminare una sandbox

>[!WARNING]
>
>Non è possibile eliminare la sandbox di produzione predefinita. Tuttavia, qualsiasi sandbox di produzione creata dall&#39;utente e utilizzata per la condivisione bidirezionale dei segmenti con [!DNL Audience Manager] o [!DNL Audience Core Service] può essere eliminata dopo un messaggio di avviso.

L’eliminazione di una sandbox di produzione o di sviluppo comporta la rimozione definitiva di tutte le risorse associate a tale sandbox, incluse le autorizzazioni.

Seleziona la sandbox da eliminare dall’elenco delle sandbox. Nel pannello di navigazione a destra visualizzato, selezionare **[!UICONTROL Delete]**.

![Dashboard della sandbox con la sandbox selezionata e l&#39;opzione Elimina evidenziata.](../images/ui/delete.png)

Viene visualizzata una finestra di dialogo in cui viene richiesto di confermare la scelta. Selezionare **[!UICONTROL Continue]** per continuare.

![Viene visualizzata la finestra di dialogo Elimina con l&#39;opzione Continua evidenziata.](../images/ui/delete-warning.png)

Nella finestra di conferma finale, immettere il nome della sandbox nella finestra di dialogo e selezionare **[!UICONTROL Continue]**.

![La finestra di dialogo Elimina con il campo del nome di conferma e l&#39;opzione Continua è evidenziata.](../images/ui/delete-confirm.png)

## Passaggi successivi

Questo documento illustra come gestire le sandbox nell’interfaccia utente di Experience Platform. Ora che sai come gestire le sandbox, scopri come migliorare la precisione della configurazione tra le sandbox ed esportare e importare facilmente le configurazioni sandbox tra sandbox con la guida alla [funzione per gli strumenti sandbox](./sandbox-tooling.md).

Per informazioni su come gestire le sandbox utilizzando l&#39;API Sandbox, consulta la [guida per gli sviluppatori di sandbox](../api/getting-started.md).
