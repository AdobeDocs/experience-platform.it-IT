---
title: Guida introduttiva all’inoltro degli eventi
description: Segui questa esercitazione passo per passo per iniziare a utilizzare l’inoltro degli eventi in Adobe Experience Platform.
feature: Event Forwarding
exl-id: f82bfac9-dc2d-44de-a308-651300f107df
source-git-commit: 0a95d09eb1ce59e45d52372c4b08725c009001c3
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 74%

---

# Guida introduttiva all&#39;inoltro degli eventi

>[!NOTE]
>
>L’inoltro di eventi è una funzione a pagamento inclusa nelle offerte Adobe Real-time Customer Data Platform Connections, Prime o Ultimate.

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Per utilizzare Adobe Experience Platform, i dati devono essere inviati ad Adobe Experience Platform Edge Network utilizzando una o più delle tre opzioni seguenti:

* [Adobe Experience Platform Web SDK](../../extensions/client/web-sdk/overview.md)
* [Adobe Experience Platform Mobile SDK](https://sdkdocs.com)
* [API del server di rete Edge](/help/server-api/overview.md)

>[!NOTE]
>Platform Web SDK e Platform Mobile SDK non richiedono l’implementazione tramite tag in Adobe Experience Platform. Tuttavia, l’utilizzo di tag per distribuire questi SDK è l’approccio consigliato.

Dopo aver inviato i dati a Edge Network, è possibile attivare le soluzioni Adobe a cui inviare i dati. Per inviare dati a una soluzione non Adobe, impostala nell’inoltro degli eventi.

## Prerequisiti

* Adobe Real-Time CDP Connections, Prime o Ultimate (contatta il team del tuo account Adobe per informazioni sui prezzi)
* Inoltro di eventi in Adobe Experience Platform
* Adobe Experience Platform Web SDK, Mobile SDK o Edge Network Server API configurati per inviare dati ad Edge Network
* Mappare i dati su Experience Data Model (XDM) (la mappatura può essere eseguita utilizzando i tag)

## Creare uno schema XDM

Crea lo schema in Adobe Experience Platform.

1. Crea uno schema selezionando **[!UICONTROL Schemi]** > **[!UICONTROL Crea schemi]** e scegliendo l’opzione **[!UICONTROL XDM ExperienceEvent]**.

1. Assegna allo schema un nome e una breve descrizione.

1. Puoi aggiungere il gruppo di campi &quot;Dettagli Web ExperienceEvent&quot; selezionando **[!UICONTROL Aggiungi]** accanto a **[!UICONTROL Gruppi di campi]**.

   >[!NOTE]
   >
   >Se necessario, è possibile aggiungere più gruppi di campi.

1. Salva lo schema e prendi nota del nome che gli hai assegnato.

Per ulteriori informazioni sugli schemi, consulta la [guida del sistema Experience Data Model (XDM)](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=it).

## Creare una proprietà di inoltro degli eventi

Nell&#39;area di lavoro **[!UICONTROL Tag]** creare una proprietà di tipo **[!UICONTROL Edge]**.

1. Seleziona **[!UICONTROL Nuova proprietà]**.

1. Assegna un nome alla proprietà.

1. Scegli il tipo di piattaforma &quot;Edge&quot;.

1. Seleziona **[!UICONTROL Salva]**.

Dopo aver creato la proprietà, passa alla scheda **[!UICONTROL Ambienti]** per la nuova proprietà e annota
gli ID dell’ambiente. Se l&#39;organizzazione Adobe utilizzata nel flusso di dati è diversa dall&#39;organizzazione Adobe utilizzata nell&#39;inoltro degli eventi, è possibile copiare l&#39;ID ambiente dalla scheda **[!UICONTROL Ambienti]** e incollarlo durante la creazione di un flusso di dati. In alternativa, è possibile selezionare l’ambiente da un menu a discesa.

## Creare un flusso di dati

Per creare il flusso di dati in Adobe Experience Platform, utilizza l’ID ambiente generato quando hai creato la proprietà di inoltro degli eventi.

1. Seleziona **[!UICONTROL Flussi di dati]** nel menu di navigazione a sinistra.

1. Assegna un nome alla configurazione e fornisci una descrizione facoltativa.
La descrizione è utile per identificare le configurazioni, qualora ne siano elencate diverse.

1. Seleziona **[!UICONTROL Salva]**.

## Abilitare l’inoltro degli eventi

Quindi configura Edge Network per inviare i dati all’inoltro di eventi e ad altri prodotti Adobe.

1. Nell&#39;area di lavoro **[!UICONTROL Datastreams]** selezionare la proprietà creata.

1. Seleziona l&#39;ambiente di sviluppo, di produzione oppure di gestione temporanea.

   In alternativa, per inviare i dati a un ambiente di inoltro degli eventi che si trova all’esterno dell’organizzazione Adobe, seleziona **[!UICONTROL Passa a modalità avanzata]** e incolla un ID. L’ID viene fornito quando crei una proprietà di inoltro degli eventi.

1. Attiva gli strumenti necessari e configura le opzioni in base alle tue esigenze.

   * Adobe Analytics richiede un ID della suite di rapporti.

   * L&#39;inoltro degli eventi in Adobe Experience Platform richiede un ID di proprietà e un ID ambiente. Si tratta del percorso di pubblicazione per la proprietà di inoltro degli eventi.

Dopo la configurazione, annota gli ID ambiente per la nuova proprietà.

## Configura l’estensione Platform Web SDK per inviare dati allo stream di dati creato in precedenza

Crea la tua proprietà nell&#39;area di lavoro **[!UICONTROL Tag]**, quindi passa a **[!UICONTROL Estensioni]** e seleziona l&#39;estensione Experience Platform Web SDK dal catalogo per configurarla e installarla.

Per informazioni dettagliate sulle opzioni di configurazione, consulta la [documentazione dell&#39;estensione Web SDK](../../extensions/client/web-sdk/overview.md).

## Creare una regola di tag per inviare dati all’SDK per web di Platform

Dopo aver eseguito le operazioni descritte qui sopra, puoi creare tutti gli elementi che sfruttano sia l’inoltro degli eventi che i tag ma che richiedono una sola richiesta dalla pagina, come le definizioni di dati, le regole e così via.

Crea una regola di caricamento della pagina utilizzando l’estensione Platform Web SDK e il tipo di azione &quot;Invia evento&quot;:

1. Apri la scheda **[!UICONTROL Regole]**, quindi seleziona **[!UICONTROL Crea nuova regola]**.

1. Denomina la regola.

1. Seleziona **[!UICONTROL Eventi Aggiungi]**.

1. Aggiungi un evento scegliendo un&#39;estensione e uno dei tipi di evento disponibili per tale estensione, quindi configura le impostazioni dell&#39;evento. Ad esempio, seleziona **[!UICONTROL Core - Window Loaded]**.

1. Aggiungi un&#39;azione utilizzando l&#39;estensione Platform SDK Web. Seleziona **[!UICONTROL Invia evento]** dall&#39;elenco **[!UICONTROL Tipo di azione]**, scegli l’istanza desiderata (istanza di Alloy già configurata in precedenza), quindi seleziona un elemento dati da aggiungere al blocco dati XDM all’interno del riscontro di Alloy.

1. Lascia le altre impostazioni predefinite per questo esempio, quindi seleziona **[!UICONTROL Salva]**.

Per un altro esempio, potresti creare una regola che invia il livello dati a Edge se l&#39;utente passa il mouse su un pulsante specifico.

## Riepilogo

Dopo aver eseguito quanto segue, sarà possibile creare delle regole di inoltro degli eventi per inoltrare i dati a destinazioni non Adobe.

* Schema Experience Data Model (prendi nota del nome che gli hai assegnato).
* Una proprietà di inoltro degli eventi (prendi nota dell’ID proprietà e degli ID ambiente)
* Un flusso di dati (prendi nota dell’ID ambiente, da non confondere con l’ID ambiente dall’inoltro degli eventi)
* Una proprietà tag
