---
title: Creare una connessione sorgente del Marketo Engage e un flusso di dati nell’interfaccia utente
description: Questa esercitazione descrive i passaggi da seguire per creare una connessione di origine del Marketo Engage e un flusso di dati nell’interfaccia utente per inserire dati B2B in Adobe Experience Platform.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: 744098777141c61ac27fe6f150c05469d5705dee
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 2%

---

# Creare un [!DNL Marketo Engage] connessione sorgente e flusso di dati nell’interfaccia utente

>[!IMPORTANT]
>
>Prima di creare un [!DNL Marketo Engage] connessione di origine e un flusso di dati, devi prima verificare di avere [ha mappato il tuo ID organizzazione Adobe](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/set-up-adobe-organization-mapping.html) in [!DNL Marketo]. Inoltre, devi anche assicurarti di aver completato [popolamento automatico [!DNL Marketo] Spazi dei nomi e schemi B2B](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md) prima di creare una connessione sorgente e un flusso di dati.

Questo tutorial descrive i passaggi necessari per creare [!DNL Marketo Engage] (in seguito denominati &quot;[!DNL Marketo]&quot;) nell’interfaccia utente per inserire dati B2B in Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Spazi dei nomi B2B e utilità di generazione automatica dello schema](../../../../connectors/adobe-applications/marketo/marketo-namespaces.md): l’utility di generazione automatica degli spazi dei nomi B2B e dello schema consente di utilizzare [!DNL Postman] per generare automaticamente i valori per gli spazi dei nomi e gli schemi B2B. Prima di creare uno schema e uno spazio dei nomi B2B, devi completare [!DNL Marketo] connessione sorgente e flusso di dati.
* [Sorgenti](../../../../home.md): un Experience Platform consente di acquisire dati da varie origini, consentendoti allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform.
* [Experience Data Model (XDM)](../../../../../xdm/home.md): framework standardizzato tramite il quale Experienci Platform organizza i dati sull’esperienza del cliente.
   * [Creare e modificare gli schemi nell’interfaccia utente](../../../../../xdm/ui/resources/schemas.md): scopri come creare e modificare gli schemi nell’interfaccia utente di.
* [Spazi dei nomi delle identità](../../../../../identity-service/features/namespaces.md): gli spazi dei nomi di identità sono un componente di [!DNL Identity Service] che fungono da indicatori del contesto a cui si riferisce un’identità. Un’identità completa include un valore ID e uno spazio dei nomi.
* [[!DNL Real-Time Customer Profile]](/help/profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../../../../sandboxes/home.md): Experienci Platform fornisce sandbox virtuali che permettono di suddividere una singola istanza Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Raccogli le credenziali richieste

Per accedere al tuo [!DNL Marketo] account di Experience Platform, è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---- | ---- |
| `munchkinId` | L&#39;ID Munchkin è l&#39;identificatore univoco di un [!DNL Marketo] dell&#39;istanza. |
| `clientId` | L’ID client univoco del tuo [!DNL Marketo] dell&#39;istanza. |
| `clientSecret` | Il segreto client univoco del tuo [!DNL Marketo] dell&#39;istanza. |

Per ulteriori informazioni sull’acquisizione di questi valori, consulta [[!DNL Marketo] guida all’autenticazione](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi descritti nella sezione successiva.

## Connetti [!DNL Marketo] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto *applicazioni Adobe* categoria, seleziona **[!UICONTROL Marketo Engage]** e quindi selezionare **[!UICONTROL Aggiungi dati]**.

>[!TIP]
>
>Le origini nel catalogo delle origini visualizzano **[!UICONTROL Configurazione]** quando una determinata origine non dispone ancora di un account autenticato. Quando esiste un account autenticato, questa opzione diventa **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini con l&#39;origine Marketo Engage selezionata.](../../../../images/tutorials/create/marketo/catalog.png)

Il **[!UICONTROL Connetti account di Marketo Engage]** viene visualizzata. In questa pagina è possibile utilizzare un nuovo account o accedere a un account esistente.

>[!BEGINTABS]

>[!TAB Crea un nuovo account]

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]** e fornisci un nome, una descrizione facoltativa e le tue credenziali.

Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![La nuova interfaccia dell’account per l’autenticazione di un nuovo account Marketo.](../../../../images/tutorials/create/marketo/new.png)

>[!TAB Usa un account esistente]

Per utilizzare un account esistente, seleziona **[!UICONTROL Account esistente]** quindi selezionare l&#39;account che si desidera utilizzare dal catalogo account esistente.

Seleziona **[!UICONTROL Avanti]** per procedere.

![Interfaccia dell&#39;account esistente in cui è possibile selezionare un account Marketo esistente.](../../../../images/tutorials/create/marketo/existing.png)

>[!ENDTABS]

## Selezionare un set di dati

Dopo aver creato [!DNL Marketo] , il passaggio successivo fornisce un&#39;interfaccia da esplorare [!DNL Marketo] set di dati.

La metà sinistra dell’interfaccia è un browser di directory, che visualizza il file 10 [!DNL Marketo] set di dati. Un sistema [!DNL Marketo] la connessione sorgente richiede l’acquisizione di nove diversi set di dati. Se utilizzi anche il [!DNL Marketo] con la funzione di marketing basato sull’account (ABM), devi anche creare un decimo flusso di dati per acquisire [!UICONTROL Account denominati] set di dati.

>[!NOTE]
>
>Per brevità, nell’esercitazione seguente vengono utilizzati [!UICONTROL Opportunità] ad esempio, ma i passaggi descritti di seguito si applicano a uno qualsiasi dei 10 [!DNL Marketo] set di dati.

Seleziona il set di dati da acquisire. Questo aggiorna l’interfaccia in modo da visualizzare un’anteprima del set di dati. Al termine, seleziona **[!UICONTROL Successivo]**.

![Interfaccia di anteprima](../../../../images/tutorials/create/marketo/preview.png)

## Fornisci i dettagli del set di dati e del flusso di dati {#provide-dataset-and-dataflow-details}

Quindi, devi fornire informazioni sul set di dati e sul flusso di dati.

### Dettagli del set di dati {#dataset-details}

Un set di dati è un costrutto di archiviazione e gestione per una raccolta di dati, in genere una tabella, che contiene uno schema (colonne) e dei campi (righe). I dati acquisiti correttamente in Experienci Platform vengono memorizzati nel data lake come set di dati. Durante questo passaggio, puoi creare un nuovo set di dati o utilizzare un set di dati esistente.

>[!BEGINTABS]

>[!TAB Utilizza un nuovo set di dati]

Per utilizzare un nuovo set di dati, seleziona **[!UICONTROL Nuovo set di dati]** quindi fornisci un nome e una descrizione facoltativa per il set di dati. Devi anche selezionare uno schema Experience Data Model (XDM) a cui aderisce il set di dati.

![La nuova interfaccia per la selezione dei set di dati.](../../../../images/tutorials/create/marketo/new-dataset.png)

>[!TAB Usa un set di dati esistente]

Se disponi già di un set di dati, seleziona **[!UICONTROL Set di dati esistente]** e quindi utilizzare il **[!UICONTROL Ricerca avanzata]** per visualizzare una finestra di tutti i set di dati dell’organizzazione, inclusi i rispettivi dettagli, ad esempio se sono abilitati o meno per l’acquisizione in Real-Time Customer Profile.

![Interfaccia di selezione del set di dati esistente.](../../../../images/tutorials/create/marketo/existing-dataset.png)

>[!ENDTABS]

### Configurazioni del flusso di dati {#dataflow-configurations}

>[!IMPORTANT]
>
>Il [!DNL Marketo] l’origine utilizza l’acquisizione in batch per acquisire tutti i record storici e l’acquisizione in streaming per gli aggiornamenti in tempo reale. Questo consente all’origine di continuare lo streaming durante l’acquisizione di eventuali record errati. Abilita **[!UICONTROL Acquisizione parziale]** e quindi impostare [!UICONTROL Soglia di errore %] al massimo per evitare errori nel flusso di dati.

Se il set di dati è abilitato per Real-Time Customer Profile, durante questo passaggio puoi attivare/disattivare **[!UICONTROL Set di dati profilo]** per abilitare i dati per l’acquisizione del profilo. Puoi anche utilizzare questo passaggio per abilitare **[!UICONTROL Diagnostica degli errori]** e **[!UICONTROL Acquisizione parziale]**.

* **[!UICONTROL Diagnostica degli errori]**: Seleziona **[!UICONTROL Diagnostica degli errori]** per indicare all’origine di produrre diagnostica degli errori a cui fare successivamente riferimento durante il monitoraggio dell’attività del set di dati e dello stato del flusso di dati.
* **[!UICONTROL Acquisizione parziale]**: [Acquisizione batch parziale](../../../../../ingestion/batch-ingestion/partial.md) è la capacità di acquisire dati contenenti errori, fino a una determinata soglia configurabile. Questa funzione consente di acquisire correttamente in Experienci Platform tutti i dati accurati, mentre tutti i dati errati vengono raggruppati separatamente con informazioni sul motivo della validità.

Durante questo passaggio, puoi abilitare **[!UICONTROL Flusso di dati di esempio]** per limitare l’acquisizione dei dati ed evitare costi aggiuntivi derivanti dall’acquisizione di tutti i dati storici, comprese le identità delle persone.

>[!BEGINSHADEBOX]

**Guida rapida all’utilizzo di un flusso di dati di esempio**

Un flusso di dati di esempio è una configurazione che puoi impostare per il tuo [!DNL Marketo] flusso di dati per limitare il tasso di acquisizione, quindi prova le funzioni di Experience Platform senza dover acquisire grandi quantità di dati.

* Abilita il flusso di dati di esempio per limitare i dati storici acquisendo fino a 100.000 record (dal più grande ID record) o fino agli ultimi 10 giorni di attività durante il processo di backfill.
* Quando utilizzi la configurazione del flusso di dati di esempio per tutte le entità B2B, devi tenere presente che alcuni record correlati potrebbero mancare perché l’intera cronologia dei dati di origine non viene acquisita.

>[!ENDSHADEBOX]

![La sezione configurazioni del flusso di dati della pagina dei dettagli del flusso di dati.](../../../../images/tutorials/create/marketo/dataflow-configurations.png)

Inoltre, se acquisisci dati dal set di dati aziendali, puoi abilitare **[!UICONTROL Escludi account non rivendicati]** per escludere dall’acquisizione gli account non rivendicati.

Quando i singoli utenti compilano un modulo, [!DNL Marketo] crea un record account fantasma in base al Nome società che non contiene altri dati. Per i nuovi flussi di dati, l’opzione per escludere gli account non rivendicati è abilitata per impostazione predefinita. Per i flussi di dati esistenti, puoi abilitare o disabilitare la funzione, con le modifiche che si applicano ai dati appena acquisiti e non ai dati esistenti.

![Escludi account non rivendicati](../../../../images/tutorials/create/marketo/unclaimed-accounts.png)

## Mappa il tuo [!DNL Marketo] campi di origine del set di dati per eseguire il targeting dei campi XDM

Il [!UICONTROL Mappatura] viene visualizzato un passaggio che fornisce un’interfaccia per mappare i campi sorgente dallo schema sorgente ai campi XDM di destinazione appropriati nello schema di destinazione.

Ogni [!DNL Marketo] il set di dati ha le proprie regole di mappatura specifiche da seguire. Per ulteriori informazioni su come eseguire la mappatura, consulta [!DNL Marketo] Set di dati per XDM:

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

In base alle tue esigenze, puoi scegliere di mappare i campi direttamente o utilizzare le funzioni di preparazione dati per trasformare i dati sorgente in modo da derivare valori calcolati o calcolati. Per i passaggi completi sull’utilizzo dell’interfaccia di mappatura, vedi [Guida dell’interfaccia utente per la preparazione dati](../../../../../data-prep/ui/mapping.md).

![Interfaccia di mappatura per i dati di Marketo.](../../../../images/tutorials/create/marketo/mapping.png)

Una volta pronti i set di mappatura, seleziona **[!UICONTROL Successivo]** e attendi alcuni istanti per la creazione del nuovo flusso di dati.

## Verifica il flusso di dati

Il **[!UICONTROL Revisione]** viene visualizzato un passaggio che consente di rivedere il nuovo flusso di dati prima di crearlo. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: mostra il tipo di origine, il percorso pertinente dell’entità di origine scelta e l’importo delle colonne all’interno di tale entità di origine.
* **[!UICONTROL Assegna set di dati e mappa campi]**: mostra in quale set di dati vengono acquisiti i dati di origine, incluso lo schema a cui aderisce il set di dati.

Dopo aver rivisto il flusso di dati, seleziona **[!UICONTROL Salva e acquisisci]** e lascia un po’ di tempo per creare il flusso di dati.

![La pagina di revisione in cui puoi confermare i dettagli del flusso di dati prima dell’acquisizione.](../../../../images/tutorials/create/marketo/review.png)

## Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni su tassi di acquisizione, successo ed errori. Per ulteriori informazioni su come monitorare i flussi di dati, consulta l’esercitazione su [monitoraggio dei flussi di dati nell’interfaccia utente](../../../../../dataflows/ui/monitor-sources.md).

## Eliminare gli attributi

Gli attributi personalizzati nei set di dati non possono essere nascosti o rimossi retroattivamente. Se desideri nascondere o rimuovere un attributo personalizzato da un set di dati esistente, devi creare un nuovo set di dati senza questo attributo personalizzato, un nuovo schema XDM e configurare un nuovo flusso di dati per il nuovo set di dati creato. È inoltre necessario disabilitare o eliminare il flusso di dati originale costituito dal set di dati con l’attributo personalizzato che si desidera nascondere o rimuovere.

## Eliminare il flusso di dati

Puoi eliminare i flussi di dati non più necessari o creati in modo errato utilizzando **[!UICONTROL Elimina]** funzione disponibile nella [!UICONTROL Flussi dati] Workspace. Per ulteriori informazioni su come eliminare i flussi di dati, consulta l’esercitazione su [eliminazione di flussi di dati nell’interfaccia utente](../../delete.md).

## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente un flusso di dati per acquisire dati B2B dal tuo [!DNL Marketo Engage] da sorgente a Experience Platform.

## Appendice {#appendix}

Le sezioni seguenti forniscono ulteriori linee guida che è possibile seguire quando si utilizza [!DNL Marketo] sorgente.

### Messaggi di errore nell’interfaccia utente {#error-messages}

Quando Platform rileva dei problemi nella configurazione, nell’interfaccia vengono visualizzati i seguenti messaggi di errore:

#### [!DNL Munchkin ID] non è mappato all’organizzazione appropriata

L&#39;autenticazione verrà negata se [!DNL Munchkin ID] non è mappato all’organizzazione Platform in uso. Configurare la mappatura tra [!DNL Munchkin ID] e la tua organizzazione utilizzando [[!DNL Marketo] Interfaccia](https://app-sjint.marketo.com/#MM0A1).

![Messaggio di errore che indica che l’istanza di Marketo non è mappata correttamente all’organizzazione Adobe.](../../../../images/tutorials/create/marketo/munchkin-not-mapped.png)

#### Identità primaria mancante

Se manca un’identità primaria, il flusso di dati non viene salvato e acquisito. Assicurati che [un’identità primaria esiste nello schema XDM](../../../../../xdm/tutorials/create-schema-ui.md), prima di tentare di configurare un flusso di dati.

![Messaggio di errore che indica che l’identità primaria non è presente nello schema XDM.](../../../../images/tutorials/create/marketo/no-primary-identity.png)

