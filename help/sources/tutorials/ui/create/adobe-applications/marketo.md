---
title: Creare una connessione Source di Marketo Engage e un flusso di dati nell’interfaccia utente
description: Questa esercitazione descrive i passaggi da seguire per creare una connessione di origine del Marketo Engage e un flusso di dati nell’interfaccia utente per inserire dati B2B in Adobe Experience Platform.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: 744098777141c61ac27fe6f150c05469d5705dee
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 2%

---

# Crea una connessione di origine [!DNL Marketo Engage] e un flusso di dati nell&#39;interfaccia utente

>[!IMPORTANT]
>
>Prima di creare una connessione di origine [!DNL Marketo Engage] e un flusso di dati, è necessario verificare di aver [mappato l&#39;ID organizzazione Adobe](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html) in [!DNL Marketo]. Inoltre, devi anche assicurarti di aver completato [la compilazione automatica dei tuoi [!DNL Marketo] spazi dei nomi e schemi B2B](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md) prima di creare una connessione di origine e un flusso di dati.

Questa esercitazione descrive i passaggi per la creazione di un connettore di origine [!DNL Marketo Engage] (di seguito &quot;[!DNL Marketo]&quot;) nell&#39;interfaccia utente per l&#39;inserimento di dati B2B in Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Spazi dei nomi B2B e utilità di generazione automatica dello schema](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md): gli spazi dei nomi B2B e l&#39;utilità di generazione automatica dello schema consentono di utilizzare [!DNL Postman] per generare automaticamente i valori per gli spazi dei nomi B2B e gli schemi. Prima di creare una connessione di origine e un flusso di dati [!DNL Marketo], è necessario completare gli spazi dei nomi e gli schemi B2B.
* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Experience Data Model (XDM)](../../../../../xdm/home.md): framework standardizzato in base al quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Creare e modificare gli schemi nell&#39;interfaccia utente](../../../../../xdm/ui/resources/schemas.md): scopri come creare e modificare gli schemi nell&#39;interfaccia utente.
* [Spazi dei nomi di identità](../../../../../identity-service/features/namespaces.md): gli spazi dei nomi di identità sono un componente di [!DNL Identity Service] che fungono da indicatori del contesto a cui si riferisce un&#39;identità. Un’identità completa include un valore ID e uno spazio dei nomi.
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Raccogli le credenziali richieste

Per accedere all&#39;account [!DNL Marketo] su Experience Platform, è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---- | ---- |
| `munchkinId` | L&#39;ID Munchkin è l&#39;identificatore univoco di un&#39;istanza [!DNL Marketo] specifica. |
| `clientId` | ID client univoco dell&#39;istanza [!DNL Marketo]. |
| `clientSecret` | Il segreto client univoco dell&#39;istanza [!DNL Marketo]. |

Per ulteriori informazioni sull&#39;acquisizione di questi valori, consultare la [[!DNL Marketo] guida all&#39;autenticazione](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi descritti nella sezione successiva.

## Connetti il tuo account [!DNL Marketo]

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria *applicazioni di Adobe*, selezionare **[!UICONTROL Marketo Engage]**, quindi **[!UICONTROL Aggiungi dati]**.

>[!TIP]
>
>Le origini nel catalogo delle origini visualizzano l&#39;opzione **[!UICONTROL Configura]** quando un&#39;origine specificata non dispone ancora di un account autenticato. Quando esiste un account autenticato, questa opzione diventa **[!UICONTROL Aggiungi dati]**.

![Catalogo origini con origine Marketo Engage selezionata.](../../../../images/tutorials/create/marketo/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti account di Marketo Engage]**. In questa pagina è possibile utilizzare un nuovo account o accedere a un account esistente.

>[!BEGINTABS]

>[!TAB Crea un nuovo account]

Per creare un nuovo account, selezionare **[!UICONTROL Nuovo account]** e fornire un nome, una descrizione facoltativa e le credenziali.

Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![Nuova interfaccia account per l&#39;autenticazione di un nuovo account Marketo.](../../../../images/tutorials/create/marketo/new.png)

>[!TAB Usa un account esistente]

Per utilizzare un account esistente, selezionare **[!UICONTROL Account esistente]**, quindi selezionare l&#39;account che si desidera utilizzare dal catalogo degli account esistente.

Seleziona **[!UICONTROL Avanti]** per procedere.

![Interfaccia account esistente in cui è possibile selezionare un account Marketo esistente.](../../../../images/tutorials/create/marketo/existing.png)

>[!ENDTABS]

## Selezionare un set di dati

Dopo aver creato l&#39;account [!DNL Marketo], il passaggio successivo fornisce un&#39;interfaccia per esplorare [!DNL Marketo] set di dati.

La metà sinistra dell&#39;interfaccia è un browser di directory che visualizza i 10 [!DNL Marketo] set di dati. Una connessione di origine [!DNL Marketo] completamente funzionante richiede l&#39;acquisizione dei nove diversi set di dati. Se utilizzi anche la funzione di marketing basato su account [!DNL Marketo], devi creare anche un decimo flusso di dati per acquisire il set di dati [!UICONTROL Account denominati].

>[!NOTE]
>
>Per motivi di brevità, nell&#39;esercitazione seguente vengono utilizzate [!UICONTROL opportunità] come esempio, ma i passaggi descritti di seguito si applicano a uno qualsiasi dei 10 [!DNL Marketo] set di dati.

Seleziona il set di dati da acquisire. Questo aggiorna l’interfaccia in modo da visualizzare un’anteprima del set di dati. Al termine, selezionare **[!UICONTROL Avanti]**.

![Interfaccia di anteprima](../../../../images/tutorials/create/marketo/preview.png)

## Fornisci i dettagli del set di dati e del flusso di dati {#provide-dataset-and-dataflow-details}

Quindi, devi fornire informazioni sul set di dati e sul flusso di dati.

### Dettagli del set di dati {#dataset-details}

Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e dei campi (righe). I dati acquisiti correttamente in Experience Platform vengono memorizzati nel data lake come set di dati. Durante questo passaggio, puoi creare un nuovo set di dati o utilizzare un set di dati esistente.

>[!BEGINTABS]

>[!TAB Utilizza un nuovo set di dati]

Per utilizzare un nuovo set di dati, selezionare **[!UICONTROL Nuovo set di dati]**, quindi specificare un nome e una descrizione facoltativa per il set di dati. Devi anche selezionare uno schema Experience Data Model (XDM) a cui aderisce il set di dati.

![Nuova interfaccia di selezione del set di dati.](../../../../images/tutorials/create/marketo/new-dataset.png)

>[!TAB Utilizza un set di dati esistente]

Se disponi già di un set di dati, seleziona **[!UICONTROL Set di dati esistente]** e quindi utilizza l&#39;opzione **[!UICONTROL Ricerca avanzata]** per visualizzare una finestra di tutti i set di dati dell&#39;organizzazione, inclusi i rispettivi dettagli, ad esempio se sono abilitati o meno per l&#39;acquisizione in Real-Time Customer Profile.

![Interfaccia di selezione del set di dati esistente.](../../../../images/tutorials/create/marketo/existing-dataset.png)

>[!ENDTABS]

### Configurazioni del flusso di dati {#dataflow-configurations}

>[!IMPORTANT]
>
>L&#39;origine [!DNL Marketo] utilizza l&#39;acquisizione in batch per acquisire tutti i record storici e l&#39;acquisizione in streaming per gli aggiornamenti in tempo reale. Questo consente all’origine di continuare lo streaming durante l’acquisizione di eventuali record errati. Abilita l&#39;opzione **[!UICONTROL Acquisizione parziale]**, quindi imposta la soglia di errore [!UICONTROL %] su un valore massimo per evitare che il flusso di dati non riesca.

Se il set di dati è abilitato per Real-Time Customer Profile, durante questo passaggio puoi attivare/disattivare **[!UICONTROL il set di dati profilo]** per abilitare i dati per l&#39;acquisizione del profilo. È inoltre possibile utilizzare questo passaggio per abilitare **[!UICONTROL Diagnostica errori]** e **[!UICONTROL Acquisizione parziale]**.

* **[!UICONTROL Diagnostica errori]**: selezionare **[!UICONTROL Diagnostica errori]** per indicare all&#39;origine di produrre diagnostica errori a cui fare successivamente riferimento durante il monitoraggio dell&#39;attività del set di dati e dello stato del flusso di dati.
* **[!UICONTROL Acquisizione parziale]**: [L&#39;acquisizione parziale in batch](../../../../../ingestion/batch-ingestion/partial.md) consente di acquisire dati contenenti errori, fino a una determinata soglia configurabile. Questa funzione consente di acquisire correttamente in Experience Platform tutti i dati accurati, mentre tutti i dati errati vengono raggruppati separatamente con informazioni sul motivo della validità.

Durante questo passaggio, puoi abilitare **[!UICONTROL Flusso di dati di esempio]** per limitare l&#39;acquisizione dei dati ed evitare costi aggiuntivi associati all&#39;acquisizione di tutti i dati storici, incluse le identità delle persone.

>[!BEGINSHADEBOX]

**Guida rapida all&#39;utilizzo del flusso di dati di esempio**

Il flusso di dati di esempio è una configurazione che puoi impostare per il flusso di dati [!DNL Marketo] in modo da limitare il tasso di acquisizione, quindi prova le funzionalità di Experience Platform senza dover acquisire grandi quantità di dati.

* Abilita il flusso di dati di esempio per limitare i dati storici acquisendo fino a 100.000 record (dal più grande ID record) o fino agli ultimi 10 giorni di attività durante il processo di backfill.
* Quando utilizzi la configurazione del flusso di dati di esempio per tutte le entità B2B, devi tenere presente che alcuni record correlati potrebbero mancare perché l’intera cronologia dei dati di origine non viene acquisita.

>[!ENDSHADEBOX]

![La sezione relativa alle configurazioni del flusso di dati nella pagina dei dettagli del flusso di dati.](../../../../images/tutorials/create/marketo/dataflow-configurations.png)

Inoltre, se si acquisiscono dati dal set di dati aziendali, è possibile abilitare **[!UICONTROL Escludi account non rivendicati]** per escludere gli account non rivendicati dall&#39;acquisizione.

Quando i singoli utenti compilano un modulo, [!DNL Marketo] crea un record account fantasma in base al Nome società che non contiene altri dati. Per i nuovi flussi di dati, l’opzione per escludere gli account non rivendicati è abilitata per impostazione predefinita. Per i flussi di dati esistenti, puoi abilitare o disabilitare la funzione, con le modifiche che si applicano ai dati appena acquisiti e non ai dati esistenti.

![Escludi account non rivendicati](../../../../images/tutorials/create/marketo/unclaimed-accounts.png)

## Mappa i campi di origine del set di dati [!DNL Marketo] ai campi XDM di destinazione

Viene visualizzato il passaggio [!UICONTROL Mappatura] che fornisce un&#39;interfaccia per mappare i campi sorgente dallo schema sorgente ai campi XDM di destinazione appropriati nello schema di destinazione.

Ogni set di dati [!DNL Marketo] ha le proprie regole di mappatura specifiche da seguire. Per ulteriori informazioni su come mappare [!DNL Marketo] set di dati su XDM, vedere:

* [Attività](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [Programmi](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [Iscrizioni al programma](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [Aziende](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [Elenchi statici](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [Appartenenze a elenchi statici](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [Account denominati](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [Opportunità](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [Ruoli di contatto opportunità](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [Persone](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

In base alle tue esigenze, puoi scegliere di mappare i campi direttamente o utilizzare le funzioni di preparazione dati per trasformare i dati sorgente in modo da derivare valori calcolati o calcolati. Per i passaggi completi sull&#39;utilizzo dell&#39;interfaccia di mappatura, consulta la [Guida dell&#39;interfaccia utente della preparazione dati](../../../../../data-prep/ui/mapping.md).

![Interfaccia di mapping per i dati di Marketo.](../../../../images/tutorials/create/marketo/mapping.png)

Quando i set di mappatura sono pronti, seleziona **[!UICONTROL Successivo]** e attendi alcuni istanti per la creazione del nuovo flusso di dati.

## Verifica il flusso di dati

Viene visualizzato il passaggio **[!UICONTROL Rivedi]**, che consente di rivedere il nuovo flusso di dati prima che venga creato. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: mostra il tipo di origine, il percorso pertinente dell&#39;entità di origine selezionata e la quantità di colonne all&#39;interno di tale entità di origine.
* **[!UICONTROL Assegna set di dati e mappa i campi]**: mostra in quale set di dati vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati aderisce.

Dopo aver rivisto il flusso di dati, seleziona **[!UICONTROL Salva e acquisisci]** e lascia un po&#39; di tempo per la creazione del flusso di dati.

![Pagina di revisione in cui puoi confermare i dettagli del flusso di dati prima dell&#39;acquisizione.](../../../../images/tutorials/create/marketo/review.png)

## Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni su tassi di acquisizione, successo ed errori. Per ulteriori informazioni su come monitorare i flussi di dati, consulta l&#39;esercitazione sul [monitoraggio dei flussi di dati nell&#39;interfaccia utente](../../../../../dataflows/ui/monitor-sources.md).

## Eliminare gli attributi

Gli attributi personalizzati nei set di dati non possono essere nascosti o rimossi retroattivamente. Se desideri nascondere o rimuovere un attributo personalizzato da un set di dati esistente, devi creare un nuovo set di dati senza questo attributo personalizzato, un nuovo schema XDM e configurare un nuovo flusso di dati per il nuovo set di dati creato. È inoltre necessario disabilitare o eliminare il flusso di dati originale costituito dal set di dati con l’attributo personalizzato che si desidera nascondere o rimuovere.

## Eliminare il flusso di dati

È possibile eliminare i flussi di dati non più necessari o creati in modo errato utilizzando la funzione **[!UICONTROL Elimina]** disponibile nell&#39;area di lavoro [!UICONTROL Flussi di dati]. Per ulteriori informazioni su come eliminare i flussi di dati, vedere l&#39;esercitazione sull&#39;eliminazione di [flussi di dati nell&#39;interfaccia utente](../../delete.md).

## Passaggi successivi

Seguendo questa esercitazione, hai creato un flusso di dati per acquisire dati B2B dall&#39;origine [!DNL Marketo Engage] all&#39;Experience Platform.

## Appendice {#appendix}

Le sezioni seguenti forniscono ulteriori linee guida che è possibile seguire quando si utilizza l&#39;origine [!DNL Marketo].

### Messaggi di errore nell’interfaccia utente {#error-messages}

Quando Platform rileva dei problemi nella configurazione, nell’interfaccia vengono visualizzati i seguenti messaggi di errore:

#### [!DNL Munchkin ID] non è mappato all&#39;organizzazione appropriata

L&#39;autenticazione verrà negata se [!DNL Munchkin ID] non è mappato all&#39;organizzazione Platform in uso. Configura la mappatura tra [!DNL Munchkin ID] e l&#39;organizzazione utilizzando l&#39;[[!DNL Marketo] interfaccia](https://app-sjint.marketo.com/#MM0A1).

![Messaggio di errore che indica che l&#39;istanza di Marketo non è mappata correttamente all&#39;organizzazione Adobe.](../../../../images/tutorials/create/marketo/munchkin-not-mapped.png)

#### Identità primaria mancante

Se manca un’identità primaria, il flusso di dati non viene salvato e acquisito. Prima di tentare di configurare un flusso di dati, assicurati che [esista un&#39;identità primaria nello schema XDM](../../../../../xdm/tutorials/create-schema-ui.md).

![Messaggio di errore che indica che l&#39;identità primaria non è presente nello schema XDM.](../../../../images/tutorials/create/marketo/no-primary-identity.png)

