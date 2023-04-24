---
keywords: Experience Platform;home;argomenti popolari;guida utente sandbox;guida sandbox
solution: Experience Platform
title: Guida all’interfaccia utente sandbox
description: Questo documento fornisce passaggi su come eseguire varie operazioni relative alle sandbox nell’interfaccia utente di Adobe Experience Platform.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 8%

---

# Guida all’interfaccia utente sandbox

Questo documento fornisce passaggi su come eseguire varie operazioni relative alle sandbox nell’interfaccia utente di Adobe Experience Platform.

## Visualizzare le sandbox

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sandbox]** nella navigazione a sinistra e seleziona **[!UICONTROL Sfoglia]** per aprire [!UICONTROL Sandbox] dashboard. Il dashboard elenca tutte le sandbox disponibili per la tua organizzazione, inclusi i rispettivi tipi (produzione o sviluppo).

![sandbox di visualizzazione](../images/ui/view-sandboxes.png)

## Passa da una sandbox all’altra

L’indicatore della sandbox si trova nell’intestazione superiore dell’interfaccia utente di Platform e visualizza il titolo della sandbox in uso, la sua area geografica e il relativo tipo.

![indicatore sandbox](../images/ui/sandbox-indicator.png)

Per passare da una sandbox all’altra, seleziona l’indicatore della sandbox e seleziona la sandbox desiderata dall’elenco a discesa.

![interfaccia commutatore](../images/ui/switcher-interface.png)

Una volta selezionata una sandbox, la schermata si aggiorna e si aggiorna alla sandbox selezionata.

![a commutazione di sandbox](../images/ui/sandbox-switched.png)

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
>Quando crei una nuova sandbox, devi prima aggiungerla al tuo profilo di prodotto in [Adobe Admin Console](https://adminconsole.adobe.com/) prima di iniziare a utilizzare la nuova sandbox. Consulta la documentazione su [gestione delle autorizzazioni per un profilo di prodotto](../../access-control/ui/permissions.md) per informazioni su come eseguire il provisioning di una sandbox a un profilo di prodotto.

Utilizza il seguente video per una rapida panoramica sull’utilizzo delle sandbox in Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Per creare una nuova sandbox, seleziona **[!UICONTROL Creare una sandbox]** nell’angolo in alto a destra dello schermo.

![create-sandbox](../images/ui/create-sandbox.png)

La **[!UICONTROL Creare una sandbox]** viene visualizzata la finestra di dialogo. Se stai creando una sandbox di sviluppo, seleziona **[!UICONTROL Sviluppo]** nel pannello a discesa . Per creare una nuova sandbox di produzione, seleziona **[!UICONTROL Produzione]**.

![tipo sandbox](../images/ui/sandbox-type.png)

Dopo aver selezionato il tipo, fornisci alla sandbox un nome e un titolo. Il titolo deve essere leggibile dall’uomo e deve essere sufficientemente descrittivo da essere facilmente identificabile. Il nome della sandbox è un identificatore in minuscolo da utilizzare nelle chiamate API e dovrebbe pertanto essere univoco e conciso. Il nome della sandbox deve iniziare con una lettera, contenere un massimo di 256 caratteri e contenere solo caratteri alfanumerici e trattini (-).

Al termine, seleziona **[!UICONTROL Crea]**.

![sandbox-info](../images/ui/sandbox-info.png)

Una volta completata la creazione della sandbox, aggiorna la pagina e la nuova sandbox viene visualizzata nella **[!UICONTROL Sandbox]** dashboard con stato &quot;[!UICONTROL Creazione]&quot;. Il provisioning delle nuove sandbox richiede circa 30 secondi dal sistema, dopodiché il loro stato cambia in &quot;[!UICONTROL Attivo]&quot;.

![nuovo sandbox](../images/ui/new-sandbox.png)

## Reimpostare una sandbox

>[!WARNING]
>
>Di seguito è riportato un elenco di eccezioni che possono impedire il ripristino della sandbox di produzione predefinita o di una sandbox di produzione creata dall’utente: <ul><li>Non è possibile ripristinare la sandbox di produzione predefinita se il grafico delle identità ospitato nella sandbox viene utilizzato anche da Adobe Analytics per la [Analisi multidispositivo (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=it) funzionalità.</li><li>Non è possibile ripristinare la sandbox di produzione predefinita se il grafico delle identità ospitato nella sandbox viene utilizzato anche da Adobe Audience Manager per la [Destinazioni basate su persone (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=it).</li><li>La sandbox di produzione predefinita non può essere reimpostata se contiene dati per le funzioni CDA e PBD.</li><li>Una sandbox di produzione creata dall’utente e utilizzata per la condivisione di segmenti bidirezionali con Adobe Audience Manager o con il servizio di base Audience può essere reimpostata dopo un messaggio di avviso.</li></ul>

Se si reimposta una sandbox di produzione o sviluppo, vengono eliminate tutte le risorse associate a tale sandbox (schemi, set di dati e così via), mantenendo il nome della sandbox e le relative autorizzazioni. Questa sandbox &quot;pulita&quot; continua a essere disponibile con lo stesso nome per gli utenti che vi hanno accesso.

Seleziona la sandbox da reimpostare dall’elenco delle sandbox. Nel pannello di navigazione a destra visualizzato, seleziona **[!UICONTROL Ripristino della sandbox]**.

![reset](../images/ui/reset.png)

Viene visualizzata una finestra di dialogo che richiede di confermare la scelta. Seleziona **[!UICONTROL Continua]** per procedere.

![avviso di reset](../images/ui/reset-warning.png)

Nella finestra di conferma finale, immetti il nome della sandbox nella finestra di dialogo e seleziona **[!UICONTROL Reimposta]**.

![reset-confirm](../images/ui/reset-confirm.png)

## Eliminare una sandbox

>[!WARNING]
>
>Non è possibile eliminare la sandbox di produzione predefinita. Tuttavia, qualsiasi sandbox di produzione creata dall’utente utilizzato per la condivisione di segmenti bidirezionale con [!DNL Audience Manager] o [!DNL Audience Core Service] può essere eliminato dopo un messaggio di avviso.

L’eliminazione di una sandbox di produzione o di sviluppo comporta la rimozione definitiva di tutte le risorse associate a tale sandbox, comprese le autorizzazioni.

Seleziona la sandbox da eliminare dall’elenco delle sandbox. Nel pannello di navigazione a destra visualizzato, seleziona **[!UICONTROL Elimina]**.

![delete](../images/ui/delete.png)

Viene visualizzata una finestra di dialogo che richiede di confermare la scelta. Seleziona **[!UICONTROL Continua]** per procedere.

![avviso di cancellazione](../images/ui/delete-warning.png)

Nella finestra di conferma finale, immetti il nome della sandbox nella finestra di dialogo e seleziona  **[!UICONTROL Continua]**.

![delete-confirm](../images/ui/delete-confirm.png)

## Passaggi successivi

Questo documento illustra come gestire le sandbox all’interno dell’interfaccia utente di Experience Platform. Per informazioni su come gestire le sandbox utilizzando l’API Sandbox, consulta la sezione [guida per sviluppatori di sandbox](../api/getting-started.md).
