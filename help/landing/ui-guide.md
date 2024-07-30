---
keywords: Experience Platform;home;argomenti popolari;Adobe Experience Platform;guida utente;guida interfaccia utente;guida interfaccia utente piattaforma;introduzione a piattaforma;dashboard;
solution: Experience Platform
title: Panoramica dell’interfaccia utente di Experience Platform
description: Adobe Experience Platform
exl-id: 47f9a3fb-731d-4ade-8069-faaa18f224dc
source-git-commit: 9844a7bf5e7198e7d5112ec924220aba71cdc14b
workflow-type: tm+mt
source-wordcount: '1947'
ht-degree: 2%

---

# Guida all’interfaccia utente di Adobe Experience Platform

Questa guida offre un’introduzione all’utilizzo dell’interfaccia utente di Adobe Experience Platform, spiegando a cosa servono i vari componenti e fornendo collegamenti verso ulteriori informazioni.

Per ulteriori informazioni su Adobe Experience Platform, leggere l&#39;[panoramica dell&#39;Experience Platform](home.md).

## Schermata iniziale

Dopo aver effettuato l&#39;accesso a Adobe Experience Platform, ti trovi nella pagina [!UICONTROL Home], che comprende le sezioni [dashboard delle metriche](#metrics), [dati recenti](#recent-data) e [apprendimento consigliato](#recommended-learning).

![](images/user-guide/homepage.png)

### Metriche

Il dashboard delle metriche fornisce schede che forniscono informazioni su set di dati, profili, segmenti e destinazioni all’interno della tua organizzazione.

![](images/user-guide/homepage-dashboard.png)

La sezione **[!UICONTROL Set di dati]** mostra il numero di set di dati all&#39;interno dell&#39;organizzazione. Questo numero viene aggiornato quando viene creato un nuovo set di dati. Ulteriori informazioni sui set di dati sono disponibili nella [panoramica dei set di dati](../catalog/datasets/overview.md).

La sezione **[!UICONTROL Profili]** mostra il numero totale di persone con profili all&#39;interno dell&#39;organizzazione, esclusi i frammenti di profilo. Questo numero totale di persone rappresenta il pubblico indirizzabile totale e viene aggiornato una volta ogni 24 ore. Per ulteriori informazioni sui profili, consulta la [panoramica dei profili cliente in tempo reale](../profile/home.md).

La sezione **[!UICONTROL Segmenti]** mostra il numero totale di segmenti creati nell&#39;organizzazione. Questo numero viene aggiornato quando viene creato un nuovo segmento. Ulteriori informazioni sui segmenti sono disponibili nella [Panoramica del servizio di segmentazione](../segmentation/home.md).

La sezione **[!UICONTROL Destinazioni]** mostra il numero totale di destinazioni create per l&#39;organizzazione. Questo numero viene aggiornato quando viene creata una nuova destinazione. Ulteriori informazioni sulle destinazioni sono disponibili nella [panoramica sulle destinazioni](../destinations/home.md).

### Dati recenti

Il dashboard dati recente fornisce informazioni su set di dati, origini, segmenti e destinazioni creati di recente.

![](images/user-guide/homepage-recent.png)

Nella sezione **[!UICONTROL Set di dati recenti]** sono elencati gli ultimi cinque set di dati creati nell&#39;organizzazione. Questo elenco viene aggiornato ogni volta che viene creato un nuovo set di dati. È possibile selezionare un set di dati dall&#39;elenco per visualizzare Ulteriori informazioni sul set di dati specificato oppure selezionare **[!UICONTROL Visualizza tutto]** per visualizzare un elenco di tutti i set di dati creati. Ulteriori informazioni sui set di dati sono disponibili nella [panoramica dei set di dati](../catalog/datasets/overview.md).

Nella sezione **[!UICONTROL Origini recenti]** sono elencati gli ultimi cinque connettori di origine creati nell&#39;organizzazione. Questo elenco viene aggiornato ogni volta che viene creato un nuovo connettore di origine. È possibile selezionare una connessione di origine dall&#39;elenco per visualizzare Ulteriori informazioni sul connettore specificato oppure selezionare **[!UICONTROL Visualizza tutto]** per visualizzare un elenco di tutte le connessioni di origine create. Ulteriori informazioni sulle origini sono disponibili nella [panoramica delle origini](../sources/home.md).

Nella sezione **[!UICONTROL Segmenti recenti]** sono elencate le ultime cinque definizioni di segmenti create all&#39;interno dell&#39;organizzazione. Questo elenco viene aggiornato ogni volta che viene creata una nuova definizione di segmento. È possibile selezionare una definizione di segmento dall&#39;elenco per visualizzare Ulteriori informazioni sulla definizione di segmento specificata oppure selezionare **[!UICONTROL Visualizza tutto]** per visualizzare un elenco di tutte le definizioni di segmento create. Ulteriori informazioni sui segmenti sono disponibili nella [Panoramica del servizio di segmentazione](../segmentation/home.md).

Nella sezione **[!UICONTROL Destinazioni recenti]** sono elencate le ultime cinque destinazioni create all&#39;interno dell&#39;organizzazione. Questo elenco viene aggiornato ogni volta che viene creata una nuova destinazione. È possibile selezionare una destinazione dall&#39;elenco per visualizzare Ulteriori informazioni sulla destinazione specificata oppure selezionare **[!UICONTROL Visualizza tutto]** per visualizzare un elenco di tutte le destinazioni create. Ulteriori informazioni sulle destinazioni sono disponibili nella [panoramica sulle destinazioni](../destinations/home.md).

### Risorse di apprendimento consigliate

La sezione **[!UICONTROL Apprendimento consigliato]** fornisce collegamenti a documentazione utile per iniziare a utilizzare Adobe Experience Platform.

![](images/user-guide/homepage-recommended.png)

## Barra di navigazione superiore

La barra di navigazione superiore nell’interfaccia utente di Platform mostra l’organizzazione a cui sei attualmente connesso e fornisce diversi controlli importanti.

Sul lato sinistro della barra di navigazione è presente il logo Adobe Experience Platform. Se selezioni questo logo in qualsiasi momento, torna alla schermata iniziale dell’interfaccia utente di Platform.

![](./images/user-guide/homepage-top-nav-bar.png)

### Commutatore organizzazione

Il primo elemento sul lato destro della barra di navigazione superiore è il **commutatore organizzazione**.

![](./images/user-guide/homepage-ims-org-switcher.png)

Selezionando il selettore si apre un menu a discesa contenente le organizzazioni a cui hai accesso, se disponibili. Per passare a un’altra organizzazione, seleziona un’opzione elencata.

### Cambiare applicazioni

L&#39;elemento successivo sul lato destro della navigazione superiore è il **commutatore applicazione**, rappresentato dall&#39;icona ![commutatore applicazione](/help/images/icons/apps.png). Quando selezioni questa icona, puoi passare da un’applicazione Adobe a cui la tua organizzazione ha accesso, come Experience Platform, Analytics, Assets e altre.

### Aiuto

A destra del commutatore dell&#39;applicazione si trova il menu **Guida e supporto tecnico**, rappresentato dall&#39;icona ![punto interrogativo/Guida](/help/images/icons/help.png). Quando selezioni questa icona, viene visualizzato un menu a comparsa contenente diverse risorse di aiuto e supporto. Nella scheda **[!UICONTROL Guida]** è disponibile un elenco della documentazione relativa alla pagina in cui si è connessi. La scheda **[!UICONTROL Supporto]** consente di creare un ticket di supporto con il team di supporto Adobe. La scheda **[!UICONTROL Feedback]** consente di inviare ad Adobe commenti e suggerimenti su Platform.

![](images/user-guide/homepage-help-clicked.png)

### Notifiche e annunci

Nella sezione **notifications**, rappresentata dall&#39;icona ![bell/Notifications and Announcements](/help/images/icons/bell.png). La scheda **[!UICONTROL Notifiche]** mostra informazioni importanti sul prodotto e altri aggiornamenti rilevanti, mentre la scheda **[!UICONTROL Annunci]** mostra informazioni sulla manutenzione del servizio.

### Profilo utente

L&#39;elemento finale nella barra di navigazione superiore è rappresentato dalle **impostazioni utente**, rappresentate dall&#39;icona ![impostazioni utente/Profilo utente](images/user-guide/profile-icon.png). Seleziona questa icona per modificare le preferenze o uscire.

Puoi alternare tra il tema chiaro e scuro per l’interfaccia Platform con lo switch che si trova appena sotto il tuo nome e l’e-mail. Seleziona il tema desiderato.

![](images/theme.png)

### Sandbox

La barra della sandbox si trova immediatamente sotto la barra di navigazione superiore. Questa barra mostra quale sandbox stai utilizzando attualmente per Platform. Ulteriori informazioni sulle sandbox sono disponibili nella [panoramica sulle sandbox](../sandboxes/home.md).

## Pannello di navigazione a sinistra {#left-nav}

Nella barra di navigazione a sinistra della schermata sono elencati tutti i diversi servizi supportati nell’interfaccia utente di Platform.

Fai clic sull’icona del menu per mostrare o nascondere il pannello di navigazione a sinistra.

![](images/user-guide/hidemenu.png)

Per bloccare la navigazione in posizione aperta, fai nuovamente clic su dopo aver visualizzato il pannello.

>[!IMPORTANT]
>
>La barra di navigazione a sinistra mostra solo le funzioni a cui sei in grado di accedere. Nelle versioni precedenti di Adobe Experience Platform, gli elementi non disponibili erano disabilitati. Se ritieni di dover accedere a una sezione che non viene visualizzata, contatta l’amministratore di sistema.

![](images/user-guide/homepage-left.png)

La sezione **[!UICONTROL Home]** ti consente di tornare alla home page dell&#39;interfaccia utente di Platform.

La sezione **[!UICONTROL Flussi di lavoro]** mostra un elenco di flussi di lavoro con più passaggi per l&#39;esecuzione di operazioni in Platform. Ulteriori informazioni sui flussi di lavoro sono disponibili nella [panoramica dei flussi di lavoro](./workflows.md).

### [!UICONTROL Connessioni]

La sezione **[!UICONTROL Origini]** consente di creare, aggiornare ed eliminare connessioni di origine, consentendo di acquisire dati da origini esterne in Platform. Ulteriori informazioni sulle origini sono disponibili nella [panoramica delle origini](../sources/home.md).

La sezione **[!UICONTROL Destinazioni]** ti consente di creare, aggiornare ed eliminare destinazioni, consentendoti di esportare dati da Platform in molte destinazioni esterne. Ulteriori informazioni sulle destinazioni sono disponibili nella [panoramica sulle destinazioni](../destinations/home.md).

### [!UICONTROL Cliente]

La sezione **[!UICONTROL Profili]** consente di sfogliare i profili dei clienti, visualizzare le metriche dei profili, creare e gestire i criteri di unione e visualizzare gli schemi di unione. Per ulteriori informazioni sull&#39;utilizzo della sezione [!UICONTROL Profili], leggere la [[!DNL Profile] guida utente](../profile/ui/user-guide.md). Per ulteriori informazioni su Real-Time Customer Profile, consulta la [Panoramica sul profilo cliente in tempo reale](../profile/home.md).

La sezione **[!UICONTROL Tipi di pubblico]** consente di creare e gestire le definizioni dei segmenti. Per ulteriori informazioni sull&#39;utilizzo della sezione [!UICONTROL Tipi di pubblico], consulta la [guida utente per la segmentazione](../segmentation/ui/overview.md). Ulteriori informazioni sul servizio di segmentazione sono disponibili nella [Panoramica del servizio di segmentazione](../segmentation/home.md).

La sezione **[!UICONTROL Identità]** ti consente di creare e gestire gli spazi dei nomi delle identità. Per ulteriori informazioni sulla sezione [!UICONTROL Identità], incluse informazioni sugli spazi dei nomi delle identità e su come utilizzare le identità nell&#39;interfaccia utente di Platform, consulta la [panoramica dello spazio dei nomi delle identità](../identity-service/features/namespaces.md).

### [!UICONTROL Privacy]

La sezione **[!UICONTROL Criteri]** ti consente di creare e gestire i criteri di utilizzo dei dati. Per ulteriori informazioni sull&#39;utilizzo della sezione Criteri, leggere la [guida utente dei criteri di utilizzo dei dati](../data-governance/policies/user-guide.md). Ulteriori informazioni sui criteri di utilizzo dei dati sono disponibili nella [panoramica dei criteri di utilizzo dei dati](../data-governance/policies/overview.md).

La sezione **[!UICONTROL Richieste]** consente di creare e gestire le richieste di accesso a dati personali. Tieni presente che per poter accedere all’interfaccia utente di Privacy Service devi essere inserito nell&#39;elenco Consentiti. Per ulteriori informazioni sull&#39;utilizzo della sezione Richieste, leggere la [guida utente di Privacy Service](../privacy-service/ui/user-guide.md). Ulteriori informazioni su Privacy Service sono disponibili nella [panoramica di Privacy Service](../privacy-service/home.md).

### [!UICONTROL Data Science]

La sezione **[!UICONTROL Notebooks]** fornisce l&#39;accesso a JupyterLab, un ambiente di sviluppo interattivo che consente di esplorare, analizzare e modellare i dati. Per ulteriori informazioni sull&#39;utilizzo della sezione Notebook, leggere la [guida utente di JupyterLab](../data-science-workspace/jupyterlab/overview.md). Ulteriori informazioni su Data Science Workspace sono disponibili nella [Panoramica di Data Science Workspace](../data-science-workspace/home.md)

La sezione **[!UICONTROL Modelli]** consente di utilizzare l&#39;apprendimento automatico e l&#39;intelligenza artificiale per creare, sviluppare, addestrare e ottimizzare modelli per effettuare previsioni. Ulteriori informazioni sulla sezione Modelli sono disponibili nell&#39;esercitazione su [formazione e valutazione di un modello](../data-science-workspace/models-recipes/train-evaluate-model-ui.md).

La sezione **[!UICONTROL Servizi]** ti consente di gestire i modelli pubblicati per l&#39;apprendimento pianificato e il punteggio, oppure di utilizzare Adobe Intelligent Services, un set di servizi di intelligenza artificiale che offre esperienze cliente personalizzate in tempo reale. Per ulteriori informazioni sulla sezione Servizi, vedere l&#39;esercitazione [Pubblicazione di un modello come servizio](../data-science-workspace/models-recipes/publish-model-service-ui.md).

### [!UICONTROL Gestione dati]

La sezione **[!UICONTROL Schemi]** consente di creare e gestire gli schemi Experience Data Model (XDM). Per ulteriori informazioni sugli schemi, leggere l&#39;esercitazione su [creazione di uno schema](../xdm/tutorials/create-schema-ui.md). Ulteriori informazioni su XDM sono disponibili nella [Panoramica del sistema XDM](../xdm/home.md).

La sezione **[!UICONTROL Set di dati]** ti consente di creare e gestire i set di dati. Ulteriori informazioni sui set di dati sono disponibili nella [guida utente per i set di dati](../catalog/datasets/user-guide.md).

La sezione **[!UICONTROL Query]** consente di creare e gestire query, registrare query SQL eseguite da Adobe Experience Platform Query Service e visualizzare le credenziali di [!DNL PostgreSQL]. Ulteriori informazioni sulle query sono disponibili nella [Guida utente di Query Service](../query-service/ui/overview.md).

La sezione **[!UICONTROL Monitoraggio]** ti consente di monitorare l&#39;acquisizione in batch e in streaming. Ulteriori informazioni sul monitoraggio sono disponibili nella [guida utente per l&#39;acquisizione dei dati di monitoraggio](../ingestion/quality/monitor-data-ingestion.md).

### [!UICONTROL Dati federati] (disponibilità limitata)

La sezione **[!UICONTROL Modelli]** consente di progettare e creare modelli di dati e schemi che definiscono la struttura, le relazioni e i vincoli dei dati. Puoi trovare ulteriori informazioni sui modelli di dati e gli schemi nella [guida utente Federated Audience Composition](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/config/datamodel/schemas).

La sezione **[!UICONTROL Audit trail]** fornisce un record dettagliato e cronologico di tutte le azioni e gli eventi eseguiti nell&#39;ambiente in tempo reale. Puoi trovare ulteriori informazioni sull&#39;audit trail nella [guida utente Federated Audience Composition](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/audit-trail/audit-trail).


La sezione **[!UICONTROL Federated databases]** consente di connettere Adobe Experience Platform al data warehouse aziendale. Ulteriori informazioni sulla connessione ai database federati sono disponibili nella [guida utente Federated Audience Composition](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/config/federated-db).

>[!AVAILABILITY]
>
>La composizione di pubblico federato è attualmente disponibile solo per un set di organizzazioni (disponibilità limitata). Per ulteriori informazioni, contatta il tuo rappresentante Adobe.

### [!UICONTROL Decisioning]

Adobe Journey Optimizer è un servizio applicativo basato su Experience Platform. Consente di utilizzare tecnologie decisionali potenti per offrire ai clienti l’offerta e l’esperienza migliore al momento giusto, in tutti i punti di contatto. Per ulteriori informazioni su Journey Optimizer, incluso l&#39;utilizzo di [!UICONTROL Offerte] e [!UICONTROL Attività], visita la [documentazione di Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=it).

### [!UICONTROL Amministrazione]

L’interfaccia utente di Platform fornisce una dashboard attraverso la quale puoi visualizzare informazioni importanti sull’utilizzo delle licenze della tua organizzazione, acquisite durante un’istantanea giornaliera. Accedi a questo dashboard selezionando **[!UICONTROL Utilizzo licenze]** nell&#39;area di navigazione. Per ulteriori informazioni sul dashboard di utilizzo delle licenze, visitare la [guida del dashboard di utilizzo delle licenze](./license-usage-and-guardrails/license-usage-dashboard.md).

>[!IMPORTANT]
>
>La funzionalità del dashboard utilizzo licenze è attualmente in formato alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

## Passaggi successivi

Una volta letta questa guida, potrai conoscere la home page e i principali elementi di navigazione dell’interfaccia utente di Platform. Per informazioni più dettagliate su come lavorare nell’interfaccia utente, consulta la documentazione per ogni singolo servizio di Platform. I collegamenti a questa documentazione sono forniti nella sezione [navigazione a sinistra](#left-nav) trovata in precedenza in questo documento.
