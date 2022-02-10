---
title: Configurare il Datastream per l'SDK Web di Experience Platform
description: 'Scopri come configurare i flussi di dati. '
keywords: configurazione;datastreams;datastreamId;edge;datastream id;Impostazioni ambiente;edgeConfigId;identità;sincronizzazione id abilitata;ID contenitore di sincronizzazione ID;Sandbox;ingresso streaming;set di dati evento;target;codice client;token di proprietà;ID ambiente di Target;destinazioni cookie;destinazioni url;impostazioni Analytics Blockreport id suite;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 012ebbadc7149747df1414360eca6451836d6bbc
workflow-type: tm+mt
source-wordcount: '1090'
ht-degree: 1%

---


# Configurare un datastream

La configurazione per Adobe Experience Platform Web SDK è suddivisa tra due posizioni. La [configura, comando](configuring-the-sdk.md) nell’SDK controlla gli elementi che devono essere gestiti sul client, come il `edgeDomain`. I Datastreams gestiscono tutte le altre configurazioni per l&#39;SDK. Quando viene inviata una richiesta a Adobe Experience Platform Edge Network, la `edgeConfigId` viene utilizzato per fare riferimento alla configurazione lato server. Questo consente di aggiornare la configurazione senza dover apportare modifiche al codice sul sito web.

Per questa funzione è necessario eseguire il provisioning della tua organizzazione. Contatta il tuo Customer Success Manager (CSM) per ricevere l&#39;inserire nell&#39;elenco Consentiti.

## Creare una configurazione del datastream

Puoi creare e gestire i datastreams nell’interfaccia utente Raccolta dati selezionando **[!UICONTROL Datastreams]** nella navigazione a sinistra.

![navigazione dello strumento datastreams](../images/datastreams/config.png)

>[!NOTE]
>
>Mentre puoi accedere al [!UICONTROL Datastreams] indipendentemente dal fatto che si utilizzino le funzionalità di gestione tag di Platform, è necessario disporre delle autorizzazioni per gli sviluppatori per gestire direttamente i datastreams. Consulta la sezione [autorizzazioni utente](../../tags/ui/administration/user-permissions.md) per ulteriori informazioni, consulta la documentazione sui tag .

Crea un datastream facendo clic su **[!UICONTROL Nuovo Datastream]** nell’area in alto a destra dello schermo. Dopo aver specificato un nome e una descrizione, viene richiesto di specificare le impostazioni predefinite per ogni ambiente. Le impostazioni disponibili sono descritte di seguito.

Durante la creazione di un datastream, vengono creati automaticamente tre ambienti con impostazioni identiche. Questi tre ambienti sono *dev*, *stadio* e *prod*. Corrispondono ai tre ambienti predefiniti per i tag. Quando crei una libreria di tag in un ambiente di sviluppo, la libreria utilizza automaticamente l&#39;ambiente di sviluppo dalla configurazione. È possibile modificare le impostazioni nei singoli ambienti nel modo desiderato.

L&#39;ID utilizzato nell&#39;SDK come `edgeConfigId` è un ID composito che specifica la configurazione e l’ambiente (ad esempio, `1c86778b-cdba-4684-9903-750e52912ad1:stage`). Se nell&#39;ID composito non è presente alcun ambiente (ad esempio, `stage` nell’esempio precedente), viene utilizzato l’ambiente di produzione.

Di seguito sono riportate le impostazioni disponibili per ogni ambiente di configurazione. La maggior parte delle sezioni può essere abilitata o disabilitata. Se disabilitata, le impostazioni vengono salvate ma non sono attive.

## [!UICONTROL ID di terze parti] impostazioni

La sezione ID di terze parti è l’unica sezione sempre attiva. Sono disponibili due impostazioni: &quot;[!UICONTROL Sincronizzazione ID di terze parti abilitata]&quot; e &quot;[!UICONTROL ID di terze parti ID ID del contenitore di sincronizzazione ID]&quot;.

![Sezione Identità dell’interfaccia utente di configurazione](../images/datastreams/edge_configuration_identity.png)

### [!UICONTROL Sincronizzazione ID di terze parti abilitata]

Controlla se l&#39;SDK esegue o meno le sincronizzazioni di identità con partner di terze parti.

### [!UICONTROL ID di terze parti ID ID del contenitore di sincronizzazione ID]

Le sincronizzazioni ID possono essere raggruppate in contenitori per consentire l’esecuzione di sincronizzazioni ID diverse in momenti diversi. Questo controlla quale contenitore di sincronizzazioni ID viene eseguito per un determinato ID di configurazione.

## Impostazioni Adobe Experience Platform

Le impostazioni elencate qui consentono di inviare dati a Adobe Experience Platform. Abilita questa sezione solo se hai acquistato Adobe Experience Platform.

![Blocco delle impostazioni Adobe Experience Platform](../images/datastreams/platform-config.png)

| Campo | Descrizione |
| --- | --- |
| [!UICONTROL Sandbox] | **(Obbligatorio)** Seleziona la sandbox Platform a cui desideri inviare i dati. Le sandbox sono partizioni virtuali in Adobe Experience Platform che ti consentono di isolare i dati e le implementazioni da altre parti della tua organizzazione.<br><br>Una volta creato un datastream, la relativa sandbox non può essere modificata. La [!UICONTROL Sandbox] il campo di selezione non è pertanto disponibile quando si modifica un datastream esistente.<br><br>Per ulteriori dettagli sul ruolo delle sandbox in Experience Platform, consulta la sezione [documentazione sandbox](../../sandboxes/home.md). |
| [!UICONTROL Set di dati evento] | **(Obbligatorio)** Seleziona il set di dati della piattaforma a cui verranno inviati i dati evento cliente. Questo schema deve utilizzare [Classe ExperienceEvent XDM](../../xdm/classes/experienceevent.md). |
| [!UICONTROL Set di dati del profilo] | Seleziona il set di dati della piattaforma a cui verranno inviati i dati degli attributi del cliente. Questo schema deve utilizzare [Classe di profilo individuale XDM](../../xdm/classes/individual-profile.md). |
| [!UICONTROL Offer Decisioning] | Seleziona questa casella di controllo per abilitare l’Offer decisioning per un’implementazione Platform Web SDK. Consulta la guida su [utilizzo di Offer Decisioning con Platform Web SDK](../personalization/offer-decisioning/offer-decisioning-overview.md) per ulteriori dettagli sull’implementazione. Per ulteriori informazioni sulle funzionalità di Offer Decisioning, consulta la [Documentazione di Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=it). |
| [!UICONTROL Segmentazione Edge] | Seleziona questa casella di controllo per abilitare [segmentazione dei bordi](../../segmentation/ui/edge-segmentation.md) per questo datastream. Quando l’SDK per web di Platform invia i dati tramite un datastream abilitato per la segmentazione edge, nella risposta vengono restituite tutte le appartenenze al segmento aggiornate per il profilo in questione.<br><br>Questa opzione può essere utilizzata in combinazione con [!UICONTROL Destinazioni personalizzazione] per [casi d’uso per la personalizzazione di pagine successive](../../destinations/ui/configure-personalization-destinations.md). |
| [!UICONTROL Destinazioni personalizzazione] | Se utilizzato in combinazione con il [!UICONTROL Segmentazione Edge] questa opzione consente al datastream di connettersi a motori di personalizzazione come Adobe Target. Fai riferimento alla documentazione sulle destinazioni per i passaggi specifici su [configurazione delle destinazioni di personalizzazione](../../destinations/ui/configure-personalization-destinations.md). |

## Impostazioni di Adobe Target

Per configurare Adobe Target, devi fornire un codice client. Gli altri campi sono facoltativi.

![Blocco delle impostazioni di Adobe Target](../images/datastreams/edge_configuration_target.png)

>[!NOTE]
>
>L&#39;organizzazione associata al codice cliente deve corrispondere all&#39;organizzazione in cui viene creato l&#39;ID di configurazione.

### [!UICONTROL Codice client]

ID univoco per un account di destinazione. Per trovare questo, puoi passare a [!UICONTROL Adobe Target] > [!UICONTROL Configurazione]> [!UICONTROL Implementazione] > [!UICONTROL modificare le impostazioni] accanto al [!UICONTROL scaricare] pulsante per [!UICONTROL at.js] o [!UICONTROL mbox.js]

### [!UICONTROL Token di proprietà]

[!DNL Target] consente ai clienti di controllare le autorizzazioni tramite l’uso delle proprietà. I dettagli sono disponibili nella sezione [Autorizzazioni Enterprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) della sezione [!DNL Target] documentazione.

Il token di proprietà si trova in [!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Proprietà]

### [!UICONTROL ID ambiente di destinazione]

[Ambienti](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) in Adobe Target puoi gestire la tua implementazione in tutte le fasi di sviluppo. Questa impostazione specifica l’ambiente da utilizzare con ogni ambiente.

Adobe consiglia di impostarlo in modo diverso per ogni `dev`, `stage`e `prod` ambienti datastream per semplificare le operazioni. Tuttavia, se hai già definito ambienti Adobe Target, puoi utilizzarli.

## Impostazioni Adobe Audience Manager

Per inviare dati a Adobe Audience Manager è sufficiente abilitare questa sezione. Le altre impostazioni sono facoltative ma incoraggiate.

![Adobe Blocco delle impostazioni di Gestione dell&#39;audience](../images/datastreams/edge_configuration_aam.png)

### [!UICONTROL Destinazioni cookie abilitate]

Consente all’SDK di condividere le informazioni sui segmenti tramite [Destinazioni cookie](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) da [!DNL Audience Manager].

### [!UICONTROL Destinazioni URL abilitate]

Consente all’SDK di condividere le informazioni sui segmenti tramite [Destinazioni URL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Sono configurati in [!DNL Audience Manager].

## Impostazioni di Adobe Analytics

Controlla se i dati vengono inviati ad Adobe Analytics. Ulteriori dettagli sono disponibili nella sezione [Panoramica di Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Blocco impostazioni Adobe Analytics](../images/datastreams/edge_configuration_aa.png)

### [!UICONTROL ID suite di rapporti]

La suite di rapporti si trova nella sezione Adobe Analytics Admin in [!UICONTROL Amministratore > Suite di rapporti]. Se sono specificate più suite di rapporti, i dati vengono copiati in ciascuna suite di rapporti.
