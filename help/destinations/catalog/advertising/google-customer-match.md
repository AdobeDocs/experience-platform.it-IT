---
keywords: Google customer match;Google customer match;Google Customer Match;Google Customer Match
title: Connessione Customer Match di Google
description: Google Customer Match consente di utilizzare i dati online e offline per raggiungere e coinvolgere nuovamente i clienti tra le proprietà possedute e gestite di Google, come Ricerca, Shopping, Gmail e YouTube.
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: 4fed44edb3e201422f765493c9019be1cddffccc
workflow-type: tm+mt
source-wordcount: '1548'
ht-degree: 0%

---

# [!DNL Google Customer Match] connection

## Panoramica {#overview}

[Google Customer ](https://support.google.com/google-ads/answer/6379332?hl=en) Matchlets consente di utilizzare i dati online e offline per raggiungere e coinvolgere nuovamente i clienti nelle proprietà di Google possedute e gestite, ad esempio:  [!DNL Search],  [!DNL Shopping],  [!DNL Gmail], e  [!DNL YouTube].

![Destinazione Customer Match di Google nell’interfaccia utente di Adobe Experience Platform](../../assets/catalog/advertising/google-customer-match/catalog.png)

## Casi di utilizzo

Per comprendere meglio come e quando utilizzare la destinazione [!DNL Google Customer Match], di seguito sono riportati alcuni esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa funzione.

### Caso d&#39;uso n. 1

Un marchio di abbigliamento atletico vuole raggiungere i clienti esistenti attraverso [!DNL Google Search] e [!DNL Google Shopping] per personalizzare offerte e articoli in base ai loro acquisti precedenti e alla cronologia di navigazione. Il marchio dell’abbigliamento può acquisire indirizzi e-mail dal proprio CRM all’Experience Platform e creare segmenti dai propri dati offline. Quindi, possono inviare questi segmenti a [!DNL Google Customer Match] da utilizzare in [!DNL Search] e [!DNL Shopping], ottimizzando le spese pubblicitarie.

### Caso d&#39;uso n. 2

Un&#39;importante azienda tecnologica ha lanciato un nuovo telefono. Per promuovere questo nuovo modello di telefono, stanno cercando di sensibilizzare i clienti sulle nuove caratteristiche e funzionalità del telefono ai clienti che possiedono i modelli precedenti dei loro telefoni.

Per promuovere il rilascio, caricano gli indirizzi e-mail dal loro database CRM in Experience Platform, utilizzando gli indirizzi e-mail come identificatori. I segmenti vengono creati in base ai clienti che possiedono modelli di telefono precedenti. Quindi i segmenti vengono inviati a [!DNL Google Customer Match], in modo che l&#39;azienda possa eseguire il targeting dei clienti attuali, dei clienti che possiedono modelli di telefono precedenti e di clienti simili su [!DNL YouTube].

## Governance dei dati per le destinazioni [!DNL Google Customer Match] {#data-governance}

Alcune destinazioni in Experience Platform hanno determinate regole e obblighi per i dati inviati o ricevuti dalla piattaforma di destinazione. Sei responsabile di comprendere i limiti e gli obblighi dei tuoi dati e come li utilizzi in Adobe Experience Platform e nella piattaforma di destinazione. Adobe Experience Platform fornisce strumenti di governance dei dati per aiutarti a gestire alcuni di questi obblighi di utilizzo dei dati. [Ulteriori ](../../../data-governance/labels/overview.md) informazioni sugli strumenti e i criteri di governance dei dati.

## Identità supportate {#supported-identities}

[!DNL Google Customer Match] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | Google Advertising ID | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per gli inserzionisti | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi IDFA. |
| phone_sha256_e.164 | Numeri di telefono in formato E164, con hash con l&#39;algoritmo SHA256 | Sia il testo normale che i numeri di telefono con hash SHA256 sono supportati da Adobe Experience Platform. Segui le istruzioni riportate nella sezione [Requisiti di corrispondenza ID](#id-matching-requirements-id-matching-requirements) e utilizza rispettivamente i namespace appropriati per il testo normale e i numeri di telefono con hash. Quando il campo di origine contiene attributi senza hash, seleziona l&#39;opzione **[!UICONTROL Applica trasformazione]** per fare in modo che [!DNL Platform] hash automaticamente i dati all&#39;attivazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con l’algoritmo SHA256 | Gli indirizzi e-mail con hash SHA256 e di testo normale sono supportati da Adobe Experience Platform. Segui le istruzioni riportate nella sezione [Requisiti di corrispondenza ID](#id-matching-requirements-id-matching-requirements) e utilizza rispettivamente i namespace appropriati per gli indirizzi e-mail in testo normale e con hash. Quando il campo di origine contiene attributi senza hash, seleziona l&#39;opzione **[!UICONTROL Applica trasformazione]** per fare in modo che [!DNL Platform] hash automaticamente i dati all&#39;attivazione. |
| user_id | ID utente personalizzati | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi personalizzato. |

## Tipo di esportazione {#export-type}

**Esportazione segmento** : esporta tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono e altri) utilizzati nella  [!DNL Google Customer Match] destinazione.

## [!DNL Google Customer Match] prerequisiti dell’account {#google-account-prerequisites}

Prima di configurare una destinazione [!DNL Google Customer Match] in Experience Platform, assicurati di leggere e rispettare i criteri di Google per l&#39;utilizzo di [!DNL Customer Match], descritti nella [documentazione di supporto di Google](https://support.google.com/google-ads/answer/6299717).

Quindi, assicurati che il tuo account [!DNL Google] sia configurato per un [!DNL Standard] o per un livello di accesso superiore. Per ulteriori informazioni, consulta la [documentazione di Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) .

### Elenco consentiti {#allowlist}

Prima di creare la destinazione [!DNL Google Customer Match] in Experience Platform, assicurati che l&#39;account [!DNL Google Ads] sia conforme alla [policy di Customer Match di Google](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

I clienti con account conformi vengono automaticamente inseriti nell’elenco Consentiti da Google.

## Requisiti di corrispondenza ID {#id-matching-requirements}

[!DNL Google] richiede che non siano inviate informazioni personali identificabili (PII) in modo chiaro. Pertanto, i tipi di pubblico attivati in [!DNL Google Customer Match] possono essere contrassegnati da identificatori *con hash* come indirizzi e-mail o numeri di telefono.

A seconda del tipo di ID che trasferisci in Adobe Experience Platform, devi soddisfare i requisiti corrispondenti.

## Requisiti di hashing del numero di telefono {#phone-number-hashing-requirements}

Esistono due metodi per attivare i numeri di telefono in [!DNL Google Customer Match]:

* **Inserimento di numeri** di telefono non elaborati: è possibile acquisire i numeri di telefono non elaborati in  [!DNL E.164] formato in  [!DNL Platform] e questi vengono automaticamente crittografati al momento dell’attivazione. Se scegli questa opzione, accertati di inserire sempre i numeri di telefono non elaborati nello spazio dei nomi `Phone_E.164` .
* **Inserimento di numeri** di telefono con hash: è possibile pre-hash i numeri di telefono prima dell’inserimento in  [!DNL Platform]. Se scegli questa opzione, accertati di inserire sempre i numeri di telefono con hash nello spazio dei nomi `PHONE_SHA256_E.164` .

>[!NOTE]
>
>I numeri di telefono acquisiti nello spazio dei nomi `Phone` non possono essere attivati in [!DNL Google Customer Match].

## Requisiti di hash e-mail {#hashing-requirements}

Puoi aggiungere hash agli indirizzi e-mail prima di inviarli in Adobe Experience Platform oppure utilizzare indirizzi e-mail in modo chiaro nell’Experience Platform e inserirli [!DNL Platform] all’attivazione.

Per ulteriori informazioni sui requisiti di hashing di Google e su altre restrizioni all’attivazione, consulta le sezioni seguenti nella documentazione di Google:

* [[!DNL Customer Match] con indirizzo e-mail, indirizzo o ID utente](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] considerazioni](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [Customer Match con numero di telefono](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Corrispondenza cliente con ID dispositivo mobile](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


Per informazioni sull’acquisizione degli indirizzi e-mail in Experience Platform, consulta la [panoramica sull’acquisizione batch](../../../ingestion/batch-ingestion/overview.md) e la [panoramica sull’acquisizione in streaming](../../../ingestion/streaming-ingestion/overview.md).

Se scegli di aggiungere l’hash agli indirizzi e-mail da solo, assicurati di soddisfare i requisiti di Google, descritti nei collegamenti di cui sopra.

## Utilizzo di spazi dei nomi personalizzati {#custom-namespaces}

Prima di poter utilizzare lo spazio dei nomi `User_ID` per inviare dati a Google, assicurati di sincronizzare i tuoi identificatori utilizzando [!DNL gTag]. Per informazioni dettagliate, consulta la [documentazione ufficiale di Google](https://support.google.com/google-ads/answer/9199250) .

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

## Configurare la destinazione - Procedura dettagliata sul video {#video}

Il video seguente illustra i passaggi per configurare una destinazione [!DNL Google Customer Match] e attivare i segmenti. Le fasi sono inoltre illustrate in sequenza nelle sezioni successive.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## Connetti alla destinazione {#connect-destination}

In **[!UICONTROL Destinazioni]** > **[!UICONTROL Catalogo]**, scorri fino alla categoria **[!UICONTROL Pubblicità]** . Seleziona [!DNL Google Customer Match], quindi seleziona **[!UICONTROL Configura]**.

![Connessione alla destinazione Customer Match di Google](../../assets/catalog/advertising/google-customer-match/connect.png)

>[!NOTE]
>
>Se esiste una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Attiva]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Attiva]** e **[!UICONTROL Configura]**, consulta la sezione [Catalogo](../../ui/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.

Nel passaggio **Account**, se in precedenza hai impostato una connessione alla destinazione [!DNL Google Customer Match], seleziona **[!UICONTROL Account esistente]** e seleziona la connessione esistente. In alternativa, è possibile selezionare **[!UICONTROL Nuovo account]** per impostare una nuova connessione a [!DNL Google Customer Match]. Per accedere e collegare Adobe Experience Cloud al tuo account [!DNL Google Ad], seleziona **[!UICONTROL Connetti a destinazione]**.

>[!NOTE]
>
>Experience Platform supporta la convalida delle credenziali nel processo di autenticazione. Se immetti credenziali errate nel tuo account [!DNL Google Ad], viene visualizzato un messaggio di errore per assicurarti di non completare il flusso di lavoro con credenziali errate.

![Connessione alla destinazione Customer Match di Google - passaggio di autenticazione](../../assets/catalog/advertising/google-customer-match/connection.png)

Una volta confermate le credenziali e quando Adobe Experience Cloud è connesso al tuo account Google, puoi selezionare **[!UICONTROL Avanti]** per procedere al passaggio **[!UICONTROL Autenticazione]**.

![Credenziali confermate](../../assets/catalog/advertising/google-customer-match/connection-success.png)

Nel passaggio **[!UICONTROL Autenticazione]**, immetti un **[!UICONTROL Nome]** e una **[!UICONTROL Descrizione]** per il flusso di attivazione e compila il tuo Google **[!UICONTROL Account ID]**.

In questo passaggio, puoi anche selezionare qualsiasi **[!UICONTROL azione di marketing]** applicabile a questa destinazione. Le azioni di marketing indicano l’intento per il quale i dati vengono esportati nella destinazione. Puoi scegliere tra azioni di marketing definite da Adobi o creare una tua azione di marketing. Per ulteriori informazioni sulle azioni di marketing, consulta la [Panoramica sui criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

Seleziona **[!UICONTROL Crea destinazione]** dopo aver compilato i campi precedenti.

>[!IMPORTANT]
>
> * L&#39;azione di marketing **[!UICONTROL Combina con PII]** è selezionata per impostazione predefinita per la destinazione [!DNL Google Customer Match] e non può essere rimossa.
> * Per le destinazioni [!DNL Google Customer Match]. **[!UICONTROL L&#39;]** ID account è l&#39;ID cliente con Google. Il formato dell&#39;ID è xxx-xxx-xxxx.


![Connetti Customer Match di Google - passaggio di autenticazione](../../assets/catalog/advertising/google-customer-match/authentication.png)

La destinazione viene ora creata. Puoi selezionare **[!UICONTROL Salva e esci]** se desideri attivare i segmenti in un secondo momento oppure puoi selezionare **[!UICONTROL Avanti]** per continuare il flusso di lavoro e selezionare i segmenti da attivare. In entrambi i casi, consulta la sezione successiva [Attivare i segmenti su [!DNL Google Customer Match]](#activate-segments), per il resto del flusso di lavoro.

## Attiva i segmenti in [!DNL Google Customer Match] {#activate-segments}

Per istruzioni su come attivare i segmenti su [!DNL Google Customer Match], consulta [Attivare i dati sulle destinazioni](../../ui/activate-destinations.md).


Nel passaggio **[!UICONTROL Pianificazione segmenti]** , devi fornire l’ [!UICONTROL ID app] quando invii segmenti [!DNL IDFA] o [!DNL GAID] a [!DNL Google Customer Match].

![ID app di Google Customer Match](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

Per informazioni su come trovare il [!DNL App ID], consulta la [documentazione ufficiale di Google](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid).

## Verifica che l’attivazione del segmento sia avvenuta correttamente {#verify-activation}

Dopo aver completato il flusso di attivazione, passa al tuo account **[!UICONTROL Google Ads]**. I segmenti attivati vengono visualizzati nel tuo account Google come elenchi di clienti. Tieni presente che a seconda della dimensione del segmento, alcuni tipi di pubblico non vengono compilati a meno che non vi siano più di 100 utenti attivi da servire.

Quando mappi un segmento con gli ID mobili [!DNL IDFA] e [!DNL GAID] , [!DNL Google Customer Match] crea un segmento separato per ogni mappatura ID. L&#39;account [!DNL Google Ads] mostra due segmenti diversi, uno per [!DNL IDFA] e uno per la mappatura [!DNL GAID].

## Risorse aggiuntive {#additional-resources}

* [Integrare Google Customer Match - Esercitazione video](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)
