---
title: Connessione Pega Customer Decision Hub
description: Utilizza la destinazione Pega Customer Decision Hub in Adobe Experience Platform per inviare gli attributi del profilo e i dati di appartenenza al segmento a Pega Customer Decision Hub per le decisioni di prossima azione.
source-git-commit: 475b3b6dceefe968ffb451193cee4d7ed6387c86
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 1%

---


# Connessione Pega Customer Decision Hub

## Panoramica {#overview}

Utilizza la [!DNL Pega Customer Decision Hub] destinazione in Adobe Experience Platform per l’invio di attributi di profilo e dati di appartenenza al segmento a [!DNL Pega Customer Decision Hub] per le decisioni sulle migliori azioni successive.

Iscrizione al segmento di profilo da Adobe Experience Platform, quando viene caricato in [!DNL Pega Customer Decision Hub], può essere utilizzato come predicatore nei modelli adattivi e contribuire a fornire i dati contestuali e comportamentali giusti a scopo decisionale per le migliori azioni successive.

>[!IMPORTANT]
>
>Questa pagina della documentazione è stata creata da Pegasystems. Per qualsiasi domanda o richiesta di aggiornamento, si prega di contattare Pega direttamente [qui](mailto:support@pega.com).

## Casi d’uso

Per aiutarti a capire meglio come e quando utilizzare la [!DNL Customer Decision Hub] destinazione : di seguito sono riportati alcuni esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Telecomunicazioni

Un addetto al marketing desidera sfruttare le informazioni provenienti dalla prossima migliore azione basata su modelli di scienza dei dati, come fornito da [!DNL Pega Customer Decision Hub] per il coinvolgimento del cliente. [!DNL Pega Customer Decision Hub] dipende fortemente dall’intento del cliente, ad esempio &quot;Interested_In_5G&quot;, &quot;Interested_in_Unlimited_Dataplan&quot; o &quot;Interest_in_iPhone_Accessories&quot;.

### Servizi finanziari

Un addetto al marketing desidera ottimizzare le offerte per i clienti che si sono abbonati o hanno annullato l’abbonamento alle newsletter di Pension Plan o Retirement Plan. Le società di servizi finanziari possono acquisire più ID cliente dai propri CRM in Adobe Experience Platform, creare segmenti dai propri dati offline e inviare profili che entrano ed escono dai segmenti a [!DNL Pega Customer Decision Hub] per le decisioni di next-best-action (NBA) nei canali in uscita.

## Prerequisiti {#prerequisites}

Prima di poter utilizzare questa destinazione per esportare dati da Adobe Experience Platform, assicurati di completare i seguenti prerequisiti in [!DNL Pega Customer Decision Hub]:

* Configura il componente di appartenenza al segmento di Adobe nel tuo [!DNL Pega Customer Decision Hub] istanza.
* Configurare OAuth 2.0 [Registrazione client tramite credenziali client](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) tipo di sovvenzione nel tuo [!DNL Pega Customer Decision Hub] istanza.
* Configura [flusso di dati in tempo reale](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flow)  ad Adobe flusso di dati di appartenenza al segmento nel [!DNL Pega Customer Decision Hub] istanza.

## Identità supportate {#supported-identities}

[!DNL Pega Customer Decision Hub] supporta l’attivazione di ID utente personalizzati descritti nella tabella seguente. Per ulteriori dettagli, consulta [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione |
|---|---|
| *CustomerID* | Identificatore utente comune che identifica in modo univoco un profilo in [!DNL Pega Customer Decision Hub] e Adobe Experience Platform |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Esporta tutti i membri di un segmento con l’identificatore (*CustomerID*), attributi (cognome, nome, posizione, ecc.) e i dati di appartenenza al segmento. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono sempre connessioni basate su API. Non appena un profilo viene aggiornato in Experience Platform, in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Per ulteriori informazioni, consulta [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Collegati alla destinazione {#connect}

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione , compila i campi elencati nelle due sezioni seguenti.

### Autentica a destinazione {#authenticate}

#### Autenticazione credenziali client OAuth 2 {#oauth-2-client-credentials-authentication}

![Immagine della schermata dell’interfaccia utente in cui è possibile connettersi alla destinazione Pega CDH utilizzando OAuth 2 con autenticazione delle credenziali client](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

Compila i campi seguenti e seleziona **[!UICONTROL Connetti alla destinazione]**:

* **[!UICONTROL URL token di accesso]**: L’URL del token di accesso OAuth 2 sul tuo [!DNL Pega Customer Decision Hub] istanza.
* **[!UICONTROL ID client]**: OAuth 2 [!DNL client ID] generato nella [!DNL Pega Customer Decision Hub] istanza.
* **[!UICONTROL Segreto client]**: OAuth 2 [!DNL client secret] generato nella [!DNL Pega Customer Decision Hub] istanza.

### Compila i dettagli della destinazione {#destination-details}

Dopo aver stabilito la connessione di autenticazione a [!DNL Pega Customer Decision Hub], fornire le seguenti informazioni per la destinazione:

![Immagine della schermata dell&#39;interfaccia utente che mostra i campi completati per i dettagli della destinazione Pega CDH](../../assets/catalog/personalization/pega/pega-connect-destination.png)

Per configurare i dettagli della destinazione, compila i campi richiesti e seleziona **[!UICONTROL Successivo]**.

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Nome host]**: Il nome host dell’hub decisionale del cliente Pega in cui il profilo viene esportato come dati json.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo in streaming](../../ui/activate-streaming-profile-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

### Attributi di destinazione {#attributes}

In [[!UICONTROL Seleziona attributi]](../../ui/activate-streaming-profile-destinations.md#select-attributes) Adobe consiglia di selezionare un identificatore univoco dal [schema unione](../../../profile/home.md#profile-fragments-and-union-schemas). Seleziona l’identificatore univoco e tutti gli altri campi XDM da esportare nella destinazione.

### Esempio di mappatura: attivazione degli aggiornamenti dei profili in [!DNL Pega Customer Decision Hub]

Di seguito è riportato un esempio di corretta mappatura dell’identità durante l’esportazione dei profili in [!DNL Pega Customer Decision Hub].

Selezione dei campi di origine:

* Seleziona un identificatore (ad esempio: CustomerID) come identità sorgente che identifica in modo univoco un profilo in Adobe Experience Platform e [!DNL Pega Customer Decision Hub].
* Seleziona le modifiche dell’attributo del profilo di origine XDM da esportare e aggiornare in [!DNL Pega Customer Decision Hub].

Selezione dei campi di destinazione:

* Seleziona la `CustomerID` spazio dei nomi come identità di destinazione.
* Seleziona i nomi degli attributi di profilo di destinazione che devono essere mappati sugli attributi di profilo di origine XDM corrispondenti.

![Mappatura identità](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## Esportazione di dati / Convalida esportazione dati {#exported-data}

Un aggiornamento dell’appartenenza a un segmento per un profilo consente di inserire l’identificatore del segmento, il nome e gli stati nel datastore di appartenenza al segmento di marketing Pega. I dati di iscrizione sono associati a un cliente che utilizza Progettazione profili cliente in [!DNL Pega Customer Decision Hub], come illustrato di seguito.
![Immagine della schermata dell’interfaccia utente in cui è possibile associare i dati di appartenenza al segmento di Adobe al cliente, utilizzando Progettazione profili cliente](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

I dati relativi all’appartenenza al segmento vengono utilizzati nei criteri di coinvolgimento di Pega Next-Best-Action Designer per le decisioni sulle migliori azioni successive, come illustrato di seguito.
![Immagine della schermata dell’interfaccia utente in cui è possibile aggiungere campi di iscrizione al segmento come condizioni in Criteri di coinvolgimento di Pega Next-Best-Action Designer](../../assets/catalog/personalization/pega/pega-profile-designer-engagment.png)

I campi dei dati di appartenenza al segmento del cliente vengono aggiunti come predicatori nei modelli adattivi, come mostrato di seguito.
![Immagine della schermata dell&#39;interfaccia utente in cui è possibile aggiungere campi di appartenenza al segmento come predicatori nei modelli adattivi, utilizzando Predizione Studio](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## Risorse aggiuntive {#additional-resources}

Vedi [Configurazione di una registrazione client OAuth 2.0](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) in [!DNL Pega Customer Decision Hub].

Vedi [Creazione di un’esecuzione in tempo reale per i flussi di dati](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) in [!DNL Pega Customer Decision Hub].

Vedi [Gestire i record cliente in Progettazione profili cliente](https://docs.pega.com/whats-new-pega-platform/manage-customer-records-customer-profile-designer-86).

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).
