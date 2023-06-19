---
title: Collegare l’account RainFocus a Experience Platform utilizzando l’interfaccia utente
description: Scopri come collegare il tuo account RainFocus a Experience Platform utilizzando l’interfaccia utente.
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: e90f05c44943f55630bd02d3b8bf04b01d07f320
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 1%

---

# Connetti [!DNL RainFocus] Experience Platform dell’account tramite l’interfaccia utente

>[!NOTE]
>
>Il [!DNL RainFocus] sorgente in versione beta. Consulta la [panoramica sulle origini](../../../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Questo tutorial descrive come collegare [!DNL RainFocus] gestione di eventi e dati analitici di account e streaming per Adobe Experience Platform.

>[!IMPORTANT]
>
>Questa pagina della documentazione è stata creata da [!DNL RainFocus] team. Per eventuali richieste di informazioni o richieste di aggiornamento, contattaci direttamente all’indirizzo clientcare<span>@rainfocus.com o visita il [[!DNL RainFocus] Centro risorse](https://help.rainfocus.com/hc/en-us)

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

### Prerequisiti

Prima di collegare il [!DNL RainFocus] per Experience Platform, devi prima completare le seguenti attività preliminari:

* [Raccogli le credenziali richieste](../../../../connectors/analytics/rainfocus.md#gather-required-credentials)
* [Creare uno schema XDM e definire il campo di identità](../../../../connectors/analytics/rainfocus.md#create-an-xdm-schema-and-define-the-identity-field)
* [Creare un profilo di integrazione in RainFocus](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus)

Una volta completata la configurazione dei prerequisiti, puoi procedere con i passaggi descritti di seguito.

## Collega il tuo account RainFocus a Experience Platform

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere all’area di lavoro origini. Il *[!UICONTROL Catalogo]* Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto *[!UICONTROL Analytics]* categoria, seleziona **[!UICONTROL Esperienza RainFocus]**, quindi selezionare **[!UICONTROL Aggiungi dati]**.

![Le origini vengono catalogate nell’interfaccia utente di Experience Platform con l’origine RainFocus selezionata.](/help/sources/images/tutorials/create/rainfocus/rainfocus_sources-rf.png)

## Selezionare i dati

Viene visualizzato il passaggio Seleziona dati, che fornisce un’interfaccia per la selezione dei dati da portare all’Experience Platform.

* La parte sinistra dell’interfaccia è un browser che ti consente di visualizzare i flussi di dati disponibili all’interno del tuo account;
* La parte destra dell’interfaccia consente di visualizzare in anteprima fino a 100 righe di dati da un file JSON.

Seleziona **[!UICONTROL Carica file]** per caricare un file JSON dal sistema locale. In alternativa, puoi trascinare e rilasciare il file JSON da caricare nel pannello Trascina i file.

Carica il payload JSON di esempio scaricato da **RainFocus**.

![Il passaggio seleziona dati nel flusso di lavoro origini.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-upload.png)

Una volta caricato il file, l’interfaccia di anteprima si aggiorna e mostra un’anteprima dello schema caricato. L’interfaccia di anteprima consente di esaminare il contenuto e la struttura di un file. Puoi anche utilizzare l’utility Campo di ricerca per accedere a elementi specifici dallo schema.

Al termine, seleziona **[!UICONTROL Successivo]**.

![Passaggio di anteprima dei dati del flusso di lavoro origini.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-json-preview.png)

## Dettaglio del flusso di dati

Il **Dettagli del flusso di dati** Questo passaggio ti fornisce le opzioni per utilizzare un set di dati esistente o stabilirne uno nuovo per il flusso di dati, nonché l’opportunità di fornire un nome e una descrizione per il flusso di dati. Durante questo passaggio, puoi anche configurare le impostazioni per l’acquisizione del profilo, la diagnostica degli errori, l’acquisizione parziale e gli avvisi.

Al termine, seleziona **[!UICONTROL Successivo]**.

![Il passaggio dei dettagli del flusso di dati del flusso di lavoro sorgenti.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-setup.png)

## Mappatura {#mapping}

Viene visualizzato il passaggio Mappatura, che fornisce un’interfaccia per mappare i campi sorgente dallo schema sorgente ai campi XDM di destinazione appropriati nello schema di destinazione.

Questo Experience Platform fornisce consigli intelligenti per campi mappati automaticamente in base allo schema o al set di dati di destinazione selezionato. Puoi regolare manualmente le regole di mappatura in base ai tuoi casi d’uso. In base alle tue esigenze, puoi scegliere di mappare i campi direttamente o utilizzare le funzioni di preparazione dati per trasformare i dati sorgente in modo da derivare valori calcolati o calcolati. Per i passaggi completi sull’utilizzo dell’interfaccia mapper e dei campi calcolati, vedi la [Guida dell’interfaccia utente per la preparazione dati](../../../../../data-prep/ui/mapping.md).

Una volta mappati correttamente i dati di origine, seleziona **[!UICONTROL Successivo]**.

![Passaggio di mappatura del flusso di lavoro origini.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-mappings.png)

## Revisione

Il **Revisione** viene visualizzato un passaggio che consente di rivedere il nuovo flusso di dati prima di crearlo. I dettagli sono raggruppati nelle seguenti categorie:

* **Connessione**: mostra il tipo di origine, il percorso pertinente del file di origine scelto e la quantità di colonne all’interno di tale file di origine.
* **Assegna set di dati e mappa campi**: mostra in quale set di dati vengono acquisiti i dati di origine, incluso lo schema a cui aderisce il set di dati.

Dopo aver rivisto il flusso di dati, seleziona **Fine** e lascia un po’ di tempo per creare il flusso di dati.

![Passaggio di revisione del flusso di lavoro origini.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-compelete.png)

## Ottieni l’URL dell’endpoint di streaming {#get-your-streaming-endpoint-url}

Una volta creato il flusso di dati di streaming, ora puoi recuperare l’URL dell’endpoint di streaming. Questo endpoint verrà utilizzato per abbonarsi al webhook, consentendo alla tua origine di streaming di comunicare con Experience Platform.

Per recuperare l’endpoint di streaming, vai al *[!UICONTROL Attività flusso di dati]* pagina del flusso di dati appena creato e copia l’endpoint dalla parte inferiore della sezione *[!UICONTROL Proprietà]* pannello.

![La pagina dell’attività Flusso di dati nell’area di lavoro delle origini, con l’URL dell’endpoint di streaming evidenziato.](/help/sources/images/tutorials/create/rainfocus/rainfocus_source-dataflow-api.png)

## Attivare il profilo di integrazione in RainFocus

Una volta completato il flusso di dati e recuperato l’URL dell’endpoint di streaming, ora puoi attivare [!DNL Integration Profile] in [!DNL RainFocus].

* Accedi a [[!DNL RainFocus] piattaforma](https://app.rainfocus.com). Nella navigazione principale, seleziona **[!DNL Libraries]** e **[!DNL Integration Profiles]**
* Apri [!DNL Integration Profile] creato in precedenza come parte del [prerequisiti](../../../../connectors/analytics/rainfocus.md#create-an-integration-profile-in-rainfocus).
* Incolla il **ID flusso di dati** e **Endpoint di streaming** copiato dal flusso di dati in Experience Platform e seleziona **Salva**

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione per il tuo [!DNL RainFocus] , che consente di eseguire lo streaming dei dati di gestione degli eventi e analisi da Experience Platform.

## Risorse aggiuntive

I seguenti documenti forniscono ulteriori indicazioni sulle sfumature relative al [!DNL RainFocus] sorgente.

* [Centro assistenza RainFocus](https://help.rainfocus.com/hc/en-us)
* [Creare un account di servizio Adobe (JWT) nel portale Adobe Developer](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)
* [Creare uno schema nell’API](../../../../../xdm/tutorials/create-schema-api.md)
* [Creare uno schema nell’interfaccia utente](../../../../../xdm/tutorials/create-schema-ui.md)
* [Definire i campi di identità nell’interfaccia utente](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)