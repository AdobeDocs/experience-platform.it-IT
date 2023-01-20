---
title: Integrazione del registro di controllo del servizio query
description: I registri di controllo del servizio query conservano i record per varie azioni dell’utente per creare un audit trail per la risoluzione dei problemi o per rispettare le politiche di gestione dei dati aziendali e i requisiti normativi. Questa esercitazione fornisce una panoramica delle funzioni del registro di controllo specifiche di Query Service.
exl-id: 5fdc649f-3aa1-4337-965f-3f733beafe9d
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 2%

---

# [!DNL Query Service] integrazione del registro di controllo

Adobe Experience Platform [!DNL Query Service] l’integrazione del registro di controllo fornisce record delle azioni utente relative alle query. I registri di controllo sono uno strumento essenziale per la risoluzione dei problemi e il rispetto delle politiche di gestione dei dati aziendali e dei requisiti normativi. La funzionalità ti consente di restituire un registro delle azioni per molti tipi di eventi e di filtrare ed esportare i record. I registri sono accessibili tramite l’interfaccia utente di Platform o [API query di controllo](https://www.adobe.io/experience-platform-apis/references/audit-query/) e scaricato in formato CSV o JSON.

Per ulteriori informazioni sull’interfaccia utente dei registri di controllo, consulta [documento di panoramica dei registri di controllo](../../landing/governance-privacy-security/audit-logs/overview.md). Per ulteriori informazioni sull’esecuzione di chiamate alle API di Platform, consulta [guida API dei registri di controllo](../../landing/api-guide.md).

## Prerequisiti

Devi avere la [!DNL Data Governance] [!UICONTROL Visualizza registro attività utente] autorizzazione abilitata per visualizzare il dashboard del registro di controllo nell’interfaccia utente di Platform. L’autorizzazione viene abilitata tramite l’Adobe [Admin Console](https://adminconsole.adobe.com/). Se non disponi dei privilegi di amministratore per abilitare questa autorizzazione, contatta l’amministratore della tua organizzazione. Consulta la documentazione sul controllo degli accessi per [istruzioni complete sull&#39;aggiunta di autorizzazioni tramite Admin Console](../../access-control/home.md).

## [!DNL Query Service] categorie del registro di controllo {#audit-log-categories}

Le categorie del registro di controllo fornite da [!DNL Query Service] sono le seguenti.

| Categoria | Descrizione |
|---|---|
| [!UICONTROL Query] | Questa categoria ti consente di controllare le esecuzioni delle query. |
| [!UICONTROL Modello di query] | Questa categoria ti consente di controllare le varie azioni (creazione, aggiornamento ed eliminazione) eseguite in un modello di query. |
| [!UICONTROL Query pianificata] | Questa categoria ti consente di controllare le pianificazioni create, aggiornate o eliminate in [!DNL Query Service]. |

## Eseguire un [!DNL Query Service] registro di controllo {#perform-an-audit-log}

Per eseguire un controllo di audit per [!DNL Query Service] attività, seleziona **[!UICONTROL Audit]** dalla navigazione a sinistra, seguita dall’icona funnel (![Icona filtro.](../images/audit-log/filter.png)) per visualizzare un elenco di controlli filtro per limitare i risultati.

![Dashboard del registro di controllo dell’interfaccia utente di Platform con &quot;Audit&quot; nella navigazione a sinistra e i controlli del filtro evidenziati.](../images/audit-log/filter-controls.png)

Da [!UICONTROL Audit] dashboard [!UICONTROL Registro attività] è possibile filtrare tutte le azioni registrate di Platform in base a una delle [!DNL Query Service] categorie. I risultati del registro possono essere ulteriormente filtrati in base al periodo di tempo in cui sono stati eseguiti, all’azione/funzione intrapresa o all’utente che ha eseguito la query. Consulta la documentazione del registro di controllo per [istruzioni complete su come filtrare i registri in base a categoria, azione, utente e stato](../../landing/governance-privacy-security/audit-logs/overview.md#managing-audit-logs-in-the-ui).

I dati del registro di controllo restituiti contengono le seguenti informazioni su tutte le query che soddisfano i criteri di filtro selezionati.

| Nome colonna | Descrizione |
|---|---|
| [!UICONTROL Marca temporale] | Data e ora esatte dell’azione eseguita in un `month/day/year hour:minute AM/PM` formato. |
| [!UICONTROL Nome risorsa] | Il valore per [!UICONTROL Nome risorsa] Il campo dipende dalla categoria selezionata come filtro. Quando utilizzi [!UICONTROL Query pianificata] categoria **nome della pianificazione**. Quando utilizzi [!UICONTROL Modello di query] questa è la categoria **nome modello**. Quando utilizzi [!UICONTROL Query] questa è la categoria **session ID** |
| [!UICONTROL Categoria] | Questo campo corrisponde alla categoria selezionata dall’utente nel menu a discesa del filtro. |
| [!UICONTROL Azione] | Può essere creato, eliminato, aggiornato o eseguito. Le azioni disponibili dipendono dalla categoria selezionata come filtro. |
| [!UICONTROL Utente] | Questo campo fornisce l’ID utente che ha eseguito la query. |

![Il dashboard Audit con il registro attività filtrato evidenziato.](../images/audit-log/filtered-activity.png)

>[!NOTE]
>
>Maggiori dettagli di query vengono forniti scaricando i risultati del registro in formato CSV o JSON, rispetto a quelli visualizzati per impostazione predefinita nel dashboard del registro di controllo.

## Pannello Dettagli

Seleziona una riga di risultati del registro di controllo per aprire un pannello dei dettagli a destra della schermata.

![Controlla la scheda del registro attività del dashboard con il pannello dei dettagli evidenziato.](../images/audit-log/details-panel.png)

Il pannello dei dettagli può essere utilizzato per trovare il [!UICONTROL ID risorsa] e [!UICONTROL Stato dell’evento].

Il valore del [!UICONTROL ID risorsa] cambia a seconda della categoria utilizzata nel controllo di audit.

* Quando utilizzi [!UICONTROL Query] la categoria [!UICONTROL ID risorsa] è  **session ID**.
* Quando utilizzi [!UICONTROL Modello di query] la categoria [!UICONTROL ID risorsa] è **ID modello** e con prefisso `[!UICONTROL templateID:]`.
* Quando utilizzi [!UICONTROL Query pianificata] la categoria [!UICONTROL ID risorsa] è  **ID pianificazione** e con prefisso `[!UICONTROL scheduleID:]`.

Il valore del [!UICONTROL Stato dell’evento] cambia a seconda della categoria utilizzata nel controllo di audit.

* Quando utilizzi [!UICONTROL Query] la categoria [!UICONTROL Stato dell’evento] fornisce un elenco di tutti **ID query** eseguito dall’utente all’interno di tale sessione.
* Quando utilizzi [!UICONTROL Modello di query] la categoria [!UICONTROL Stato dell’evento] fornisce **nome modello** come prefisso per lo stato dell’evento.
* Quando utilizzi [!UICONTROL Pianificazione query] la categoria [!UICONTROL Stato dell’evento] fornisce **nome della pianificazione** come prefisso per lo stato dell’evento.

## Filtri disponibili per [!DNL Query Service] categorie del registro di controllo {#available-filters}

I filtri disponibili variano a seconda della categoria selezionata nel menu a discesa. Nella tabella seguente sono descritti i filtri disponibili per [[!DNL Query Service] categorie del registro di controllo](#audit-log-categories).

| Filtro | Descrizione |
|---|---|
| Categoria | Consulta la sezione [[!DNL Query Service] categorie del registro di controllo](#audit-log-categories) per un elenco completo delle categorie disponibili. |
| Azione | Quando si fa riferimento a [!DNL Query Service] categorie di controllo, l&#39;aggiornamento è un **modifica del modulo esistente**, elimina è **rimozione del programma o del modello**, crea **creazione di una nuova pianificazione o di un nuovo modello** e execute is **esecuzione di una query**. |
| Utente | Immetti l’ID utente completo (ad esempio, johndoe@acme.com) per filtrare in base all’utente. |
| Stato | La [!UICONTROL Consenti], [!UICONTROL Completato]e [!UICONTROL Errore] le opzioni filtrano i registri in base a &quot;Status&quot; o &quot;Event Status&quot;, mentre il [!UICONTROL Nega] l’opzione verrà rimossa **tutto** registri. |
| Data | Seleziona una data di inizio e/o una data di fine per definire un intervallo di date in cui filtrare i risultati. |

## Passaggi successivi

Leggendo questo documento, si ha una migliore comprensione del [!DNL Query Service] la funzionalità di registro di controllo e come può essere utilizzata per filtrare il [!DNL Query Service] azioni dell’utente.

Se utilizzi [!DNL Query Service] per la risoluzione dei problemi, si consiglia di leggere la [guida alla risoluzione dei problemi](../troubleshooting-guide.md).
