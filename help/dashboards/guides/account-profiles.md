---
title: Guida al dashboard dei profili account
description: Adobe Experience Platform fornisce un dashboard tramite il quale puoi visualizzare informazioni importanti sui profili account B2B della tua organizzazione.
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 05e63064dc8eb3f070a383f508cc4a86d4f5e9cc
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# [!UICONTROL Profili account] dashboard

L’interfaccia utente di Adobe Experience Platform fornisce un dashboard attraverso il quale è possibile visualizzare informazioni importanti sui profili dell’account, acquisite durante un’istantanea giornaliera. Questa guida illustra come accedere e utilizzare [!UICONTROL Profili account] dashboard nell’interfaccia utente e fornisce ulteriori informazioni sulle visualizzazioni visualizzate nel dashboard.

Per una panoramica di tutte le funzioni dell’interfaccia utente del profilo account, visita la [guida all’interfaccia utente del profilo account](../../rtcdp/accounts/account-profile-ui-guide.md).

## Introduzione

Devi avere diritto a [Real-time Customer Data Platform B2B Edition](../../rtcdp/b2b-overview.md) per accedere al B2B [!UICONTROL Profili account] dashboard.

## Dati dei profili account

La [!UICONTROL Profili account] dashboard visualizza un&#39;istantanea di informazioni unificate sull&#39;account provenienti da più origini nei diversi canali di marketing e nei diversi sistemi attualmente utilizzati dalla tua organizzazione per archiviare le informazioni sull&#39;account cliente.

I dati di profilo nello snapshot mostrano esattamente come vengono visualizzati nel momento specifico in cui è stata acquisita l&#39;istantanea. In altre parole, l&#39;istantanea non è un&#39;approssimazione o un campione dei dati, e [!UICONTROL Profili account] il dashboard non viene aggiornato in tempo reale.

>[!NOTE]
>
>Eventuali modifiche o aggiornamenti apportati ai dati dall&#39;acquisizione dello snapshot non verranno visualizzati nel dashboard fino all&#39;acquisizione dello snapshot successivo.

## Esplora [!UICONTROL Profili account] dashboard

Per passare al [!UICONTROL Profili account] nell’interfaccia utente di Platform, seleziona **[!UICONTROL Profili]** sotto [!UICONTROL Account] nel pannello di navigazione a sinistra.

![Interfaccia utente di Platform con profili account nella barra di navigazione a sinistra evidenziata e visualizzata la scheda panoramica .](../images/account-profiles/account-profiles-dashboard.png)

Da [!UICONTROL Profili account] dashboard puoi [sfogliare i profili account acquisiti nella tua organizzazione](#browse-account-profiles)oppure [visualizzare in un primo tempo tutti i dati del profilo account utilizzando i widget](#standard-widgets) che visualizzano gli aspetti dei dati.

## Sfoglia profili account {#browse-account-profiles}

La [!UICONTROL Sfoglia] La scheda ti consente di cercare e visualizzare i profili account di sola lettura acquisiti nell’organizzazione utilizzando un ID account proveniente da un’origine aziendale connessa o immettendo direttamente i dettagli sorgente. Da qui puoi vedere importanti informazioni appartenenti al profilo account, tra cui nome, settore, ricavi e segmento.

Seleziona la [!UICONTROL ID profilo] dai risultati visualizzati nel [!UICONTROL Sfoglia] per aprire [!UICONTROL Dettagli] per il profilo dell’account.

![Nella scheda Sfoglia Profili account sono visualizzati i risultati e l’ID profilo è evidenziato.](../images/account-profiles/account-profiles-browse-tab.png)

Le informazioni sul profilo dell&#39;account visualizzate nel [!UICONTROL Dettagli] è stata unita una scheda da più frammenti di profilo per formare una singola vista del singolo account. Consulta la documentazione su [esplorazione dei profili account in Real-time Customer Data Platform](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) per ulteriori informazioni sulle funzionalità di visualizzazione del profilo account nell’interfaccia utente di Platform.

## La [!UICONTROL Profili account] [!UICONTROL Panoramica] {#overview}

La [!UICONTROL Panoramica] La scheda è composta da widget che forniscono metriche di sola lettura per trasmettere informazioni importanti sui profili del tuo account. Seleziona **[!UICONTROL Modifica dashboard]** per modificare l&#39;aspetto della [!UICONTROL Panoramica] spostamento e ridimensionamento dei widget.

![La scheda Panoramica dei profili account con il dashboard Modifica evidenziato.](../images/account-profiles/modify-dashboard.png)

Fai riferimento al documento su [modifica delle dashboard](../customize/modify.md) e [Panoramica della libreria Widget](../customize/widget-library.md) per saperne di più.

## Widget standard {#standard-widgets}

Adobe fornisce widget standard che puoi utilizzare per visualizzare diverse metriche correlate ai profili del tuo account.

Per ulteriori informazioni su ciascuno dei widget standard disponibili, seleziona il nome di un widget dal seguente elenco:

* [Conti totali per branca di attività economica](#total-accounts-by-industry)
* [Profili account aggiunti](#account-profiles-added)

### Conti totali per branca di attività economica {#total-accounts-by-industry}

Questo widget visualizza il numero totale di account in una singola metrica e utilizza un grafico ad anello per illustrare le dimensioni proporzionali dei conteggi per i settori che compongono il numero complessivo. La chiave fornisce informazioni sulla codifica dei colori per i diversi settori che compongono il grafico ad anello.

I singoli conteggi per i diversi settori vengono visualizzati in una finestra di dialogo quando il cursore passa sopra la rispettiva sezione del grafico ad anello.

![I conti totali per widget di settore.](../images/account-profiles/total-accounts-by-industry-widget.png)

### Profili account aggiunti {#account-profiles-added}

Questo widget utilizza un grafico a barre con codici a colori per illustrare il conteggio dei profili aggiunti a un account in un determinato periodo di tempo e la proporzione di settori diversi che costituiscono tali profili aggiunti. I settori sono codificati a colori e una chiave fornisce le informazioni sulla codifica dei colori per i diversi settori che compongono il grafico a barre. Il periodo di analisi viene selezionato dal menu a discesa del widget. Il grafico a barre può essere visualizzato in un periodo di 30 giorni, 90 giorni e 12 mesi.

>[!NOTE]
>
>Poiché i profili vengono aggiunti solo a un account e non vengono mai rimossi, il numero più basso possibile di profili aggiunti in un periodo di tempo è zero.

![I profili account hanno aggiunto un widget.](../images/account-profiles/accounts-profiles-added-widget.png)

## Passaggi successivi

Seguendo questo documento è ora possibile individuare il [!UICONTROL Profili account] dashboard. È inoltre necessario comprendere le metriche visualizzate nei widget disponibili. Per ulteriori informazioni sull’utilizzo dei profili account come parte dei dati B2B nell’interfaccia utente di Experience Platform, consulta la sezione [panoramica dei profili account](../../rtcdp/accounts/account-profile-overview.md) per Adobe Real-Time CDP, B2B Edition.
