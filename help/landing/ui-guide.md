---
keywords: Experience Platform;home;argomenti popolari;Adobe Experience Platform;guida utente;guida utente;guida interfaccia utente;guida interfaccia utente piattaforma;introduzione alla piattaforma;dashboard;
solution: Experience Platform
title: Panoramica dell’interfaccia utente di Experience Platform
topic-legacy: ui guide
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1695'
ht-degree: 3%

---

# Guida all’interfaccia utente di Adobe Experience Platform

Questa guida offre un’introduzione all’utilizzo dell’interfaccia utente di Adobe Experience Platform, spiegando a cosa servono i vari componenti e fornendo collegamenti a ulteriori informazioni.

Per ulteriori informazioni su Adobe Experience Platform, consulta la [Panoramica Experience Platform](home.md).

## Schermata principale

Dopo aver effettuato l’accesso a Adobe Experience Platform, ti trovi sulla pagina [!UICONTROL Home], composta dalle sezioni [dashboard delle metriche](#metrics), [dati recenti](#recent-data) e [apprendimento consigliato](#recommended-learning).

![](images/user-guide/homepage.png)

### Metriche

Il dashboard delle metriche fornisce schede che forniscono informazioni su set di dati, profili, segmenti e destinazioni all’interno dell’organizzazione.

![](images/user-guide/homepage-dashboard.png)

La sezione **[!UICONTROL Datasets]** mostra il numero di set di dati all’interno dell’organizzazione IMS. Questo numero viene aggiornato quando viene creato un nuovo set di dati. Ulteriori informazioni sui set di dati sono disponibili nella [panoramica dei set di dati](../catalog/datasets/overview.md).

La sezione **[!UICONTROL Profiles]** mostra il numero totale di persone con profili all’interno dell’organizzazione IMS, esclusi i frammenti di profilo. Questo numero totale di persone rappresenta il pubblico indirizzabile totale e viene aggiornato una volta ogni 24 ore. Ulteriori informazioni sui profili sono disponibili nella [Panoramica del profilo cliente in tempo reale](../profile/home.md).

La sezione **[!UICONTROL Segments]** mostra il numero totale di segmenti creati all’interno dell’organizzazione IMS. Questo numero viene aggiornato quando viene creato un nuovo segmento. Ulteriori informazioni sui segmenti sono disponibili nella [Panoramica del servizio di segmentazione](../segmentation/home.md).

La sezione **[!UICONTROL Destinations]** mostra il numero totale di destinazioni create per l’organizzazione IMS. Questo numero viene aggiornato al momento della creazione di una nuova destinazione. Ulteriori informazioni sulle destinazioni sono disponibili nella [panoramica delle destinazioni](../destinations/home.md).

### Dati recenti

La dashboard dati recente fornisce informazioni su set di dati, origini, segmenti e destinazioni creati di recente.

![](images/user-guide/homepage-recent.png)

La sezione **[!UICONTROL Recent datasets]** elenca i cinque set di dati creati più di recente all’interno dell’organizzazione IMS. Questo elenco viene aggiornato ogni volta che viene creato un nuovo set di dati. Puoi selezionare un set di dati dall’elenco per visualizzare ulteriori informazioni sul set di dati specificato oppure selezionare **[!UICONTROL View all]** per visualizzare un elenco di tutti i set di dati creati. Ulteriori informazioni sui set di dati sono disponibili nella [panoramica dei set di dati](../catalog/datasets/overview.md).

La sezione **[!UICONTROL Recent sources]** elenca i cinque connettori sorgente creati più di recente all’interno dell’organizzazione IMS. Questo elenco viene aggiornato ogni volta che viene creato un nuovo connettore di origine. È possibile selezionare una connessione di origine dall&#39;elenco per visualizzare ulteriori informazioni sul connettore specificato oppure selezionare **[!UICONTROL View all]** per visualizzare un elenco di tutte le connessioni di origine create. Ulteriori informazioni sulle sorgenti sono disponibili nella [panoramica delle sorgenti](../sources/home.md).

La sezione **[!UICONTROL Recent segments]** elenca le cinque definizioni di segmenti create più di recente all’interno dell’organizzazione IMS. Questo elenco viene aggiornato ogni volta che viene creata una nuova definizione di segmento. Puoi selezionare una definizione di segmento dall’elenco per visualizzare ulteriori informazioni sulla definizione di segmento specificata oppure selezionare **[!UICONTROL View all]** per visualizzare un elenco di tutte le definizioni di segmento create. Ulteriori informazioni sui segmenti sono disponibili nella [Panoramica del servizio di segmentazione](../segmentation/home.md).

Nella sezione **[!UICONTROL Recent destinations]** sono elencate le cinque destinazioni create più di recente all’interno dell’organizzazione IMS. Questo elenco viene aggiornato ogni volta che viene creata una nuova destinazione. Puoi selezionare una destinazione dall’elenco per visualizzare ulteriori informazioni sulla destinazione specificata oppure selezionare **[!UICONTROL View all]** per visualizzare un elenco di tutte le destinazioni create. Ulteriori informazioni sulle destinazioni sono disponibili nella [panoramica delle destinazioni](../destinations/home.md).

### Apprendimento consigliato

La sezione **[!UICONTROL Recommended learning]** fornisce collegamenti a documenti utili per iniziare a utilizzare Adobe Experience Platform.

![](images/user-guide/homepage-recommended.png)

## Barra di navigazione superiore

La barra di navigazione superiore nell’interfaccia utente di Platform mostra l’organizzazione IMS a cui hai effettuato l’accesso e fornisce diversi controlli importanti.

Sul lato sinistro della barra di navigazione è presente il logo Adobe Experience Platform. Selezionando questa opzione in qualsiasi momento, tornerai alla schermata iniziale dell’interfaccia utente di Platform.

![](./images/user-guide/homepage-top-nav-bar.png)

### Switcher di organizzazione IMS

Il primo elemento a destra della barra di navigazione superiore è il **commutatore dell&#39;organizzazione IMS**.

![](./images/user-guide/homepage-ims-org.png)

Selezionando il commutatore si apre un menu a discesa delle organizzazioni IMS a cui hai accesso, se disponibili. Seleziona un’opzione elencata per passare a tale organizzazione IMS.

![](./images/user-guide/homepage-ims-org-switcher.png)

### Applicazioni switch

L&#39;elemento successivo sul lato destro della navigazione superiore è il **commutatore dell&#39;applicazione**, rappresentato dall&#39;icona ![commutatore dell&#39;applicazione](./images/user-guide/app-switcher-icon.png). Quando selezioni questa icona, puoi passare da un’applicazione Adobe a cui l’organizzazione IMS ha accesso, ad Experience Platform, Analytics, Assets e Launch.

### Aiuto

A destra dello switcher dell&#39;applicazione c&#39;è il menu **guida e supporto**, rappresentato dall&#39;icona ![punto interrogativo/help](./images/user-guide/help-icon.png). Quando selezioni questa icona, viene visualizzato un menu di selezione contenente diverse risorse di aiuto e supporto. La scheda **[!UICONTROL Help]** mostra un elenco della documentazione pertinente per la pagina in uso. La scheda **[!UICONTROL Support]** ti consente di creare un ticket di supporto con il team di supporto Adobe. La scheda **[!UICONTROL Feedback]** ti consente di inviare ad Adobe feedback su Platform.

![](images/user-guide/homepage-help-clicked.png)

### Notifiche e annunci

Nella sezione **notifiche**, rappresentata dall&#39;icona ![bell/Notifications and Announcements](images/user-guide/notification-icon.png). La scheda **[!UICONTROL Notifications]** mostra informazioni importanti sul prodotto e altri aggiornamenti rilevanti, mentre la scheda **[!UICONTROL Announcements]** contiene informazioni sulla manutenzione del servizio.

### Profilo utente

L&#39;elemento finale sulla barra di navigazione superiore è rappresentato dalle **impostazioni utente**, rappresentate dall&#39;icona ![impostazioni utente/Profilo utente](images/user-guide/profile-icon.png). Seleziona questa icona per modificare le preferenze o disconnetterti.

### Sandbox

Immediatamente sotto la barra di navigazione superiore si trova la barra sandbox. Questa barra mostra quale sandbox si sta utilizzando attualmente per Platform. Ulteriori informazioni sulle sandbox sono disponibili nella [panoramica sulle sandbox](../sandboxes/home.md).

## Navigazione a sinistra {#left-nav}

Nella navigazione a sinistra della schermata sono elencati tutti i diversi servizi supportati nell’interfaccia utente di Platform.

>[!IMPORTANT]
>
>Alcune sezioni sulla barra di navigazione a sinistra potrebbero non essere visualizzate o disattivate. Questo perché non hai accesso a queste funzioni. Se ritieni di dover accedere a queste sezioni, contatta l’amministratore di sistema.

![](images/user-guide/homepage-left.png)

La sezione **[!UICONTROL Home]** ti consente di tornare alla home page dell’interfaccia utente di Platform.

La sezione **[!UICONTROL Workflows]** mostra un elenco di flussi di lavoro a più passaggi per l’esecuzione di operazioni all’interno di Platform. Ulteriori informazioni sui flussi di lavoro sono disponibili nella [panoramica dei flussi di lavoro](./workflows.md).

### [!UICONTROL Connections]

La sezione **[!UICONTROL Sources]** ti consente di creare, aggiornare ed eliminare connessioni sorgente, consentendoti di acquisire dati da sorgenti esterne in Platform. Ulteriori informazioni sulle sorgenti sono disponibili nella [panoramica delle sorgenti](../sources/home.md).

La sezione **[!UICONTROL Destinations]** ti consente di creare, aggiornare ed eliminare destinazioni, consentendoti di esportare dati da Platform in molte destinazioni esterne. Ulteriori informazioni sulle destinazioni sono disponibili nella [panoramica delle destinazioni](../destinations/home.md).

### [!UICONTROL Customer]

La sezione **[!UICONTROL Profiles]** consente di sfogliare i profili dei clienti, visualizzare le metriche del profilo, creare e gestire i criteri di unione e visualizzare gli schemi di unione. Per ulteriori informazioni sull&#39;utilizzo della sezione [!UICONTROL Profiles], leggere la [[!DNL Profile] guida utente](../profile/ui/user-guide.md). Ulteriori informazioni sul Profilo del cliente in tempo reale sono disponibili nella [Panoramica del profilo del cliente in tempo reale](../profile/home.md).

La sezione **[!UICONTROL Segments]** ti consente di creare e gestire le definizioni dei segmenti. Per ulteriori informazioni sull&#39;utilizzo della sezione [!UICONTROL Segments], consulta la [guida utente alla segmentazione](../segmentation/ui/overview.md). Ulteriori informazioni sul servizio di segmentazione sono disponibili nella [panoramica del servizio di segmentazione](../segmentation/home.md).

La sezione **[!UICONTROL Identities]** consente di creare e gestire i namespace di identità. Per ulteriori informazioni sulla sezione [!UICONTROL Identities], incluse informazioni sugli spazi dei nomi di identità e su come utilizzare le identità nell’interfaccia utente di Platform, consulta la [panoramica dello spazio dei nomi di identità](../identity-service/namespaces.md).

### [!UICONTROL Privacy]

La sezione **[!UICONTROL Policies]** ti consente di creare e gestire i criteri di utilizzo dei dati. Per ulteriori informazioni sull&#39;utilizzo della sezione Criteri, consulta la [guida utente relativa ai criteri di utilizzo dei dati](../data-governance/policies/user-guide.md). Ulteriori informazioni sui criteri di utilizzo dei dati sono disponibili nella [panoramica dei criteri di utilizzo dei dati](../data-governance/policies/overview.md).

La sezione **[!UICONTROL Requests]** ti consente di creare e gestire le richieste di accesso a dati personali. Tieni presente che devi essere inserito nell&#39;elenco Consentiti per poter accedere all’interfaccia utente di Privacy Service. Per ulteriori informazioni sull&#39;utilizzo della sezione Richieste, consulta la [guida utente Privacy Service](../privacy-service/ui/user-guide.md). Ulteriori informazioni su Privacy Service sono disponibili in [Panoramica di Privacy Service](../privacy-service/home.md).

### [!UICONTROL Data Science]

La sezione **[!UICONTROL Notebooks]** consente di accedere a JupyterLab, un ambiente di sviluppo interattivo che consente di esplorare, analizzare e modellare i dati. Per ulteriori informazioni sull&#39;utilizzo della sezione Notebook, leggere la [Guida utente di JupyterLab](../data-science-workspace/jupyterlab/overview.md). Ulteriori informazioni su Data Science Workspace sono disponibili nella [Panoramica di Data Science Workspace](../data-science-workspace/home.md)

La sezione **[!UICONTROL Models]** ti consente di sfruttare l’apprendimento automatico e l’intelligenza artificiale per creare, sviluppare, addestrare e ottimizzare i modelli per effettuare previsioni. Ulteriori informazioni sulla sezione Modelli sono disponibili nell&#39;esercitazione su [formazione e valutazione di un modello](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

La sezione **[!UICONTROL Services]** ti consente di gestire i modelli pubblicati per l’addestramento e il punteggio pianificati oppure di sfruttare i servizi intelligenti di Adobe, un set di servizi AI che offrono esperienze cliente personalizzate in tempo reale. Per ulteriori informazioni sulla sezione Servizi, consulta l’ [Esercitazione Pubblicazione di un modello come servizio](../data-science-workspace/models-recipes/publish-model-service-ui.md) .

### [!UICONTROL Data management]

La sezione **[!UICONTROL Schemas]** ti consente di creare e gestire gli schemi Experience Data Model (XDM). Per ulteriori informazioni sugli schemi, leggi l’esercitazione su [creazione di uno schema](../xdm/tutorials/create-schema-ui.md). Ulteriori informazioni su XDM sono disponibili in [Panoramica del sistema XDM](../xdm/home.md).

La sezione **[!UICONTROL Datasets]** ti consente di creare e gestire i set di dati. Ulteriori informazioni sui set di dati sono disponibili nella [guida utente dei set di dati](../catalog/datasets/user-guide.md).

La sezione **[!UICONTROL Queries]** consente di creare e gestire query, registrare query SQL create da Adobe Experience Platform Query Service e visualizzare le credenziali PostgreSQL. Ulteriori informazioni sulle query sono disponibili nella [Guida utente del servizio query](../query-service/ui/overview.md).

La sezione **[!UICONTROL Monitoring]** ti consente di monitorare l’acquisizione in batch e in streaming. Ulteriori informazioni sul monitoraggio sono disponibili nella [guida utente per l&#39;acquisizione di dati di monitoraggio](../ingestion/quality/monitor-data-ingestion.md).

### [!UICONTROL Decisioning]

Offer Decisioning è un servizio applicativo integrato con Adobe Experience Platform. Consente di sfruttare Experience Platform per offrire ai clienti la migliore offerta ed esperienza possibile in tutti i punti di contatto al momento giusto. Per ulteriori informazioni sugli Offer decisioning, tra cui lavorare con [!UICONTROL Offers] e [!UICONTROL Activities], visita la documentazione [Offer Decisioning](https://experienceleague.adobe.com/docs/offer-decisioning.html).

### [!UICONTROL Administration]

L’interfaccia utente di Platform (UI) fornisce una dashboard attraverso la quale è possibile visualizzare informazioni importanti sull’utilizzo delle licenze dell’organizzazione, acquisite durante un’istantanea giornaliera. Per accedervi, seleziona **[!UICONTROL License usage]** nella navigazione. Per ulteriori informazioni sul dashboard di utilizzo della licenza, visita la [guida all&#39;utilizzo della licenza](license-usage-dashboard.md).

>[!IMPORTANT]
>
>La funzionalità del dashboard di utilizzo della licenza è attualmente in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

## Passaggi successivi

Questa guida contiene informazioni sulla home page e sui principali elementi di navigazione dell’interfaccia utente di Platform. Per informazioni più dettagliate sull’utilizzo dell’interfaccia utente, consulta la documentazione relativa a ciascun servizio Platform. I collegamenti a questa documentazione sono forniti nella sezione [navigazione a sinistra](#left-nav) trovata in precedenza in questo documento.
