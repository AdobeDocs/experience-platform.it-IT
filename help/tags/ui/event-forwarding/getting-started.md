---
title: Guida introduttiva all’inoltro degli eventi
description: Segui questa esercitazione passo per passo per iniziare a utilizzare l’inoltro degli eventi in Adobe Experience Platform.
feature: Event Forwarding
exl-id: f82bfac9-dc2d-44de-a308-651300f107df
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 67%

---

# Guida introduttiva all&#39;inoltro degli eventi

>[!NOTE]
>
>L’inoltro di eventi è una funzione a pagamento inclusa nelle offerte Adobe Real-Time Customer Data Platform Connections, Prime o Ultimate.

Per utilizzare Adobe Experience Platform, i dati devono essere inviati ad Adobe Experience Platform Edge Network utilizzando una o più delle tre opzioni seguenti:

* [Adobe Experience Platform Web SDK](../../extensions/client/web-sdk/overview.md)
* [Adobe Experience Platform Mobile SDK](https://sdkdocs.com)
* [API Edge Network](https://developer.adobe.com/data-collection-apis/docs/)

>[!NOTE]
>Experience Platform Web SDK e Experience Platform Mobile SDK non richiedono la distribuzione tramite tag in Adobe Experience Platform. Tuttavia, l’utilizzo di tag per distribuire questi SDK è l’approccio consigliato.

Dopo aver inviato i dati a Edge Network, è possibile attivare le soluzioni Adobe a cui inviare i dati. Per inviare dati a una soluzione non Adobe, impostala nell’inoltro degli eventi.

## Prerequisiti

* Connessioni Adobe Real-Time CDP, Prime o Ultimate (contatta il team del tuo account Adobe per informazioni sui prezzi)
* Inoltro di eventi in Adobe Experience Platform
* API Adobe Experience Platform Web SDK, Mobile SDK o Edge Network configurate per l’invio di dati ad Edge Network
* Mappare i dati su Experience Data Model (XDM) (la mappatura può essere eseguita utilizzando i tag)

## Creare uno schema XDM

Crea lo schema in Adobe Experience Platform.

1. Per creare un nuovo schema, seleziona **[!UICONTROL Schemas]** > **[!UICONTROL Create Schema]** e scegli l’opzione **[!UICONTROL XDM ExperienceEvent]**.

1. Assegna allo schema un nome e una breve descrizione.

1. È possibile aggiungere il gruppo di campi &quot;Dettagli Web ExperienceEvent&quot; selezionando **[!UICONTROL Add]** accanto a **[!UICONTROL Field Groups]**.

   >[!NOTE]
   >
   >Se necessario, è possibile aggiungere più gruppi di campi.

1. Salva lo schema e prendi nota del nome che gli hai assegnato.

Per ulteriori informazioni sugli schemi, consulta la [guida del sistema Experience Data Model (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=it).

## Creare una proprietà di inoltro degli eventi

Nell&#39;area di lavoro **[!UICONTROL Tags]** creare una proprietà di tipo **[!UICONTROL Edge]**.

1. Seleziona **[!UICONTROL New Property]**.

1. Assegna un nome alla proprietà.

1. Scegli il tipo di piattaforma &quot;Edge&quot;.

1. Seleziona **[!UICONTROL Save]**.

Dopo aver creato la proprietà, passa alla scheda **[!UICONTROL Environments]** per la nuova proprietà e annota
gli ID dell’ambiente. Se l&#39;organizzazione Adobe utilizzata nel flusso di dati è diversa dall&#39;organizzazione Adobe utilizzata nell&#39;inoltro degli eventi, è possibile copiare l&#39;ID ambiente dalla scheda **[!UICONTROL Environments]** e incollarlo durante la creazione di un flusso di dati. In alternativa, è possibile selezionare l’ambiente da un menu a discesa.

## Creare un flusso di dati

Per creare il flusso di dati in Adobe Experience Platform, utilizza l’ID ambiente generato quando hai creato la proprietà di inoltro degli eventi.

1. Selezionare **[!UICONTROL Datastreams]** nel menu di navigazione a sinistra.

1. Assegna un nome alla configurazione e fornisci una descrizione facoltativa.
La descrizione è utile per identificare le configurazioni, qualora ne siano elencate diverse.

1. Seleziona **[!UICONTROL Save]**.

## Abilitare l’inoltro degli eventi {#enable-event-forwarding}

Quindi configura Edge Network per inviare i dati all’inoltro di eventi e ad altri prodotti Adobe.

1. Nell&#39;area di lavoro **[!UICONTROL Datastreams]** selezionare la proprietà creata.

1. Seleziona l&#39;ambiente di sviluppo, di produzione oppure di gestione temporanea.

   In alternativa, per inviare i dati a un ambiente di inoltro degli eventi che si trova all&#39;esterno dell&#39;organizzazione Adobe, selezionare **[!UICONTROL Switch to Advanced Mode]** e incollare un ID. L’ID viene fornito quando crei una proprietà di inoltro degli eventi.

1. Attiva gli strumenti necessari e configura le opzioni in base alle tue esigenze.

   * Adobe Analytics richiede un ID della suite di rapporti.

   * L&#39;inoltro degli eventi in Adobe Experience Platform richiede un ID di proprietà e un ID ambiente. Si tratta del percorso di pubblicazione per la proprietà di inoltro degli eventi.

Dopo la configurazione, annota gli ID ambiente per la nuova proprietà.

## Configura l’estensione Experience Platform Web SDK per inviare dati allo stream di dati creato in precedenza

Crea la proprietà nell&#39;area di lavoro **[!UICONTROL Tags]**, quindi passa a **[!UICONTROL Extensions]** e seleziona l&#39;estensione Experience Platform Web SDK dal catalogo per configurarla e installarla.

Per informazioni dettagliate sulle opzioni di configurazione, consulta la [documentazione dell&#39;estensione Web SDK](../../extensions/client/web-sdk/overview.md).

## Creare una regola di tag per inviare dati ad Experience Platform Web SDK

Dopo aver eseguito le operazioni descritte qui sopra, puoi creare tutti gli elementi che sfruttano sia l’inoltro degli eventi che i tag ma che richiedono una sola richiesta dalla pagina, come le definizioni di dati, le regole e così via.

Crea una regola di caricamento della pagina utilizzando l’estensione Experience Platform Web SDK e il tipo di azione &quot;Invia evento&quot;:

1. Apri la scheda **[!UICONTROL Rules]**, quindi seleziona **[!UICONTROL Create New Rule]**.

1. Denomina la regola.

1. Seleziona **[!UICONTROL Events Add]**.

1. Aggiungi un evento scegliendo un&#39;estensione e uno dei tipi di evento disponibili per tale estensione, quindi configura le impostazioni dell&#39;evento. Ad esempio, seleziona **[!UICONTROL Core - Window Loaded]**.

1. Aggiungi un’azione utilizzando l’estensione Experience Platform Web SDK. Seleziona **[!UICONTROL Send Event]** dall&#39;elenco **[!UICONTROL Action Type]**, scegli l&#39;istanza desiderata (istanza di Alloy già configurata in precedenza), quindi seleziona un elemento dati da aggiungere al blocco dati XDM all&#39;interno del riscontro di Alloy.

1. Lascia le altre impostazioni predefinite per questo esempio, quindi seleziona **[!UICONTROL Save]**.

Per un altro esempio, potresti creare una regola che invia il livello dati a Edge se l’utente passa il puntatore su un pulsante specifico.

## Riepilogo

Dopo aver eseguito quanto segue, sarà possibile creare delle regole di inoltro degli eventi per inoltrare i dati a destinazioni non Adobe.

* Schema Experience Data Model (prendi nota del nome che gli hai assegnato).
* Una proprietà di inoltro degli eventi (prendi nota dell’ID proprietà e degli ID ambiente)
* Un flusso di dati (prendi nota dell’ID ambiente, da non confondere con l’ID ambiente dall’inoltro degli eventi)
* Una proprietà tag
