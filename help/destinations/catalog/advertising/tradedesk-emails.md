---
title: (Beta) La connessione Trade Desk - CRM
description: Attiva i profili nel tuo account Trade Desk per il targeting del pubblico e la soppressione in base ai dati CRM.
source-git-commit: 69bf43f86ab3369ad0c7febcb69ec41d3bcac8bb
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 3%

---


# (Beta) [!DNL Trade Desk] - Connessione CRM

>[!IMPORTANT]
>
> [!DNL The Trade Desk - CRM] la destinazione in Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

## Panoramica {#overview}

>[!IMPORTANT]
>
> Questa pagina della documentazione è stata creata da *[!DNL Trade Desk]* squadra. Per qualsiasi richiesta di informazioni o aggiornamento, contatta il tuo [!DNL Trade Desk] rappresentante.

Questo documento è progettato per facilitare l’attivazione dei profili [!DNL Trade Desk] account per il targeting e la soppressione del pubblico in base ai dati CRM.

>[!TIP]
>
>Utilizzo [!DNL The Trade Desk] Destinazione CRM per la mappatura dei dati CRM, come e-mail o indirizzo e-mail con hash. Utilizza la [altra destinazione commerciale](/help/destinations/catalog/advertising/tradedesk.md) nel catalogo Adobe Experience Platform per i cookie e le mappature ID dispositivo.

[!DNL The Trade Desk] (TTD) non gestisce direttamente in qualsiasi momento il file di caricamento degli indirizzi e-mail né lo gestisce [!DNL The Trade Desk] archivia le e-mail non crittografate.

## Prerequisiti {#prerequisites}

Prima di attivare i segmenti in [!DNL The Trade Desk], è necessario contattare [!DNL The Trade Desk] account manager per firmare il contratto di onboarding CRM. [!DNL The Trade Desk] concederà quindi l&#39;autorizzazione e condividerà l&#39;ID inserzionista per configurare la destinazione.

## Requisiti di corrispondenza ID (#id-matching-requirements)

A seconda del tipo di ID che trasferisci in Adobe Experience Platform, devi soddisfare i requisiti corrispondenti. Per piacere, leggi le [Panoramica dello spazio dei nomi identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=it) per ulteriori informazioni.

## Identità supportate {#supported-identities}

[!DNL The Trade Desk] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](/help/identity-service/namespaces.md).

Gli indirizzi e-mail con hash SHA256 e di testo normale sono supportati da Adobe Experience Platform. Segui le istruzioni riportate nella sezione sui requisiti di corrispondenza ID e utilizza rispettivamente gli spazi dei nomi appropriati per gli indirizzi e-mail in testo normale e con hash.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| E-mail | Indirizzi e-mail (testo cancellato) | Seleziona la `Email` identità di destinazione quando l’identità di origine è uno spazio dei nomi e-mail o un attributo. |
| Email_LC_SHA256 | È necessario eseguire l’hash degli indirizzi e-mail utilizzando SHA256 e le lettere minuscole. Assicurati di seguire qualsiasi [normalizzazione delle e-mail](https://github.com/UnifiedID2/uid2docs/tree/main/api#email-address-normalization) regole richieste. Non potrai modificare questa impostazione in un secondo momento. | Seleziona la `Email_LC_SHA256` identità target quando l&#39;identità di origine è uno spazio dei nomi o un attributo Email_LC_SHA256. |

{style=&quot;table-layout:auto&quot;}

## Requisiti di hashing e-mail (#hashing-requirements)

Puoi aggiungere hash agli indirizzi e-mail prima di acquisirli in Adobe Experience Platform o utilizzare indirizzi e-mail non elaborati.

Per informazioni sull’acquisizione degli indirizzi e-mail in Experience Platform, consulta la [panoramica sull’acquisizione in batch](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/overview.html?lang=it).

Se scegli di aggiungere con hash gli indirizzi e-mail, assicurati di soddisfare i seguenti requisiti:

* Rimuovere gli spazi iniziali e finali.
* Converti tutti i caratteri ASCII in caratteri minuscoli.
* In `gmail.com` indirizzi e-mail, rimuovi i seguenti caratteri dalla parte del nome utente dell’indirizzo e-mail:
   * Il periodo (. (codice ASCII 46). Ad esempio, normalizza `jane.doe@gmail.com` a `janedoe@gmail.com`.
   * Il segno più (+ (codice ASCII 43)) e tutti i caratteri successivi. Ad esempio, normalizza `janedoe+home@gmail.com` a `janedoe@gmail.com`.

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (e-mail o e-mail con hash) utilizzati nella destinazione Trade Desk. |
| Frequenza delle esportazioni | **[!UICONTROL Batch giornaliero]** | Poiché un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il profilo (identità) viene aggiornato una volta al giorno a valle della piattaforma di destinazione. Ulteriori informazioni [caricamenti in batch](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en#file-based). |

{style=&quot;table-layout:auto&quot;}

## Collegati alla destinazione {#connect}

### Autentica a destinazione (#authenticate)

[!DNL The Trade Desk] La destinazione CRM è un caricamento di file batch giornaliero e non richiede l&#39;autenticazione da parte dell&#39;utente.

### Compila i dettagli di destinazione (#fill-in-details)

Prima di poter inviare o attivare i dati del pubblico a una destinazione, è necessario impostare una connessione alla piattaforma di destinazione specifica. Quando [configurazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) questa destinazione, devi fornire le seguenti informazioni:

* **[!UICONTROL Tipo di conto]**: Scegli la **[!UICONTROL Account esistente]** opzione .
* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID inserzionista]**: le [!DNL Trade Desk Advertiser ID], che può essere condiviso dal tuo [!DNL Trade Desk] Account Manager oppure [!DNL Advertiser Preferences] in [!DNL Trade Desk] Interfaccia utente.

Quando ci si connette alla destinazione, l’impostazione di un criterio di governance dei dati è completamente facoltativa. Rivedi l&#39;Experience Platform [panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/policies/overview.html?lang=en) per ulteriori dettagli.

## Attiva i segmenti in questa destinazione {#activate}

Vedi [attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en) per istruzioni su come attivare i segmenti di pubblico in una destinazione.

In **[!UICONTROL Pianificazione]** È possibile configurare la pianificazione e i nomi dei file per ciascun segmento che si sta esportando. La configurazione della pianificazione è obbligatoria, ma il nome del file è facoltativo.

>[!NOTE]
>
>Tutti i segmenti attivati in [!DNL The Trade Desk] La destinazione CRM viene impostata automaticamente su una frequenza giornaliera e un’esportazione completa di file.

In **[!UICONTROL Mappatura]** È necessario selezionare attributi o namespace di identità dalla colonna di origine ed eseguire il mapping alla colonna di destinazione.

Di seguito è riportato un esempio di corretta mappatura dell’identità durante l’attivazione dei segmenti in [!DNL The Trade Desk] Destinazione CRM.

>[!IMPORTANT]
>
> [!DNL The Trade Desk] La destinazione di gestione delle relazioni con i clienti non accetta indirizzi e-mail non elaborati e con hash come identità nello stesso flusso di attivazione. Crea flussi di attivazione separati per indirizzi e-mail non elaborati e con hash.

Selezione dei campi di origine:

* Seleziona la `Email` spazio dei nomi o attributo come identità di origine se si utilizza l’indirizzo e-mail non elaborato durante l’inserimento dei dati.
* Seleziona la `Email_LC_SHA256` spazio dei nomi o attributo come identità sorgente se hai hashing gli indirizzi e-mail dei clienti all’inserimento di dati in Platform.

Selezione dei campi di destinazione:

* Seleziona la `Email` spazio dei nomi come identità di destinazione quando lo spazio dei nomi o l&#39;attributo di origine è `Email`.
* Seleziona la `Email_LC_SHA256` spazio dei nomi come identità di destinazione quando lo spazio dei nomi o l&#39;attributo di origine è `Email_LC_SHA256`.

## Convalida esportazione dati (#validate)

Per convalidare tali dati viene esportato correttamente da Experience Platform e in [!DNL The Trade Desk], trova i segmenti sotto il riquadro dati 1PD Adobe in [!DNL The Trade Desk] Data Management Platform (DMP). Di seguito sono riportati i passaggi per trovare l’ID corrispondente all’interno della [!DNL Trade Desk] Interfaccia utente:

1. Per prima cosa, fai clic sul pulsante **[!UICONTROL Dati]** Scheda e revisione **[!UICONTROL Prime parti]**.
2. Scorri verso il basso nella pagina, sotto **[!UICONTROL Dati importati]**, troverai la **[!UICONTROL Adobe 1PD Tile]**.
3. Fai clic su**[!UICONTROL Adobe 1PD]** riquadro e elenca tutti i segmenti attivati [!DNL Trade Desk] destinazione per l&#39;inserzionista. È inoltre possibile utilizzare la funzione di ricerca.
4. L’ID segmento n. dall’Experience Platform verrà visualizzato come Nome segmento nella sezione [!DNL Trade Desk] Interfaccia utente.

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).
