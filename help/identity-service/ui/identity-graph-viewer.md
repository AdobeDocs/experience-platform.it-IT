---
title: Visualizzatore grafico identità
description: Un grafico delle identità è una mappa delle relazioni tra identità diverse per un particolare cliente, che fornisce una rappresentazione visiva di come il cliente interagisce con il tuo marchio su diversi canali.
exl-id: ccd5f8d8-595b-4636-9191-553214e426bd
source-git-commit: 4bf939011e6246a553f67805ff99a70610782ea6
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 1%

---

# Visualizzatore grafico di identità

Un grafico delle identità è una mappa delle relazioni tra identità diverse per un particolare cliente, che fornisce una rappresentazione visiva di come il cliente interagisce con il tuo marchio su diversi canali. Tutti i grafici dell’identità del cliente vengono gestiti e aggiornati collettivamente da Adobe Experience Platform Identity Service in tempo quasi reale, in risposta all’attività del cliente.

Il visualizzatore del grafico delle identità nell’interfaccia utente di Platform ti consente di visualizzare e comprendere meglio quali sono le identità dei clienti unite e in che modo. Il visualizzatore consente di trascinare e interagire con diverse parti del grafico, consentendoti di esaminare relazioni di identità complesse, eseguire il debug in modo più efficiente e beneficiare di una maggiore trasparenza nell’utilizzo delle informazioni.

Il seguente documento fornisce passaggi su come accedere e utilizzare il visualizzatore grafico delle identità nell’interfaccia utente di Platform.

## Video tutorial

Il video seguente ha lo scopo di supportare la comprensione del visualizzatore grafico dell’identità.

>[!VIDEO](https://video.tv.adobe.com/v/331030/?quality=12&learn=on)

## Introduzione

Lavorare con il visualizzatore grafico dell&#39;identità richiede una comprensione dei vari servizi Adobe Experience Platform coinvolti. Prima di iniziare a lavorare con il visualizzatore grafico delle identità, controlla la documentazione relativa ai seguenti servizi:

- [[!DNL Identity Service]](../home.md): Ottieni una visione migliore dei singoli clienti e del loro comportamento attraverso il collegamento delle identità tra dispositivi e sistemi.
- [Profilo cliente in tempo reale](../../profile/home.md): I grafici di identità vengono utilizzati dal profilo cliente in tempo reale per creare una visualizzazione completa e unica degli attributi e del comportamento del cliente.

### Terminologia

- **Identità (nodo):** Un&#39;identità o un nodo sono dati unici di un&#39;entità, in genere una persona. Un&#39;identità è composta da uno spazio dei nomi dell&#39;identità e un valore di identità. Ad esempio, un&#39;identità completa potrebbe essere costituita da uno spazio dei nomi di identità per **E-mail**, combinato con un valore di identità di **pettirosso<span>@email.com**.
- **Collegamento (bordo):** Un collegamento o un bordo rappresenta la connessione tra le identità. I collegamenti di identità includono proprietà quali le marche temporali stabilite per la prima volta e aggiornate per l’ultima volta. Il primo timestamp stabilito definisce la data e l&#39;ora in cui una nuova identità è collegata a un&#39;identità esistente. L’ultima marca temporale aggiornata definisce la data e l’ora dell’ultimo aggiornamento di un collegamento di identità esistente.
- **Grafico (cluster):** Un grafico o un cluster è un gruppo di identità e collegamenti che rappresentano una persona.

## Accedere al visualizzatore grafico delle identità {#access-identity-graph-viewer}

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Identità]** nella navigazione a sinistra e seleziona **[!UICONTROL Grafico di identità]** dall’elenco delle schede nell’intestazione.

![Area di lavoro Identità nell’interfaccia utente di Experience Platform, con la scheda Grafico identità selezionata.](../images/graph-viewer/identity-graph.png)

Per visualizzare un grafico delle identità, fornisci uno spazio dei nomi delle identità e il relativo valore, quindi seleziona **[!UICONTROL Visualizza]**.

>[!TIP]
>
>Seleziona l’icona della tabella ![icona tabella](../images/identity-graph-viewer/table-icon.png) per visualizzare un pannello con un elenco di tutti i namespace identità disponibili nell’organizzazione. È possibile utilizzare uno qualsiasi dei namespace di identità, purché a essi sia collegato un valore di identità valido. Per ulteriori informazioni, consulta la sezione [guida allo spazio dei nomi identità](../namespaces.md).

![Spazio dei nomi identità e il valore corrispondente, forniti nella schermata di ricerca di Identity Graph.](../images/graph-viewer/namespace-and-value.png)

## Interfaccia del visualizzatore del grafico delle identità

L’interfaccia del visualizzatore del grafico delle identità è composta da diversi elementi con cui puoi interagire e comprendere meglio i tuoi dati di identità.

![Interfaccia del visualizzatore grafico di identità.](../images/graph-viewer/identity-graph-viewer-main.png)

Il grafico identità visualizza tutte le identità collegate allo spazio dei nomi identità e alla combinazione di valori immessa. Ogni nodo è costituito da uno spazio dei nomi identità e dal relativo valore corrispondente. Puoi selezionare, tenere premuto e trascinare qualsiasi nodo per interagire con il grafico. In alternativa, puoi passare il cursore del mouse su un nodo per visualizzare le informazioni sul valore di identità corrispondente. Seleziona **[!UICONTROL Visualizza grafico]** per nascondere o visualizzare il grafico.

>[!IMPORTANT]
>
>Un grafico delle identità richiede la generazione di almeno due identità collegate e una combinazione valida di spazio dei nomi identità e valore. Il numero massimo di identità visualizzabili dal visualizzatore grafico è 150. Consulta la sezione [appendice](#appendix) per ulteriori informazioni, consulta la sezione seguente.

![Il visualizzatore del grafico dell&#39;identità con cinque identità collegate.](../images/graph-viewer/graph.png)

Seleziona un collegamento all’interno del grafico per visualizzare il set di dati e l’ID batch che contribuiscono a tale collegamento. La selezione di un collegamento aggiorna anche la barra a destra per fornire ulteriori informazioni sui dettagli dell’origine dati, nonché proprietà come le marche temporali stabilite per la prima volta e aggiornate.

![Il collegamento di identità tra i nodi e-mail e GAID selezionati.](../images/graph-viewer/identity-link.png)

La [!UICONTROL Identità] La tabella fornisce una visualizzazione diversa dei dati di identità, elencando lo spazio dei nomi identità e la combinazione di valori di identità in un formato tabulare. Quando si seleziona un nodo nel grafico, la riga evidenziata viene aggiornata nella sezione [!UICONTROL Identità] tabella.

![La tabella Identità con l’elenco delle identità collegate all’interno del grafico.](../images/graph-viewer/identities-table.png)

Utilizza il menu a discesa per ordinare tra i dati del grafico ed evidenziare informazioni su uno specifico spazio dei nomi di identità. Ad esempio, seleziona **[!UICONTROL E-mail]** dal menu per visualizzare i dati specifici dello spazio dei nomi dell’identità e-mail.

![Nella tabella Identità vengono visualizzati solo i dati e-mail.](../images/graph-viewer/sort-email.png)

La barra a destra visualizza informazioni su un’identità selezionata, inclusa l’ultima marca temporale aggiornata. La barra a destra visualizza anche informazioni sull’origine dati che corrispondono all’identità selezionata, tra cui l’ID batch, il nome del set di dati, l’ID del set di dati e il nome dello schema.

La tabella seguente fornisce informazioni aggiuntive sulle proprietà dell’origine dati visualizzate nella barra a destra:

| Origine dati | Descrizione |
| --- | --- | 
| ID batch | Identificatore generato automaticamente che corrisponde ai dati batch. |
| ID set di dati | Identificatore generato automaticamente che corrisponde al set di dati. |
| Nome del set di dati | Nome del set di dati che contiene i dati batch. |
| Nome dello schema | Nome dello schema. Lo schema fornisce un set di regole che rappresentano e convalidano la struttura e il formato dei dati. |

![La barra a destra, che visualizza i dati di identità e l’origine dati delle informazioni.](../images/graph-viewer/right-rail.png)

È inoltre possibile utilizzare *[!UICONTROL Origine dati]* per visualizzare un elenco delle origini dati che contribuiscono alle tue identità. Seleziona [!UICONTROL Origine dati] per una visualizzazione tabulare dei set di dati e degli ID batch.

![Scheda dell’origine dati selezionata.](../images/graph-viewer/data-source-table.png)

Utilizza il cursore per filtrare i dati del grafico in base al momento in cui sono state stabilite le identità per la prima volta. Per impostazione predefinita, il visualizzatore del grafico delle identità visualizza tutte le identità collegate all’interno del grafico. Tieni premuto e trascina il cursore per regolare l’ora dell’ultima marca temporale in cui è stata collegata una nuova identità al grafico. Nell’esempio seguente, il grafico mostra che è stato stabilito il collegamento di identità più recente (GAID) su **[!UICONTROL 19/08/2020,:29:29]**.

![Il cursore timestamp del visualizzatore grafico selezionato.](../images/graph-viewer/slider-one.png)

Regola il cursore per vedere che è stato impostato un altro collegamento di identità (E-mail) su **[!UICONTROL 19/08/2020,:25:15:00]**.

![Il cursore della marca temporale del visualizzatore grafico è stato regolato in base all’ultimo nuovo collegamento stabilito.](../images/graph-viewer/slider-two.png)

È inoltre possibile regolare il cursore per visualizzare la prima iterazione del grafico. Nell’esempio seguente, il visualizzatore del grafico di identità mostra che il grafico è stato creato per la prima volta **[!UICONTROL 19/08/2020,:11:16:00]**, con i suoi primi collegamenti ECID, Email e Phone.

![Il cursore della marca temporale del visualizzatore grafico è stato regolato in base al primo nuovo collegamento stabilito.](../images/graph-viewer/slider-three.png)

## Appendice

La sezione seguente fornisce informazioni aggiuntive su come utilizzare il visualizzatore grafico delle identità.

### Informazioni sui messaggi di errore

Possono verificarsi errori quando si accede al visualizzatore grafico dell’identità. Di seguito è riportato un elenco di prerequisiti e limitazioni di cui tenere conto quando si lavora con il visualizzatore grafico dell’identità.

- Un valore di identità deve esistere nello spazio dei nomi selezionato.
- Il visualizzatore del grafico delle identità richiede almeno due identità collegate da generare. È possibile che ci sia un solo valore di identità e nessuna identità collegata, e in questo caso, il valore esisterebbe solo in [!DNL Profile] visualizzatore.
- Il visualizzatore del grafico delle identità non può superare il massimo di 150 identità.

![schermo di errore](../images/graph-viewer/error-screen.png)

### Accedere al visualizzatore del grafico delle identità dai set di dati

Puoi anche accedere al visualizzatore del grafico delle identità utilizzando l’interfaccia set di dati. Dai set di dati [!UICONTROL Sfoglia] , seleziona un set di dati con cui desideri interagire, quindi seleziona **[!UICONTROL Anteprima set di dati]**

![preview-set di dati](../images/identity-graph-viewer/preview-dataset.png)

Dalla finestra di anteprima, seleziona un’icona dell’impronta digitale per visualizzare le identità rappresentate dal visualizzatore grafico dell’identità.

>[!TIP]
>
>L’icona dell’impronta digitale viene visualizzata solo se il set di dati presenta due o più identità.

![impronta digitale](../images/identity-graph-viewer/fingerprint.png)

## Passaggi successivi

Leggendo questo documento, hai imparato a esplorare i grafici di identità dei tuoi clienti nell’interfaccia utente di Platform. Per ulteriori informazioni sulle identità in Platform, consulta la [Panoramica del servizio Identity](../home.md)

## Changelog

| Data | Azione |
| ---- | ------ |
| 2021-01 | <ul><li>È stato aggiunto il supporto per lo streaming di dati acquisiti e sandbox non di produzione.</li><li>Correzioni di bug minori.</li></ul> |
| 2021-02 | <ul><li>Il visualizzatore del grafico di identità è accessibile tramite l’anteprima del set di dati.</li><li>Correzioni di bug minori.</li><li>Il visualizzatore del grafico di identità è reso generalmente disponibile.</li></ul> |
| 2023-01 | <ul><li>Aggiornamenti dell’interfaccia utente.</li></ul> |
