---
title: Guida dell’interfaccia utente di Graph Simulation
description: Scopri come utilizzare la simulazione del grafico nell’interfaccia utente del servizio Identity.
badge: Beta
exl-id: 89f0cf6e-c43f-40ec-859a-f3b73a6da8c8
source-git-commit: 2a2e3fcc4c118925795951a459a2ed93dfd7f7d7
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 1%

---

# Guida dell&#39;interfaccia utente di [!DNL Graph Simulation]

>[!AVAILABILITY]
>
>Le regole di collegamento del grafo delle identità sono attualmente in versione beta. Contatta il team del tuo account di Adobe per informazioni sui criteri di partecipazione. La funzione e la documentazione sono soggette a modifiche.

[!DNL Graph Simulation] è uno strumento nell&#39;interfaccia utente di Identity Service che consente di simulare il comportamento di un grafo delle identità in base a una combinazione specifica di identità e alla configurazione dell&#39;[algoritmo di ottimizzazione delle identità](./identity-optimization-algorithm.md).

Leggi questo documento per scoprire come utilizzare [!DNL Graph Simulation] per comprendere meglio il comportamento del grafo delle identità e il funzionamento dell&#39;algoritmo del grafo.

## Scopri l&#39;interfaccia [!DNL Graph Simulation] {#interface}

Puoi accedere a [!DNL Graph Simulation] nell&#39;interfaccia utente di Adobe Experience Platform. Seleziona **[!UICONTROL Identità]** dal menu di navigazione a sinistra, quindi seleziona **[!UICONTROL Simulazione grafico]** dall&#39;intestazione superiore.

![Interfaccia Graph Simulation nell&#39;interfaccia utente di Adobe Experience Platform.](../images/graph-simulation/graph-simulation.png)

L&#39;interfaccia [!DNL Graph Simulation] può essere divisa in tre sezioni:

>[!BEGINTABS]

>[!TAB Eventi]

Eventi: utilizza il pannello **[!UICONTROL Eventi]** per aggiungere identità per simulare un grafico. Un’identità completa deve avere uno spazio dei nomi dell’identità e il valore di identità corrispondente. Per simulare un grafico è necessario aggiungere almeno due identità. Puoi anche selezionare **[!UICONTROL Carica esempio]** per inserire un evento e una configurazione dell&#39;algoritmo preconfigurati.

![Pannello eventi dello strumento Simulazione grafico.](../images/graph-simulation/events.png)

>[!TAB Configurazione algoritmo]

Configurazione dell&#39;algoritmo: utilizza il pannello **[!UICONTROL Configurazione dell&#39;algoritmo]** per aggiungere e configurare l&#39;algoritmo di ottimizzazione per gli spazi dei nomi. Puoi trascinare uno spazio dei nomi per modificarne la classificazione di priorità. È inoltre possibile selezionare **[!UICONTROL Univoco per grafico]** per determinare se uno spazio dei nomi è univoco.

![Configurazione dell&#39;algoritmo dello strumento di simulazione del grafico.](../images/graph-simulation/algorithm-configuration.png)

>[!TAB Visualizzatore grafico simulato]

Visualizzatore grafico simulato: il visualizzatore grafico simulato visualizza il grafico risultante in base agli eventi aggiunti e all’algoritmo configurato. Una linea retta tra due identità significa che è stabilito un collegamento. Una riga punteggiata indica che un collegamento è stato rimosso.

![Pannello visualizzatore grafico simulato, con esempio di grafico simulato.](../images/graph-simulation/simulated-graph.png)

>[!ENDTABS]

## Aggiungi eventi {#add-events}

Per iniziare, selezionare **[!UICONTROL Aggiungi eventi]**.

![Pulsante Aggiungi eventi selezionato.](../images/graph-simulation/add-events.png)

Viene visualizzata una finestra popup per [!UICONTROL Evento #1]. Da qui, inserisci la combinazione di spazio dei nomi e valore di identità. Puoi utilizzare il menu a discesa per selezionare uno spazio dei nomi delle identità. In alternativa, puoi digitare le prime lettere di uno spazio dei nomi e quindi selezionare le opzioni fornite nel menu a discesa. Dopo aver selezionato lo spazio dei nomi, fornisci un valore di identità che corrisponda allo spazio dei nomi.

![Finestra #1 eventi con interfaccia vuota.](../images/graph-simulation/event-one.png)

>[!TIP]
>
>Il valore di identità immesso durante gli esercizi [!DNL Graph Simulation] non deve necessariamente essere un valore di identità reale e può essere un semplice segnaposto.

Una volta completata la prima identità, selezionare l&#39;icona di aggiunta (**`+`**) per aggiungere una seconda identità.

![La prima identità completa di {Email: tom@acme.com} viene immessa nel pannello Eventi di Graph Simulation.](../images/graph-simulation/event-one-added.png)

Quindi, ripeti gli stessi passaggi e aggiungi una seconda identità. Per generare un grafo di identità sono necessarie due identità complete. Nell&#39;esempio seguente, un ECID viene aggiunto come spazio dei nomi e gli viene fornito un valore di `111`. Al termine, selezionare **[!UICONTROL Salva]**.

![Una seconda identità di {ECID: 111} è stata aggiunta all&#39;evento #1.](../images/graph-simulation/first-event.png)

L&#39;interfaccia [!UICONTROL Events] viene aggiornata per visualizzare il primo evento, che in questo caso è: `{Email: tom@acme.com, ECID: 111}`.

![Interfaccia eventi aggiornata con {Email: tom@acme.com, ECID: 111}.](../images/graph-simulation/add-second-event.png)

Quindi, ripeti gli stessi passaggi per aggiungere un secondo evento. Per #2 evento, aggiungere `{Email: summer@acme.com}` come prima identità, quindi aggiungere lo stesso `{ECID: 111}` come seconda identità, creando un secondo evento di: `{Email: summer@acme.com}, {ECID: 111}`. Al termine, si dovrebbero avere due eventi, uno per `{Email: tom@acme.com, ECID: 111}` e uno per `{Email: summer@acme.com}, {ECID: 111}`.

![Interfaccia eventi aggiornata con due eventi.](../images/graph-simulation/two-events.png)

### Carica esempio {#load-example}

Seleziona **[!UICONTROL Carica esempio]** per impostare un grafico di esempio con un algoritmo predefinito e una configurazione dell&#39;evento.

![Opzione Carica esempio selezionata.](../images/graph-simulation/load-example.png)

Viene visualizzata una finestra popup che fornisce gli scenari grafici disponibili tra cui è possibile scegliere:

| Grafico di esempio | Descrizione | Esempio |
| --- | --- | --- |
| Dispositivo condiviso | Per dispositivo condiviso si intendono gli scenari in cui due utenti diversi accedono allo stesso singolo dispositivo. | Un marito e una moglie condividono un iPad per la navigazione internet e l&#39;e-commerce. |
| Telefono non valido (non univoco) | Un numero di telefono non valido o non univoco si riferisce a scenari in cui due utenti diversi utilizzano lo stesso numero di telefono per creare un account. | Una madre e sua figlia utilizzano il numero di telefono della loro casa condivisa per iscriversi a qualsiasi account di e-commerce. |
| Valori di identità “non validi” | I valori di identità &quot;errati&quot; si riferiscono a scenari in cui il servizio Identity genera identificatori IDFA non univoci a causa di un’implementazione errata. | WebSDK invia erroneamente un valore `user_null` per ogni evento a causa di problemi di implementazione del codice. |

![Una finestra che visualizza gli esempi preconfigurati disponibili: dispositivo condiviso, telefono non valido e valori di identità non validi.](../images/graph-simulation/example-options.png)

Selezionare una delle opzioni per caricare [!DNL Graph Simulation] con eventi e algoritmi preconfigurati. Puoi comunque effettuare ulteriori configurazioni per qualsiasi esempio di scenario grafico precaricato.

![Gli eventi e l&#39;algoritmo configurati per un telefono non valido.](../images/graph-simulation/example-loaded.png)

Al termine, selezionare **[!UICONTROL Simula]**.

![Grafico di esempio simulato per un telefono non valido.](../images/graph-simulation/example-simulated.png)

### Usa versione testo {#use-text-version}

Puoi anche utilizzare la modalità testo per configurare gli eventi. Per utilizzare la modalità testo, selezionare l&#39;icona delle impostazioni, quindi selezionare **[!UICONTROL Testo (utenti avanzati)]**.

![Icona impostazioni selezionata.](../images/graph-simulation/settings.png)

Puoi inserire manualmente le identità con la modalità testo. Utilizzare i due punti (`:`) per distinguere il valore di identità corrispondente allo spazio dei nomi immesso, quindi utilizzare una virgola (`,`) per separare le identità. Per distinguere eventi diversi tra loro, utilizza una nuova riga per ogni evento.

![Il pannello eventi utilizza la versione in modalità testo.](../images/graph-simulation/text-version.png)

### Modifica evento {#edit-event}

Per modificare un evento, selezionare i puntini di sospensione (`...`) accanto a un determinato evento, quindi selezionare **[!UICONTROL Modifica]**.

![Icona dell&#39;evento di modifica selezionata.](../images/graph-simulation/edit.png)

### Elimina evento {#delete-event}

Per eliminare un evento, selezionare i puntini di sospensione (`...`) accanto a un determinato evento, quindi selezionare **[!UICONTROL Elimina]**.

![Icona Elimina evento selezionata.](../images/graph-simulation/delete.png)

## Configurare l’algoritmo {#configure-algorithm}

>[!IMPORTANT]
>
>L’algoritmo configurato determina il modo in cui Identity Service tratta gli spazi dei nomi inseriti negli eventi. Qualsiasi configurazione creata in [!DNL Graph Simulation UI] non viene salvata nelle impostazioni di identità.

Dopo aver aggiunto gli eventi, puoi ora configurare l’algoritmo che verrà utilizzato per simulare il grafico. Per iniziare, selezionare **[!UICONTROL Aggiungi configurazione]**.

![Pannello di configurazione dell&#39;algoritmo.](../images/graph-simulation/add-config.png)

Viene visualizzata una riga di configurazione vuota. Innanzitutto, inserisci lo stesso spazio dei nomi utilizzato per gli eventi. In questo caso, inizia immettendo E-mail. Dopo aver immesso lo spazio dei nomi, le colonne per [!UICONTROL Identity Symbol] e [!UICONTROL Identity Type] vengono compilate automaticamente.

![Prima voce di configurazione.](../images/graph-simulation/add-namespace.png)

Quindi, ripeti gli stessi passaggi e aggiungi il secondo spazio dei nomi, che in questo caso è l’ECID. Una volta inseriti tutti i namespace, puoi iniziare a configurarne le priorità e l’univocità.

* **Priorità dello spazio dei nomi**: la priorità di uno spazio dei nomi ne determina l&#39;importanza relativa rispetto agli altri spazi dei nomi in un dato grafico delle identità. Ad esempio, se il grafo delle identità dispone di quattro spazi dei nomi diversi: CRMID, ECID, E-mail e Apple IDFA, puoi configurare le priorità per determinare un ordine di importanza per i quattro spazi dei nomi.
* **Spazio dei nomi univoco**: se uno spazio dei nomi è designato come univoco, Identity Service genererà dei grafici avvertendo che può esistere una sola identità con uno spazio dei nomi univoco specifico. Ad esempio, se lo spazio dei nomi E-mail è designato come spazio dei nomi univoco, un grafico può avere una sola identità con E-mail. Se sono presenti più identità con lo spazio dei nomi E-mail, il collegamento meno recente verrà rimosso.

Per configurare la priorità dello spazio dei nomi, seleziona e trascina le righe dello spazio dei nomi nell’ordine di priorità desiderato, con la riga superiore che rappresenta la priorità più alta e la riga inferiore che rappresenta la priorità più bassa. Per designare uno spazio dei nomi come univoco, selezionare la casella di controllo **[!UICONTROL Univoco per grafico]**.

Al termine, selezionare **[!UICONTROL Simula]**.

![Tutti gli spazi dei nomi configurati.](../images/graph-simulation/all-namespaces.png)

## Visualizza grafico simulato

La sezione [!UICONTROL Grafico simulato] visualizza i grafici delle identità generati in base agli eventi aggiunti e all&#39;algoritmo configurato.

| Icone del grafico | Descrizione |
| --- | --- |
| Linea continua | Una linea continua rappresenta un collegamento stabilito tra due identità. |
| Linea punteggiata | Una linea tratteggiata rappresenta un collegamento rimosso tra due identità. |
| Numero in linea | Un numero su una riga rappresenta la marca temporale di quando è stato generato quel determinato collegamento. Il numero più basso (1) rappresenta il primo collegamento stabilito. |

Nel grafico di esempio seguente, esiste una linea tratteggiata tra `{Email: tom@acme.com}` e `{ECID: 111}` per i motivi seguenti:

* L’e-mail è stata designata come univoca durante il passaggio di configurazione dell’algoritmo. Pertanto, in un grafico può esistere una sola identità con uno spazio dei nomi e-mail.
* Il collegamento tra `{Email: tom@acme.com}` e `{ECID: 111}` è stata la prima identità stabilita (#1 evento). È il collegamento più vecchio e viene quindi rimosso.

![Pannello visualizzatore grafico simulato, con esempio di grafico simulato.](../images/graph-simulation/simulated-graph.png)

## Passaggi successivi

Dopo aver letto questo documento, saprai come utilizzare lo strumento [!DNL Graph Simulation] per comprendere meglio come vengono trattati i dati di identità in base a un particolare set di regole e configurazioni. Per ulteriori informazioni, leggere i seguenti documenti:

* [Regole di collegamento del grafo delle identità](./overview.md)
* [Guida alla configurazione](./configuration.md)
* [Algoritmo di ottimizzazione identità](./identity-optimization-algorithm.md)
* [Priorità dello spazio dei nomi](./namespace-priority.md)
* [Esempio di configurazioni del grafico](./example-configurations.md)
