---
title: Connessione Medallia
description: Attiva profili per sondaggi Medallia mirati e raccolta di feedback per comprendere meglio le esigenze e le aspettative dei clienti.
exl-id: 2c2766eb-7be1-418c-bf17-d119d244de92
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 2%

---

# Connessione Medallia

## Panoramica {#overview}

Attiva profili per sondaggi Medallia mirati e raccolta di feedback per comprendere meglio le esigenze e le aspettative dei clienti.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team Medallia. Per eventuali richieste di informazioni o richieste di aggiornamento, contattatele direttamente all&#39;indirizzo adobe-integrations@medallia.com.

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la destinazione Medallia, ecco alcuni esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### #1 del caso d’uso

Un brand B2B vuole valutare e semplificare il suo programma di onboarding. Vorrebbe inviare sondaggi personalizzati in tempo reale ai clienti che hanno appena completato il processo di onboarding.

### #2 del caso d’uso

Un rivenditore cerca di comprendere meglio le preferenze del cliente per l’evasione degli ordini. Desiderano inviare un breve sondaggio SMS di 1 domanda ai clienti che hanno effettuato acquisti online e in-store nell&#39;ultimo mese.

## Prerequisiti {#prerequisites}

Per stabilire il collegamento Medallia sono necessarie le seguenti informazioni:
* **URL endpoint token OAuth**
* **ID client**
* **Segreto client**
* **URL gateway API**
* **Nome API importazione**

Collabora con il tuo team di consegna Medallia per ottenere questi dettagli.

## Identità supportate {#supported-identities}

Medallia supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| e-mail | Indirizzo e-mail | Seleziona l’identità del target e-mail quando desideri inviare sondaggi con inviti e-mail. Quando un profilo è associato a più indirizzi e-mail, Medallia attiverà l’invito solo alla prima e-mail. |
| telefono | Numeri di telefono con hash in formato E.164 | Seleziona l’identità del destinatario del telefono quando desideri inviare sondaggi basati su SMS. Il numero di telefono deve essere in formato E.164, che include un segno più (+), un codice internazionale di chiamata del paese, un prefisso locale e un numero di telefono. Ad esempio: (+)(prefisso del paese)(prefisso dell&#39;area)(numero di telefono). Quando un profilo è associato a più numeri di telefono, Medallia attiverà l’invito solo al primo numero di telefono. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri appena qualificati di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connetti alla destinazione]**.

* **[!UICONTROL URL endpoint token OAuth]**: in genere assume la forma di https://instance.medallia.tld/oauth/tenant/token.
* **[!UICONTROL ID client]**: ottieni dal team di consegna Medallia.
* **[!UICONTROL Segreto client]**: ottieni dal team di consegna Medallia.

![Immagine che mostra la schermata di autenticazione per questa destinazione.](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL URL gateway API]**: ottieni dal team di consegna Medallia. In genere assume la forma di https://instance-tenant.apis.medallia.com.
* **[!UICONTROL Importa nome API]**: richiedi al team di consegna Medallia. Nome dell’API di importazione Medallia (nota anche come feed web) da utilizzare in questa connessione. Puoi attivare tipi di pubblico diversi per diverse API di importazione per attivare diversi programmi di sondaggio.

![Immagine che mostra la schermata dei dettagli della destinazione per questa destinazione.](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

### Mappare attributi e identità {#map}

I seguenti spazi dei nomi delle identità di destinazione devono essere mappati a seconda del caso d’uso:
* Per i sondaggi basati su e-mail, **email** deve essere mappato come campo di destinazione utilizzando **Campo di destinazione** > **Seleziona spazio dei nomi delle identità** > **email**
* Per i sondaggi basati su SMS, **phone** deve essere mappato come campo di destinazione utilizzando **Campo di destinazione** > **Seleziona spazio dei nomi identità** > **phone**. I numeri di telefono devono essere in formato E.164, che include un segno più (+), un codice internazionale di chiamata, un prefisso locale e un numero di telefono

È consigliabile inoltre mappare attributi personalizzati target aggiuntivi per creare sondaggi personalizzati e aggiungere al record del sondaggio informazioni aggiuntive sul cliente:

* I sondaggi personalizzati in genere indirizzano il cliente per nome
   * Mappa il nome del cliente su **Campo di destinazione** > **Seleziona attributi personalizzati** > **Nome attributo** > **Nome utente**
   * Mappa il cognome del cliente su **Campo di destinazione** > **Seleziona attributi personalizzati** > **Nome attributo** > **Cognome**
* Aggiungi mappature per qualsiasi altro attributo personalizzato di destinazione come desiderato

![Immagine che mostra un esempio di mappatura per identità e attributi.](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> Condividi con il tuo team di consegna Medallia i **nomi attributo** esatti per ogni attributo personalizzato di destinazione mappato utilizzando **Campo di destinazione** > **Seleziona attributi personalizzati** > **Nome attributo**. Puoi acquisire una schermata della pagina di mappatura da condividere direttamente.

## Dati esportati {#exported-data}

Dopo aver attivato i segmenti nella destinazione, informa il team di consegna Medallia, che sarà in grado di convalidare i dati esportati da Adobe Experience Platform a Medallia. Tieni presente che i sondaggi possono essere attivati all’interno di Medallia solo dopo la corretta verifica dei dati; prima di questo, i dati verranno esportati in Medallia ma non attiveranno i sondaggi per i clienti.

Di seguito è riportato un esempio di JSON dei dati esportati, che utilizza la mappatura di esempio tratta dalla schermata precedente nella sezione **Mappa attributi e identità**:

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  "John" ,
        "lastname":  "Smith",
        "contactId": "jsmith120002",
    }
]
```

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).
