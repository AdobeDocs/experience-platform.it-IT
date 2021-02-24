---
keywords: linkedin connection;linkedin connection;linkedin destinations;linkedin;
title: Collegamento in connessione Audiences Matched
description: Attiva profili per le campagne LinkedIn per il targeting dell'audience, la personalizzazione e la soppressione, in base a e-mail con hash.
translation-type: tm+mt
source-git-commit: db2e5d51a5ed07b91997df8a566272c86a7c1708
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---


# [!DNL LinkedIn Matched Audience] connection

Attiva profili per le tue campagne [!DNL LinkedIn] per il targeting dell&#39;audience, la personalizzazione e la soppressione, in base a e-mail con hash e ID mobili.

![Destinazione LinkedIn nell’interfaccia utente di Adobe Experience Platform](../../assets/catalog/social/linkedin/catalog.png)

## Casi d’uso

Per comprendere meglio come e quando utilizzare la destinazione [!DNL LinkedIn Matched Audience], ecco un caso d&#39;uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa funzione.

Un&#39;azienda di software organizza una conferenza e desidera tenersi in contatto con i partecipanti e mostrare loro offerte personalizzate in base al loro stato di partecipazione alla conferenza. L&#39;azienda può inserire indirizzi e-mail o ID dispositivo mobile da [!DNL CRM] in Adobe Experience Platform, creare segmenti dai propri dati offline e inviare questi segmenti alla [!DNL LinkedIn] piattaforma social, ottimizzando le spese pubblicitarie.

## Specifiche di destinazione {#destination-specs}

[!DNL LinkedIn Matched Audience] supporta l&#39;attivazione delle seguenti identità: e-mail con hash  [!DNL GAID], e  [!DNL IDFA].

### Tipo di esportazione {#export-type}

**Esportazione**  segmento - vengono esportati tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono, ecc.) utilizzato nella destinazione [!DNL LinkedIn Matched Audience].

### Prerequisiti per l&#39;account LinkedIn {#LinkedIn-account-prerequisites}

Prima di poter utilizzare la destinazione [!UICONTROL LinkedIn Matched Audience], assicurarsi che l&#39;account [!DNL LinkedIn Campaign Manager] disponga del livello di autorizzazione [!DNL Creative Manager] o superiore.

Per informazioni su come modificare le [!DNL LinkedIn Campaign Manager] autorizzazioni utente, vedere [Aggiungi, Modifica e rimuovi autorizzazioni utente sugli account pubblicitari](https://www.linkedin.com/help/lms/answer/5753) nella documentazione di LinkedIn.

### Requisiti di corrispondenza ID {#id-matching-requirements}

[!DNL LinkedIn Matched Audience] richiede che non siano inviate informazioni personali (PII) in modo chiaro. Di conseguenza, è possibile disattivare gli identificatori [!DNL LinkedIn Matched Audience] con hash *con*, ad esempio indirizzi e-mail o ID dispositivo mobile.

A seconda del tipo di ID che trasferisci in Adobe Experience Platform, devi soddisfare i requisiti corrispondenti.

#### Requisiti di hashing e-mail {#email-hashing-requirements}

Potete scegliere di hash gli indirizzi e-mail prima di inviarli in Adobe Experience Platform, oppure potete scegliere di lavorare con gli indirizzi e-mail in  Experience Platform e ottenere l&#39;hash del nostro algoritmo al momento dell&#39;attivazione.

Per informazioni sull&#39;acquisizione di indirizzi e-mail in  Experience Platform, vedere la [panoramica sull&#39;assimilazione batch](/help/ingestion/batch-ingestion/overview.md) e la [panoramica sull&#39;assimilazione in streaming](/help/ingestion/streaming-ingestion/overview.md).

Se selezionate l’hash degli indirizzi e-mail, accertatevi di soddisfare i seguenti requisiti:

- Rifilate tutti gli spazi iniziali e finali dalla stringa e-mail. Ad esempio: `johndoe@example.com`, non `<space>johndoe@example.com<space>`;
- Durante l&#39;hashing delle stringhe e-mail, assicurarsi di eseguire l&#39;hash della stringa minuscola;
   - Esempio: `example@email.com`, non `EXAMPLE@EMAIL.COM`;
- Verificate che la stringa con hash sia in lettere minuscole
   - Esempio: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, non `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- Non saldare la stringa.

>[!NOTE]
>
>I dati provenienti dagli spazi dei nomi senza hash vengono automaticamente crittografati da [!DNL Platform] al momento dell&#39;attivazione.
> I dati origine attributo non vengono automaticamente crittografati.
> 
> Durante il passaggio [Mappatura identità](../../ui/activate-destinations.md#identity-mapping), quando il campo di origine contiene attributi non crittografati, selezionare l&#39;opzione **[!UICONTROL Apply transformation]** affinché [!DNL Platform] cancelli automaticamente i dati all&#39;attivazione.
> 
> L&#39;opzione **[!UICONTROL Apply transformation]** viene visualizzata solo quando si selezionano gli attributi come campi di origine. Non viene visualizzato quando si scelgono gli spazi dei nomi.

![Trasformazione mapping identità](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Connetti alla destinazione {#connect-destination}

Per connettersi alla destinazione [!DNL LinkedIn Matched Audience], vedere [Flusso di lavoro di autenticazione delle destinazioni social network](./workflow.md).

## Attivare i segmenti su [!DNL LinkedIn Matched Audience] {#activate-segments}

Per istruzioni su come attivare i segmenti in [!DNL LinkedIn Matched Audience], vedere [Attivare i dati sulle destinazioni](../../ui/activate-destinations.md).

## Dati esportati {#exported-data}

L&#39;attivazione corretta implica la creazione di un&#39;audience [!DNL LinkedIn] personalizzata a livello di programmazione in [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). L&#39;appartenenza al segmento nel pubblico viene aggiunta e rimossa man mano che gli utenti sono qualificati o non qualificati per i segmenti attivati.

>[!TIP]
>
>L&#39;integrazione tra Adobe Experience Platform e [!DNL LinkedIn Matched Audience] supporta i backfill storici del pubblico. Tutte le qualifiche del segmento storico vengono inviate a [!DNL LinkedIn] quando si attivano i segmenti nella destinazione.