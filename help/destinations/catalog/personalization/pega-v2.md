---
title: (V2) Connessione del pubblico in tempo reale Pega CDH
description: Utilizza la destinazione del pubblico in tempo reale Pega Customer Decision Hub in Adobe Experience Platform per inviare gli attributi del profilo e i dati sull’iscrizione del pubblico a Pega Customer Decision Hub per prendere decisioni sulle migliori azioni successive.
source-git-commit: a51f6bd189bc25018cf25e69fe23bc9f6b3372dd
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 3%

---

# (V2) Connessione del pubblico in tempo reale Pega CDH

## Panoramica {#overview}

Utilizza la destinazione (V2) [!DNL Pega CDH Realtime Audience] in Adobe Experience Platform per inviare gli attributi del profilo e i dati sull&#39;iscrizione del pubblico a [!DNL Pega Customer Decision Hub] per le decisioni sulle azioni migliori successive.

L&#39;iscrizione al pubblico di profilo da Adobe Experience Platform, quando caricata in [!DNL Pega Customer Decision Hub], può essere utilizzata come predittore nei modelli adattivi e contribuire a fornire i dati contestuali e comportamentali corretti per le decisioni da intraprendere al meglio.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti da Pegasystems. Per richieste di informazioni o richieste di aggiornamento, contatta direttamente Pega [qui](mailto:support@pega.com).

## Casi d’uso {#use-cases}

Per capire meglio come e quando utilizzare la destinazione [!DNL Customer Decision Hub], ecco alcuni esempi di casi d&#39;uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Telecomunicazioni {#telecommunications}

Un addetto al marketing desidera sfruttare le informazioni provenienti da un&#39;azione migliore basata su un modello di data science, come consegnato da [!DNL Pega Customer Decision Hub] per il coinvolgimento dei clienti. [!DNL Pega Customer Decision Hub] si basa in modo significativo sulle intenzioni dei clienti, ad esempio &quot;Interested_In_5G&quot;, &quot;Interested_in_Unlimited_Dataplan&quot; o &quot;Interest_in_iPhone_accessories&quot; per determinare le decisioni NBA (Next-Best-Action) nei canali in uscita.

### Servizi finanziari {#financial-services}

Un addetto al marketing desidera ottimizzare le offerte per i clienti che hanno effettuato o annullato l’abbonamento alle newsletter del piano pensionistico o del piano pensionistico. Le società di servizi finanziari possono acquisire più ID cliente dai propri CRM in Adobe Experience Platform, creare tipi di pubblico dai propri dati offline e inviare profili che entrano ed escono dai tipi di pubblico a [!DNL Pega Customer Decision Hub] per il decisioning NBA (Next-Best-Action) nei canali in uscita.

## Prerequisiti {#prerequisites}

Prima di poter utilizzare questa destinazione per esportare i dati da Adobe Experience Platform, assicurarsi di completare i seguenti prerequisiti in [!DNL Pega Customer Decision Hub]:

* Configura il [componente di integrazione Profilo Adobe Experience Platform e Appartenenza al pubblico](https://docs.pega.com/bundle/components/page/customer-decision-hub/components/adobe-membership-component.html) nell&#39;istanza [!DNL Pega Customer Decision Hub].
* Configurare il tipo di concessione OAuth 2.0 [Registrazione client utilizzando le credenziali client](https://docs.pega.com/bundle/platform/page/platform/security/configure-oauth-2-client-registration.html) nell&#39;istanza [!DNL Pega Customer Decision Hub].
* Configura il flusso di dati [esecuzione in tempo reale](https://docs.pega.com/bundle/platform/page/platform/decision-management/data-flow-run-real-time-create.html) per il flusso di dati di iscrizione al pubblico di Adobe nella tua istanza [!DNL Pega Customer Decision Hub].

## Identità supportate {#supported-identities}

[!DNL Pega Customer Decision Hub] supporta l&#39;attivazione degli ID utente personalizzati descritti nella tabella seguente. Per ulteriori dettagli, vedi [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| `CustomerID` | ID cliente | Identificatore utente comune che identifica in modo univoco un profilo in [!DNL Pega Customer Decision Hub] e Adobe Experience Platform. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Esporta tutti i membri di un pubblico con identificatore (*CustomerID*), attributi (cognome, nome, posizione, ecc.) e dati di appartenenza al pubblico. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni sempre basate su API. Non appena un profilo viene aggiornato in Experience Platform, in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Per ulteriori informazioni, consulta [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

#### Autenticazione credenziali client OAuth 2 {#oauth-2-client-credentials-authentication}

![Immagine della schermata dell&#39;interfaccia utente in cui è possibile connettersi alla destinazione Pega CDH, utilizzando OAuth 2 con autenticazione delle credenziali client](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

Compila i campi seguenti e seleziona **[!UICONTROL Connetti alla destinazione]**:

* **[!UICONTROL URL token di accesso]**: l&#39;URL del token di accesso OAuth 2 nell&#39;istanza [!DNL Pega Customer Decision Hub].
* **[!UICONTROL ID client]**: OAuth 2 [!DNL client ID] generato nell&#39;istanza [!DNL Pega Customer Decision Hub].
* **[!UICONTROL Segreto client]**: OAuth 2 [!DNL client secret] generato nell&#39;istanza [!DNL Pega Customer Decision Hub].

### Inserire i dettagli della destinazione {#destination-details}

Dopo aver stabilito la connessione di autenticazione a [!DNL Pega Customer Decision Hub], fornire le seguenti informazioni per la destinazione:

![Immagine della schermata dell&#39;interfaccia utente che mostra i campi completati per i dettagli della destinazione Pega CDH](../../assets/catalog/personalization/pega/pega-connect-destination-v2.png)

Per configurare i dettagli per la destinazione, compila i campi obbligatori e seleziona **[!UICONTROL Successivo]**.

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Nome host Pega CDH]**: il nome host Pega Customer Decision Hub in cui il profilo viene esportato come dati JSON.
* **[!UICONTROL Alias applicazione]**: l&#39;alias applicazione configurato per l&#39;account Customer Decision Hub. Per ulteriori informazioni, vedere [Aggiunta di un alias URL applicazione](https://docs.pega.com/bundle/platform/page/platform/user-experience/adding-application-url-alias.html) nell&#39;istanza [!DNL Pega Customer Decision Hub].

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attiva dati pubblico nelle destinazioni di esportazione del profilo di streaming](../../ui/activate-streaming-profile-destinations.md).

### Mappatura {#mapping}

Nel passaggio [!UICONTROL Mappatura], seleziona un identificatore univoco dallo schema di unione e dagli altri campi XDM da esportare nella destinazione.

### Esempio di mappatura: attivazione degli aggiornamenti del profilo in [!DNL Pega Customer Decision Hub] {#mapping-example}

Di seguito è riportato un esempio di mapping di identità corretto durante l&#39;esportazione dei profili in [!DNL Pega Customer Decision Hub].

* Selezionare un&#39;identità di origine che identifica in modo univoco un profilo in Adobe Experience Platform e [!DNL Pega Customer Decision Hub]. Esempio: `CustomerID`.
* Selezionare gli attributi del profilo di destinazione a cui si desidera associare gli attributi del profilo di origine selezionati.

![Mappatura identità](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## Dati esportati / Convalida esportazione dati {#exported-data}

In caso di esito positivo, l’iscrizione al pubblico per un profilo inserirebbe l’identificatore del pubblico, il nome e gli stati nell’archivio dati di iscrizione al pubblico di marketing Pega. I dati di iscrizione sono associati a un cliente che utilizza il profilo cliente Designer in [!DNL Pega Customer Decision Hub], come illustrato di seguito.

![Immagine della schermata dell&#39;interfaccia utente in cui è possibile associare i dati di iscrizione al pubblico di Adobe al cliente tramite il profilo cliente Designer](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

I dati di iscrizione del pubblico vengono utilizzati nei criteri di coinvolgimento Designer per le azioni migliori successive di Pega, come illustrato di seguito.

![Immagine della schermata dell&#39;interfaccia utente in cui è possibile aggiungere campi di iscrizione al pubblico come condizioni in Criteri di coinvolgimento di Pega Next-Best-Action Designer](../../assets/catalog/personalization/pega/pega-profile-designer-engagement.png)

I campi dati di iscrizione del pubblico del cliente vengono aggiunti come predittori nei modelli adattivi, come mostrato di seguito.

![Immagine della schermata dell&#39;interfaccia utente in cui è possibile aggiungere campi di appartenenza al pubblico come predicatori nei modelli adattivi, utilizzando Prediction Studio](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni, fare riferimento alla seguente documentazione di [!DNL Pega]:

* [Configurazione di una registrazione client OAuth 2.0](https://docs.pega.com/bundle/platform/page/platform/security/configure-oauth-2-client-registration.html)
* [Creazione di un&#39;esecuzione in tempo reale per i flussi di dati](https://docs.pega.com/bundle/platform/page/platform/decision-management/data-flow-run-real-time-create.html)
* [Gestire i record cliente in Customer Profile Designer](https://docs.pega.com/bundle/customer-decision-hub/page/customer-decision-hub/implement/profile-designer-data-management.html)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).
