---
title: Collegare l’account RainFocus a Experience Platform utilizzando l’interfaccia utente
description: Scopri come collegare il tuo account RainFocus a Experience Platform utilizzando l’interfaccia utente.
badge: Beta
exl-id: a349e37e-9f2c-47ff-8360-ccbe578dce27
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 1%

---

# Connetti il tuo account [!DNL RainFocus] ad Experience Platform utilizzando l&#39;interfaccia utente

>[!NOTE]
>
>L&#39;origine [!DNL RainFocus] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, vedere la [panoramica origini](../../../../home.md#terms-and-conditions).

Questo tutorial illustra i passaggi necessari per collegare l&#39;account [!DNL RainFocus] e inviare i dati di analisi e gestione degli eventi a Adobe Experience Platform.

>[!IMPORTANT]
>
>Il connettore di origine e la pagina della documentazione vengono creati e gestiti dal team [!DNL RainFocus]. Per eventuali richieste di informazioni o richieste di aggiornamento, contattali direttamente all&#39;indirizzo clientcare<span>@rainfocus.com o visita il [[!DNL RainFocus] Centro assistenza](https://help.rainfocus.com/hc/en-us)

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato in base al quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

### Prerequisiti

Prima di connettere l&#39;account [!DNL RainFocus] ad Experience Platform, è necessario completare le seguenti attività preliminari:

* [Raccogli le credenziali richieste](../../../../connectors/analytics/rainfocus.md#gather-required-credentials)
* [Creare uno schema XDM e definire il campo di identità](../../../../connectors/analytics/rainfocus.md#create-an-xdm-schema-and-define-the-identity-field)
* [Creare un profilo di integrazione in RainFocus](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus)

Una volta completata la configurazione dei prerequisiti, puoi procedere con i passaggi descritti di seguito.

## Collega il tuo account RainFocus a Experience Platform

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro origini. Nella schermata *[!UICONTROL Catalogo]* sono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria *[!UICONTROL Analytics]*, selezionare **[!UICONTROL Esperienza RainFocus]**, quindi **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini nell&#39;interfaccia utente di Experience Platform con l&#39;origine RainFocus selezionata.](/help/sources/images/tutorials/create/rainfocus/rainfocus_sources-rf.png)

## Selezionare i dati

Viene visualizzato il passaggio Seleziona dati, che fornisce un’interfaccia per la selezione dei dati da portare all’Experience Platform.

* La parte sinistra dell’interfaccia è un browser che ti consente di visualizzare i flussi di dati disponibili all’interno del tuo account;
* La parte destra dell’interfaccia consente di visualizzare in anteprima fino a 100 righe di dati da un file JSON.

Seleziona **[!UICONTROL Carica file]** per caricare un file JSON dal sistema locale. In alternativa, puoi trascinare e rilasciare il file JSON da caricare nel pannello Trascina i file.

Carica il payload JSON di esempio scaricato da **RainFocus**.

![Il passaggio di selezione dei dati nel flusso di lavoro delle origini.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-upload.png)

Una volta caricato il file, l’interfaccia di anteprima si aggiorna e mostra un’anteprima dello schema caricato. L’interfaccia di anteprima consente di esaminare il contenuto e la struttura di un file. Puoi anche utilizzare l’utility Campo di ricerca per accedere a elementi specifici dallo schema.

Al termine, selezionare **[!UICONTROL Avanti]**.

![Passaggio di anteprima dati del flusso di lavoro origini.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-preview.png)

## Dettaglio del flusso di dati

Viene visualizzato il passaggio **Dettagli flusso di dati** che fornisce le opzioni per utilizzare un set di dati esistente o stabilirne uno nuovo per il flusso di dati, nonché l&#39;opportunità di fornire un nome e una descrizione per il flusso di dati. Durante questo passaggio, puoi anche configurare le impostazioni per l’acquisizione del profilo, la diagnostica degli errori, l’acquisizione parziale e gli avvisi.

Al termine, selezionare **[!UICONTROL Avanti]**.

![Passaggio dei dettagli del flusso di dati del flusso di lavoro delle origini.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-setup.png)

## Mappatura {#mapping}

Viene visualizzato il passaggio Mappatura, che fornisce un’interfaccia per mappare i campi sorgente dallo schema sorgente ai campi XDM di destinazione appropriati nello schema di destinazione.

Questo Experience Platform fornisce consigli intelligenti per campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso. In base alle tue esigenze, puoi scegliere di mappare i campi direttamente o utilizzare le funzioni di preparazione dati per trasformare i dati sorgente in modo da derivare valori calcolati o calcolati. Per i passaggi completi sull&#39;utilizzo dell&#39;interfaccia mapper e dei campi calcolati, consulta la [guida dell&#39;interfaccia utente della preparazione dati](../../../../../data-prep/ui/mapping.md).

Una volta mappati correttamente i dati di origine, seleziona **[!UICONTROL Avanti]**.

![Passaggio di mappatura del flusso di lavoro di origine.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-mappings.png)

## Controlla

Viene visualizzato il passaggio **Rivedi**, che consente di rivedere il nuovo flusso di dati prima che venga creato. I dettagli sono raggruppati nelle seguenti categorie:

* **Connessione**: mostra il tipo di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all&#39;interno di tale file di origine.
* **Assegna set di dati e mappa i campi**: mostra in quale set di dati vengono acquisiti i dati di origine, incluso lo schema a cui il set di dati aderisce.

Dopo aver rivisto il flusso di dati, seleziona **Fine** e attendi che venga creato un po&#39; di tempo.

![Passaggio di revisione del flusso di lavoro origini.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-compelete.png)

## Ottieni l’URL dell’endpoint di streaming {#get-your-streaming-endpoint-url}

Una volta creato il flusso di dati di streaming, ora puoi recuperare l’URL dell’endpoint di streaming. Questo endpoint verrà utilizzato per abbonarsi al webhook, consentendo alla tua origine di streaming di comunicare con Experience Platform.

Per recuperare l&#39;endpoint di streaming, vai alla pagina *[!UICONTROL Attività flusso di dati]* del flusso di dati appena creato e copia l&#39;endpoint dalla parte inferiore del pannello *[!UICONTROL Proprietà]*.

![Pagina dell&#39;attività del flusso di dati nell&#39;area di lavoro origini, con l&#39;URL dell&#39;endpoint di streaming evidenziato.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-api.png)

## Attivare il profilo di integrazione in RainFocus

Una volta completato il flusso di dati e recuperato l&#39;URL dell&#39;endpoint di streaming, puoi attivare [!DNL Integration Profile] in [!DNL RainFocus].

* Accedi alla [[!DNL RainFocus] piattaforma](https://app.rainfocus.com). Nella navigazione principale, selezionare **[!DNL Libraries]** e **[!DNL Integration Profiles]**
* Apri [!DNL Integration Profile] creato in precedenza come parte dei [prerequisiti](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus).
* Incolla l&#39;**ID flusso di dati** e l&#39;**endpoint di streaming** copiati dal flusso di dati in Experience Platform e seleziona **Salva**

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione per l&#39;origine [!DNL RainFocus], che ti consente di eseguire lo streaming dei dati di analisi e gestione degli eventi su Experience Platform.

## Risorse aggiuntive

I documenti seguenti forniscono ulteriori indicazioni sulle sfumature che circondano l&#39;origine [!DNL RainFocus].

* [Centro assistenza RainFocus](https://help.rainfocus.com/hc/en-us)
* [Creare un account di servizio Adobe (JWT) nel portale Adobe Developer](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)
* [Creare uno schema nell’API](../../../../../xdm/tutorials/create-schema-api.md)
* [Creare uno schema nell’interfaccia utente](../../../../../xdm/tutorials/create-schema-ui.md)
* [Definisci i campi di identità nell&#39;interfaccia utente](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)
