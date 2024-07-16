---
title: Integrazione del registro di controllo di Query Service
description: I registri di audit di Query Service conservano i record relativi a varie azioni dell’utente per formare un audit trail per la risoluzione dei problemi o il rispetto delle politiche aziendali di gestione dei dati e dei requisiti normativi. Questa esercitazione fornisce una panoramica delle funzioni del registro di controllo specifiche di Query Service.
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 1%

---

# Integrazione del registro di controllo di [!DNL Query Service]

L&#39;integrazione del registro di controllo di Adobe Experience Platform [!DNL Query Service] fornisce record delle azioni utente correlate alle query. I registri di audit sono uno strumento essenziale per la risoluzione dei problemi e il rispetto delle politiche aziendali di gestione dei dati e dei requisiti normativi. La funzionalità ti consente di restituire un registro delle azioni per molti tipi di eventi, nonché di filtrare ed esportare i record. È possibile accedere ai registri tramite l&#39;interfaccia utente di Platform o l&#39;[API di query di controllo](https://www.adobe.io/experience-platform-apis/references/audit-query/) e scaricarli in formato CSV o JSON.

Per ulteriori informazioni sull&#39;interfaccia utente dei registri di controllo, consulta il [documento di panoramica dei registri di controllo](../../landing/governance-privacy-security/audit-logs/overview.md). Per ulteriori informazioni sull&#39;esecuzione di chiamate alle API di Platform, consulta la [guida dell&#39;API dei registri di controllo](../../landing/api-guide.md).

## Prerequisiti

Per visualizzare il dashboard del registro di controllo nell&#39;interfaccia utente di Platform, è necessario che sia abilitata l&#39;autorizzazione [!DNL Data Governance] [!UICONTROL Visualizza registro attività utente]. L&#39;autorizzazione è abilitata tramite l&#39;Adobe [Admin Console](https://adminconsole.adobe.com/). Se non disponi dei privilegi di amministratore per abilitare questa autorizzazione, contatta l’amministratore della tua organizzazione. Consulta la documentazione sul controllo degli accessi per [istruzioni complete sull&#39;aggiunta di autorizzazioni tramite Admin Console](../../access-control/home.md).

## [!DNL Query Service] categorie del registro di controllo {#audit-log-categories}

Le categorie del registro di controllo fornite da [!DNL Query Service] sono le seguenti.

| Categoria | Descrizione |
|---|---|
| [!UICONTROL Query] | Questa categoria consente di controllare le esecuzioni delle query. |
| [!UICONTROL Modello query] | Questa categoria consente di controllare le varie azioni (creazione, aggiornamento ed eliminazione) eseguite su un modello di query. |
| [!UICONTROL Query pianificata] | Questa categoria consente di controllare le pianificazioni create, aggiornate o eliminate in [!DNL Query Service]. |

## Esegui un registro di controllo [!DNL Query Service] {#perform-an-audit-log}

Per eseguire un controllo di audit per le attività [!DNL Query Service], seleziona **[!UICONTROL Audit]** dal menu di navigazione a sinistra, seguito dall&#39;icona funnel (![Icona filtro.](../images/audit-log/filter.png)) per visualizzare un elenco di controlli filtro per limitare i risultati.

![Dashboard del registro di controllo dell&#39;interfaccia utente di Platform con &quot;Audits&quot; nella navigazione a sinistra e controlli filtro evidenziati.](../images/audit-log/filter-controls.png)

Dalla scheda [!UICONTROL Audit] della dashboard [!UICONTROL Registro attività], è possibile filtrare tutte le azioni di Platform registrate in base a una qualsiasi delle categorie [!DNL Query Service]. I risultati del registro possono essere ulteriormente filtrati in base al periodo di tempo in cui sono stati eseguiti, all’azione/funzione intrapresa o all’utente che ha eseguito la query. Consulta la documentazione del registro di controllo per [istruzioni complete su come filtrare i registri in base a categoria, azione, utente e stato](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui).

I dati del registro di controllo restituiti contengono le seguenti informazioni su tutte le query che soddisfano i criteri di filtro selezionati.

| Nome colonna | Descrizione |
|---|---|
| [!UICONTROL Timestamp] | Data e ora esatte dell&#39;azione eseguita nel formato `month/day/year hour:minute AM/PM`. |
| [!UICONTROL Nome risorsa] | Il valore del campo [!UICONTROL Nome risorsa] dipende dalla categoria scelta come filtro. Quando si utilizza la categoria [!UICONTROL Query pianificata], si tratta del **nome pianificazione**. Quando si utilizza la categoria [!UICONTROL Modello query], questo è il **nome modello**. Quando si utilizza la categoria [!UICONTROL Query], questo è l&#39;**ID sessione** |
| [!UICONTROL Categoria] | Questo campo corrisponde alla categoria selezionata dall’utente nel menu a discesa del filtro. |
| [!UICONTROL Azione] | Può essere creata, eliminata, aggiornata o eseguita. Le azioni disponibili dipendono dalla categoria scelta come filtro. |
| [!UICONTROL Utente] | Questo campo fornisce l’ID utente che ha eseguito la query. |

![Dashboard dei controlli di audit con il registro attività filtrato evidenziato.](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>Vengono forniti più dettagli sulle query scaricando i risultati del registro in formato CSV o JSON di quanti ne vengano visualizzati per impostazione predefinita nel dashboard del registro di controllo.

## Pannello Dettagli

Seleziona una riga di risultati del registro di controllo per aprire un pannello dei dettagli a destra dello schermo.

![Controlla la scheda del registro attività della dashboard con il pannello dei dettagli evidenziato.](../images/audit-log/details-panel.png)

Il pannello dei dettagli può essere utilizzato per trovare l&#39;[!UICONTROL ID risorsa] e lo [!UICONTROL stato evento].

Il valore di [!UICONTROL ID risorsa] varia a seconda della categoria utilizzata nel controllo di audit.

* Quando si utilizza la categoria [!UICONTROL Query], [!UICONTROL ID risorsa] è l&#39;**ID sessione**.
* Quando si utilizza la categoria [!UICONTROL Modello di query], l&#39;[!UICONTROL ID risorsa] è il **ID modello** con prefisso `[!UICONTROL templateID:]`.
* Quando si utilizza la categoria [!UICONTROL Query pianificata], l&#39;[!UICONTROL ID risorsa] è l&#39;**ID pianificazione** con prefisso `[!UICONTROL scheduleID:]`.

Il valore dello stato [!UICONTROL Evento] cambia a seconda della categoria utilizzata nel controllo di audit.

* Quando si utilizza la categoria [!UICONTROL Query], il campo [!UICONTROL Stato evento] fornisce un elenco di tutti i **ID query** eseguiti dall&#39;utente in quella sessione.
* Quando si utilizza la categoria [!UICONTROL Modello query], il campo [!UICONTROL Stato evento] fornisce il nome **modello** come prefisso per lo stato dell&#39;evento.
* Quando si utilizza la categoria [!UICONTROL Pianificazione query], il campo [!UICONTROL Stato evento] fornisce il **nome pianificazione** come prefisso per lo stato dell&#39;evento.

## Filtri disponibili per [!DNL Query Service] categorie di log di controllo {#available-filters}

I filtri disponibili variano a seconda della categoria selezionata nel menu a discesa. La tabella seguente descrive i filtri disponibili per [[!DNL Query Service] categorie di log di controllo](#audit-log-categories).

| Filtro | Descrizione |
|---|---|
| Categoria | Consulta la sezione [[!DNL Query Service] categorie del registro di controllo](#audit-log-categories) per un elenco completo delle categorie disponibili. |
| Azione | Quando si fa riferimento a [!DNL Query Service] categorie di controllo, l&#39;aggiornamento è una **modifica al modulo esistente**, l&#39;eliminazione è la **rimozione della pianificazione o del modello**, la creazione è **creazione di una nuova pianificazione o modello** ed esecuzione è **esecuzione di una query**. |
| Utente | Immetti l’ID utente completo (ad esempio, johndoe@acme.com) da filtrare per utente. |
| Stato | Le opzioni [!UICONTROL Consenti], [!UICONTROL Operazione completata] e [!UICONTROL Errore] filtrano i registri in base allo &quot;Stato&quot; o allo &quot;Stato evento&quot;, mentre l&#39;opzione [!UICONTROL Nega] filtrerà **tutti** i registri. |
| Data | Seleziona una data di inizio e/o una data di fine per definire un intervallo di date in base al quale filtrare i risultati. |

## Passaggi successivi

La lettura di questo documento consente di comprendere meglio la funzionalità del registro di controllo di [!DNL Query Service] e come può essere utilizzata per filtrare le azioni utente di [!DNL Query Service].

Se si utilizza la funzionalità del registro di controllo di [!DNL Query Service] per la risoluzione dei problemi, si consiglia di leggere la [guida alla risoluzione dei problemi](../troubleshooting-guide.md).
