---
title: Strumenti sandbox
description: Esporta e importa facilmente le configurazioni Sandbox tra sandbox.
source-git-commit: 900cb35f6cb758f145904666c709c60dc760eff2
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 8%

---


# [!BADGE Beta] Strumenti sandbox

>[!IMPORTANT]
>
>Il **Strumenti sandbox** La funzione descritta di seguito è disponibile solo per alcuni clienti beta.

>[!NOTE]
>
>Gli strumenti sandbox sono una funzionalità fondamentale che supporta sia [!DNL Real-Time Customer Data Platform] e [!DNL Journey Optimizer] per migliorare l&#39;efficienza del ciclo di sviluppo e la precisione della configurazione.<br><br>Per utilizzare la funzione strumenti sandbox, è necessario disporre delle due autorizzazioni di controllo dell&#39;accesso basate sul ruolo seguenti:<br>- `manage-sandbox` o `view-sandbox`<br>- `manage-package`

Migliora la precisione della configurazione nelle sandbox ed esporta e importa facilmente le configurazioni sandbox tra sandbox con la funzione di strumenti sandbox. Utilizza gli strumenti sandbox per ridurre il time-to-value per il processo di implementazione e spostare le configurazioni corrette tra le sandbox.

È possibile utilizzare la funzione degli strumenti sandbox per selezionare oggetti diversi ed esportarli in un pacchetto. Un pacchetto può essere costituito da un singolo oggetto, più oggetti o un’intera sandbox. Tutti gli oggetti inclusi in un pacchetto devono appartenere alla stessa sandbox.

## Oggetti supportati per gli strumenti sandbox {#supported-objects}

Nella tabella seguente sono elencati gli oggetti attualmente supportati per gli strumenti sandbox:

| Piattaforma | Oggetto |
| --- | --- |
| [!DNL Adobe Journey Optimizer] | Percorsi |
| Customer Data Platform | Origini |
| Customer Data Platform | Segmenti |
| Customer Data Platform | Identità |
| Customer Data Platform | Criteri |
| Customer Data Platform | Schemi |
| Customer Data Platform | Set di dati |

I seguenti oggetti vengono importati ma sono in stato di bozza o disabilitato:

| Funzione | Oggetto | Stato |
| --- | --- | --- |
| Stato importazione | Flusso di dati di origine | Bozza |
| Stato importazione | Percorso | Bozza |
| Profilo unificato | Schema | Disabilitata |
| Profilo unificato | Set di dati | Disabilitata |
| Criteri | Criteri di consenso | Disabilitata |
| Criteri | Criteri di governance dei dati | Disabilitata |

I casi edge elencati di seguito non sono inclusi nella confezione:

* Relazioni tra gli schemi

## Esportare oggetti in un pacchetto {#export-objects}

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_exit_package"
>title="Salva ed esci dal pacchetto"
>abstract="Per uscire dal pacchetto e salvare, gli utenti possono semplicemente utilizzare l’opzione Indietro."

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_remove_object"
>title="Rimuovere un oggetto"
>abstract="L’utente deve selezionare la riga e quindi utilizzare l’opzione Elimina (disponibile al momento della selezione) per rimuoverla."

>[!CONTEXTUALHELP]
>id="platform_sandbox_package_expiry"
>title="Impostazioni di scadenza pacchetto"
>abstract="La data è impostata per 90 giorni a partire da oggi. Questa data continua a cambiare fino alla pubblicazione del pacchetto. Se un utente visita il pacchetto in stato di bozza domani, la data viene spostata di +1 giorno (a meno che non sia stata impostata dall’utente)."

>[!CONTEXTUALHELP]
>id="platform_sandbox_tooling_package_status"
>title="Stato pacchetto"
>abstract="Per impostazione predefinita, lo stato è impostato su bozza. Dopo la pubblicazione del pacchetto, lo stato viene modificato in pubblicato. Non è possibile apportare modifiche dopo la pubblicazione del pacchetto."

>[!NOTE]
>
>È possibile importare un pacchetto solo se si dispone dell&#39;autorizzazione per accedere agli oggetti.

Questo esempio documenta il processo di esportazione di uno schema e di aggiunta a un pacchetto. È possibile utilizzare lo stesso processo per esportare altri oggetti, ad esempio set di dati, percorsi e molto altro.

### Aggiungi oggetto a un nuovo pacchetto {#add-object-to-new-package}

Seleziona **[!UICONTROL Schemi]** dal menu di navigazione a sinistra, quindi seleziona la **[!UICONTROL Sfoglia]** , in cui sono elencati gli schemi disponibili. Quindi, seleziona i puntini di sospensione (`...`) accanto allo schema selezionato, e un menu a discesa visualizza i controlli. Seleziona **[!UICONTROL Aggiungi al pacchetto]** dal menu a discesa.

![Elenco di schemi che mostrano il menu a discesa che evidenzia [!UICONTROL Aggiungi al pacchetto] controllo.](../images/ui/sandbox-tooling/add-to-package.png)

Dalla sezione **[!UICONTROL Aggiungi al pacchetto]** , seleziona la **[!UICONTROL Crea nuovo pacchetto]** opzione. Fornisci un [!UICONTROL Nome] per il pacchetto e un&#39;opzione [!UICONTROL Descrizione], quindi seleziona **[!UICONTROL Aggiungi]**.

![Il [!UICONTROL Aggiungi al pacchetto] dialogo con [!UICONTROL Crea nuovo pacchetto] selezionato ed evidenziazione [!UICONTROL Aggiungi].](../images/ui/sandbox-tooling/create-new-package.png)

Viene visualizzata di nuovo la **[!UICONTROL Schemi]** ambiente. È ora possibile aggiungere altri oggetti al pacchetto creato seguendo i passaggi successivi elencati di seguito.

### Aggiungere un oggetto a un pacchetto esistente e pubblicarlo {#add-object-to-existing-package}

Per visualizzare un elenco degli schemi disponibili, seleziona **[!UICONTROL Schemi]** dal menu di navigazione a sinistra, quindi seleziona la **[!UICONTROL Sfoglia]** scheda. Quindi, seleziona i puntini di sospensione (`...`) accanto allo schema selezionato per visualizzare le opzioni di controllo in un menu a discesa. Seleziona **[!UICONTROL Aggiungi al pacchetto]** dal menu a discesa.

![Elenco di schemi che mostrano il menu a discesa che evidenzia [!UICONTROL Aggiungi al pacchetto] controllo.](../images/ui/sandbox-tooling/add-to-package.png)

Il **[!UICONTROL Aggiungi al pacchetto]** viene visualizzata. Seleziona la **[!UICONTROL Pacchetto esistente]** , quindi selezionare **[!UICONTROL Nome pacchetto]** e selezionare il pacchetto richiesto. Infine, seleziona **[!UICONTROL Aggiungi]** per confermare le scelte effettuate.

![[!UICONTROL Aggiungi al pacchetto] , visualizzando un pacchetto selezionato dal menu a discesa.](../images/ui/sandbox-tooling/add-to-existing-package.png)

Viene elencato l&#39;elenco degli oggetti aggiunti al pacchetto. Per pubblicare il pacchetto e renderlo disponibile per l’importazione in sandbox, seleziona **[!UICONTROL Pubblica]**.

![Un elenco di oggetti nel pacchetto, che evidenzia [!UICONTROL Pubblica] opzione.](../images/ui/sandbox-tooling/publish-package.png)

Seleziona **[!UICONTROL Pubblica]** per confermare la pubblicazione del pacchetto.

![Finestra di conferma della pubblicazione del pacchetto, con evidenziazione [!UICONTROL Pubblica] opzione.](../images/ui/sandbox-tooling/publish-package-confirmation.png)

>[!NOTE]
>
>Una volta pubblicato, il contenuto del pacchetto non può essere modificato. Per evitare problemi di compatibilità, accertati che siano state selezionate tutte le risorse necessarie. Se è necessario apportare modifiche, è necessario creare un nuovo pacchetto.

Viene visualizzata di nuovo la **[!UICONTROL Pacchetti]** scheda in [!UICONTROL Sandbox] ambiente, in cui puoi visualizzare il nuovo pacchetto pubblicato.

![Elenco dei pacchetti sandbox che evidenziano il nuovo pacchetto pubblicato.](../images/ui/sandbox-tooling/published-packages.png)

## Importare un pacchetto in una sandbox di destinazione {#import-package-to-target-sandbox}

Per importare il pacchetto in una sandbox di destinazione, passa a Sandbox **[!UICONTROL Sfoglia]** e seleziona l’opzione più (+) accanto al nome della sandbox.

![Le sandbox **[!UICONTROL Sfoglia]** evidenziare la selezione del pacchetto di importazione.](../images/ui/sandbox-tooling/browse-sandboxes.png)

Utilizzando il menu a discesa, seleziona la **[!UICONTROL Nome pacchetto]** desideri importare nella sandbox di destinazione. Aggiungi un elemento **[!UICONTROL Nome processo]**, che verrà utilizzato per il monitoraggio futuro, quindi seleziona **[!UICONTROL Successivo]**.

![La pagina dei dettagli di importazione che mostra [!UICONTROL Nome pacchetto] selezione a discesa](../images/ui/sandbox-tooling/import-package-to-sandbox.png)

Il [!UICONTROL Oggetto pacchetto e dipendenze] fornisce un elenco di tutte le risorse incluse in questo pacchetto. Il sistema rileva automaticamente gli oggetti dipendenti necessari per la corretta importazione degli oggetti padre selezionati.

![Il [!UICONTROL Oggetto pacchetto e dipendenze] mostra un elenco di risorse incluse nel pacchetto.](../images/ui/sandbox-tooling/package-objects-and-dependencies.png)

>[!NOTE]
>
>Gli oggetti dipendenti possono essere sostituiti con quelli esistenti nella sandbox di destinazione, consentendo di riutilizzare gli oggetti esistenti anziché creare una nuova versione. Ad esempio, quando importi un pacchetto che include schemi, puoi riutilizzare gli spazi dei nomi dei gruppi di campi personalizzati e delle identità esistenti nella sandbox di destinazione. In alternativa, quando importi un pacchetto che include Percorsi, puoi riutilizzare i segmenti esistenti nella sandbox di destinazione.

Per utilizzare un oggetto esistente, selezionare l&#39;icona della matita accanto all&#39;oggetto dipendente. Vengono visualizzate le opzioni per creare nuovi o utilizzare quelli esistenti. Seleziona **[!UICONTROL Usa esistente]**.

![Il [!UICONTROL Oggetto pacchetto e dipendenze] pagina che mostra le opzioni oggetto dipendente [!UICONTROL Crea nuovo] e [!UICONTROL Usa esistente].](../images/ui/sandbox-tooling/use-existing-object.png)

Il **[!UICONTROL Gruppo di campi]** mostra un elenco di gruppi di campi disponibili per l’oggetto. Seleziona i gruppi di campi richiesti, quindi seleziona **[!UICONTROL Salva]**.

![Un elenco di campi visualizzati sul [!UICONTROL Gruppo di campi] , evidenziando [!UICONTROL Salva] selezione. ](../images/ui/sandbox-tooling/field-group-list.png)

Viene visualizzata di nuovo la [!UICONTROL Oggetto pacchetto e dipendenze] pagina. Da qui, seleziona **[!UICONTROL Fine]** per completare l&#39;importazione del pacchetto.

![Il [!UICONTROL Oggetto pacchetto e dipendenze] mostra un elenco delle risorse incluse nel pacchetto, evidenziando [!UICONTROL Fine].](../images/ui/sandbox-tooling/finish-object-dependencies.png)

## Esportare e importare un’intera sandbox

### Esportare un’intera sandbox {#export-entire-sandbox}

Per esportare un’intera sandbox, passa a [!UICONTROL Sandbox] **[!UICONTROL Pacchetti]** e seleziona **[!UICONTROL Crea pacchetto]**.

![Il [!UICONTROL Sandbox] **[!UICONTROL Pacchetti]** evidenziazione scheda [!UICONTROL Crea pacchetto].](../images/ui/sandbox-tooling/create-sandbox-package.png)

Seleziona **[!UICONTROL Intera sandbox]** per il tipo di pacchetto nel [!UICONTROL Crea pacchetto] . Fornisci un [!UICONTROL Nome pacchetto] per il pacchetto e selezionare **[!UICONTROL Sandbox]** dal menu a discesa. Infine, seleziona **[!UICONTROL Crea]** per confermare i dati immessi.

![Il [!UICONTROL Crea pacchetto] finestra di dialogo che mostra i campi completati ed evidenzia [!UICONTROL Crea].](../images/ui/sandbox-tooling/create-package-dialog.png)

Il pacchetto è stato creato correttamente, seleziona **[!UICONTROL Pubblica]** per pubblicare il pacchetto.

![Elenco dei pacchetti sandbox che evidenziano il nuovo pacchetto pubblicato.](../images/ui/sandbox-tooling/publish-entire-sandbox-packages.png)

Viene visualizzata di nuovo la **[!UICONTROL Pacchetti]** scheda in [!UICONTROL Sandbox] ambiente, in cui puoi visualizzare il nuovo pacchetto pubblicato.

### Importare l’intero pacchetto sandbox {#import-entire-sandbox-package}

Per importare il pacchetto in una sandbox di destinazione, passa a [!UICONTROL Sandbox] **[!UICONTROL Sfoglia]** e seleziona l’opzione più (+) accanto al nome della sandbox.

![Le sandbox **[!UICONTROL Sfoglia]** evidenziare la selezione del pacchetto di importazione.](../images/ui/sandbox-tooling/browse-entire-package-sandboxes.png)

Utilizzando il menu a discesa, seleziona la sandbox completa utilizzando **[!UICONTROL Nome pacchetto]** a discesa. Aggiungi un elemento **[!UICONTROL Nome processo]**, che verrà utilizzato per il monitoraggio futuro, quindi seleziona **[!UICONTROL Successivo]**.

![La pagina dei dettagli di importazione che mostra [!UICONTROL Nome pacchetto] selezione a discesa](../images/ui/sandbox-tooling/import-full-sandbox-package.png)

>[!NOTE]
>
>Tutti gli oggetti vengono creati come nuovi dal pacchetto quando si importa un’intera sandbox. Gli oggetti non sono elencati nella [!UICONTROL Oggetto pacchetto e dipendenze] , in quanto possono esservi più pagine. Viene visualizzato un messaggio in linea che informa sui tipi di oggetto non supportati.

Sei portato al [!UICONTROL Oggetto pacchetto e dipendenze] pagina in cui è possibile visualizzare il numero di oggetti e dipendenze importati ed esclusi. Da qui, seleziona **[!UICONTROL Importa]** per completare l&#39;importazione del pacchetto.

![Il [!UICONTROL Oggetto pacchetto e dipendenze] mostra il messaggio in linea dei tipi di oggetto non supportati, evidenziando [!UICONTROL Importa].](../images/ui/sandbox-tooling/finish-dependencies-entire-sandbox.png)

## Monitorare i processi di importazione e visualizzare i dettagli degli oggetti di importazione

Per visualizzare gli oggetti e i dettagli importati, passare alla [!UICONTROL Sandbox] **[!UICONTROL Importazioni]** e selezionare il pacchetto dall&#39;elenco. In alternativa, utilizza la barra di ricerca per cercare il pacchetto.

![Le sandbox [!UICONTROL Importazioni] nella scheda viene evidenziata la selezione del pacchetto di importazione.](../images/ui/sandbox-tooling/imports-tab.png)

### Visualizza oggetti importati {#view-imported-objects}

Il giorno **[!UICONTROL Importazioni]** scheda in [!UICONTROL Sandbox] ambiente, seleziona **[!UICONTROL Visualizza oggetti importati]** nel riquadro dei dettagli a destra.

Seleziona **[!UICONTROL Visualizza oggetti importati]** dal riquadro dei dettagli a destra nella **[!UICONTROL Importazioni]** scheda in [!UICONTROL Sandbox] ambiente.

![Le sandbox [!UICONTROL Importazioni] La scheda evidenzia [!UICONTROL Visualizza oggetti importati] nel riquadro di destra.](../images/ui/sandbox-tooling/view-imported-objects.png)

Utilizzare le frecce per espandere gli oggetti e visualizzare l&#39;elenco completo dei campi importati nel pacchetto.

![Le sandbox [!UICONTROL Oggetti importati] visualizzazione di un elenco di oggetti importati nel pacchetto.](../images/ui/sandbox-tooling/expand-imported-objects.png)

### Visualizza dettagli importazione {#view-import-details}

Seleziona **[!UICONTROL Visualizza dettagli importazione]** dal riquadro dei dettagli a destra nella **[!UICONTROL Importazioni]** nell’ambiente Sandbox.

![Le sandbox [!UICONTROL Importazioni] La scheda evidenzia [!UICONTROL Visualizza dettagli importazione] nel riquadro di destra.](../images/ui/sandbox-tooling/view-import-details.png)

Il **[!UICONTROL Dettagli importazione]** mostra una suddivisione dettagliata delle importazioni.

![Il [!UICONTROL Dettagli importazione] finestra di dialogo che mostra una ripartizione dettagliata delle importazioni.](../images/ui/sandbox-tooling/import-details.png)

>[!NOTE]
>
>Al termine di un’importazione, riceverai notifiche nell’interfaccia utente di Platform. Puoi accedere a queste notifiche dall’icona degli avvisi. Se un processo non riesce, puoi passare alla risoluzione dei problemi da qui.

## Passaggi successivi

Questo documento illustra come utilizzare la funzione di strumenti sandbox nell’interfaccia utente di Experienci Platform. Per informazioni sulle sandbox, consulta [guida utente sulle sandbox](../ui/user-guide.md).

Per informazioni su come eseguire diverse operazioni utilizzando l’API Sandbox, consulta [guida per gli sviluppatori sulle sandbox](../api/getting-started.md). Per una panoramica di alto livello delle sandbox in questo Experience Platform, consulta [panoramica della documentazione](../home.md).
