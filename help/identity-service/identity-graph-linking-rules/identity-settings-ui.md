---
title: Interfaccia utente per le impostazioni delle identità
description: Scopri come utilizzare l’interfaccia utente delle impostazioni di identità.
exl-id: 738b7617-706d-46e1-8e61-a34855ab976e
source-git-commit: cfe0181104f09bfd91b22d165c23154a15cd5344
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---

# Interfaccia utente per l’impostazione dell’identità

>[!AVAILABILITY]
>
>Le regole di collegamento del grafo identità sono attualmente a disponibilità limitata. Contatta il team del tuo account Adobe per informazioni su come accedere alla funzione nelle sandbox di sviluppo.

Le impostazioni di identità sono una funzione dell’interfaccia utente di Adobe Experience Platform Identity Service che consente di designare spazi dei nomi univoci e configurare la priorità dello spazio dei nomi.

Leggi questa guida per scoprire come configurare le impostazioni di identità nell’interfaccia utente.

## Prerequisiti

Prima di iniziare a utilizzare le impostazioni di identità, leggi i seguenti documenti:

* [Regole di collegamento del grafo delle identità](./overview.md)
* [Algoritmo di ottimizzazione identità](./identity-optimization-algorithm.md)
* [Guida all’implementazione](./implementation-guide.md)
* [Esempi di configurazioni di grafo](./example-configurations.md)
* [Priorità dello spazio dei nomi](./namespace-priority.md)
* [Simulazione dei grafici](./graph-simulation.md)

## Configurare le impostazioni di identità

Per accedere alle impostazioni di identità, passa all&#39;area di lavoro del servizio Identity nell&#39;interfaccia utente di Adobe Experience Platform, quindi seleziona **[!UICONTROL Impostazioni]**.

![Pulsante delle impostazioni di identità selezionato.](../images/rules/identities-ui.png)

La pagina delle impostazioni delle identità è divisa in due sezioni: [!UICONTROL Spazi dei nomi delle persone] e [!UICONTROL Spazi dei nomi dei dispositivi o dei cookie]. Gli spazi dei nomi delle persone sono identificatori di singoli individui. Possono essere ID multi-dispositivo, indirizzi e-mail e numeri di telefono. Gli spazi dei nomi dei dispositivi o dei cookie sono identificatori per dispositivi e browser web e non possono avere una priorità maggiore degli spazi dei nomi delle persone. Inoltre, non è possibile designare un dispositivo o uno spazio dei nomi cookie come spazio dei nomi univoco.

### Configurare la priorità dello spazio dei nomi

Per configurare la priorità dello spazio dei nomi, seleziona uno spazio dei nomi nel menu delle impostazioni dell’identità, quindi trascina e rilascia lo spazio dei nomi nell’ordine desiderato. Posiziona uno spazio dei nomi più in alto nell’elenco per assegnargli una priorità più alta, e viceversa, posiziona uno spazio dei nomi più in basso nell’elenco per assegnargli una priorità più bassa. Anche lo spazio dei nomi con la priorità più elevata deve essere designato come spazio dei nomi univoco.

![Area di lavoro delle impostazioni delle identità con uno spazio dei nomi della persona evidenziato.](../images/rules/namespace-priority.png)

### Designare uno spazio dei nomi univoco

Per designare uno spazio dei nomi univoco, selezionare la casella di controllo [!UICONTROL Univoco per grafico] che corrisponde a tale spazio dei nomi. Puoi selezionare più spazi dei nomi univoci per la configurazione delle impostazioni di identità.

![Due spazi dei nomi selezionati e definiti come univoci.](../images/rules/unique-namespace.png)

Una volta stabiliti gli spazi dei nomi univoci, i grafici non saranno più in grado di avere più identità che contengono uno spazio dei nomi univoco. Ad esempio, se hai designato CRMID come spazio dei nomi univoco, un grafo può avere una sola identità con lo spazio dei nomi CRMID. Per ulteriori informazioni, leggere la [panoramica dell&#39;algoritmo di ottimizzazione delle identità](./identity-optimization-algorithm.md#unique-namespace).

Al termine, seleziona **[!UICONTROL Avanti]**. Viene visualizzato un messaggio di conferma. Utilizzare questa opportunità per verificare che le configurazioni siano corrette, quindi selezionare **[!UICONTROL Fine]**.

![La pagina di convalida con Fine evidenziata.](../images/rules/finish.png)

Viene visualizzato un messaggio di avviso che indica che i grafici esistenti saranno interessati dall&#39;algoritmo del grafico solo se i grafici vengono aggiornati **dopo il salvataggio delle impostazioni** e che l&#39;identità primaria dei frammenti di evento nel profilo cliente in tempo reale non verrà aggiornata anche dopo le modifiche della priorità dello spazio dei nomi. Inoltre, ti viene comunicato che saranno necessarie fino a **sei ore** per rendere effettive le nuove impostazioni. Per confermare, immetti il nome della sandbox, quindi seleziona **[!UICONTROL Conferma]**.

![Finestra di conferma che visualizza un avviso relativo a un ritardo di sei ore prima dell&#39;elaborazione delle configurazioni.](../images/rules/confirm-settings.png)

## Passaggi successivi

Per ulteriori informazioni sulle regole di collegamento del grafico delle identità, consulta la documentazione seguente:

* [Panoramica delle regole di collegamento del grafico delle identità](./overview.md)
* [Algoritmo di ottimizzazione identità](./identity-optimization-algorithm.md)
* [Guida all’implementazione](./implementation-guide.md)
* [Esempi di configurazioni di grafo](./example-configurations.md)
* [Risoluzione dei problemi e domande frequenti](./troubleshooting.md)
* [Priorità dello spazio dei nomi](./namespace-priority.md)
* [Interfaccia utente simulazione grafico](./graph-simulation.md)