---
title: Interfaccia utente per le impostazioni delle identità
description: Scopri come utilizzare l’interfaccia utente delle impostazioni di identità.
badge: Beta
source-git-commit: 72773f9ba5de4387c631bd1aa0c4e76b74e5f1dc
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# Interfaccia utente per l’impostazione dell’identità

>[!AVAILABILITY]
>
>Questa funzione non è ancora disponibile; il programma beta per le regole di collegamento del grafo delle identità dovrebbe iniziare a luglio per le sandbox di sviluppo. Contatta il team del tuo account di Adobe per informazioni sui criteri di partecipazione.

Le impostazioni di identità sono una funzione dell’interfaccia utente di Adobe Experience Platform Identity Service che consente di designare spazi dei nomi univoci e configurare la priorità dello spazio dei nomi.

Leggi questa guida per scoprire come configurare le impostazioni di identità nell’interfaccia utente.

## Prerequisiti

Prima di iniziare a utilizzare le impostazioni di identità, leggi i seguenti documenti:

* [Guida alla configurazione delle regole di collegamento del grafico delle identità](./configuration.md)
* [Algoritmo di ottimizzazione identità](./identity-optimization-algorithm.md)
* [Priorità dello spazio dei nomi](./namespace-priority.md)
* [Simulazione del grafico](./graph-simulation.md)

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

Una volta stabiliti gli spazi dei nomi univoci, i grafici non saranno più in grado di avere più identità che contengono uno spazio dei nomi univoco. Ad esempio, se hai designato l’ID del sistema di gestione delle relazioni con i clienti come spazio dei nomi univoco, un grafico può avere una sola identità con lo spazio dei nomi dell’ID del sistema di gestione delle relazioni con i clienti. Per ulteriori informazioni, leggere la [panoramica dell&#39;algoritmo di ottimizzazione delle identità](./identity-optimization-algorithm.md#unique-namespace).

Al termine, seleziona **[!UICONTROL Avanti]**. Viene visualizzato un messaggio di conferma. Utilizzare questa opportunità per verificare che le configurazioni siano corrette, quindi selezionare **[!UICONTROL Fine]**.

![La pagina di convalida con Fine evidenziata.](../images/rules/finish.png)

Viene visualizzato un avviso che indica che le nuove impostazioni non avranno implicazioni sui collegamenti esistenti in un grafo di identità e sui frammenti di profilo di evento esperienza già acquisiti. Inoltre, viene visualizzato un messaggio che informa che sono necessarie fino a sei ore affinché le nuove impostazioni vengano applicate al sistema. Per confermare, immetti il nome della sandbox, quindi seleziona **[!UICONTROL Conferma]**.

![Finestra di conferma che visualizza un avviso relativo a un ritardo di sei ore prima dell&#39;elaborazione delle configurazioni.](../images/rules/confirm-settings.png)

## Passaggi successivi

Ora hai configurato le priorità dello spazio dei nomi e definito gli spazi dei nomi univoci utilizzando la pagina dell’interfaccia utente delle impostazioni delle identità. Per ulteriori informazioni, leggere la [panoramica delle regole di collegamento del grafico delle identità](./overview.md).