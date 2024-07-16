---
keywords: Experience Platform;home;argomenti popolari;guida utente sandbox;guida sandbox
solution: Experience Platform
title: Guida all’interfaccia utente Sandbox
description: In questo documento sono descritti i passaggi necessari per eseguire varie operazioni relative alle sandbox nell’interfaccia utente di Adobe Experience Platform.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: 0db23e475d6546ebb886a56d5915d023ea215125
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 5%

---

# Guida all’interfaccia utente Sandbox

In questo documento sono descritti i passaggi necessari per eseguire varie operazioni relative alle sandbox nell’interfaccia utente di Adobe Experience Platform.

## Visualizza sandbox

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Sandbox]** nell&#39;area di navigazione a sinistra, quindi seleziona **[!UICONTROL Sfoglia]** per aprire il dashboard [!UICONTROL Sandbox]. Il dashboard elenca tutte le sandbox disponibili per la tua organizzazione, compresi i rispettivi tipi (produzione o sviluppo).

![view-sandboxes](../images/ui/view-sandboxes.png)

## Passare da una sandbox all’altra

L’indicatore della sandbox si trova nell’intestazione superiore dell’interfaccia utente di Platform e mostra il titolo, l’area e il tipo della sandbox in cui ti trovi attualmente.

![indicatore-sandbox](../images/ui/sandbox-indicator.png)

Per passare da una sandbox all’altra, seleziona l’indicatore sandbox e seleziona la sandbox desiderata dall’elenco a discesa.

![interfaccia-commutatore](../images/ui/switcher-interface.png)

Una volta selezionata una sandbox, la schermata si aggiorna e si aggiorna alla sandbox selezionata.

![sandbox-switched](../images/ui/sandbox-switched.png)

## Creare una nuova sandbox {#create}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxname"
>title="Nome sandbox"
>abstract="Il nome della sandbox è il testo utilizzato nel back-end per creare un ID univoco per questa sandbox."

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtitle"
>title="Titolo sandbox"
>abstract="Il titolo della sandbox è il nome visualizzato che rappresenta la sandbox nei menu e nei menu a discesa nell’interfaccia di Experience Platform."

>[!NOTE]
>
>Per creare una nuova sandbox è necessario aggiungerla a un ruolo in [[!UICONTROL Autorizzazioni]](../../access-control/abac/ui/permissions.md) prima di poter iniziare a utilizzarla. Per informazioni su come eseguire il provisioning di una sandbox per un ruolo, consulta la documentazione [gestione delle sandbox per un ruolo](../../access-control/abac/ui/permissions.md#managing-sandboxes-for-role).

Il video seguente offre una rapida panoramica sull’utilizzo delle Sandbox in Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Per creare una nuova sandbox, seleziona **[!UICONTROL Crea sandbox]** nell&#39;angolo in alto a destra dello schermo.

![create-sandbox](../images/ui/create-sandbox.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Crea sandbox]**. Se stai creando una sandbox di sviluppo, seleziona **[!UICONTROL Sviluppo]** nel pannello a discesa. Per creare una nuova sandbox di produzione, seleziona **[!UICONTROL Produzione]**.

![tipo-sandbox](../images/ui/sandbox-type.png)

Dopo aver selezionato il tipo, assegna alla sandbox un nome e un titolo. Il titolo deve essere leggibile e sufficientemente descrittivo da essere facilmente identificabile. Il nome della sandbox è un identificatore tutto minuscolo da utilizzare nelle chiamate API e deve quindi essere univoco e conciso. Il nome della sandbox deve iniziare con una lettera, contenere un massimo di 256 caratteri e contenere solo caratteri alfanumerici e trattini (-).

Al termine, selezionare **[!UICONTROL Crea]**.

![informazioni-sandbox](../images/ui/sandbox-info.png)

Dopo aver completato la creazione della sandbox, aggiorna la pagina e la nuova sandbox viene visualizzata nel dashboard **[!UICONTROL Sandbox]** con lo stato &quot;[!UICONTROL Creazione]&quot;. Il provisioning di nuove sandbox richiede circa 30 secondi dal sistema, dopo di che il loro stato cambia in &quot;[!UICONTROL Attivo]&quot;.

![new-sandbox](../images/ui/new-sandbox.png)

## Ripristinare una sandbox

>[!WARNING]
>
>Di seguito è riportato un elenco di eccezioni che possono impedire la reimpostazione della sandbox di produzione predefinita o di una sandbox di produzione creata dall&#39;utente:
>* Non è possibile reimpostare la sandbox di produzione predefinita se il grafo delle identità ospitato nella sandbox è utilizzato anche da Adobe Analytics per la funzione [Cross Device Analytics (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=it).
>* Non è possibile reimpostare la sandbox di produzione predefinita se il grafo delle identità ospitato nella sandbox è utilizzato anche da Adobe Audience Manager per le [Destinazioni basate sulle persone (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=it).
>* Non è possibile ripristinare la sandbox di produzione predefinita se contiene dati per entrambe le funzioni CDA e PBD.
>* Una sandbox di produzione creata dall’utente e utilizzata per la condivisione bidirezionale dei segmenti con Adobe Audience Manager o Audience Core Service può essere reimpostata dopo un messaggio di avviso.
>* Prima di avviare il ripristino di una sandbox, ti verrà richiesto di eliminare manualmente le composizioni per assicurarti che i dati del pubblico associato siano puliti correttamente.

### Eliminare le composizioni del pubblico

La composizione del pubblico non è attualmente integrata con la funzionalità di ripristino della sandbox, pertanto i tipi di pubblico dovranno essere eliminati manualmente prima di eseguire il ripristino della sandbox.

Seleziona **[!UICONTROL Tipi di pubblico]** dal menu di navigazione a sinistra, quindi seleziona **[!UICONTROL Composizioni]**.

![Scheda [!UICONTROL Composizioni] nell&#39;area di lavoro [!UICONTROL Tipi di pubblico].](../images/ui/audiences.png)

Quindi, seleziona i puntini di sospensione (`...`) accanto al primo pubblico, quindi seleziona **[!UICONTROL Elimina]**.

![Il menu del pubblico evidenzia l&#39;opzione [!UICONTROL Elimina].](../images/ui/delete-composition.png)

Viene visualizzata una conferma dell&#39;eliminazione e viene visualizzata di nuovo la scheda **[!UICONTROL Composizioni]**.

Ripeti i passaggi precedenti con tutte le tue composizioni. Questo eliminerà tutti i tipi di pubblico dall’inventario dei tipi di pubblico. Una volta rimossi tutti i tipi di pubblico, puoi continuare a reimpostare la sandbox.

### Reimpostazione di una sandbox

Se si ripristina una sandbox di produzione o di sviluppo, vengono eliminate anche tutte le risorse associate a tale sandbox (schemi, set di dati e così via), mantenendo il nome della sandbox e le autorizzazioni associate. Questa sandbox &quot;pulita&quot; continua a essere disponibile con lo stesso nome per gli utenti che vi hanno accesso.

Seleziona la sandbox da reimpostare dall’elenco delle sandbox. Nel pannello di navigazione a destra visualizzato, seleziona **[!UICONTROL Ripristino sandbox]**.

![reimposta](../images/ui/reset.png)

Viene visualizzata una finestra di dialogo in cui viene richiesto di confermare la scelta. Seleziona **[!UICONTROL Continua]** per continuare.

![reset-warning](../images/ui/reset-warning.png)

Nella finestra di conferma finale, immetti il nome della sandbox nella finestra di dialogo e seleziona **[!UICONTROL Reimposta]**.

![ripristina-conferma](../images/ui/reset-confirm.png)

## Eliminare una sandbox

>[!WARNING]
>
>Non è possibile eliminare la sandbox di produzione predefinita. Tuttavia, qualsiasi sandbox di produzione creata dall&#39;utente e utilizzata per la condivisione bidirezionale dei segmenti con [!DNL Audience Manager] o [!DNL Audience Core Service] può essere eliminata dopo un messaggio di avviso.

L’eliminazione di una sandbox di produzione o di sviluppo comporta la rimozione definitiva di tutte le risorse associate a tale sandbox, incluse le autorizzazioni.

Seleziona la sandbox da eliminare dall’elenco delle sandbox. Nel pannello di navigazione a destra visualizzato, seleziona **[!UICONTROL Elimina]**.

![elimina](../images/ui/delete.png)

Viene visualizzata una finestra di dialogo in cui viene richiesto di confermare la scelta. Seleziona **[!UICONTROL Continua]** per continuare.

![elimina-avvertenza](../images/ui/delete-warning.png)

Nella finestra di conferma finale, immetti il nome della sandbox nella finestra di dialogo e seleziona **[!UICONTROL Continua]**.

![elimina-conferma](../images/ui/delete-confirm.png)

## Passaggi successivi

Questo documento illustra come gestire le sandbox nell’interfaccia utente di Experience Platform. Per informazioni su come gestire le sandbox utilizzando l&#39;API Sandbox, consulta la [guida per gli sviluppatori di sandbox](../api/getting-started.md).
