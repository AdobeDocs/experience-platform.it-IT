---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;sorgente connettori;sorgenti sdk;sdk;SDK
title: Modello di documentazione self-service per l’interfaccia utente
description: Scopri come creare una connessione di origine YOURSOURCE utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 6471c0a2-22e8-4133-a76f-ee3c5c669ef8
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 1%

---

# Creare un *YOUR SOURCE* connessione sorgente nell’interfaccia utente

*Durante l&#39;analisi di questo modello, sostituire o eliminare tutti i paragrafi in corsivo, a partire da questo.*

*Inizia aggiornando i metadati (titolo e descrizione) nella parte superiore della pagina. Ignora tutte le istanze di UICONTROL in questa pagina. Questo tag aiuta i nostri processi di traduzione automatica a tradurre correttamente la pagina nelle diverse lingue supportate. Dopo l’invio, aggiungeremo dei tag alla documentazione.*

Questo tutorial descrive i passaggi necessari per creare *YOUR SOURCE* connettore di origine che utilizza l’interfaccia utente di Platform.

## Panoramica

*Fornisci una breve panoramica della tua azienda, compreso il valore che offre ai clienti. Includi un collegamento alla pagina Home della documentazione del prodotto, per ulteriori informazioni.*

>[!IMPORTANT]
>
>Il connettore di origine e la pagina della documentazione vengono creati e gestiti da *YourSource* team. Per eventuali richieste di informazioni o richieste di aggiornamento, contattatele direttamente all&#39;indirizzo *Inserisci il collegamento o l’indirizzo e-mail a cui puoi accedere per gli aggiornamenti*.

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

## Connetti *YOUR SOURCE* account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto *CATEGORIA DELLA TUA SORGENTE* categoria, seleziona *YOUR SOURCE* e quindi selezionare **[!UICONTROL Aggiungi dati]**.

>[!TIP]
>
>Di seguito sono riportati alcuni esempi di schermate. Durante la creazione della documentazione, sostituisci le immagini con le schermate della sorgente effettiva. È possibile utilizzare lo stesso motivo e colore di marcatura, nonché gli stessi nomi di file. Assicurati che la schermata acquisisca l’intera schermata dell’interfaccia utente di Platform. Per informazioni su come caricare le schermate, consulta la guida su [invio della documentazione per la revisione](./github.md).

![catalogo](../assets/ui/catalog.png)

Il **[!UICONTROL Connetti l’account SORGENTE]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la *YOUR SOURCE* account con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![esistente](../assets/ui/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]** e quindi fornisci un nome, una descrizione facoltativa e le tue credenziali. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![nuovo](../assets/ui/new.png)

## Passaggi successivi

*I flussi di lavoro per i passaggi rimanenti della creazione di un flusso di dati sono modulari. Se desideri effettuare una chiamata per la tua sorgente, consulta la sezione Risorse aggiuntive di seguito.*

Seguendo questa esercitazione, hai stabilito una connessione con il tuo *YOUR SOURCE* account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per inserire i dati in Platform](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html).

## Risorse aggiuntive

*Questa è una sezione facoltativa in cui puoi fornire ulteriori collegamenti alla documentazione del prodotto o a qualsiasi altro passaggio, schermata o aspetto ritenuto importante per il successo del cliente. Puoi utilizzare questa sezione per aggiungere informazioni o suggerimenti sull’intero flusso di lavoro della sorgente, in particolare se si verificano particolari &quot;gotchas&quot; che un utente finale potrebbe incontrare.*
