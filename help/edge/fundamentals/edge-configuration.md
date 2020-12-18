---
title: Configurazione Edge
seo-title: 'Configurazione Edge per l''SDK Web del Experience Platform '
description: 'Scoprite come configurare  Experience Platform Edge Network. '
seo-description: 'Scoprite come configurare  Experience Platform Edge Network. '
keywords: configuration;edge;edge configuration id;Environment Settings;edgeConfigId;identity;id sync enabled;ID Sync Container ID;Sandbox;Streaming Inlet;Event Dataset;target;client code;Property Token;Target Environment ID;Cookie Destinations;url Destinations;Analytics Settings Blockreport suite id;
translation-type: tm+mt
source-git-commit: 94b3faf3157f4e1f4e46b6055914a04883dc44fa
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 1%

---


# Configurazione di Edge

La configurazione per Adobe Experience Platform Web SDK è suddivisa in due posizioni. Il [comando di configurazione](configuring-the-sdk.md) nell&#39;SDK controlla gli elementi che devono essere gestiti sul client, come il `edgeDomain`. La configurazione edge gestisce tutte le altre configurazioni per l’SDK. Quando una richiesta viene inviata ad Adobe Experience Platform Edge Network, la `edgeConfigId` viene utilizzata per fare riferimento alla configurazione lato server. Questo consente di aggiornare la configurazione senza dover apportare modifiche al codice sul sito Web.

Per questa funzione è necessario effettuare il provisioning dell&#39;organizzazione. Contatta il tuo Customer Success Manager (CSM) per ottenere il inserire nell&#39;elenco Consentiti .

## Creazione di una configurazione Edge

Le configurazioni Edge possono essere create  Adobe [!DNL Experience Platform Launch] utilizzando lo strumento di configurazione edge.

![navigazione tramite strumento di configurazione del bordo](../../assets/edge_configuration_nav.png)

>[!NOTE]
>
>Lo strumento di configurazione edge è disponibile per i clienti del elenco consentiti , indipendentemente dal fatto che utilizzino [!DNL Experience Platform Launch] come gestore di tag. Inoltre, gli utenti richiedono le autorizzazioni Sviluppo in [!DNL Experience Platform Launch]. Per ulteriori informazioni, consultate l&#39;articolo [Autorizzazioni utente](https://docs.adobe.com/content/help/it-IT/launch/using/reference/admin/user-permissions.html) nella documentazione [!DNL Experience Platform Launch].

Per creare una configurazione dei bordi, fate clic su **[!UICONTROL New Edge Configuration]** nell&#39;area in alto a destra dello schermo. Dopo aver fornito un nome e una descrizione, viene richiesto di specificare le impostazioni predefinite per ogni ambiente. Le impostazioni disponibili sono descritte di seguito.

Quando create una configurazione Edge, vengono creati automaticamente tre ambienti con impostazioni identiche. Questi tre ambienti sono *dev*, *stage* e *prod*. Corrispondono ai tre ambienti predefiniti in [!DNL Experience Platform Launch]. Quando si crea una libreria [!DNL Experience Platform Launch] in un ambiente di sviluppo, la libreria utilizza automaticamente l&#39;ambiente di sviluppo dalla configurazione. È possibile modificare le impostazioni in singoli ambienti con la massima flessibilità.

L&#39;ID utilizzato nell&#39;SDK come `edgeConfigId` è un ID composito che specifica la configurazione e l&#39;ambiente (ad esempio, `1c86778b-cdba-4684-9903-750e52912ad1:stage`). Se nell&#39;ID composito non è presente alcun ambiente (ad esempio, `stage` nell&#39;esempio precedente), viene utilizzato l&#39;ambiente di produzione.

Di seguito sono riportate le impostazioni disponibili per ogni ambiente di configurazione. La maggior parte delle sezioni può essere abilitata o disattivata. Se disabilitata, le impostazioni vengono salvate ma non sono attive.

## [!UICONTROL Identity] Impostazioni

La sezione identità è l&#39;unica sezione sempre attiva. Sono disponibili due impostazioni: &quot;[!UICONTROL ID Syncs Enabled]&quot; e &quot;[!UICONTROL ID Sync Container ID]&quot;.

![Sezione Identità dell’interfaccia utente di configurazione](../../assets/edge_configuration_identity.png)

### [!UICONTROL ID Sync Enabled]

Controlla se l’SDK esegue o meno sincronizzazioni di identità con partner di terze parti.

### [!UICONTROL ID Sync Container ID]

Le sincronizzazioni ID possono essere raggruppate in contenitori per consentire l’esecuzione di diverse sincronizzazioni ID in momenti diversi. Questo controlla quale contenitore di sincronizzazione ID viene eseguito per un determinato ID di configurazione.

## Impostazioni Adobe Experience Platform

Le impostazioni elencate qui consentono di inviare i dati ad Adobe Experience Platform. Abilita questa sezione solo se hai acquistato l’Adobe Experience Platform.

![Blocco delle impostazioni Adobe Experience Platform](../../assets/edge_configuration_aep.png)

### [!UICONTROL Sandbox]

Le sandbox sono posizioni in Adobe Experience Platform che consentono ai clienti di isolare i dati e le implementazioni l&#39;una dall&#39;altra. Per ulteriori dettagli sul funzionamento, consultare la [Documentazione sandbox](../../sandboxes/home.md).

### [!UICONTROL Streaming Inlet]

Un ingresso in streaming è un&#39;origine HTTP in Adobe Experience Platform. Questi vengono creati nella scheda &quot;[!UICONTROL Sources]&quot; dell&#39;Adobe Experience Platform come API HTTP.

### [!UICONTROL Event Dataset]

Le configurazioni Edge supportano l&#39;invio di dati a set di dati con uno schema di classe [!UICONTROL Experience Event].

##  Adobe Target Settings

Per configurare  Adobe Target, dovete fornire un codice client. Gli altri campi sono facoltativi.

![ blocco impostazioni Adobe Target](../../assets/edge_configuration_target.png)

>[!NOTE]
>
>L&#39;organizzazione associata al codice client deve corrispondere all&#39;organizzazione in cui viene creato l&#39;ID di configurazione.

### [!UICONTROL Client Code]

L&#39;ID univoco per un account di destinazione. Per trovare questo percorso, è possibile passare a [!UICONTROL Adobe Target] > [!UICONTROL Setup] [!UICONTROL Implementation] > [!UICONTROL edit settings] accanto al pulsante [!UICONTROL download] per [!UICONTROL at.js] o [!UICONTROL mbox.js]

### [!UICONTROL Property Token]

[!DNL Target] consente ai clienti di controllare le autorizzazioni mediante l&#39;uso di proprietà. I dettagli sono disponibili nella sezione [Autorizzazioni Enterprise](https://docs.adobe.com/content/help/en/target/using/administer/manage-users/enterprise/properties-overview.html) della documentazione [!DNL Target].

Il token proprietà si trova in [!UICONTROL Adobe Target] > [!UICONTROL setup] > [!UICONTROL Properties]

### [!UICONTROL Target Environment ID]

[Gli ](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html) ambienti  Adobe Target consentono di gestire la propria implementazione in tutte le fasi dello sviluppo. Questa impostazione specifica quale ambiente utilizzare con ciascun ambiente.

 Adobe consiglia di impostare questa impostazione in modo diverso per ciascuno degli ambienti di configurazione `dev`, `stage` e `prod` periferici per semplificare le cose. Tuttavia, se avete già  ambienti Adobe Target definiti, potete utilizzarli.

## Impostazioni Adobe Audience Manager

Per inviare i dati ad Adobe Audience Manager è sufficiente abilitare questa sezione. Le altre impostazioni sono facoltative ma incoraggiate.

![ Adobe Audience Manage settings block](../../assets/edge_configuration_aam.png)

### [!UICONTROL Cookie Destinations Enabled]

Consente all&#39;SDK di condividere le informazioni sul segmento tramite [Cookie Destinations](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html) da [!DNL Audience Manager].

### [!UICONTROL URL Destinations Enabled]

Consente all&#39;SDK di condividere le informazioni sul segmento tramite [Destinazioni URL](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html). Questi sono configurati in [!DNL Audience Manager].

##  Adobe Analytics Settings

Controlla se i dati vengono inviati a  Adobe Analytics. Ulteriori dettagli sono disponibili in [Analytics Overview](../data-collection/adobe-analytics/analytics-overview.md).

![ Adobe Analytics Settings Block](../../assets/edge_configuration_aa.png)

### [!UICONTROL Report Suite ID]

La suite di rapporti si trova nella sezione  Adobe Analytics Admin in [!UICONTROL Admin > ReportSuites]. Se vengono specificate più suite di rapporti, i dati vengono copiati in ciascuna suite di rapporti.
