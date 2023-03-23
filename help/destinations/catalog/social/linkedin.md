---
keywords: collegamento;collegamento;collegamento;collegamento;collegamento;destinazioni;linkedin;
title: Connessione Linkedin Matched Audiences
description: Attiva profili per le campagne LinkedIn per il targeting del pubblico, la personalizzazione e la soppressione, in base a e-mail con hash.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: fd2019feb25b540612a278cbea5bf5efafe284dc
workflow-type: tm+mt
source-wordcount: '1035'
ht-degree: 1%

---

# [!DNL LinkedIn Matched Audiences] connection

## Panoramica {#overview}

Attiva profili per i [!DNL LinkedIn] campagne per il targeting del pubblico, la personalizzazione e la soppressione, basate su e-mail con hash e ID mobili.

![Destinazione linkedIn nell’interfaccia utente Adobe Experience Platform](../../assets/catalog/social/linkedin/catalog.png)

## Casi d’uso

Per aiutarti a capire meglio come e quando utilizzare il [!DNL LinkedIn Matched Audiences] destinazione, questo è un caso d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa funzione.

Una società di software organizza una conferenza e desidera mantenere i contatti con i partecipanti e mostrare loro offerte personalizzate in base al loro stato di partecipazione alla conferenza. L’azienda può acquisire indirizzi e-mail o ID di dispositivi mobili dal proprio [!DNL CRM] in Adobe Experience Platform. Quindi, possono creare segmenti dai propri dati offline e inviare tali segmenti a [!DNL LinkedIn] piattaforma sociale, ottimizzando la spesa pubblicitaria.

## Identità supportate {#supported-identities}

[!DNL LinkedIn Matched Audiences] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | Google Advertising ID | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per gli inserzionisti | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi IDFA. |
| email_lc_sha256 | Indirizzi e-mail con hash con l’algoritmo SHA256 | Gli indirizzi e-mail con hash SHA256 e di testo normale sono supportati da Adobe Experience Platform. Segui le istruzioni riportate nella sezione [Requisiti di corrispondenza ID](#id-matching-requirements-id-matching-requirements) e utilizza i namespace appropriati rispettivamente per il testo normale e per le e-mail con hash. Quando il campo di origine contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] hash automaticamente i dati all’attivazione. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono e altri) utilizzati nel [!DNL LinkedIn Matched Audiences] destinazione. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Prerequisiti per l’account linkedIn {#LinkedIn-account-prerequisites}

Prima di poter utilizzare il [!UICONTROL Pubblico abbinato a linkedIn] destinazione, assicurati [!DNL LinkedIn Campaign Manager] l&#39;account [!DNL Creative Manager] livello di autorizzazione o superiore.

Per scoprire come modificare il [!DNL LinkedIn Campaign Manager] autorizzazioni utente, vedi [Aggiungere, modificare e rimuovere le autorizzazioni utente sugli account pubblicitari](https://www.linkedin.com/help/lms/answer/5753) nella documentazione di LinkedIn.

## Requisiti di corrispondenza ID {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] richiede che non siano inviate informazioni personali identificabili (PII) in modo chiaro. Pertanto, il pubblico è stato attivato in [!DNL LinkedIn Matched Audiences] può essere disattivato *distrutto* identificatori, ad esempio indirizzi e-mail o ID di dispositivi mobili.

A seconda del tipo di ID che trasferisci in Adobe Experience Platform, devi soddisfare i requisiti corrispondenti.

## Requisiti di hash e-mail {#email-hashing-requirements}

Puoi aggiungere hash agli indirizzi e-mail prima di inviarli in Adobe Experience Platform oppure utilizzare gli indirizzi e-mail in modo chiaro nell’Experience Platform e avere [!DNL Platform] hashing su attivazione.

Per informazioni sull’acquisizione degli indirizzi e-mail in Experience Platform, consulta la [panoramica sull’acquisizione in batch](/help/ingestion/batch-ingestion/overview.md) e [panoramica sull’acquisizione in streaming](/help/ingestion/streaming-ingestion/overview.md).

Se scegli di aggiungere con hash gli indirizzi e-mail, assicurati di soddisfare i seguenti requisiti:

* Taglia tutti gli spazi iniziali e finali dalla stringa e-mail. Ad esempio: `johndoe@example.com`, not `<space>johndoe@example.com<space>`;
* Quando esegui l’hashing delle stringhe e-mail, assicurati di utilizzare l’hash della stringa in minuscolo;
   * Esempio: `example@email.com`, not `EXAMPLE@EMAIL.COM`;
* Assicurati che la stringa con hash sia tutto minuscola
   * Esempio: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, not `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Non saldare la stringa.

>[!NOTE]
>
>I dati provenienti da spazi dei nomi senza hash vengono automaticamente crittografati da [!DNL Platform] all&#39;attivazione.
> I dati di origine degli attributi non vengono crittografati automaticamente.
> 
> Periodo [Mappatura identità](../../ui/activate-segment-streaming-destinations.md#mapping) quando il campo di origine contiene attributi senza hash, seleziona **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] hash automaticamente i dati all’attivazione.
> 
> La **[!UICONTROL Applica trasformazione]** viene visualizzata solo quando selezioni gli attributi come campi di origine. Non viene visualizzato quando si selezionano i namespace.

![Trasformazione mappatura identità](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione , compila i campi elencati nelle due sezioni seguenti.

Il video seguente illustra anche i passaggi per configurare un [!DNL LinkedIn Matched Audiences] destinazione e attivazione dei segmenti.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>L&#39;interfaccia utente di Experience Platform viene aggiornata frequentemente e potrebbe essere cambiata dopo la registrazione di questo video. Per informazioni aggiornate, consulta la sezione [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Autentica a destinazione {#authenticate}

1. Trova il [!DNL LinkedIn Matched Audiences] destinazione nel catalogo di destinazione e selezionare **[!UICONTROL Configurazione]**.
2. Seleziona **[!UICONTROL Connetti alla destinazione]**.
   ![Autenticazione in LinkedIn](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. Immetti le tue credenziali LinkedIn e seleziona **Accesso**.

### Compila i dettagli della destinazione {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="ID account"
>abstract="L’ID del tuo account LinkedIn Campaign Manager. Puoi trovare questo ID nel tuo account LinkedIn Campaign Manager."

Per configurare i dettagli della destinazione, compila i campi obbligatori e facoltativi riportati di seguito. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID account]**: Le [!DNL LinkedIn Campaign Manager Account ID]. Puoi trovare questo ID nel tuo [!DNL LinkedIn Campaign Manager] conto.

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

## Dati esportati {#exported-data}

Un&#39;attivazione riuscita significa che un [!DNL LinkedIn] il pubblico personalizzato viene creato a livello di programmazione in [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). L’appartenenza al segmento nel pubblico verrà aggiunta e rimossa man mano che gli utenti sono qualificati o non qualificati per i segmenti attivati.

>[!TIP]
>
>Integrazione tra Adobe Experience Platform e [!DNL LinkedIn Matched Audiences] supporta i backfills dello storico del pubblico. Tutte le qualifiche dei segmenti storici vengono inviate a [!DNL LinkedIn] quando attivi i segmenti sulla destinazione.
