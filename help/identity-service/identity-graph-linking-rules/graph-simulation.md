---
title: Graph Simulation UI Guide
description: Learn how to use the Graph Simulation in the Identity Service UI.
exl-id: 89f0cf6e-c43f-40ec-859a-f3b73a6da8c8
source-git-commit: 7174c2c0d8c4ada8d5bba334492bad396c1cfb34
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 3%

---

# Guida dell&#39;interfaccia utente della [!DNL Graph Simulation] {#graph-simulation}

>[!CONTEXTUALHELP]
>id="platform_identities_graphsimulation"
>title="Simulazione del grafico"
>abstract="Simula grafici per comprendere come il servizio Identity collega le identità e come funziona l’algoritmo di ottimizzazione delle identità."

>[!AVAILABILITY]
>
>* Le regole di collegamento del grafo delle identità sono attualmente a disponibilità limitata. Contatta il team del tuo account Adobe per informazioni su come accedere alla funzione nelle sandbox di sviluppo.
>
>* Per poter accesso il strumento, il account deve avere il **autorizzazione Visualizza Identity [!DNL Graph Simulation] Graph**. Per ulteriori informazioni, leggi la [guida sulle autorizzazioni nel controllo](../../access-control/abac/ui/permissions.md) accesso basato su attributi.

[!DNL Graph Simulation]è un strumento nel servizio Identity interfaccia che è possibile utilizzare per simulare il comportamento di un grafico di identità in base a una particolare combinazione di identità e la modalità di configurazione dell&#39;algoritmo [](./identity-optimization-algorithm.md)di ottimizzazione delle identità.

Per ulteriori informazioni sull&#39;uso dell&#39;interfaccia [!DNL Graph Simulation] nell&#39;area di lavoro interfaccia del servizio Identity, guarda il video seguente:

>[!VIDEO](https://video.tv.adobe.com/v/3444032/?learn=on&enablevpops)

Leggi questo documento per scoprire come utilizzarlo [!DNL Graph Simulation] per comprendere meglio il comportamento del grafico di identità e il funzionamento dell&#39;algoritmo del grafico.

## Impara a conoscere l&#39;interfaccia [!DNL Graph Simulation] {#interface}

Puoi accesso [!DNL Graph Simulation] nella Adobe Experience Platform interfaccia. Seleziona **[!UICONTROL Identità]** dal navigazione sinistro, quindi seleziona **[!UICONTROL Simulazione]** grafico dall&#39;intestazione superiore.

![L&#39;interfaccia di simulazione grafica nel Adobe Experience Platform interfaccia.](../images/graph-simulation/graph-simulation.png)

L&#39;interfaccia [!DNL Graph Simulation] può essere suddivisa in tre sezioni:

>[!BEGINTABS]

>[!TAB Eventi]

Eventi: usa il **[!UICONTROL pannello Eventi]** per aggiungere identità e simulare un grafico. Un&#39;identità completa deve disporre di uno spazio dei nomi identità e del relativo valore di identità. È necessario aggiungere almeno due identità per simulare un grafico. Puoi anche selezionare **[!UICONTROL Esempio]** di caricamento per inserire un evento preconfigurato e una configurazione dell&#39;algoritmo.

![Il pannello Eventi di Graph Simulation strumento.](../images/graph-simulation/events.png)

>[!TAB Configurazione dell&#39;algoritmo]

Algorithm configuration: Use the **[!UICONTROL Algorithm configuration]** panel to add and configure the optimization algorithm for your namespaces. You can drag and drop a namespace to modify their respective priority ranking. You can also select **[!UICONTROL Unique Per Graph]** to determine if a namespace is unique.

![The algorithm configuration of the Graph Simulation tool.](../images/graph-simulation/algorithm-configuration.png)

>[!TAB Grafico simulato visualizzatore]

Grafico simulato visualizzatore: il grafico simulato visualizza visualizzatore il grafico risultante in base agli eventi aggiunti e all&#39;algoritmo configurato. Una linea retta tra due identità significa che viene stabilita una collegare. Una linea tratteggiata indica che un collegare è stato rimosso.

![Il grafico simulato visualizzatore pannello, con un esempio di grafico simulato.](../images/graph-simulation/simulated-graph.png)

>[!ENDTABS]

## Aggiungi eventi {#add-events}

Per iniziare, seleziona **[!UICONTROL Aggiungi eventi]**.

![L&#39;opzione Aggiungi eventi pulsante selezionata.](../images/graph-simulation/add-events.png)

A pop-up window appears for [!UICONTROL Event #1]. Da qui, inserisci la combinazione di namespace identità e valore identità. Puoi utilizzare il menu a discesa per selezionare un namespace identità. In alternativa, è possibile digitare le prime lettere di uno spazio dei nomi e quindi selezionare le opzioni fornite nel menu a discesa. Dopo aver selezionato il namespace, fornisci un valore di identità corrispondente al namespace.

![La finestra dell&#39;evento #1 con un&#39;interfaccia vuota.](../images/graph-simulation/event-one.png)

>[!TIP]
>
>I valori di identità immessi durante [!DNL Graph Simulation] gli esercizi non devono necessariamente essere valori di identità reali e possono essere semplici segnaposto.

Una volta completata la prima identità, seleziona l&#39;icona Aggiungi (**`+`**) per aggiungere una seconda identità.

![La prima identità completa di {Email: tom@acme.com} viene immessa nel pannello Eventi di Graph Simulation.](../images/graph-simulation/event-one-added.png)

Successivo, ripetere gli stessi passaggi e aggiungere una seconda identità. Per generare un grafico delle identità sono necessarie due identità complete. Nell&#39;esempio seguente viene aggiunto un ECID come spazio dei nomi e viene fornito il valore .`111` Al termine, selezionare **[!UICONTROL Salva]**.

![Una seconda identità di {ECID: 111} viene aggiunta all&#39;evento #1.](../images/graph-simulation/first-event.png)

L&#39;interfaccia [!UICONTROL Eventi] viene aggiornata per visualizzare il primo evento, che in questo caso è: `{Email: tom@acme.com, ECID: 111}`.

![Gli eventi aggiornati si interfacciano con {Email: tom@acme.com, ECID: 111}.](../images/graph-simulation/add-second-event.png)

Quindi, ripeti gli stessi passaggi per aggiungere un secondo evento. Per l&#39;evento #2, aggiungi `{Email: summer@acme.com}` come prima identità e quindi aggiungi la stessa `{ECID: 111}` come seconda identità, creando così un secondo evento di: `{Email: summer@acme.com}, {ECID: 111}`. Al termine, si dovrebbero tenere due eventi, uno per `{Email: tom@acme.com, ECID: 111}` e uno per `{Email: summer@acme.com}, {ECID: 111}`.

![Gli eventi aggiornati si interfacciano con due eventi.](../images/graph-simulation/two-events.png)

### Carica esempio {#load-example}

Selezionare **[!UICONTROL Carica esempio]** per impostare un grafico di esempio con un algoritmo e una configurazione di evento predefiniti.

![Opzione Carica esempio selezionata.](../images/graph-simulation/load-example.png)

Viene visualizzata una finestra finestra a comparsa che fornisce gli scenari grafici disponibili tra cui scegliere:

| Esempio di grafico | Descrizione | Esempio |
| --- | --- | --- |
| Dispositivo condiviso | L dispositivo condivisa si riferisce a scenari in cui due utenti diversi accedono allo stesso dispositivo. | Un marito e una moglie condividono un iPad per navigare in Internet e e-commerce. |
| Telefono non valido (non univoco) | Telefono non valido o non univoco si riferisce a scenari in cui due utenti diversi utilizzano lo stesso numero di telefono per creare un account. | Una madre e sua figlia usano il loro numero di telefono di casa condiviso per registrarsi per qualsiasi account e-commerce. |
| Valori di identità “non validi” | &quot;Bad&quot; identity values refer to scenarios where Identity Service generates non-unique IDFAs due to erroneous implementation. | WebSDK erroneously sends a `user_null` value for every event due to code implementation issues. |

![A window that displays the available pre-configured examples: shared device, invalid phone, and bad identity values.](../images/graph-simulation/example-options.png)

Select any of the options to load [!DNL Graph Simulation] with pre-configured events and algorithm. È comunque possibile effettuare ulteriori configurazioni per qualsiasi esempio di scenario grafico precaricato.

![Eventi e algoritmo configurati per non valido telefono.](../images/graph-simulation/example-loaded.png)

Al termine, selezionare **[!UICONTROL Simula]**.

![Esempio di grafico simulato per non valido telefono.](../images/graph-simulation/example-simulated.png)

### Usa versione testo {#use-text-version}

È inoltre possibile utilizzare la modalità testo per configurare gli eventi. To use text mode, select the settings icon, and then select **[!UICONTROL Text (Advanced users)]**.

![Icona delle impostazioni selezionata.](../images/graph-simulation/settings.png)

Puoi inserire manualmente le tue identità con la modalità testo. Utilizzare i due punti (`:`) per distinguere il valore di identità corrispondente allo spazio dei nomi immesso, quindi utilizzare una virgola (`,`) per separare le identità. Per distinguere eventi diversi l&#39;uno dall&#39;altro, utilizzare una nuova riga per ogni evento.

![Il pannello Eventi utilizza la versione in modalità testo.](../images/graph-simulation/text-version.png)

### Modifica evento {#edit-event}

Per modificare un evento, seleziona i puntini di sospensione (`...`) accanto a un determinato evento, quindi seleziona **[!UICONTROL Modifica]**.

![Icona Modifica evento selezionata.](../images/graph-simulation/edit.png)

### Elimina evento {#delete-event}

Per eliminare un evento, selezionare i puntini di sospensione (`...`) accanto a un determinato evento, quindi selezionare **[!UICONTROL Elimina]**.

![Icona dell&#39;evento di eliminazione selezionata.](../images/graph-simulation/delete.png)

## Configura algoritmo {#configure-algorithm}

>[!IMPORTANT]
>
>The algorithm that you configure dictates how Identity Service treats the namespaces that you inputted in your events. Any configuration that you put together in the [!DNL Graph Simulation UI] are not saved in identity settings.

Once you have added your events, you can now configure the algorithm that will be used to simulate your graph. Per iniziare, selezionare **[!UICONTROL Aggiungi configurazione]**.

![Il pannello di configurazione dell&#39;algoritmo.](../images/graph-simulation/add-config.png)

Viene visualizzata una riga di configurazione vuota. Innanzitutto, inserisci lo stesso namespace che hai usato per gli eventi. In questo caso, inizia inserendo Email. Dopo aver immesso lo spazio dei nomi, le colonne per [!UICONTROL Identity Symbol] e [!UICONTROL Identity Type] vengono compilate automaticamente.

![La prima voce di configurazione.](../images/graph-simulation/add-namespace.png)

Successivo, ripetere gli stessi passaggi e aggiungere il secondo namespace, che in questo caso è l&#39;ECID. Una volta inseriti tutti i namespace, puoi iniziare a configurarne le priorità e l&#39;univocità.

* **Priorità** spazio dei nomi: la priorità di uno spazio dei nomi determina la sua importanza relativa rispetto agli altri spazi dei nomi in un determinato grafico di identità. Ad esempio, se il grafico delle identità ha quattro spazi dei nomi diversi: CRMID, ECID, Email e Apple IDFA, puoi configurare le priorità per determinare un ordine di importanza per i quattro namespace.
* **Spazio dei nomi** univoco: se uno spazio dei nomi è designato come univoco, Identity Service genererà grafici con l&#39;avvertenza che può esistere una sola identità con un determinato spazio dei nomi univoco. Ad esempio, se il namespace Email è designato come namespace univoco, un grafico può avere una sola identità con Email. Se esiste più di un&#39;identità con lo spazio dei nomi Email, la collegare meno recente verrà rimossa.

Per configurare la priorità dello spazio dei nomi, selezionare e trascinare le righe dello spazio dei nomi nell&#39;ordine di priorità desiderato, con la riga superiore che rappresenta la priorità più alta e la riga inferiore che rappresenta la priorità inferiore. Per designare un namespace come univoco, selezionare la casella di **[!UICONTROL controllo Univoco per grafico]** .

Al termine, selezionare **[!UICONTROL Simula]**.

![Tutti i namespace configurati.](../images/graph-simulation/all-namespaces.png)

## Visualizza grafico simulato

Nella [!UICONTROL sezione Grafico] simulato vengono visualizzati i grafici di identità generati in base agli eventi aggiunti e all&#39;algoritmo configurato.

| Graph icons | Descrizione |
| --- | --- |
| Linea continua | Una linea continua rappresenta un collegamento stabilito tra due identità. |
| Linea punteggiata | Una linea tratteggiata rappresenta un collegare rimosso tra due identità. |
| Numero on line | Un numero su una riga rappresenta il timestamp di quando è stato generato il collegare specificato. Il numero più basso (1) rappresenta il primo collegare stabilito. |

Nel grafico di esempio riportato di seguito, esiste una linea tratteggiata tra e `{ECID: 111}` per `{Email: tom@acme.com}` i seguenti motivi:

* L&#39;e-mail è stata designata come univoca durante la fase di configurazione dell&#39;algoritmo. Pertanto, in un grafico può esistere una sola identità con uno spazio dei nomi Email.
* Il collegare tra `{Email: tom@acme.com}` e `{ECID: 111}` fu la prima identità stabilita (Evento #1). È il collegare più vecchio e viene quindi rimosso.

![Il grafico simulato visualizzatore pannello, con un esempio di grafico simulato.](../images/graph-simulation/simulated-graph.png)

## Passaggi successivi

Leggendo questo documento, ora sai come utilizzare il [!DNL Graph Simulation] strumento per comprendere meglio come vengono trattati i tuoi dati di identità in base a un particolare insieme di regole e configurazioni. Per ulteriori informazioni, leggere i seguenti documenti:

* [Panoramica delle regole di collegamento del grafico di identità](./overview.md)
* [Algoritmo di ottimizzazione delle identità](./identity-optimization-algorithm.md)
* [Guida all&#39;implementazione](./implementation-guide.md)
* [Risoluzione dei problemi e domande frequenti](./troubleshooting.md)
* [Esempi di configurazioni del grafico](./example-configurations.md)
* [Priorità dello spazio dei nomi](./namespace-priority.md)
* [Interfaccia utente per le impostazioni delle identità](./identity-settings-ui.md)
