---
keywords: Experience Platform;home;popular topics;identity graph viewer;Identity graph viewer;graph viewer;Graph viewer;identity namespace;Identity namespace;identity;Identity;Identity service;identity service
solution: Experience Platform
title: Servizio Adobe Experience Platform Identity
topic: tutorial
description: Un grafico di identità è una mappa delle relazioni tra identità diverse per un particolare cliente, che fornisce una rappresentazione visiva del modo in cui il cliente interagisce con il proprio marchio tra canali diversi.
translation-type: tm+mt
source-git-commit: ef1025dfacc91b13c064db99e6304f2c09abb3d9
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 1%

---


# (Beta) Visualizzatore grafico identità

>[!NOTE]
>
>Il visualizzatore del grafico dell&#39;identità è attualmente in versione beta. Le sue caratteristiche sono soggette a modifiche.

Un grafico di identità è una mappa delle relazioni tra identità diverse per un particolare cliente, che fornisce una rappresentazione visiva del modo in cui il cliente interagisce con il proprio marchio tra canali diversi. Tutti i grafici dell&#39;identità del cliente vengono gestiti e aggiornati collettivamente da Adobe Experience Platform Identity Service in tempo quasi reale, in risposta all&#39;attività del cliente.

Il visualizzatore grafico dell&#39;identità nell&#39;interfaccia utente della piattaforma consente di visualizzare e capire meglio le identità dei clienti unite e in che modo. Il visualizzatore consente di trascinare e interagire con diverse parti del grafico, consentendo di esaminare complesse relazioni di identità, eseguire il debug in modo più efficiente e sfruttare una maggiore trasparenza con il modo in cui vengono utilizzate le informazioni.

## Introduzione

Per utilizzare il visualizzatore grafico dell&#39;identità è necessario conoscere i diversi servizi Adobe Experience Platform coinvolti. Prima di iniziare a lavorare con il visualizzatore grafico dell&#39;identità, consulta la documentazione relativa ai seguenti servizi:

- [[!DNL Identity Service]](../home.md): Ottenete una visione migliore dei singoli clienti e del loro comportamento, collegando le identità tra dispositivi e sistemi.

### Terminologia

- **Identità (nodo):** Un&#39;identità o un nodo è un dato univoco per un&#39;entità, in genere una persona. Un&#39;identità è composta da uno spazio dei nomi e un valore di identità.
- **Collegamento (bordo):** Un collegamento o un bordo rappresenta la connessione tra le identità.
- **Grafico (cluster):** Un grafico o un cluster è un gruppo di identità e collegamenti che rappresentano una persona.

## Accesso al visualizzatore del grafico dell&#39;identità

Per utilizzare il visualizzatore grafico dell&#39;identità nell&#39;interfaccia utente, selezionate **[!UICONTROL Identities]** nel menu di navigazione a sinistra, quindi selezionate la **[!UICONTROL Identity graph]** scheda. Dalla **[!UICONTROL Identity Namespace]** schermata, fate clic sull&#39; **[!UICONTROL Select identity namespace]** icona per cercare lo spazio nomi che intendete utilizzare.

![namespace-screen](../images/identity-graph-viewer/identity-namespace.png)

Viene visualizzato il **[!UICONTROL Select identity namespace]** pannello. Questa schermata contiene un elenco di spazi dei nomi disponibili per l&#39;organizzazione, con informazioni su uno spazio dei nomi **[!UICONTROL Display name]**, **[!UICONTROL Identity symbol]**, **[!UICONTROL Owner]**, **[!UICONTROL Last updated]** data e **[!UICONTROL Description]**. È possibile utilizzare uno qualsiasi degli spazi dei nomi forniti a condizione che vi sia collegato un valore di identità valido.

Selezionate lo spazio nomi che intendete utilizzare e fate clic **[!UICONTROL Select]** per continuare.

![select-identity-namespace](../images/identity-graph-viewer/select-identity-namespace.png)

Dopo aver selezionato uno spazio nomi, immettete il valore corrispondente per un cliente specifico nella **[!UICONTROL Identity value]** casella di testo e selezionate **[!UICONTROL View]**.

![add-identity-value](../images/identity-graph-viewer/identity-value-filled.png)

Viene visualizzato il visualizzatore del grafico dell&#39;identità. Sul lato sinistro dello schermo è riportato il grafico dell&#39;identità che visualizza tutte le identità collegate allo spazio dei nomi selezionato e il valore dell&#39;identità immesso. Ogni nodo di identità è costituito da uno spazio dei nomi e dal valore ID corrispondente. Potete selezionare e mantenere qualsiasi identità da trascinare e interagire con il grafico. In alternativa, puoi passare il puntatore del mouse su un&#39;identità per visualizzare informazioni sul suo valore ID. L’output del grafico viene visualizzato anche come elenco al centro dello schermo.

>[!IMPORTANT]
>
>Un grafico dell&#39;identità richiede la generazione di almeno due identità collegate, nonché una coppia di nomi e ID valida. Il numero massimo di identità visualizzabili dal visualizzatore grafico è 400. Per ulteriori informazioni, consulta la sezione [appendice](#appendix) seguente.

![identity-graph](../images/identity-graph-viewer/graph-viewer.png)

Selezionare un&#39;identità per aggiornare la riga evidenziata nella **[!UICONTROL Identities]** tabella e per aggiornare le informazioni fornite nella barra a destra, che include l&#39;identità **[!UICONTROL Value]**, **[!UICONTROL Batch ID]** e la relativa **[!UICONTROL Last updated]** data.

![select-identity](../images/identity-graph-viewer/select-identity.png)

Potete filtrare attraverso un grafico e isolare uno specifico spazio nomi utilizzando l&#39;opzione di ordinamento nella parte superiore della **[!UICONTROL Identities]** tabella. Dal menu a discesa, selezionate lo spazio nomi da evidenziare.

![filter-by-namespace](../images/identity-graph-viewer/filter-namespace.png)

Il visualizzatore grafico restituisce un valore che evidenzia lo spazio nomi selezionato. L&#39;opzione del filtro aggiorna inoltre la **[!UICONTROL Identities]** tabella in modo da restituire informazioni solo per lo spazio dei nomi selezionato.

![filtrato](../images/identity-graph-viewer/filtered.png)

L’angolo superiore destro della casella del visualizzatore grafico contiene le opzioni per l’ingrandimento. Selezionate l’icona **(+)** per ingrandire il grafico oppure l’icona **(-)** per ridurre lo zoom.

![zoom](../images/identity-graph-viewer/zoom.png)

Per visualizzare ulteriori informazioni sui batch, selezionateli **[!UICONTROL Data source]** dall’intestazione. Nella **[!UICONTROL Data source]** tabella è visualizzato un elenco di **[!UICONTROL Batch IDs]** elementi associati al grafico, nonché il relativo **[!UICONTROL Linked IDs]**, schema di origine e data di inserimento.

![data-source](../images/identity-graph-viewer/data-source-table.png)

Potete selezionare uno qualsiasi dei collegamenti all&#39;interno di un grafico di identità per visualizzare tutti i batch di origine che hanno contribuito al collegamento.

![select-links](../images/identity-graph-viewer/select-edge.png)

In alternativa, potete selezionare un batch per visualizzare tutti i collegamenti a cui ha contribuito questo batch.

![select-links](../images/identity-graph-viewer/select-batch.png)

I grafici di identità con cluster di identità più grandi sono accessibili anche tramite il visualizzatore grafico di identità.

![grande cluster](../images/identity-graph-viewer/large-cluster.png)

## Appendice

La sezione seguente contiene informazioni aggiuntive sull’utilizzo del visualizzatore grafico dell’identità.

### Informazioni sui messaggi di errore

Gli errori possono verificarsi quando si accede al visualizzatore del grafico dell&#39;identità. Di seguito è riportato un elenco di prerequisiti e limitazioni di cui tenere conto quando si utilizza il visualizzatore grafico dell’identità.

- Un valore di identità deve esistere nello spazio nomi selezionato.
- Il visualizzatore del grafico dell&#39;identità richiede almeno due identità collegate da generare.
- Il visualizzatore grafico dell&#39;identità non può superare il massimo di 400 identità.
- Il visualizzatore del grafico dell&#39;identità non è attualmente accessibile nelle sandbox non di produzione.
- Il visualizzatore del grafico dell&#39;identità al momento supporta solo i dati acquisiti in batch e non visualizza i dati acquisiti utilizzando le origini di streaming.

![error-screen](../images/identity-graph-viewer/error-screen.png)

## Passaggi successivi

Leggendo questo documento, hai imparato a esplorare i grafici di identità dei clienti nell&#39;interfaccia utente della piattaforma. Per ulteriori informazioni sulle identità in Piattaforma, consulta la panoramica del Servizio [identità](../home.md)