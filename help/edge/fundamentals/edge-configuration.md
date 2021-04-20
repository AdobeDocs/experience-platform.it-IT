---
title: Creare una configurazione Edge per Experience Platform Web SDK
description: 'Scopri come configurare Experience Platform Edge Network. '
keywords: configurazione;edge;id configurazione edge;Impostazioni ambiente;edgeConfigId;identità;sincronizzazione id abilitata;ID contenitore sincronizzazione ID;Sandbox;ingresso streaming;set di dati evento;target;codice client;token proprietà;ID ambiente di Target;destinazioni cookie;destinazioni url;destinazioni;impostazioni di Analytics Blockreport id suite;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
translation-type: tm+mt
source-git-commit: d4ed6c8fa9c86eb2beec829ab24c381b665c2f03
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 1%

---

# Creare una configurazione edge

La configurazione per Adobe Experience Platform Web SDK è suddivisa tra due posizioni. Il [comando di configurazione](configuring-the-sdk.md) nell&#39;SDK controlla gli elementi che devono essere gestiti sul client, come il `edgeDomain`. La configurazione perimetrale gestisce tutte le altre configurazioni dell’SDK. Quando una richiesta viene inviata a Adobe Experience Platform Edge Network, viene utilizzato `edgeConfigId` per fare riferimento alla configurazione lato server. Questo consente di aggiornare la configurazione senza dover apportare modifiche al codice sul sito web.

Per questa funzione è necessario eseguire il provisioning della tua organizzazione. Contatta il tuo Customer Success Manager (CSM) per ricevere l&#39;inserire nell&#39;elenco Consentiti.

## Creazione di una configurazione Edge

Le configurazioni dei bordi possono essere create in Adobe [!DNL Experience Platform Launch] utilizzando lo strumento di configurazione dei bordi.

![navigazione dello strumento di configurazione del bordo](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>Lo strumento di configurazione edge è disponibile per i clienti dell’elenco consentiti indipendentemente dal fatto che utilizzino [!DNL Experience Platform Launch] come gestore di tag. Inoltre, gli utenti devono disporre delle autorizzazioni di sviluppo in [!DNL Experience Platform Launch]. Per ulteriori informazioni, consulta l’articolo [Autorizzazioni utente](https://docs.adobe.com/content/help/it-IT/launch/using/reference/admin/user-permissions.html) nella documentazione [!DNL Experience Platform Launch] .

Crea una configurazione del bordo facendo clic su **[!UICONTROL New Edge Configuration]** nell’area in alto a destra dello schermo. Dopo aver specificato un nome e una descrizione, viene richiesto di specificare le impostazioni predefinite per ogni ambiente. Le impostazioni disponibili sono descritte di seguito.

Durante la creazione di una configurazione perimetrale, vengono creati automaticamente tre ambienti con impostazioni identiche. Questi tre ambienti sono *dev*, *stage* e *prod*. Corrispondono ai tre ambienti predefiniti in [!DNL Experience Platform Launch]. Quando si crea una libreria [!DNL Experience Platform Launch] in un ambiente di sviluppo, la libreria utilizza automaticamente l&#39;ambiente di sviluppo dalla configurazione. È possibile modificare le impostazioni nei singoli ambienti nel modo desiderato.

L&#39;ID utilizzato nell&#39;SDK come `edgeConfigId` è un ID composito che specifica la configurazione e l&#39;ambiente (ad esempio, `1c86778b-cdba-4684-9903-750e52912ad1:stage`). Se nell’ID composito non è presente alcun ambiente (ad esempio, `stage` nell’esempio precedente), viene utilizzato l’ambiente di produzione.

Di seguito sono riportate le impostazioni disponibili per ogni ambiente di configurazione. La maggior parte delle sezioni può essere abilitata o disabilitata. Se disabilitata, le impostazioni vengono salvate ma non sono attive.

## [!UICONTROL Third Party ID] Impostazioni

La sezione ID di terze parti è l’unica sezione sempre attiva. Sono disponibili due impostazioni: &quot;[!UICONTROL Third Party ID Sync Enabled]&quot; e &quot;[!UICONTROL Third Party ID Sync Container ID]&quot;.

![Sezione Identità dell’interfaccia utente di configurazione](../../assets/edge_configuration_identity.png)

### [!UICONTROL Third Party ID Sync Enabled]

Controlla se l&#39;SDK esegue o meno le sincronizzazioni di identità con partner di terze parti.

### [!UICONTROL Third Party ID Sync Container ID]

Le sincronizzazioni ID possono essere raggruppate in contenitori per consentire l’esecuzione di sincronizzazioni ID diverse in momenti diversi. Questo controlla quale contenitore di sincronizzazioni ID viene eseguito per un determinato ID di configurazione.

## Impostazioni Adobe Experience Platform

Le impostazioni elencate qui consentono di inviare dati a Adobe Experience Platform. Abilita questa sezione solo se hai acquistato Adobe Experience Platform.

![Blocco delle impostazioni Adobe Experience Platform](../../assets/edge_configuration_aep.png)

### [!UICONTROL Sandbox]

Le sandbox sono posizioni in Adobe Experience Platform che consentono ai clienti di isolare i propri dati e implementazioni l’una dall’altra. Per ulteriori dettagli sul loro funzionamento, consulta la [documentazione sulle sandbox](../../sandboxes/home.md).

### [!UICONTROL Streaming Inlet]

Un ingresso in streaming è una sorgente HTTP in Adobe Experience Platform. Questi vengono creati nella scheda &quot;[!UICONTROL Sources]&quot; in Adobe Experience Platform come API HTTP.

### [!UICONTROL Event Dataset]

Le configurazioni di Edge supportano l’invio di dati a set di dati con uno schema di classe [!UICONTROL Experience Event].

## Impostazioni di Adobe Target

Per configurare Adobe Target, devi fornire un codice client. Gli altri campi sono facoltativi.

![Blocco delle impostazioni di Adobe Target](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>L&#39;organizzazione associata al codice cliente deve corrispondere all&#39;organizzazione in cui viene creato l&#39;ID di configurazione.

### [!UICONTROL Client Code]

ID univoco per un account di destinazione. Per trovarlo, puoi passare a [!UICONTROL Adobe Target] > [!UICONTROL Setup] [!UICONTROL Implementation] > [!UICONTROL edit settings] accanto al pulsante [!UICONTROL download] per [!UICONTROL at.js] o [!UICONTROL mbox.js]

### [!UICONTROL Property Token]

[!DNL Target] consente ai clienti di controllare le autorizzazioni tramite l’uso delle proprietà. I dettagli sono disponibili nella sezione [Autorizzazioni Enterprise](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html) della documentazione [!DNL Target] .

Il token di proprietà si trova in [!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Properties]

### [!UICONTROL Target Environment ID]

[](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) Gli ambienti Adobe Target consentono di gestire la tua implementazione in tutte le fasi di sviluppo. Questa impostazione specifica l’ambiente da utilizzare con ogni ambiente.

Adobe consiglia di impostarlo in modo diverso per ciascuno degli ambienti di configurazione `dev`, `stage` e `prod` edge per semplificare le operazioni. Tuttavia, se hai già definito ambienti Adobe Target, puoi utilizzarli.

## Impostazioni Adobe Audience Manager

Per inviare dati a Adobe Audience Manager è sufficiente abilitare questa sezione. Le altre impostazioni sono facoltative ma incoraggiate.

![Adobe Blocco delle impostazioni di Gestione dell&#39;audience](../../assets/edge_configuration_aam.png)

### [!UICONTROL Cookie Destinations Enabled]

Consente all&#39;SDK di condividere le informazioni sui segmenti tramite [Cookie Destinations](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) (Destinazioni cookie) da [!DNL Audience Manager].

### [!UICONTROL URL Destinations Enabled]

Consente all&#39;SDK di condividere le informazioni sui segmenti tramite [Destinazioni URL](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Questi sono configurati in [!DNL Audience Manager].

## Impostazioni di Adobe Analytics

Controlla se i dati vengono inviati ad Adobe Analytics. Ulteriori dettagli sono disponibili in [Panoramica di Analytics](../data-collection/adobe-analytics/analytics-overview.md).

![Blocco impostazioni Adobe Analytics](../../assets/edge_configuration_aa.png)

### [!UICONTROL Report Suite ID]

La suite di rapporti si trova nella sezione Adobe Analytics Admin in [!UICONTROL Admin > ReportSuites]. Se sono specificate più suite di rapporti, i dati vengono copiati in ciascuna suite di rapporti.
