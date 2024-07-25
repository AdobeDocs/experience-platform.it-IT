---
keywords: Experience Platform;home;argomenti popolari;intervallo date
title: Guida all’interfaccia utente per gli avvisi
description: Scopri come gestire gli avvisi nell’interfaccia utente di Experience Platform.
feature: Alerts
exl-id: 4ba3ef2b-7394-405e-979d-0e5e1fe676f3
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# Guida all’interfaccia utente Avvisi

L’interfaccia utente di Adobe Experience Platform consente di visualizzare una cronologia degli avvisi ricevuti in base alle metriche rivelate da Adobe Experience Platform Observability Insights. L’interfaccia utente consente inoltre di visualizzare, abilitare, disabilitare e sottoscrivere le regole di avviso disponibili.

>[!NOTE]
>
>Per un&#39;introduzione agli avvisi in Experience Platform, consulta la [panoramica degli avvisi](./overview.md).

Per iniziare, seleziona **[!UICONTROL Avvisi]** nel menu di navigazione a sinistra.

![Pagina Avvisi che evidenzia [!UICONTROL Avvisi] nel menu di navigazione a sinistra.](../images/alerts/ui/workspace.png)

## Gestire le regole di avviso

Nella scheda **[!UICONTROL Sfoglia]** sono elencate le regole disponibili che possono attivare un avviso.

![Nella scheda [!UICONTROL Sfoglia] viene visualizzato un elenco degli avvisi disponibili.](../images/alerts/ui/rules.png)

Seleziona una regola dall’elenco per visualizzarne la descrizione e i parametri di configurazione nella barra a destra, inclusi soglia e gravità.

![Regola di avviso evidenziata con i dettagli nella barra a destra.](../images/alerts/ui/rule-details.png)

Selezionare i puntini di sospensione (**...**) accanto al nome di una regola e un menu a discesa visualizza i controlli per abilitare o disabilitare l&#39;avviso (a seconda dello stato corrente) e per sottoscrivere o annullare l&#39;abbonamento alle notifiche e-mail per l&#39;avviso.

![I puntini di sospensione selezionati mostrano il menu a discesa.](../images/alerts/ui/disable-subscribe.png)

## Gestisci gli iscritti agli avvisi

>[!NOTE]
>
> Per assegnare un avviso a un ID utente Adobe, un indirizzo e-mail esterno o un elenco di gruppi e-mail, devi essere un amministratore.

Nella scheda **[!UICONTROL Sfoglia]** sono elencate le regole disponibili che possono attivare un avviso.

![Elenco delle regole di avviso disponibili visualizzato nella scheda [!UICONTROL Sfoglia].](../images/alerts/ui/rules.png)

Selezionare i puntini di sospensione (**...**) accanto al nome di una regola. In un elenco a discesa vengono visualizzati i controlli. Selezionare **[!UICONTROL Gestisci sottoscrittori avvisi]**.

![Selezionare i puntini di sospensione per visualizzare il menu a discesa. L&#39;opzione [!UICONTROL Gestisci sottoscrittori avvisi] è evidenziata.](../images/alerts/ui/manage-alert-subscribers.png)

Viene visualizzata la pagina [!UICONTROL Gestisci abbonati agli avvisi]. Per assegnare le notifiche a utenti specifici, inserisci il loro ID utente Adobe, l’indirizzo e-mail esterno o un elenco di gruppi e-mail, quindi premi Invio.

>[!NOTE]
>
>Per inviare questa notifica a più utenti contemporaneamente, fornisci un elenco di ID utente o indirizzi e-mail separati da virgole.

![Nella pagina Gestione abbonati agli avvisi sono visualizzati gli indirizzi e-mail immessi.](../images/alerts/ui/manage-alert-add-email.png)

Gli indirizzi e-mail vengono visualizzati nell’elenco degli abbonati correnti elencati. Seleziona **[!UICONTROL Aggiorna]**.

![La pagina Gestisci sottoscrittori avvisi evidenzia i sottoscrittori e [!UICONTROL Aggiorna].](../images/alerts/ui/manage-alert-subscribers-added-email.png)

Gli utenti sono stati aggiunti all&#39;elenco di notifiche di avviso. Gli utenti inviati riceveranno notifiche e-mail relative a questo avviso, come illustrato nell’immagine seguente.

![Esempio di messaggio di posta elettronica della notifica di avviso ricevuta.](../images/alerts/ui/manage-alert-subscribers-email.png)

## Abilita avvisi e-mail

Le notifiche degli avvisi possono essere inviate direttamente al tuo indirizzo e-mail.

Seleziona l&#39;icona a forma di campana (![icona a forma di campana](/help/images/icons/bell.png)) nella barra multifunzione superiore a destra per visualizzare notifiche e annunci. Nel menu a discesa visualizzato, seleziona l&#39;icona cog (![icona cog](/help/images/icons/settings.png)) per accedere alla pagina delle preferenze di Experience Cloud.

![Elenco di avvisi che evidenziano l&#39;icona del campanello e l&#39;icona del barattolo.](../images/alerts/ui/edit-preferences.png)

Viene visualizzata la pagina **Profilo**. Seleziona **[!UICONTROL Notifiche]** nella barra di navigazione a sinistra per accedere alle preferenze degli avvisi e-mail.

![La pagina Profilo evidenzia [!UICONTROL Notifiche] nella navigazione a sinistra.](../images/alerts/ui/profile.png)

Scorri fino alla sezione **E-mail** nella parte inferiore della pagina e seleziona **[!UICONTROL Notifiche istantanee]**

![La sezione E-mail è evidenziata nella pagina Profilo.](../images/alerts/ui/notifications.png)

Tutti gli avvisi a cui sei abbonato verranno ora inviati all’indirizzo e-mail connesso al tuo account Adobe ID.

## Visualizza cronologia avvisi

La scheda **[!UICONTROL Cronologia]** mostra la cronologia degli avvisi ricevuti per l&#39;organizzazione, inclusa la regola che ha attivato l&#39;avviso, la data di attivazione e la data di risoluzione (se applicabile).

![Nella scheda [!UICONTROL Cronologia] viene visualizzato un elenco degli avvisi ricevuti.](../images/alerts/ui/history.png)

Seleziona un avviso elencato e nella barra a destra vengono visualizzati ulteriori dettagli, tra cui un breve riepilogo dell’evento che ha attivato l’avviso.

![Un avviso evidenziato mostra i dettagli nella barra a destra.](../images/alerts/ui/history-details.png)

## Passaggi successivi

Questo documento fornisce una panoramica su come visualizzare e gestire gli avvisi nell’interfaccia utente di Platform. Per ulteriori informazioni sulle funzionalità del servizio, consulta la panoramica su [Observability Insights](../home.md).
