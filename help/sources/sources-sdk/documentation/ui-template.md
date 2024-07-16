---
keywords: Experience Platform;home;argomenti popolari;origini;connettori;sorgente connettori;sorgenti sdk;sdk;SDK
title: Modello di documentazione self-service per l’interfaccia utente
description: Scopri come creare una connessione di origine YOURSOURCE utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 6471c0a2-22e8-4133-a76f-ee3c5c669ef8
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 1%

---

# Crea una connessione di origine *YOURSOURCE* nell&#39;interfaccia utente

*Sostituire o eliminare tutti i paragrafi in corsivo a partire da questo modello.*

*Per iniziare, aggiorna i metadati (titolo e descrizione) nella parte superiore della pagina. Ignora tutte le istanze di UICONTROL in questa pagina. Questo tag aiuta i nostri processi di traduzione automatica a tradurre correttamente la pagina nelle diverse lingue supportate. Dopo l&#39;invio aggiungeremo i tag alla documentazione.*

Questo tutorial descrive i passaggi per creare un connettore di origine *YOURSOURCE* tramite l&#39;interfaccia utente di Platform.

## Panoramica

*Fornisci una breve panoramica della tua azienda, compreso il valore che offre ai clienti. Includi un collegamento alla home page della documentazione del prodotto, per ulteriori informazioni.*

>[!IMPORTANT]
>
>Il connettore di origine e la pagina della documentazione vengono creati e gestiti dal team *YourSource*. Per eventuali richieste di informazioni o richieste di aggiornamento, è possibile contattarle direttamente all&#39;indirizzo *Inserire il collegamento o l&#39;indirizzo di posta elettronica a cui è possibile accedere per gli aggiornamenti*.

## Prerequisiti

*Aggiungere informazioni in questa sezione su qualsiasi elemento di cui i clienti devono essere a conoscenza prima di iniziare a configurare l&#39;origine nell&#39;interfaccia utente di Adobe Experience Platform. Informazioni su:*

* *da aggiungere a un elenco consentiti*
* *requisiti per l&#39;hashing delle e-mail*
* *qualsiasi specifica account sul tuo lato*
* *come ottenere le credenziali di autenticazione per connettersi alla piattaforma*

### Raccogli le credenziali richieste

Per connettere *YOURSOURCE* a Platform, è necessario fornire i valori per le proprietà di connessione seguenti:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| *credenziali uno* | *Aggiungere qui una breve descrizione alle credenziali di autenticazione dell&#39;origine* | *Aggiungi qui un esempio delle credenziali di autenticazione dell&#39;origine* |
| *credenziali due* | *Aggiungere qui una breve descrizione alle credenziali di autenticazione dell&#39;origine* | *Aggiungi qui un esempio delle credenziali di autenticazione dell&#39;origine* |
| *credenziali tre* | *Aggiungere qui una breve descrizione alle credenziali di autenticazione dell&#39;origine* | *Aggiungi qui un esempio delle credenziali di autenticazione dell&#39;origine* |

Per ulteriori informazioni su queste credenziali, vedere la documentazione relativa all&#39;autenticazione di *YOURSOURCE*. *Aggiungi qui il collegamento alla documentazione di autenticazione della tua piattaforma*.

## Connetti il tuo account *YOURSOURCE*

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria *CATEGORIA* DELL&#39;ORIGINE, selezionare *ORIGINE PERSONALE*, quindi **[!UICONTROL Aggiungi dati]**.

>[!TIP]
>
>Di seguito sono riportati alcuni esempi di schermate. Durante la creazione della documentazione, sostituisci le immagini con le schermate della sorgente effettiva. È possibile utilizzare lo stesso motivo e colore di marcatura, nonché gli stessi nomi di file. Assicurati che la schermata acquisisca l’intera schermata dell’interfaccia utente di Platform. Per informazioni su come caricare le schermate, consulta la guida in [invio della documentazione per la revisione](./github.md).

![catalogo](../assets/ui/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti account YOURSOURCE]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona l&#39;account *YOURSOURCE* con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Next]** per continuare.

![esistente](../assets/ui/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e le tue credenziali. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![nuovo](../assets/ui/new.png)

## Passaggi successivi

*I flussi di lavoro per i passaggi rimanenti della creazione di un flusso di dati sono modulari. In caso di chiamate specifiche che si desidera effettuare per quanto riguarda la propria origine, vedere la sezione Risorse aggiuntive di seguito.*

Seguendo questa esercitazione, hai stabilito una connessione al tuo account *YOURSOURCE*. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per inserire dati in Platform](https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/dataflow/crm.html).

## Risorse aggiuntive

*Questa è una sezione facoltativa in cui puoi fornire ulteriori collegamenti alla documentazione del tuo prodotto o qualsiasi altro passaggio, schermata, sfumature che ritieni importanti per il successo del cliente. È possibile utilizzare questa sezione per aggiungere informazioni o suggerimenti sull&#39;intero flusso di lavoro dell&#39;origine, soprattutto se sono presenti particolari &quot;gotchas&quot; che un utente finale potrebbe incontrare.*
