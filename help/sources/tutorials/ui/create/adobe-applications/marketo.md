---
keywords: Experience Platform;home;argomenti comuni;connettore sorgente Marketo;connettore Marketo;sorgente Marketo;Marketo
solution: Experience Platform
title: Creare un connettore sorgente di Marketo Engage nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Questa esercitazione fornisce passaggi per creare un connettore di origine di Marketo Engage nell’interfaccia utente per inserire dati B2B in Adobe Experience Platform.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
source-git-commit: 21617c6ec364fc05d7b8b6d00daa68608d1ed318
workflow-type: tm+mt
source-wordcount: '1336'
ht-degree: 0%

---

# Crea un [!DNL Marketo Engage] connettore sorgente nell’interfaccia utente

Questa esercitazione fornisce i passaggi per la creazione di un [!DNL Marketo Engage] (in appresso denominato &quot;[!DNL Marketo]&quot;) connettore di origine nell&#39;interfaccia utente per inserire dati B2B in Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [Origini](../../../../home.md): L’Experience Platform consente di acquisire dati da varie sorgenti e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform.
* [Experience Data Model (XDM)](../../../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   * [Creare e modificare schemi nell’interfaccia utente](../../../../../xdm/ui/resources/schemas.md): Scopri come creare e modificare schemi nell’interfaccia utente di .
* [Namespace Identity](../../../../../identity-service/namespaces.md): Gli spazi dei nomi di identità sono un componente di [!DNL Identity Service] che fungono da indicatori del contesto a cui si riferisce un&#39;identità. Un&#39;identità completa include un valore ID e uno spazio dei nomi.
* [[!DNL Real-time Customer Profile]](/help/profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza di Platform in ambienti virtuali separati per sviluppare e sviluppare applicazioni di esperienza digitale.

### Raccogli credenziali richieste

Per accedere al tuo [!DNL Marketo] su Platform, devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `munchkinId` | L&#39;ID Munchkin è l&#39;identificatore univoco per uno specifico [!DNL Marketo] istanza. |
| `clientId` | L&#39;ID client univoco del tuo [!DNL Marketo] istanza. |
| `clientSecret` | Il segreto client univoco del tuo [!DNL Marketo] istanza. |

Per ulteriori informazioni sull&#39;acquisizione di questi valori, consulta la sezione [[!DNL Marketo] guida all’autenticazione](../../../../connectors/adobe-applications/marketo/marketo-auth.md).

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi descritti nella sezione successiva.

## Collega il tuo [!DNL Marketo] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in questa schermata vengono visualizzate diverse sorgenti per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando la barra di ricerca.

Sotto la [!UICONTROL Applicazioni di Adobe] categoria, seleziona **[!UICONTROL Marketo Engage]**. Quindi, seleziona **[!UICONTROL Aggiungi dati]** per creare una nuova [!DNL Marketo] flusso di dati.

![catalogo](../../../../images/tutorials/create/marketo/catalog.png)

La **[!UICONTROL Connetti al Marketo Engage]** viene visualizzata la pagina . In questa pagina puoi utilizzare un nuovo account o accedere a un account esistente.

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome account, una descrizione facoltativa e il tuo [!DNL Marketo] credenziali di autenticazione. Al termine, seleziona **[!UICONTROL Connetti alla sorgente]** e quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

![nuovo account](../../../../images/tutorials/create/marketo/new.png)

### Account esistente

Per creare un flusso di dati con un account esistente, seleziona **[!UICONTROL Account esistente]** quindi seleziona la [!DNL Marketo] account che desideri utilizzare. Seleziona **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/marketo/existing.png)

## Selezionare un set di dati

Dopo aver creato il [!DNL Marketo] il passaggio successivo fornisce un’interfaccia da esplorare [!DNL Marketo] set di dati.

La metà sinistra dell&#39;interfaccia è un browser di directory, che visualizza il 10 [!DNL Marketo] set di dati. Un funzionamento completo [!DNL Marketo] la connessione di origine richiede l’acquisizione dei nove set di dati diversi. Se utilizzi anche il [!DNL Marketo] funzionalità di marketing basato sull’account (ABM), quindi devi anche creare un decimo flusso di dati per acquisire il [!UICONTROL Account denominati] set di dati.

>[!NOTE]
>
>Per motivi di brevità, l’esercitazione seguente utilizza [!UICONTROL Account denominati] ad esempio, ma i passaggi descritti di seguito si applicano a uno qualsiasi dei 10 [!DNL Marketo] set di dati.

Seleziona il set di dati da acquisire prima, quindi seleziona **[!UICONTROL Successivo]**.

![select-data](../../../../images/tutorials/create/marketo/select-data.png)

## Mappa [!DNL Marketo] schemi a Platform

La [!UICONTROL Mappatura] viene visualizzato un passaggio che fornisce un&#39;interfaccia per la mappatura [!DNL Marketo] schemi per Platform.

Scegli un set di dati in entrata in cui acquisire i dati. Puoi utilizzare un set di dati esistente o crearne uno nuovo.

### Utilizzare un set di dati esistente

Per acquisire dati in un set di dati esistente, seleziona **[!UICONTROL Set di dati esistente]**, quindi seleziona l’icona del set di dati .

![set di dati esistente](../../../../images/tutorials/create/marketo/existing-dataset.png)

La **[!UICONTROL Seleziona set di dati]** viene visualizzata la finestra di dialogo . Trova il set di dati con lo schema appropriato da utilizzare, selezionalo, quindi seleziona **[!UICONTROL Conferma]**.

![select-existing-dataset](../../../../images/tutorials/create/marketo/select-dataset.png)

### Utilizzare un nuovo set di dati

Per acquisire dati in un nuovo set di dati, seleziona **[!UICONTROL Nuovo set di dati]** e immetti un nome e una descrizione per il set di dati nei campi forniti.

È possibile cercare uno schema immettendone il nome nel **[!UICONTROL Seleziona schema]** barra di ricerca. Puoi anche selezionare l’icona a discesa per visualizzare un elenco degli schemi esistenti. In alternativa, è possibile selezionare **[!UICONTROL Ricerca avanzata]** per accedere alla pagina degli schemi esistenti, compresi i relativi dettagli.

Attiva/disattiva la **[!UICONTROL Set di dati del profilo]** per abilitare il set di dati di destinazione per [!DNL Profile], che consente di creare una visualizzazione olistica degli attributi e dei comportamenti di un’entità. Dati da tutti [!DNL Profile]I set di dati abilitati verranno inclusi in [!DNL Profile] e le modifiche vengono applicate al salvataggio del flusso di dati.

![create-new-dataset](../../../../images/tutorials/create/marketo/new-dataset-schema.png)

Dopo aver selezionato uno schema, scorri verso il basso per visualizzare la finestra di dialogo di mappatura per iniziare a mappare [!DNL Marketo] campi set di dati per i campi XDM di destinazione appropriati.

### Mappa il tuo [!DNL Marketo] campi di origine del set di dati per eseguire il targeting dei campi XDM

Ogni [!DNL Marketo] Il set di dati ha le proprie regole di mappatura specifiche da seguire. Per ulteriori informazioni su come eseguire la mappatura, consulta quanto segue [!DNL Marketo] set di dati in XDM:

* [Attività](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [Programmi](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [Partecipazioni al programma](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [Aziende](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [Elenchi statici](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [appartenenze a elenchi statici](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [Account denominati](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [Opportunità](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [Ruoli di contatto opportunità](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [Persone](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

Seleziona **[!UICONTROL Anteprima dati]** per visualizzare i risultati della mappatura in base al set di dati selezionato.

![mappatura](../../../../images/tutorials/create/marketo/mapping.png)

La [!UICONTROL Anteprima] popover offre un’interfaccia per esplorare i risultati della mappatura di fino a 100 righe di dati di esempio dal set di dati selezionato.

![anteprima](../../../../images/tutorials/create/marketo/mapping-preview.png)

Una volta mappati i campi di origine ai campi di destinazione appropriati, seleziona **[!UICONTROL Chiudi]**.

## Fornire i dettagli del flusso di dati

La [!UICONTROL Dettaglio flusso di dati] viene visualizzato un passaggio che ti consente di fornire un nome e una breve descrizione del nuovo flusso di dati.

![dettaglio del flusso di dati](../../../../images/tutorials/create/marketo/dataflow-detail.png)

Abilita la **[!UICONTROL Diagnostica degli errori]** per consentire la generazione dettagliata di messaggi di errore per i batch appena acquisiti, che puoi scaricare utilizzando l’API. Per ulteriori informazioni, consulta l’esercitazione su [recupero della diagnostica degli errori di acquisizione dei dati](../../../../../ingestion/quality/error-diagnostics.md).

![errori](../../../../images/tutorials/create/marketo/errors.png)

La [!DNL Marketo] connettore utilizza l’acquisizione batch per acquisire tutti i record storici e utilizza l’acquisizione in streaming per aggiornamenti in tempo reale. Questo consente al connettore di continuare lo streaming durante l’acquisizione di eventuali record errati. Abilita la **[!UICONTROL Acquisizione parziale]** attivare/disattivare e quindi impostare la [!UICONTROL Soglia errore %] per evitare errori nel flusso di dati.

**[!UICONTROL Acquisizione parziale]** consente di acquisire dati contenenti errori fino a una determinata soglia. Per ulteriori informazioni, consulta la sezione [panoramica dell’acquisizione parziale in batch](../../../../../ingestion/batch-ingestion/partial.md).

Dopo aver fornito i dettagli del flusso di dati e impostato la soglia di errore su max, seleziona **[!UICONTROL Successivo]**.

![assimilazione parziale](../../../../images/tutorials/create/marketo/partial-ingestion.png)

## Controlla il tuo flusso di dati

La **[!UICONTROL Revisione]** viene visualizzato un passaggio che consente di rivedere il nuovo flusso di dati prima della creazione. I dettagli sono raggruppati nelle seguenti categorie:

* **[!UICONTROL Connessione]**: Mostra il tipo di origine, il percorso pertinente dell&#39;entità di origine selezionata e la quantità di colonne all&#39;interno dell&#39;entità di origine.
* **[!UICONTROL Assegna set di dati e campi mappa]**: Mostra il set di dati in cui vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati aderisce.

Dopo aver esaminato il flusso di dati, seleziona **[!UICONTROL Fine]** e lascia un certo tempo per la creazione del flusso di dati.

![revisione](../../../../images/tutorials/create/marketo/review.png)

## Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni sui tassi di acquisizione, sul successo e sugli errori. Per ulteriori informazioni su come monitorare i flussi di dati, consulta l’esercitazione su [monitoraggio dei flussi di dati nell’interfaccia utente](../../../../../dataflows/ui/monitor-sources.md).

## Eliminare gli attributi

Gli attributi personalizzati nei set di dati non possono essere nascosti o rimossi retroattivamente. Se desideri nascondere o rimuovere un attributo personalizzato da un set di dati esistente, devi creare un nuovo set di dati senza questo attributo personalizzato, un nuovo schema XDM e configurare un nuovo flusso di dati per il nuovo set di dati creato. È inoltre necessario disattivare o eliminare il flusso di dati originale costituito dal set di dati con l’attributo personalizzato che si desidera nascondere o rimuovere.

## Elimina il flusso di dati

È possibile eliminare i flussi di dati che non sono più necessari o che sono stati creati in modo errato utilizzando **[!UICONTROL Elimina]** funzione disponibile nella [!UICONTROL Flussi di dati] workspace. Per ulteriori informazioni su come eliminare i flussi di dati, consulta l’esercitazione su [eliminazione dei flussi di dati nell’interfaccia utente](../../delete.md).

## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente un flusso di dati da importare [!DNL Marketo] dati. I dati in arrivo possono ora essere utilizzati dai servizi della piattaforma a valle, come [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Per ulteriori informazioni, consulta i seguenti documenti:

* [[!DNL Real-time Customer Profile] panoramica](/help/profile/home.md)
* [[!DNL Data Science Workspace] panoramica](/help/data-science-workspace/home.md)
