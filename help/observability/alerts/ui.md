---
keywords: Experience Platform;home;argomenti popolari;intervallo date
title: Guida all’interfaccia utente per gli avvisi
description: Scopri come gestire gli avvisi nell’interfaccia utente di Experienci Platform.
feature: Alerts
exl-id: 4ba3ef2b-7394-405e-979d-0e5e1fe676f3
source-git-commit: 8d63e9fa4c7eb09ffb90edca612a6e6d44dd18fa
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# Guida all’interfaccia utente Avvisi

L’interfaccia utente di Adobe Experience Platform consente di visualizzare una cronologia degli avvisi ricevuti in base alle metriche rivelate da Adobe Experience Platform Observability Insights. L’interfaccia utente consente inoltre di visualizzare, abilitare, disabilitare e sottoscrivere le regole di avviso disponibili.

>[!NOTE]
>
>Per un’introduzione agli avvisi in questo Experience Platform, consulta [panoramica degli avvisi](./overview.md).

Per iniziare, seleziona **[!UICONTROL Avvisi]** nel menu di navigazione a sinistra.

![Evidenziazione pagina avvisi [!UICONTROL Avvisi] nel menu di navigazione a sinistra.](../images/alerts/ui/workspace.png)

## Gestire le regole di avviso

Il **[!UICONTROL Sfoglia]** Questa scheda elenca le regole disponibili che possono attivare un avviso.

![Un elenco degli avvisi disponibili viene visualizzato nella sezione [!UICONTROL Sfoglia] scheda.](../images/alerts/ui/rules.png)

Seleziona una regola dall’elenco per visualizzarne la descrizione e i parametri di configurazione nella barra a destra, inclusi soglia e gravità.

![Una regola di avviso evidenziata mostra i dettagli nella barra a destra.](../images/alerts/ui/rule-details.png)

Seleziona i puntini di sospensione (**...**) accanto al nome di una regola e un menu a discesa visualizza i controlli per abilitare o disabilitare l’avviso (a seconda del suo stato corrente) e per abbonarsi o annullare l’abbonamento alle notifiche e-mail per l’avviso.

![I puntini di sospensione selezionati mostrano il menu a discesa.](../images/alerts/ui/disable-subscribe.png)

## Gestire gli abbonati agli avvisi

>[!NOTE]
>
> Per assegnare un avviso a un ID utente Adobe, un indirizzo e-mail esterno o un elenco di gruppi e-mail, devi essere un amministratore.

Il **[!UICONTROL Sfoglia]** Questa scheda elenca le regole disponibili che possono attivare un avviso.

![Un elenco delle regole di avviso disponibili mostrato nella [!UICONTROL Sfoglia] scheda.](../images/alerts/ui/rules.png)

Seleziona i puntini di sospensione (**...**) accanto al nome di una regola, un menu a discesa visualizza i controlli. Seleziona **[!UICONTROL Gestire gli abbonati agli avvisi]**.

![Seleziona i puntini di sospensione per visualizzare il menu a discesa. Il [!UICONTROL Gestire gli abbonati agli avvisi] viene evidenziata.](../images/alerts/ui/manage-alert-subscribers.png)

Il [!UICONTROL Gestire gli abbonati agli avvisi] viene visualizzata. Per assegnare le notifiche a utenti specifici, inserisci il loro ID utente Adobe, l’indirizzo e-mail esterno o un elenco di gruppi e-mail, quindi premi Invio.

>[!NOTE]
>
>Per inviare questa notifica a più utenti contemporaneamente, fornisci un elenco di ID utente o indirizzi e-mail separati da virgole.

![La pagina Gestisci gli abbonati agli avvisi che mostra gli indirizzi e-mail immessi.](../images/alerts/ui/manage-alert-add-email.png)

Gli indirizzi e-mail vengono visualizzati nell’elenco degli abbonati correnti elencati. Seleziona **[!UICONTROL Aggiorna]**.

![La pagina Gestisci abbonati agli avvisi che evidenzia gli abbonati e [!UICONTROL Aggiorna].](../images/alerts/ui/manage-alert-subscribers-added-email.png)

Gli utenti sono stati aggiunti all&#39;elenco di notifiche di avviso. Gli utenti inviati riceveranno notifiche e-mail relative a questo avviso, come illustrato nell’immagine seguente.

![Un esempio di e-mail della notifica di avviso ricevuta.](../images/alerts/ui/manage-alert-subscribers-email.png)

## Abilita avvisi e-mail

Le notifiche degli avvisi possono essere inviate direttamente al tuo indirizzo e-mail.

Seleziona l’icona a forma di campana (![icona campana](../images/alerts/ui/bell-icon.png)) che si trova nella barra multifunzione superiore a destra per visualizzare notifiche e annunci. Nel menu a discesa visualizzato, seleziona l’icona del baricentro (![icona cog](../images/alerts/ui/cog-icon.png)) per accedere alla pagina delle preferenze di Experience Cloud.

![Elenco di avvisi visualizzati che evidenziano l’icona a forma di campana e l’icona a forma di campanello.](../images/alerts/ui/edit-preferences.png)

Il **Profilo** viene visualizzata. Seleziona la **[!UICONTROL Notifiche]** nella barra di navigazione a sinistra per accedere alle preferenze degli avvisi e-mail.

![Evidenziazione della pagina Profilo [!UICONTROL Notifiche] nel menu di navigazione a sinistra.](../images/alerts/ui/profile.png)

Scorri fino a **E-mail** nella parte inferiore della pagina e seleziona **[!UICONTROL Notifiche immediate]**

![La sezione E-mail è evidenziata nella pagina Profilo.](../images/alerts/ui/notifications.png)

Tutti gli avvisi a cui sei abbonato verranno ora inviati all’indirizzo e-mail connesso al tuo account Adobe ID.

## Visualizza cronologia avvisi

Il **[!UICONTROL Cronologia]** La scheda mostra la cronologia degli avvisi ricevuti per l’organizzazione, inclusa la regola che ha attivato l’avviso, la data di attivazione e la data di risoluzione (se applicabile).

![Un elenco degli avvisi ricevuti viene visualizzato in [!UICONTROL Cronologia] scheda.](../images/alerts/ui/history.png)

Seleziona un avviso elencato e nella barra a destra vengono visualizzati ulteriori dettagli, tra cui un breve riepilogo dell’evento che ha attivato l’avviso.

![Un avviso evidenziato mostra i dettagli nella barra a destra.](../images/alerts/ui/history-details.png)

## Passaggi successivi

Questo documento fornisce una panoramica su come visualizzare e gestire gli avvisi nell’interfaccia utente di Platform. Consulta la panoramica su [Observability Insights](../home.md) per ulteriori informazioni sulle funzionalità del servizio.
