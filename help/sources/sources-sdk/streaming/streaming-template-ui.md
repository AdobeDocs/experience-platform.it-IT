---
title: Modello self-service della documentazione per l’interfaccia utente di Streaming SDK
description: Scopri come portare dati in streaming da un’origine a Adobe Experience Platform utilizzando l’interfaccia utente.
hide: true
hidefromtoc: true
exl-id: 82254be0-fa31-4114-a0ec-179a990e0904
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '1198'
ht-degree: 1%

---

# Creare una connessione di origine e un flusso di dati da inviare *YOUR SOURCE* dati tramite l’interfaccia utente

*Durante l&#39;analisi di questo modello, sostituire o eliminare tutti i paragrafi in corsivo, a partire da questo.*

*Inizia aggiornando i metadati (titolo e descrizione) nella parte superiore della pagina. Ignora tutte le istanze di UICONTROL in questa pagina. Questo tag aiuta i nostri processi di traduzione automatica a tradurre correttamente la pagina nelle diverse lingue supportate. Dopo l’invio, aggiungeremo dei tag alla documentazione.*

Questo tutorial descrive i passaggi necessari per creare *YOUR SOURCE* connettore di origine che utilizza l’interfaccia utente di Platform.

## Panoramica

*Fornisci una breve panoramica della tua azienda, compreso il valore che offre ai clienti. Includi un collegamento alla pagina Home della documentazione del prodotto, per ulteriori informazioni.*

>[!IMPORTANT]
>
>Il connettore di origine e la pagina della documentazione vengono creati e gestiti da *YOUR SOURCE* team. Per eventuali richieste di informazioni o richieste di aggiornamento, contattatele direttamente all&#39;indirizzo *Inserisci il collegamento o l’indirizzo e-mail a cui puoi accedere per gli aggiornamenti*.

## Prerequisiti

*In questa sezione aggiungi informazioni su tutto ciò di cui i clienti devono essere a conoscenza prima di iniziare a impostare l’origine nell’interfaccia utente di Adobe Experience Platform. Informazioni su:*

* *necessità di aggiunta a un elenco consentiti*
* *requisiti per l’hashing delle e-mail*
* *qualsiasi specifica dell’account a tuo favore*
* *come ottenere le credenziali di autenticazione per connettersi alla piattaforma*

### Raccogli le credenziali richieste

Per connettersi *YOUR SOURCE* In Platform, è necessario fornire valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| *credenziale uno* | *Aggiungere qui una breve descrizione alle credenziali di autenticazione dell&#39;origine* | *Aggiungi qui un esempio delle credenziali di autenticazione dell&#39;origine* |
| *credenziale due* | *Aggiungere qui una breve descrizione alle credenziali di autenticazione dell&#39;origine* | *Aggiungi qui un esempio delle credenziali di autenticazione dell&#39;origine* |
| *credenziale tre* | *Aggiungere qui una breve descrizione alle credenziali di autenticazione dell&#39;origine* | *Aggiungi qui un esempio delle credenziali di autenticazione dell&#39;origine* |

Per ulteriori informazioni su queste credenziali, vedere *YOUR SOURCE* documentazione di autenticazione. *Aggiungi qui il collegamento alla documentazione di autenticazione della piattaforma*.

### Integrare *YOUR SOURCE* con il tuo webhook

*Streaming SDK richiede che la sorgente sia in grado di supportare i webhook per comunicare con Experienci Platform. In questa sezione, devi fornire i passaggi che gli utenti dovranno seguire per integrare YOURSOURCE con un webhook.*

## Connetti *YOUR SOURCE* account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto **Streaming** categoria, seleziona *YOUR SOURCE* e quindi selezionare **[!UICONTROL Aggiungi dati]**.

>[!TIP]
>
>Di seguito sono riportati alcuni esempi di schermate. Durante la creazione della documentazione, sostituisci le immagini con le schermate della sorgente effettiva. È possibile utilizzare lo stesso motivo e colore di marcatura, nonché gli stessi nomi di file. Assicurati che la schermata acquisisca l’intera schermata dell’interfaccia utente di Platform. Per informazioni su come caricare le schermate, consulta la guida su [invio della documentazione per la revisione](../documentation/github.md).

![Catalogo delle origini di Experience Platform](../assets/streaming/catalog.png)

## Selezionare i dati

Il **[!UICONTROL Seleziona dati]** viene visualizzata un’interfaccia che consente di selezionare i dati da inserire in Platform.

* La parte sinistra dell’interfaccia è un browser che ti consente di visualizzare i flussi di dati disponibili all’interno del tuo account;
* La parte destra dell’interfaccia consente di visualizzare in anteprima fino a 100 righe di dati da un file JSON.

Seleziona **[!UICONTROL Carica file]** per caricare un file JSON dal sistema locale. In alternativa, puoi trascinare e rilasciare il file JSON da caricare nella [!UICONTROL Trascinare i file] pannello.

![Il passaggio Aggiungi dati del flusso di lavoro origini.](../assets/streaming/add-data.png)

Una volta caricato il file, l’interfaccia di anteprima si aggiorna e mostra un’anteprima dello schema caricato. L’interfaccia di anteprima consente di esaminare il contenuto e la struttura di un file. È inoltre possibile utilizzare [!UICONTROL Campo di ricerca] per accedere a elementi specifici dallo schema.

Al termine, seleziona **[!UICONTROL Successivo]**.

![Passaggio di anteprima del flusso di lavoro origini.](../assets/streaming/preview.png)

## Dettaglio del flusso di dati

Il **Dettagli del flusso di dati** Questo passaggio ti fornisce le opzioni per utilizzare un set di dati esistente o stabilirne uno nuovo per il flusso di dati, nonché l’opportunità di fornire un nome e una descrizione per il flusso di dati. Durante questo passaggio, puoi anche configurare le impostazioni per l’acquisizione del profilo, la diagnostica degli errori, l’acquisizione parziale e gli avvisi.

Al termine, seleziona **[!UICONTROL Successivo]**.

![Passaggio del flusso di dati dettagliato del flusso di lavoro sorgenti.](../assets/streaming/dataflow-detail.png)

## Mappatura

Il [!UICONTROL Mappatura] viene visualizzato un passaggio che fornisce un’interfaccia per mappare i campi sorgente dallo schema sorgente ai campi XDM di destinazione appropriati nello schema di destinazione.

Platform fornisce consigli intelligenti per campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso. In base alle tue esigenze, puoi scegliere di mappare i campi direttamente o utilizzare le funzioni di preparazione dati per trasformare i dati sorgente in modo da derivare valori calcolati o calcolati. Per i passaggi completi sull’utilizzo dell’interfaccia mapper e dei campi calcolati, vedi la [Guida dell’interfaccia utente per la preparazione dati](https://experienceleague.adobe.com/docs/experience-platform/data-prep/ui/mapping.html).

Una volta mappati correttamente i dati di origine, seleziona **[!UICONTROL Successivo]**.

![Passaggio di mappatura del flusso di lavoro origini.](../assets/streaming/mapping.png)

## Revisione

Il **[!UICONTROL Revisione]** viene visualizzato un passaggio che consente di rivedere il nuovo flusso di dati prima di crearlo. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: mostra il tipo di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all’interno di tale file di origine.
* **[!UICONTROL Assegna set di dati e mappa campi]**: mostra in quale set di dati vengono acquisiti i dati di origine, incluso lo schema a cui aderisce il set di dati.

Dopo aver rivisto il flusso di dati, fai clic su **[!UICONTROL Fine]** e lascia un po’ di tempo per creare il flusso di dati.

![Passaggio di revisione del flusso di lavoro origini.](../assets/streaming/review.png)

## Ottieni l’URL dell’endpoint di streaming

Una volta creato il flusso di dati di streaming, ora puoi recuperare l’URL dell’endpoint di streaming. Questo endpoint verrà utilizzato per abbonarsi al webhook, consentendo alla tua origine di streaming di comunicare con Experienci Platform.

Per recuperare l’endpoint di streaming, vai al [!UICONTROL Attività flusso di dati] pagina del flusso di dati appena creato e copia l’endpoint dalla parte inferiore della sezione [!UICONTROL Proprietà] pannello.

![Endpoint di streaming nell’attività del flusso di dati.](../assets/testing/endpoint-test.png)

## Passaggi successivi

*I flussi di lavoro per i passaggi rimanenti della creazione di un flusso di dati sono modulari. Se desideri effettuare una chiamata per la tua sorgente, consulta la sezione Risorse aggiuntive di seguito.*

Seguendo questa esercitazione, hai stabilito una connessione con il tuo *YOUR SOURCE* account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire i dati in Platform](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html).

## Risorse aggiuntive

*Questa è una sezione facoltativa in cui puoi fornire ulteriori collegamenti alla documentazione del prodotto o a qualsiasi altro passaggio, schermata o aspetto ritenuto importante per il successo del cliente. Puoi utilizzare questa sezione per aggiungere informazioni o suggerimenti sull’intero flusso di lavoro della sorgente, in particolare se si verificano particolari &quot;gotchas&quot; che un utente finale potrebbe incontrare.*
