---
keywords: collegamento;collegamento;collegamento;collegamento;collegamento;destinazioni;linkedin;
title: Connessione Linkedin Matched Audiences
description: Attiva profili per le campagne LinkedIn per il targeting del pubblico, la personalizzazione e la soppressione, in base a e-mail con hash.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 0%

---

# [!DNL LinkedIn Matched Audiences] connection

## Panoramica {#overview}

Attiva profili per le campagne [!DNL LinkedIn] per il targeting del pubblico, la personalizzazione e la soppressione, in base a e-mail con hash e ID mobili.

![Destinazione linkedIn nell’interfaccia utente Adobe Experience Platform](../../assets/catalog/social/linkedin/catalog.png)

## Casi di utilizzo

Per comprendere meglio come e quando utilizzare la destinazione [!DNL LinkedIn Matched Audiences], ecco un caso d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa funzione.

Una società di software organizza una conferenza e desidera mantenere i contatti con i partecipanti e mostrare loro offerte personalizzate in base al loro stato di partecipazione alla conferenza. L’azienda può acquisire indirizzi e-mail o ID di dispositivi mobili dal proprio [!DNL CRM] in Adobe Experience Platform. Quindi, possono creare segmenti dai propri dati offline e inviare questi segmenti alla piattaforma social [!DNL LinkedIn] ottimizzando le spese pubblicitarie.

## Identità supportate {#supported-identities}

[!DNL LinkedIn Matched Audiences] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | Google Advertising ID | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per gli inserzionisti | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi IDFA. |
| email_lc_sha256 | Indirizzi e-mail con hash con l’algoritmo SHA256 | Gli indirizzi e-mail con hash SHA256 e di testo normale sono supportati da Adobe Experience Platform. Segui le istruzioni riportate nella sezione [Requisiti di corrispondenza ID](#id-matching-requirements-id-matching-requirements) e utilizza rispettivamente i namespace appropriati per le e-mail in testo normale e con hash. Quando il campo di origine contiene attributi senza hash, seleziona l&#39;opzione **[!UICONTROL Applica trasformazione]** per fare in modo che [!DNL Platform] hash automaticamente i dati all&#39;attivazione. |


## Tipo di esportazione {#export-type}

**Esportazione segmento** : esporta tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono e altri) utilizzati nella  [!DNL LinkedIn Matched Audiences] destinazione.

## Prerequisiti per l’account linkedIn {#LinkedIn-account-prerequisites}

Prima di poter utilizzare la destinazione [!UICONTROL LinkedIn Matched Audience] , assicurati che il tuo account [!DNL LinkedIn Campaign Manager] disponga del livello di autorizzazione [!DNL Creative Manager] o superiore.

Per informazioni su come modificare le autorizzazioni utente [!DNL LinkedIn Campaign Manager], consulta [Aggiungere, modificare e rimuovere le autorizzazioni utente sugli account pubblicitari](https://www.linkedin.com/help/lms/answer/5753) nella documentazione di LinkedIn.

## Requisiti di corrispondenza ID {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] richiede che non siano inviate informazioni personali identificabili (PII) in modo chiaro. Pertanto, i tipi di pubblico attivati in [!DNL LinkedIn Matched Audiences] possono essere cancellati dagli identificatori *hashed*, come indirizzi e-mail o ID di dispositivi mobili.

A seconda del tipo di ID che trasferisci in Adobe Experience Platform, devi soddisfare i requisiti corrispondenti.

## Requisiti di hash e-mail {#email-hashing-requirements}

Puoi aggiungere hash agli indirizzi e-mail prima di inviarli in Adobe Experience Platform oppure utilizzare indirizzi e-mail in modo chiaro nell’Experience Platform e inserirli [!DNL Platform] all’attivazione.

Per informazioni sull’acquisizione degli indirizzi e-mail in Experience Platform, consulta la [panoramica sull’acquisizione batch](/help/ingestion/batch-ingestion/overview.md) e la [panoramica sull’acquisizione in streaming](/help/ingestion/streaming-ingestion/overview.md).

Se scegli di aggiungere con hash gli indirizzi e-mail, assicurati di soddisfare i seguenti requisiti:

* Taglia tutti gli spazi iniziali e finali dalla stringa e-mail. Ad esempio: `johndoe@example.com`, non `<space>johndoe@example.com<space>`;
* Quando esegui l’hashing delle stringhe e-mail, assicurati di utilizzare l’hash della stringa in minuscolo;
   * Esempio: `example@email.com`, non `EXAMPLE@EMAIL.COM`;
* Assicurati che la stringa con hash sia tutto minuscola
   * Esempio: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, non `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Non saldare la stringa.

>[!NOTE]
>
>I dati provenienti da spazi dei nomi senza hash vengono automaticamente hashing da [!DNL Platform] al momento dell’attivazione.
> I dati di origine degli attributi non vengono crittografati automaticamente.
> 
> Durante il passaggio [Mappatura identità](../../ui/activate-segment-streaming-destinations.md#mapping), quando il campo di origine contiene attributi senza hash, seleziona l’opzione **[!UICONTROL Applica trasformazione]** per fare in modo che [!DNL Platform] hash automaticamente i dati all’attivazione.
> 
> L&#39;opzione **[!UICONTROL Applica trasformazione]** viene visualizzata solo quando selezioni gli attributi come campi di origine. Non viene visualizzato quando si selezionano i namespace.

![Trasformazione mappatura identità](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Collegati alla destinazione {#connect}

Per connetterti a questa destinazione, segui i passaggi descritti nel [tutorial sulla configurazione della destinazione](../../ui/connect-destination.md).

Il video seguente illustra anche i passaggi per configurare una destinazione [!DNL LinkedIn Matched Audiences] e attivare i segmenti.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>L&#39;interfaccia utente di Experience Platform viene aggiornata frequentemente e potrebbe essere cambiata dopo la registrazione di questo video. Per informazioni aggiornate, consulta l’ [esercitazione sulla configurazione di destinazione](../../ui/connect-destination.md) .

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID]** account: il tuo  [!DNL LinkedIn Campaign Manager Account ID]. Puoi trovare questo ID nel tuo account [!DNL LinkedIn Campaign Manager] .

## Attiva i segmenti in questa destinazione {#activate}

Per istruzioni sull’attivazione dei segmenti di pubblico a questa destinazione, consulta [Attivare i dati di pubblico per le destinazioni di esportazione dei segmenti in streaming](../../ui/activate-segment-streaming-destinations.md) .

## Dati esportati {#exported-data}

Se l&#39;attivazione ha esito positivo, in [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login) verrà creato un pubblico personalizzato a livello di programmazione. [!DNL LinkedIn] L’appartenenza al segmento nel pubblico verrà aggiunta e rimossa man mano che gli utenti sono qualificati o non qualificati per i segmenti attivati.

>[!TIP]
>
>L’integrazione tra Adobe Experience Platform e [!DNL LinkedIn Matched Audiences] supporta le versioni precedenti del pubblico. Tutte le qualifiche dei segmenti storici vengono inviate a [!DNL LinkedIn] quando attivi i segmenti nella destinazione.
