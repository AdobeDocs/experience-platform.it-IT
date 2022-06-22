---
title: Connessione Medallia
description: Attiva profili per sondaggi Medallia mirati e raccolta di feedback per comprendere meglio le esigenze e le aspettative dei clienti.
source-git-commit: be2d4e5d1f204feefc7acb7cb4518044ab3f153a
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 1%

---


# Connessione Medallia

## Panoramica {#overview}

Attiva profili per sondaggi Medallia mirati e raccolta di feedback per comprendere meglio le esigenze e le aspettative dei clienti.

>[!IMPORTANT]
>
>Questa pagina di documentazione è stata creata dal team Medallia. Per eventuali richieste di informazioni o aggiornamenti, contattatele direttamente all&#39;indirizzo adobe-integrations@medallia.com.

## Casi d’uso {#use-cases}

Per aiutarti a comprendere meglio come e quando utilizzare la destinazione Medallia, ecco alcuni esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Caso d&#39;uso n. 1

Un marchio B2B vuole valutare e semplificare il suo programma di onboarding. Vorrebbero inviare sondaggi personalizzati in tempo reale ai clienti che hanno appena completato il processo di onboarding.

### Caso d&#39;uso n. 2

Un rivenditore sta cercando di comprendere meglio le preferenze del cliente per l&#39;evasione dell&#39;ordine. Vogliono inviare un breve sondaggio SMS da 1 domanda ai clienti che hanno effettuato acquisti online e in negozio nell&#39;ultimo mese.

## Prerequisiti {#prerequisites}

Per stabilire il collegamento Medallia sono necessarie le seguenti informazioni:
* **URL endpoint token OAuth**
* **ID client**
* **Segreto client**
* **URL gateway API**
* **Importa nome API**

Collabora con il team di consegna Medallia per ottenere questi dettagli.

## Identità supportate {#supported-identities}

Medallia supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| e-mail | Indirizzo e-mail | Seleziona l’identità di destinazione dell’e-mail quando desideri inviare sondaggi e-mail di invito. Quando un profilo è associato a più indirizzi e-mail, Medallia attiverà l’invito solo per la prima e-mail. |
| telefono | Hash dei numeri di telefono in formato E.164 | Seleziona l’identità di destinazione del telefono quando desideri inviare sondaggi basati su SMS. Il numero telefonico deve essere in formato E.164, che include un segno più (+), un codice internazionale di chiamata, un prefisso locale e un numero di telefono. Ad esempio: (+)(prefisso del paese)(prefisso del paese)(numero di telefono). Quando un profilo è associato a più numeri di telefono, Medallia attiverà l’invito solo per il primo numero di telefono. |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri appena qualificati di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html). Nel flusso di lavoro di configurazione della destinazione , compila i campi elencati nelle due sezioni seguenti.

### Autentica a destinazione {#authenticate}

Per eseguire l’autenticazione nella destinazione, compila i campi richiesti e seleziona **[!UICONTROL Connetti alla destinazione]**.

* **[!UICONTROL URL endpoint token OAuth]**: In genere si presenta come https://instance.medallia.tld/oauth/tenant/token.
* **[!UICONTROL ID client]**: Ottieni dal tuo team di consegna Medallia.
* **[!UICONTROL Segreto client]**: Ottieni dal tuo team di consegna Medallia.

![Immagine che mostra la schermata di autenticazione per questa destinazione.](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### Compila i dettagli della destinazione {#destination-details}

Per configurare i dettagli della destinazione, compila i campi richiesti e seleziona **[!UICONTROL Successivo]**.

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL URL gateway API]**: Ottieni dal tuo team di consegna Medallia. In genere si presenta come https://instance-tenant.apis.medallia.com.
* **[!UICONTROL Importa nome API]**: Ottieni dal tuo team di consegna Medallia. Nome dell’API di importazione Medallia (noto anche come Feed Web) da utilizzare in questa connessione. Puoi attivare diversi segmenti su diverse API di importazione per attivare diversi programmi di sondaggio.

![Immagine che mostra la schermata dei dettagli della destinazione per questa destinazione.](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Leggi [Attivare profili e segmenti nelle destinazioni di esportazione dei segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

### Mappare attributi e identità {#map}

I seguenti namespace di identità di destinazione devono essere mappati a seconda del caso d’uso:
* Per i sondaggi via e-mail, **email** deve essere mappato come campo di destinazione utilizzando **Campo di destinazione** > **Seleziona spazio dei nomi identità** > **email**
* Per i sondaggi basati su SMS, **telefono** deve essere mappato come campo di destinazione utilizzando **Campo di destinazione** > **Seleziona spazio dei nomi identità** > **telefono**. I numeri di telefono devono essere in formato E.164, che include un segno più (+), un codice internazionale di chiamata del paese, un prefisso locale e un numero di telefono

È inoltre consigliabile mappare attributi personalizzati di destinazione aggiuntivi per creare sondaggi personalizzati e aggiungere ulteriori informazioni sul cliente al record del sondaggio:

* I sondaggi personalizzati in genere si rivolgono al cliente per nome
   * Mappa il nome del cliente su **Campo di destinazione** > **Seleziona attributi personalizzati** > **Nome attributo** > **nome**
   * Mappa il cognome del cliente su **Campo di destinazione** > **Seleziona attributi personalizzati** > **Nome attributo** > **cognome**
* Aggiungi le mappature per tutti gli altri attributi personalizzati di target desiderati

![Immagine che mostra un esempio di mappatura per identità e attributi.](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> Condividi con il tuo team di consegna Medallia esattamente **Nomi di attributo** per ogni attributo personalizzato di destinazione mappato utilizzando **Campo di destinazione** > **Seleziona attributi personalizzati** > **Nome attributo**. È possibile scattare una schermata della pagina di mappatura da condividere direttamente.

## Dati esportati {#exported-data}

Dopo aver attivato i segmenti nella destinazione, informa il team di consegna Medallia, che sarà in grado di convalidare i dati esportati da Adobe Experience Platform a Medallia. Si noti che i sondaggi possono essere attivati solo a Medallia dopo la verifica dei dati; prima di questo, i dati saranno esportati a Medallia ma non attiveranno sondaggi per i clienti.

Di seguito è fornito un esempio di JSON dei dati esportati, che utilizza la mappatura di esempio dalla schermata precedente in **Mappare attributi e identità** sezione:

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  “John” ,
        "lastname":  “Smith”,
        "contactId": "jsmith120002",
    }
]
```

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).
