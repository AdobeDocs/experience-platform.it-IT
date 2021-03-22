---
keywords: connessione facebook;connessione facebook;destinazioni facebook;facebook;instagram;messenger;facebook messenger
title: Connessione Facebook
description: Attiva profili per le tue campagne Facebook per il targeting del pubblico, la personalizzazione e la soppressione in base a e-mail con hash.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '1119'
ht-degree: 2%

---


# [!DNL Facebook] connection

## Panoramica {#overview}

Attiva profili per le campagne [!DNL Facebook] per il targeting del pubblico, la personalizzazione e la soppressione in base a e-mail con hash.

Puoi utilizzare questa destinazione per il targeting del pubblico tra [!DNL Facebook’s] la famiglia di app supportate da [!DNL Custom Audiences], inclusi [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] e [!DNL Messenger]. La selezione dell’app su cui desideri eseguire la campagna è indicata al livello di posizionamento in [!DNL Facebook Ads Manager].

![Destinazione Facebook nell’interfaccia utente Adobe Experience Platform](../../assets/catalog/social/facebook/catalog.png)

## Casi d’uso

Per comprendere meglio come e quando utilizzare la destinazione [!DNL Facebook], ecco due esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa funzione.

### Caso d&#39;uso n. 1

Un rivenditore online vuole raggiungere i clienti esistenti tramite piattaforme social e mostrare loro offerte personalizzate in base ai loro ordini precedenti. Il rivenditore online può acquisire indirizzi e-mail dal proprio CRM a Adobe Experience Platform, creare segmenti dai propri dati offline e inviare tali segmenti alla piattaforma social [!DNL Facebook] ottimizzando le spese pubblicitarie.

### Caso d&#39;uso n. 2

Una compagnia aerea ha diversi livelli di clienti (Bronze, Silver e Gold) e vuole fornire a ciascuno dei livelli offerte personalizzate tramite piattaforme social. Tuttavia, non tutti i clienti utilizzano l’app mobile della compagnia aerea e alcuni di essi non hanno effettuato l’accesso al sito web della società. Gli unici identificatori che l&#39;azienda ha di questi clienti sono gli ID di iscrizione e gli indirizzi e-mail.

Per eseguire il targeting su tali utenti attraverso i social media, possono integrare i dati del cliente dal CRM in Adobe Experience Platform, utilizzando gli indirizzi e-mail come identificatori.

Successivamente, possono utilizzare i propri dati offline, inclusi gli ID di appartenenza associati e i livelli di cliente, per creare nuovi segmenti di pubblico di cui possono eseguire il targeting attraverso la destinazione [!DNL Facebook].

## Governance dei dati per le destinazioni [!DNL Facebook] {#data-governance}

>[!IMPORTANT]
>
>I dati inviati a [!DNL Facebook] non possono includere identità unite. L’utente è responsabile del rispetto di questo obbligo e può farlo assicurando che i segmenti selezionati per l’attivazione non utilizzino un’opzione di unione nei propri criteri di unione. Ulteriori informazioni su [criteri di unione](/help/profile/ui/merge-policies.md).

## Identità supportate {#supported-identities}

[!DNL Facebook Custom Audiences] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | Google Advertising ID | Selezionare l&#39;identità di destinazione GAID quando l&#39;identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per gli inserzionisti | Seleziona l’identità di destinazione IDFA quando l’identità di origine è uno spazio dei nomi IDFA. |
| phone_sha256 | Hash dei numeri di telefono con l&#39;algoritmo SHA256 | Sia il testo normale che i numeri di telefono con hash SHA256 sono supportati da Adobe Experience Platform. Segui le istruzioni riportate nella sezione [Requisiti di corrispondenza ID](#id-matching-requirements-id-matching-requirements) e utilizza rispettivamente i namespace appropriati per il testo normale e i numeri di telefono con hash. Quando il campo di origine contiene attributi senza hash, seleziona l’opzione **[!UICONTROL Apply transformation]** per fare in modo che [!DNL Platform] hash automaticamente i dati all’attivazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con l’algoritmo SHA256 | Gli indirizzi e-mail con hash SHA256 e di testo normale sono supportati da Adobe Experience Platform. Segui le istruzioni riportate nella sezione [Requisiti di corrispondenza ID](#id-matching-requirements-id-matching-requirements) e utilizza rispettivamente i namespace appropriati per gli indirizzi e-mail in testo normale e con hash. Quando il campo di origine contiene attributi senza hash, seleziona l’opzione **[!UICONTROL Apply transformation]** per fare in modo che [!DNL Platform] hash automaticamente i dati all’attivazione. |
| extern_id | ID utente personalizzati | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi personalizzato. |

## Tipo di esportazione {#export-type}

**Esportazione segmento** : stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione Facebook.

## Prerequisiti per l’account Facebook {#facebook-account-prerequisites}

Prima di poter inviare i segmenti di pubblico a [!DNL Facebook], assicurati di soddisfare i seguenti requisiti:

- L&#39;account utente [!DNL Facebook] deve disporre dell&#39;autorizzazione **[!DNL Manage campaigns]** abilitata per l&#39;account annuncio che intendi utilizzare.
- L&#39;account aziendale **Adobe Experience Cloud** deve essere aggiunto come partner pubblicitario nel [!DNL Facebook Ad Account]. Seleziona `business ID=206617933627973`. Per ulteriori informazioni, consulta [Aggiungi partner al tuo Business Manager](https://www.facebook.com/business/help/1717412048538897) nella documentazione di Facebook .
   >[!IMPORTANT]
   >
   > Quando configuri le autorizzazioni per Adobe Experience Cloud, devi abilitare l&#39;autorizzazione **Gestisci campagne**. L&#39;autorizzazione è necessaria per l&#39;integrazione [!DNL Adobe Experience Platform].
- Leggi e firma i termini del servizio [!DNL Facebook Custom Audiences]. Per farlo, vai su `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, dove `accountID` è il tuo [!DNL Facebook Ad Account ID].

## Requisiti di corrispondenza ID {#id-matching-requirements}

[!DNL Facebook] richiede che non siano inviate informazioni personali identificabili (PII) in modo chiaro. Pertanto, i tipi di pubblico attivati in [!DNL Facebook] possono essere contrassegnati da identificatori *con hash* come indirizzi e-mail o numeri di telefono.

A seconda del tipo di ID che trasferisci in Adobe Experience Platform, devi soddisfare i requisiti corrispondenti.

## Requisiti di hashing del numero di telefono {#phone-number-hashing-requirements}

Esistono due metodi per attivare i numeri di telefono in [!DNL Facebook]:

- **Inserimento di numeri** di telefono non elaborati: è possibile inserire numeri di telefono non elaborati nel  [!DNL E.164] formato in  [!DNL Platform]. Hanno automaticamente eseguito l’hash al momento dell’attivazione. Se scegli questa opzione, accertati di inserire sempre i numeri di telefono non elaborati nello spazio dei nomi `Phone_E.164` .
- **Inserimento di numeri** di telefono con hash: è possibile pre-hash i numeri di telefono prima dell’inserimento in  [!DNL Platform]. Se scegli questa opzione, accertati di inserire sempre i numeri di telefono con hash nello spazio dei nomi `Phone_SHA256` .

>[!NOTE]
>
>I numeri di telefono acquisiti nello spazio dei nomi `Phone` non possono essere attivati in [!DNL Facebook].


## Requisiti di hash e-mail {#email-hashing-requirements}

Puoi aggiungere hash agli indirizzi e-mail prima di inviarli in Adobe Experience Platform oppure utilizzare indirizzi e-mail in modo chiaro nell’Experience Platform e inserirli [!DNL Platform] all’attivazione.

Per informazioni sull’acquisizione degli indirizzi e-mail in Experience Platform, consulta la [panoramica sull’acquisizione batch](/help/ingestion/batch-ingestion/overview.md) e la [panoramica sull’acquisizione in streaming](/help/ingestion/streaming-ingestion/overview.md).

Se scegli di aggiungere con hash gli indirizzi e-mail, assicurati di soddisfare i seguenti requisiti:

- Taglia tutti gli spazi iniziali e finali dalla stringa e-mail; esempio: `johndoe@example.com`, non `<space>johndoe@example.com<space>`;
- Quando esegui l’hashing delle stringhe e-mail, assicurati di utilizzare l’hash della stringa in minuscolo;
   - Esempio: `example@email.com`, non `EXAMPLE@EMAIL.COM`;
- Assicurati che la stringa con hash sia tutto minuscola
   - Esempio: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, non `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- Non saldare la stringa.

>[!NOTE]
>
>I dati provenienti da spazi dei nomi senza hash vengono automaticamente hashing da [!DNL Platform] al momento dell’attivazione.
> I dati di origine degli attributi non vengono crittografati automaticamente. Quando il campo di origine contiene attributi senza hash, seleziona l’opzione **[!UICONTROL Apply transformation]** per fare in modo che [!DNL Platform] hash automaticamente i dati all’attivazione.
> L’opzione **[!UICONTROL Apply transformation]** viene visualizzata solo quando selezioni gli attributi come campi di origine. Non viene visualizzato quando si selezionano i namespace.

![Trasformazione mappatura identità](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Utilizzo di spazi dei nomi personalizzati {#custom-namespaces}

Prima di poter utilizzare lo spazio dei nomi `Extern_ID` per inviare dati a [!DNL Facebook], assicurati di sincronizzare i tuoi identificatori utilizzando [!DNL Facebook Pixel]. Per informazioni dettagliate, consulta la [documentazione ufficiale](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) .

## Connetti alla destinazione {#connect-destination}

Per connetterti alla destinazione [!DNL Facebook], vedi [Flusso di lavoro di autenticazione delle destinazioni social network](./workflow.md).

## Attiva i segmenti in [!DNL Facebook] {#activate-segments}

Per istruzioni su come attivare i segmenti su [!DNL Facebook], consulta [Attivare i dati sulle destinazioni](../../ui/activate-destinations.md).

Nel passaggio **[!UICONTROL Segment schedule]** , devi fornire [!UICONTROL Origin of audience] quando invii segmenti a [!DNL Facebook Custom Audiences].

![Origine del pubblico su Facebook](../../assets/catalog/social/facebook/facebook-origin-audience.png)

## Dati esportati {#exported-data}

Per [!DNL Facebook], una corretta attivazione implica la creazione programmatica di un pubblico personalizzato [!DNL Facebook] in [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/) a livello di programmazione. L’appartenenza al segmento nel pubblico verrà aggiunta e rimossa man mano che gli utenti sono qualificati o non qualificati per i segmenti attivati.

>[!TIP]
>
>L’integrazione tra Adobe Experience Platform e [!DNL Facebook] supporta le versioni precedenti del pubblico. Tutte le qualifiche dei segmenti storici vengono inviate a [!DNL Facebook] quando attivi i segmenti nella destinazione.