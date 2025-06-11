---
title: Visualizza altro
description: Scopri le diverse opzioni di visualizzazione per i dati analizzati SQL. Dal dashboard personalizzato è possibile visualizzare i risultati tabulati dell’analisi o scaricare i dati elaborati in formato CSV.
exl-id: f57d85cf-dbd2-415c-bf01-8faa49871377
source-git-commit: 87675263b817a2026741d6bdd094010831d6ea28
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 1%

---

# Visualizza altro {#view-more}

Dopo aver creato un [insight personalizzato](./overview.md) utilizzando la [modalità query pro](./overview.md#query-pro-mode), è possibile visualizzare i dati del grafico in più formati. Puoi visualizzare i risultati sotto forma di tabella, esportare i dati in formato CSV o inviare un messaggio e-mail.

## Risultati tabulati {#tabulated-results}

Per ogni grafico creato utilizzando la modalità query pro tramite SQL, puoi visualizzare i risultati tabulati dell’analisi nell’interfaccia utente di Experience Platform.

Dal dashboard personalizzato, selezionare i puntini di sospensione (`...`) in qualsiasi widget per accedere alle opzioni [!UICONTROL Visualizza altro] e [!UICONTROL Visualizza SQL].

![Dashboard personalizzato con menu a discesa dei puntini di sospensione di insight ed evidenziate le opzioni Visualizza altro e Visualizza SQL.](../images/sql-insights-query-pro-mode/ellipses-dropdown.png)

## Esporta {#export}

Dalla finestra di dialogo **[!UICONTROL Visualizza altro]**, esporta i dati della tabella scaricando direttamente un file CSV o inviando un collegamento all&#39;e-mail per il download sicuro in un secondo momento.

>[!IMPORTANT]
>
>Per accedere alle opzioni di esportazione, l&#39;amministratore deve concedere l&#39;autorizzazione **[!UICONTROL Esporta dati dashboard]**. Se il pulsante [!UICONTROL Esporta] è disattivato, contattare l&#39;amministratore. Per ulteriori informazioni sulle autorizzazioni del dashboard, vedere [Panoramica sul controllo degli accessi](../../access-control/home.md).

>[!NOTE]
>
>Le esportazioni di sola visualizzazione non richiedono l&#39;autorizzazione [!UICONTROL Esporta dati dashboard]. Ad esempio, esportando i dati elaborati dalle [informazioni sul dashboard personalizzato in formato PDF](./export-pdf.md) o dalle [informazioni sul dashboard dell&#39;interfaccia utente di Platform](../download.md).

### Scarica CSV {#download-csv}

Nella finestra di dialogo [!UICONTROL Visualizza altro], seleziona **[!UICONTROL Esporta]**, quindi scegli **[!UICONTROL Scarica CSV]** per scaricare i dati del grafico in formato CSV.

>[!NOTE]
>
>Il download del file CSV è limitato ai primi 500 record.

![Una finestra di dialogo che visualizza un&#39;anteprima del tuo insight e i risultati tabulari del tuo SQL che ha generato insight.](../images/sql-insights-query-pro-mode/view-more-download-csv.png)

### Invia come e-mail {#send-as-email}

Per esportare più di 500 record, selezionare **[!UICONTROL Esporta]** e scegliere **[!UICONTROL Invia come messaggio di posta elettronica]** dalla finestra di dialogo [!UICONTROL Esporta file]. Questa opzione invia in modo sicuro un collegamento per il download all’indirizzo e-mail associato ad Adobe. Il nome del destinatario e l&#39;indirizzo e-mail Adobe registrato vengono visualizzati nella sezione [!UICONTROL Destinatari] della finestra di dialogo.

![Visualizza altri dati del grafico con le opzioni Esporta e Invia come messaggio e-mail evidenziate.](../images/sql-insights-query-pro-mode/send-as-email.png)

Dopo aver selezionato [!UICONTROL Invia come messaggio e-mail], Adobe genera un rapporto e invia un&#39;e-mail al tuo indirizzo Adobe registrato. L’e-mail include un collegamento sicuro per il download che richiede l’autenticazione tramite Experience Platform.

>[!NOTE]
>
>È necessario scaricare il rapporto entro 24 ore dalla generazione del collegamento; dopo di che, il file scade.

![Viene visualizzata l&#39;interfaccia utente di Experience Platform con la finestra di dialogo Generazione file riuscita contenente l&#39;opzione Scarica report.](../images/sql-insights-query-pro-mode/download-report.png)

Per proteggere i dati, Adobe ospita in modo sicuro i file esportati anziché inviarli come allegati. Access richiede l’autenticazione tramite l’interfaccia utente di Experience Platform e Adobe verifica che il file sia scaricato solo dal destinatario previsto.

Questo metodo consente di esportare **fino a 10.000 record** e garantisce l&#39;accesso sicuro ai dati sensibili.

## Ordina per colonna {#sort-column}

Quando si visualizzano i risultati tabulati, è possibile utilizzare la funzionalità di ordinamento per colonna in ordine crescente o decrescente. Dal dashboard personalizzato, selezionare i puntini di sospensione (`...`) in qualsiasi tabella per accedere all&#39;opzione [!UICONTROL Visualizza altro].

![Dashboard personalizzato con il menu a discesa dei puntini di sospensione di una tabella ed evidenziata l&#39;opzione Visualizza altro.](../images/sql-insights-query-pro-mode/advanced-ellipses-dropdown.png)

Puoi ordinare le colonne selezionando il menu a discesa accanto al nome della colonna, quindi selezionando **[!UICONTROL Ordine crescente]** o **[!UICONTROL Ordine decrescente]**.

>[!NOTE]
>
>Le opzioni [!UICONTROL Ordinamento crescente] e [!UICONTROL Ordinamento decrescente] verranno visualizzate solo per le colonne configurate con [funzionalità di ordinamento](./overview.md#advanced-attributes).

![Elenco a discesa delle colonne della tabella che mostra le opzioni Ordinamento crescente e Ordinamento decrescente evidenziate.](../images/sql-insights-query-pro-mode/advanced-sort-dropdown.png)

## Ridimensionare una colonna {#resize-column}

Puoi ridimensionare le colonne nei risultati tabulati per migliorare la leggibilità dei dati. Dal dashboard personalizzato, selezionare i puntini di sospensione (`...`) per consentire alla tabella di accedere all&#39;opzione [!UICONTROL Visualizza altro]. Utilizza il menu a discesa accanto al nome della colonna per ridimensionarla, quindi seleziona **[!UICONTROL Ridimensiona colonna]**.

![Elenco a discesa delle colonne della tabella che mostra l&#39;opzione Ridimensiona colonna evidenziata.](../images/sql-insights-query-pro-mode/advanced-resize-dropdown.png)

Seleziona il dispositivo di scorrimento e trascina verso sinistra o destra per regolare la dimensione della colonna in base alle esigenze.

![Tabella in cui è evidenziata la barra di ridimensionamento colonne.](../images/sql-insights-query-pro-mode/advanced-resize-column.png)

## Paginazione tabella {#table-pagination}

La paginazione viene applicata automaticamente alle tabelle nella funzionalità [!UICONTROL Visualizza altro], eliminando la necessità di modificare manualmente le query SQL. Questa funzione garantisce che i dati vengano presentati in un formato più gestibile, facilitando il processo di navigazione tra set di dati di grandi dimensioni.

È possibile visualizzare fino a 500 record per pagina. Per spostarsi tra i record, utilizzare **[!UICONTROL >]** situato nella parte inferiore della pagina.

![Risultati tabulati con risultati e impaginazione evidenziati.](../images/sql-insights-query-pro-mode/advanced-table-pagination.png)

## Passaggi successivi

Dopo aver letto questo documento, ora sai come visualizzare i risultati tabulati dall’analisi SQL del grafico personalizzato e come esportare tali dati in modo sicuro. Per informazioni su come [visualizzare le istruzioni SQL alla base delle tue informazioni personalizzate](./view-sql.md), consulta il documento Visualizza SQL.

Puoi anche imparare a generare grafici dai modelli di dati esistenti nell&#39;interfaccia utente di Adobe Experience Platform con la [guida guidata alla modalità di progettazione](../standard-dashboards.md).
