---
title: Configurare il Datastream per l'SDK Web di Experience Platform
description: 'Scopri come configurare i flussi di dati. '
keywords: configurazione;datastreams;datastreamId;edge;edge configuration id;Impostazioni ambiente;edgeConfigId;identità;sincronizzazione id abilitata;ID contenitore di sincronizzazione ID;Sandbox;ingresso streaming;set di dati evento;target;codice client;token di proprietà;ID ambiente di Target;destinazioni cookie;destinazioni URL;destinazioni;impostazioni Analytics Blockreport id suite;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---


# Configurazione di un Datastream

La configurazione per Adobe Experience Platform Web SDK è suddivisa tra due posizioni. Il [comando di configurazione](configuring-the-sdk.md) nell&#39;SDK controlla gli elementi che devono essere gestiti sul client, come il `edgeDomain`. I Datastreams gestiscono tutte le altre configurazioni per l&#39;SDK. Quando una richiesta viene inviata a Adobe Experience Platform Edge Network, viene utilizzato `edgeConfigId` per fare riferimento alla configurazione lato server. Questo consente di aggiornare la configurazione senza dover apportare modifiche al codice sul sito web.

Per questa funzione è necessario eseguire il provisioning della tua organizzazione. Contatta il tuo Customer Success Manager (CSM) per ricevere l&#39;inserire nell&#39;elenco Consentiti.

## Creazione di una configurazione del Datastream

I Datastreams possono essere creati nell&#39;Adobe [!DNL Experience Platform Launch] utilizzando lo strumento di configurazione Datastream.

![navigazione dello strumento datastreams](../../assets/datastreams_config.png)

>[!NOTE]
>
>Lo strumento di configurazione dei datastreams è disponibile per i clienti dell’elenco consentiti indipendentemente dal fatto che utilizzino [!DNL Experience Platform Launch] come gestore di tag. Inoltre, gli utenti devono disporre delle autorizzazioni di sviluppo in [!DNL Experience Platform Launch]. Per ulteriori informazioni, consulta l’articolo [Autorizzazioni utente](../../tags/ui/administration/user-permissions.md) nella documentazione [!DNL Experience Platform Launch] .

Crea un datastream facendo clic su **[!UICONTROL Nuovo Datastream]** nell&#39;area in alto a destra dello schermo. Dopo aver specificato un nome e una descrizione, viene richiesto di specificare le impostazioni predefinite per ogni ambiente. Le impostazioni disponibili sono descritte di seguito.

Durante la creazione di un datastream, vengono creati automaticamente tre ambienti con impostazioni identiche. Questi tre ambienti sono *dev*, *stage* e *prod*. Corrispondono ai tre ambienti predefiniti in [!DNL Experience Platform Launch]. Quando si crea una libreria [!DNL Experience Platform Launch] in un ambiente di sviluppo, la libreria utilizza automaticamente l&#39;ambiente di sviluppo dalla configurazione. È possibile modificare le impostazioni nei singoli ambienti nel modo desiderato.

L&#39;ID utilizzato nell&#39;SDK come `edgeConfigId` è un ID composito che specifica la configurazione e l&#39;ambiente (ad esempio, `1c86778b-cdba-4684-9903-750e52912ad1:stage`). Se nell’ID composito non è presente alcun ambiente (ad esempio, `stage` nell’esempio precedente), viene utilizzato l’ambiente di produzione.

Di seguito sono riportate le impostazioni disponibili per ogni ambiente di configurazione. La maggior parte delle sezioni può essere abilitata o disabilitata. Se disabilitata, le impostazioni vengono salvate ma non sono attive.

## [!UICONTROL Impostazioni ] IDS di terze parti

La sezione ID di terze parti è l’unica sezione sempre attiva. Sono disponibili due impostazioni: &quot;[!UICONTROL Sincronizzazione ID di terze parti abilitata]&quot; e &quot;[!UICONTROL ID contenitore di sincronizzazione ID di terze parti]&quot;.

![Sezione Identità dell’interfaccia utente di configurazione](../../assets/edge_configuration_identity.png)

### [!UICONTROL Sincronizzazione ID di terze parti abilitata]

Controlla se l&#39;SDK esegue o meno le sincronizzazioni di identità con partner di terze parti.

### [!UICONTROL ID di terze parti ID ID del contenitore di sincronizzazione ID]

Le sincronizzazioni ID possono essere raggruppate in contenitori per consentire l’esecuzione di sincronizzazioni ID diverse in momenti diversi. Questo controlla quale contenitore di sincronizzazioni ID viene eseguito per un determinato ID di configurazione.

## Impostazioni Adobe Experience Platform

Le impostazioni elencate qui consentono di inviare dati a Adobe Experience Platform. Abilita questa sezione solo se hai acquistato Adobe Experience Platform.

![Blocco delle impostazioni Adobe Experience Platform](../../assets/edge_configuration_aep.png)

### [!UICONTROL Sandbox]

Le sandbox sono posizioni in Adobe Experience Platform che consentono ai clienti di isolare i propri dati e implementazioni l’una dall’altra. Per ulteriori dettagli sul loro funzionamento, consulta la [documentazione sulle sandbox](../../sandboxes/home.md).

### [!UICONTROL Ingresso streaming]

Un ingresso in streaming è una sorgente HTTP in Adobe Experience Platform. Questi vengono creati nella scheda &quot;[!UICONTROL Origini]&quot; in Adobe Experience Platform come API HTTP.

### [!UICONTROL Set di dati evento]

I datastreams supportano l&#39;invio di dati a set di dati con uno schema di classe [!UICONTROL Experience Event].

## Impostazioni di Adobe Target

Per configurare Adobe Target, devi fornire un codice client. Gli altri campi sono facoltativi.

![Blocco delle impostazioni di Adobe Target](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>L&#39;organizzazione associata al codice cliente deve corrispondere all&#39;organizzazione in cui viene creato l&#39;ID di configurazione.

### [!UICONTROL Codice client]

ID univoco per un account di destinazione. Per trovarlo, puoi passare a [!UICONTROL Adobe Target] > [!UICONTROL Configurazione] [!UICONTROL Implementazione] > [!UICONTROL modifica impostazioni] accanto al pulsante [!UICONTROL scarica] per [!UICONTROL at.js] o [!UICONTROL  2/>mbox.js]

### [!UICONTROL Token di proprietà]

[!DNL Target] consente ai clienti di controllare le autorizzazioni tramite l’uso delle proprietà. I dettagli sono disponibili nella sezione [Autorizzazioni Enterprise](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) della documentazione [!DNL Target] .

Il token di proprietà si trova in [!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Properties]

### [!UICONTROL ID ambiente di destinazione]

[](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) Gli ambienti Adobe Target consentono di gestire la tua implementazione in tutte le fasi di sviluppo. Questa impostazione specifica l’ambiente da utilizzare con ogni ambiente.

Adobe consiglia di impostarlo in modo diverso per ciascuno degli ambienti `dev`, `stage` e `prod` datastream per semplificare le operazioni. Tuttavia, se hai già definito ambienti Adobe Target, puoi utilizzarli.

## Impostazioni Adobe Audience Manager

Per inviare dati a Adobe Audience Manager è sufficiente abilitare questa sezione. Le altre impostazioni sono facoltative ma incoraggiate.

![Adobe Blocco delle impostazioni di Gestione dell&#39;audience](../../assets/edge_configuration_aam.png)

### [!UICONTROL Destinazioni cookie abilitate]

Consente all&#39;SDK di condividere le informazioni sui segmenti tramite [Cookie Destinations](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) (Destinazioni cookie) da [!DNL Audience Manager].

### [!UICONTROL Destinazioni URL abilitate]

Consente all&#39;SDK di condividere le informazioni sui segmenti tramite [Destinazioni URL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Questi sono configurati in [!DNL Audience Manager].

## Impostazioni di Adobe Analytics

Controlla se i dati vengono inviati ad Adobe Analytics. Ulteriori dettagli sono disponibili in [Panoramica di Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Blocco impostazioni Adobe Analytics](../../assets/edge_configuration_aa.png)

### [!UICONTROL ID suite di rapporti]

La suite di rapporti si trova nella sezione Amministratore Adobe Analytics in [!UICONTROL Amministratore > Suite di rapporti]. Se sono specificate più suite di rapporti, i dati vengono copiati in ciascuna suite di rapporti.
