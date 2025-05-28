---
title: Panoramica dell’estensione Algolia per l’inoltro degli eventi
description: Scopri come impostare e utilizzare l’estensione di inoltro eventi Algolia in Adobe Experience Platform. Inoltra i dati sul comportamento degli utenti tramite l’API Insights, configura le regole, mappa i campi XDM e verifica la consegna dell’evento.
last-substantial-update: 2025-05-09T00:00:00Z
source-git-commit: d1b641ed0b48357a2f4b78d6829ccab52e4889ca
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 0%

---


# Panoramica dell&#39;estensione per l&#39;inoltro degli eventi [!DNL Algolia] {#overview}

>[!NOTE]
>
>Adobe Experience Platform Launch fa ora parte delle tecnologie di raccolta dati di Adobe Experience Platform. Di conseguenza, nella documentazione del prodotto sono stati apportati aggiornamenti terminologici. Per un elenco completo di queste modifiche, consulta la [guida agli aggiornamenti terminologici](../../../../tags/term-updates.md).

Utilizza [!DNL Algolia] per fornire esperienze di ricerca veloci, rilevanti e personalizzate. Con l’ottimizzazione basata sull’intelligenza artificiale, puoi migliorare i risultati della ricerca e i consigli per aiutare gli utenti a trovare rapidamente i prodotti, i contenuti o le informazioni di cui hanno bisogno.

Utilizzare l&#39;estensione di inoltro eventi [!DNL Algolia] per inviare eventi di comportamento utente a [!DNL Algolia] tramite [!DNL Insights API]. Questi dati comportamentali consentono consigli basati sull’intelligenza artificiale, esperienze personalizzate e funzionalità di ricerca intelligente.

## Prerequisiti {#prerequisites}

Prima di installare l&#39;estensione, verificare di disporre di un account [!DNL Algolia] con accesso a [!DNL Insights API]. Se non disponi di un account, [iscriviti](https://dashboard.algolia.com/users/sign_up) e abilita l&#39;accesso all&#39;API.

Assicurarsi inoltre di aver compreso come utilizzare [!DNL Algolia] [!DNL Insights API]. Per una panoramica su come inviare eventi, consulta [invio di eventi con API Insights](https://www.algolia.com/doc/guides/sending-events/getting-started/).

Raccogliere i valori seguenti dal dashboard dell&#39;account [!DNL Algolia]:
- **[!UICONTROL ID applicazione]**
- **[!UICONTROL Chiave API di ricerca]**
- **[!UICONTROL Nome indice]**

## Installare l’estensione {#install}

Per installare l&#39;estensione [!DNL Algolia], eseguire la procedura seguente:

Passa a **[!UICONTROL Raccolta dati]** in [!DNL Adobe Experience Platform]. Selezionare la scheda **[!UICONTROL Estensioni]**.

Apri il **[!UICONTROL Catalogo]** e individua l&#39;estensione **[!UICONTROL Inoltro eventi Algolia]**, quindi seleziona **[!UICONTROL Installa]**.

![Processo di installazione per l&#39;estensione Algolia Event Forwarding in Adobe Experience Platform](../../../images/extensions/server/algolia/install-extension.png)

### Configurare l&#39;estensione {#configure-extension}

Per configurare l&#39;estensione per l&#39;inoltro degli eventi [!DNL Algolia], passare alla scheda **[!UICONTROL Estensioni]**, selezionare l&#39;estensione **[!UICONTROL Algolia]**, quindi selezionare **[!UICONTROL Configura]**.

![Schermata di configurazione per l&#39;estensione di inoltro eventi Algolia in Adobe Experience Platform](../../../images/extensions/server/algolia/configure.png)

| Proprietà | Descrizione |
|----------|-------------|
| **[!UICONTROL ID applicazione]** | Immetti l&#39;[!UICONTROL ID applicazione] trovato nel dashboard Algolia nella sezione [Chiavi API](https://www.algolia.com/account/api-keys/all). |
| **[!UICONTROL Chiave API di ricerca]** | Immetti la [!UICONTROL Chiave API di ricerca] trovata nel dashboard di Algolia nella sezione [Chiavi API](https://www.algolia.com/account/api-keys/all). |
| **[!UICONTROL Nome indice]** | Immetti il [!UICONTROL Nome indice] che contiene i tuoi prodotti o contenuti. Questo indice viene utilizzato come valore predefinito. |

{style="table-layout:auto"}

## [!DNL Algolia] tipi di azioni dell&#39;estensione di inoltro eventi {#action-types}

L&#39;estensione di inoltro degli eventi [!DNL Algolia] offre un singolo tipo di azione che può essere utilizzato nella sezione **[!UICONTROL Then]** di una regola:

### Invia evento {#send-event}

Configura l&#39;azione **[!UICONTROL Invia evento]** per inoltrare gli eventi a [!DNL Algolia]:

Seleziona **[!UICONTROL Regole]** > **[!UICONTROL Aggiungi regola]** o seleziona una regola esistente. Nella sezione **[!UICONTROL Then]** della regola, aggiungi un&#39;azione e seleziona **[!UICONTROL Estensione]**: [!DNL Algolia] Inoltro eventi > **[!UICONTROL Tipo azione]**: **[!UICONTROL Invia eventi]**.

![Configurazione dell&#39;azione Invia evento nell&#39;estensione di inoltro eventi in Algolia.](../../../images/extensions/server/algolia/send-event.png)

## Implementa il gruppo di campi evento [!DNL Algolia] {#algolia-field-group}

Assicurarsi di aggiungere il gruppo di campi evento [!DNL Algolia] allo schema prima di utilizzare l&#39;estensione di inoltro eventi [!DNL Algolia]. È uno dei gruppi di campi standard forniti tramite Experience Platform.

![Configurazione gruppo di campi evento Algolia](../../../images/extensions/server/algolia/algolia-field-groups.png)

### Aggiungi il gruppo di campi evento [!DNL Algolia] allo schema {#add-algolia-field-group}

Per aggiungere il gruppo di campi evento [!DNL Algolia]:

Passa a **[!UICONTROL Schemi]** e seleziona **[!UICONTROL Sfoglia]**.

Aggiungi un nuovo schema o aggiorna uno schema esistente da utilizzare per inviare eventi Web e passa il puntatore del mouse sull&#39;icona **[!UICONTROL Aggiungi]**. Immettere *[!DNL Algolia]* nella casella di ricerca per limitare i risultati.

Seleziona il gruppo di campi **[!DNL Algolia]Dettagli evento** > **[!UICONTROL Pulsante Aggiungi gruppo di campi]** > **[!UICONTROL Salva]**.

![Configurazione gruppo di campi profilo Algolia in Experience Platform](../../../images/extensions/server/algolia/algolia-profile-field-group.png)

### Mappa e invia dati utilizzando il tag [!UICONTROL Raccolta dati]

L&#39;estensione di inoltro eventi [!DNL Algolia] può essere utilizzata con **[!DNL Adobe Experience Platform Web SDK]** per inviare dati dal sito Web a [!DNL Algolia]. A tale scopo, creare una proprietà tag, mappare i dati all&#39;oggetto [!DNL XDM] e configurare le regole per l&#39;invio di eventi.

#### Passaggio 1: creare una proprietà tag con il SDK web

1. Crea una proprietà tag.
2. Installa l&#39;estensione [!DNL Adobe Experience Platform Web SDK].
3. Utilizzare questa estensione per mappare i dati da HTML al gruppo di campi **[!DNL Algolia]Event**.

![Esempio di un set di dati HTML mappato al gruppo di campi evento Algolia](../../../images/extensions/server/algolia/html-dataset.png)

#### Passaggio 2: creare un elemento dati per la mappatura [!DNL XDM]

1. Creare un [!UICONTROL elemento dati] utilizzando **[!DNL Adobe Experience Platform Web SDK]**.
2. Selezionare **[!UICONTROL oggetto XDM]** come tipo di elemento dati.
3. Mappa i dati ai campi [!DNL XDM] appropriati, assicurandoti che i campi specifici di [!DNL Algolia] siano compilati.

![](../../../images/extensions/server/algolia/xdm-mapping.png)

#### Passaggio 3: creare una regola per inviare eventi

1. Crea una nuova regola nella proprietà tag.
2. Aggiungi i trigger di evento richiesti, ad esempio caricamento pagina, o eventi di clic.
3. Aggiungere un&#39;azione utilizzando **[!DNL Adobe Experience Platform Web SDK]**.
4. Seleziona **[!UICONTROL Invia evento]** come tipo di azione.
5. Configurare l&#39;azione per utilizzare l&#39;elemento dati [!DNL XDM].

![Esempio di configurazione di un&#39;azione regola nell&#39;estensione di inoltro eventi Algolia](../../../images/extensions/server/algolia/rule-action.png)

#### Passaggio 4: pubblicare e testare

1. Pubblica le regole e le modifiche all’estensione nell’ambiente di destinazione.
2. Utilizzare [!DNL Adobe Experience Platform Debugger] per verificare che i dati vengano inviati a Adobe Experience Platform e inoltrati a [!DNL Algolia].

![Configura una regola per inviare eventi tramite l&#39;estensione Algolia](../../../images/extensions/server/algolia/adobe-debugger.png)

### Verifica eventi in [!DNL Algolia]

Dopo aver configurato l&#39;estensione di inoltro eventi [!DNL Algolia], è possibile verificare che gli eventi vengano inviati e ricevuti correttamente eseguendo la procedura seguente:

Passa alla dashboard di [!DNL Algolia] e vai a **[!UICONTROL Origini dati > Eventi > Debugger]**.

Selezionare l&#39;evento che corrisponde all&#39;evento inviato dall&#39;estensione di inoltro eventi di [!DNL Algolia] e verificare che i dati previsti siano presenti nell&#39;evento.

![Verifica eventi nel debugger Algolia](../../../images/extensions/server/algolia/algolia-debugger.png)

## Scenari di implementazione comuni

Utilizza l&#39;estensione di inoltro eventi [!DNL Algolia] per acquisire e inviare dati di interazione dell&#39;utente per vari casi d&#39;uso, migliorando la rilevanza della ricerca e la personalizzazione.

### Tracciare le visualizzazioni di prodotti o contenuti

Utilizza l&#39;estensione per tenere traccia di quando gli utenti visualizzano pagine di prodotti o contenuti, aiutando [!DNL Algolia] a comprendere gli interessi degli utenti.

### Tracciare gli eventi di conversione

Tieni traccia di eventi aggiuntivi al carrello, acquisti e altri eventi di conversione per ottimizzare i consigli basati sull&#39;intelligenza artificiale di [!DNL Algolia].

## Risoluzione dei problemi

In caso di problemi durante l&#39;implementazione dell&#39;estensione di inoltro degli eventi [!DNL Algolia], prendere in considerazione i seguenti passaggi per la risoluzione dei problemi:

### Gli eventi non vengono visualizzati in [!DNL Algolia]

Se gli eventi non vengono visualizzati in [!DNL Algolia], verificare quanto segue:

- **Verifica credenziali API**: verificare che **[!UICONTROL ID applicazione]** e **[!UICONTROL Chiave API]** corrispondano ai valori nel dashboard [!DNL Algolia].
- **Controlla Debugger eventi**: utilizza il debugger eventi [!DNL Algolia] per confermare se gli eventi vengono ricevuti. In caso contrario, verifica la configurazione della regola di inoltro degli eventi.
- **Verifica mapping XDM**: verificare che tutti i campi obbligatori nello schema [!DNL Algolia] siano mappati correttamente nell&#39;oggetto [!DNL XDM].

### Dati evento errati

- Verificare che l&#39;elemento dati dell&#39;oggetto [!DNL XDM] sia mappato con precisione allo schema [!DNL Algolia], con tutti i campi obbligatori.
- Verificare che i parametri dell&#39;evento corrispondano al formato e alla struttura previsti descritti nella documentazione API Insights di [!DNL Algolia].

## Passaggi successivi

Questa guida illustra come inviare dati a [!DNL Algolia] utilizzando [!DNL Algolia Event Forwarding Extension]. Per ulteriori informazioni sulle funzionalità di inoltro eventi in [!DNL Adobe Experience Platform], leggere la [panoramica sull&#39;inoltro eventi](../../../ui/event-forwarding/overview.md).

Per informazioni dettagliate su come eseguire il debug dell&#39;implementazione utilizzando lo strumento di monitoraggio di Experience Platform Debugger e inoltro eventi, leggere la [panoramica di Adobe Experience Platform Debugger](../../../../debugger/home.md) e le [attività di monitoraggio nell&#39;inoltro degli eventi](../../../ui/event-forwarding/monitoring.md).

## Risorse aggiuntive

- [[!DNL Algolia] Documentazione API approfondimenti](https://www.algolia.com/doc/rest-api/insights/)
- [[!DNL Algolia] Documentazione eventi](https://www.algolia.com/doc/guides/sending-events/getting-started/)
- [[!DNL Adobe Experience Platform] Documentazione sull&#39;inoltro degli eventi](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=it)
- [[!DNL Algolia] Panoramica delle funzionalità IA](https://www.algolia.com/products/ai-search/)
