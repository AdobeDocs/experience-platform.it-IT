---
title: Crea una connessione di origine  [!DNL Oracle NetSuite Activities]  nell'interfaccia utente
description: Scopri come creare un Oracle di connessione all’origine delle attività NetSuite utilizzando l’interfaccia utente di Adobe Experience Platform.
hide: true
hidefromtoc: true
badge: Beta
exl-id: 99ef0b50-c8d6-48d6-895f-46b7ade47520
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 2%

---

# Crea una connessione sorgente [!DNL Oracle NetSuite Activities] nell&#39;interfaccia utente

>[!NOTE]
>
>L&#39;origine [!DNL Oracle NetSuite Activities] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, vedere la [panoramica origini](../../../../home.md#terms-and-conditions).

Leggi il seguente tutorial per scoprire come portare i dati degli eventi dal tuo account [!DNL Oracle NetSuite Activities] a Adobe Experience Platform nell&#39;interfaccia utente.

## Introduzione {#getting-started}

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale [!DNL Experience Platform] organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un account [!DNL Oracle NetSuite] valido, puoi saltare il resto di questo documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/marketing-automation.md).

>[!TIP]
>
>Leggi la [[!DNL Oracle NetSuite] panoramica](../../../../connectors/marketing-automation/oracle-netsuite.md) per informazioni su come recuperare le credenziali di autenticazione.

## Connetti il tuo account [!DNL Oracle NetSuite] {#connect-account}

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria *Marketing Automation*, selezionare **[!DNL Oracle NetSuite Activities]**, quindi **[!UICONTROL Aggiungi dati]**.

![Schermata dell&#39;interfaccia utente di Platform per il catalogo con la scheda Attività NetSuite di Oracle](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/catalog-card.png)

Viene visualizzata la pagina dell&#39;account **[!UICONTROL Connect Oracle NetSuite Activities]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

>[!IMPORTANT]
>
>Il token di aggiornamento scade dopo sette giorni. Una volta scaduto il token, devi creare l’account su Experience Platform con il token aggiornato. Se non si crea un nuovo account con il token aggiornato, è possibile che venga visualizzato il seguente messaggio di errore: `The request could not be processed. Error from flow provider: The request could not be processed. Rest call failed with client error, status code 401 Unauthorized, please check your activity settings.`

### Account esistente {#existing-account}

Per utilizzare un account esistente, seleziona l&#39;account [!DNL Oracle NetSuite Activities] con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per continuare.

![Schermata dell&#39;interfaccia utente di Platform per collegare l&#39;account Oracle NetSuite Activities a un account esistente](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/existing.png)

### Nuovo account {#new-account}

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e le tue credenziali. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![Schermata dell&#39;interfaccia utente di Platform per collegare l&#39;account Oracle NetSuite Activities con un nuovo account](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/new.png)

## Passaggi successivi {#next-steps}

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Oracle NetSuite Activities]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in Platform](../../dataflow/marketing-automation.md).

## Risorse aggiuntive {#additional-resources}

Le sezioni seguenti forniscono ulteriori risorse a cui fare riferimento quando si utilizza l&#39;origine [!DNL Oracle NetSuite Activities].

### Mappatura {#mapping}

Platform fornisce consigli intelligenti per campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso. In base alle tue esigenze, puoi scegliere di mappare i campi direttamente o utilizzare le funzioni di preparazione dati per trasformare i dati sorgente in modo da derivare valori calcolati o calcolati. Per i passaggi completi sull&#39;utilizzo dell&#39;interfaccia mapper e dei campi calcolati, consulta la [guida dell&#39;interfaccia utente della preparazione dati](../../../../../data-prep/ui/mapping.md).

>[!NOTE]
>
>I campi visualizzati dipendono dalle sottoscrizioni a cui ha accesso il tuo account [!DNL Oracle NetSuite]. Ad esempio, se non hai accesso alla fatturazione, non visualizzerai i campi relativi alla fatturazione.

### Pianificazione {#scheduling}

Quando pianifichi il flusso di dati [!DNL Oracle NetSuite Activities] per l&#39;acquisizione, seleziona la seguente configurazione di frequenza e intervallo:

| Frequenza | Intervallo |
| --- | --- |
| `Once` | 1 |

Durante il recupero dei dati, [!DNL Oracle NetSuite] risponde con la data dell&#39;ultima modifica o creazione come formato data invece di una marca temporale. Pertanto, la pianificazione è limitata a un giorno.

Dopo aver fornito i valori per la pianificazione, seleziona **[!UICONTROL Successivo]**.

![Passaggio di pianificazione del flusso di lavoro di origine.](../../../../images/tutorials/create/marketing-automation/oracle-netsuite-activities/scheduling.png)
