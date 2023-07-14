---
title: (Beta) Il Trade Desk - Connessione CRM
description: Attiva i profili nel tuo account di Trade Desk per il targeting e l’eliminazione del pubblico in base ai dati CRM.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 0%

---

# (Beta) Il [!DNL Trade Desk] - Connessione CRM

>[!IMPORTANT]
>
>[!DNL The Trade Desk - CRM] La destinazione in Platform è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.
>
>Con il rilascio di EUID (European Unified ID), ora ne vengono visualizzati due [!DNL The Trade Desk - CRM] destinazioni in [catalogo delle destinazioni](/help/destinations/catalog/overview.md).
>* Se si trovano dati nell&#39;UE, utilizzare il **[!DNL The Trade Desk - CRM (EU)]** destinazione.
>* Se i dati vengono originati nelle aree APAC o NAMER, utilizzare **[!DNL The Trade Desk - CRM (NAMER & APAC)]** destinazione.
>
>Entrambe le destinazioni in Experience Platform sono attualmente in versione beta. Questa pagina della documentazione è stata creata da *[!DNL Trade Desk]* team. Per richieste di informazioni o richieste di aggiornamento, contatta il tuo [!DNL Trade Desk] rappresentativo, la documentazione e le funzionalità sono soggette a modifiche.

## Panoramica {#overview}

Questo documento è stato progettato per aiutarti ad attivare i profili nel tuo [!DNL Trade Desk] account per il targeting e l’eliminazione del pubblico in base ai dati CRM.

[!DNL The Trade Desk(TTD)] non gestisce direttamente il file di caricamento degli indirizzi e-mail in alcun momento, né [!DNL The Trade Desk] archivia le e-mail non elaborate (senza hash).

>[!TIP]
>
>Utilizzare [!DNL The Trade Desk] Destinazioni di gestione delle relazioni con i clienti per la mappatura dei dati di gestione delle relazioni con i clienti, come e-mail o indirizzo e-mail con hash. Utilizza il [altra destinazione Trade Desk](/help/destinations/catalog/advertising/tradedesk.md) nel catalogo Adobe Experience Platform per i cookie e le mappature degli ID dispositivo.

## Prerequisiti {#prerequisites}

Prima di poter attivare i tipi di pubblico su [!DNL The Trade Desk], è necessario contattare il [!DNL The Trade Desk] Account Manager per firmare il contratto di onboarding CRM. [!DNL The Trade Desk] concederà quindi l’autorizzazione e condividerà l’ID inserzionista per configurare la destinazione.

## Requisiti di corrispondenza ID {#id-matching-requirements}

A seconda del tipo di ID che acquisisci in Adobe Experience Platform, devi rispettare i requisiti corrispondenti. Leggi le [Panoramica sullo spazio dei nomi delle identità](/help/identity-service/namespaces.md) per ulteriori informazioni.

## Identità supportate {#supported-identities}

[!DNL The Trade Desk] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/namespaces.md).

Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Segui le istruzioni riportate nella sezione sui requisiti di corrispondenza ID e utilizza gli spazi dei nomi appropriati rispettivamente per gli indirizzi e-mail in testo normale e con hash.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| E-mail | Indirizzi e-mail (testo non crittografato) | Input `email` come identità di destinazione quando l’identità di origine è uno spazio dei nomi o un attributo e-mail. |
| Email_LC_SHA256 | Gli indirizzi e-mail devono avere un hash utilizzando SHA256 e lettere minuscole. Assicurati di seguire qualsiasi [normalizzazione e-mail](https://github.com/UnifiedID2/uid2docs/tree/main/api#email-address-normalization) regole richieste. Non potrai modificare questa impostazione in un secondo momento. | Input `hashed_email` come identità di destinazione quando l’identità di origine è uno spazio dei nomi o un attributo Email_LC_SHA256. |

{style="table-layout:auto"}

## Requisiti di hashing delle e-mail {#hashing-requirements}

Puoi eseguire l’hashing degli indirizzi e-mail prima di acquisirli in Adobe Experience Platform o utilizzare indirizzi e-mail non elaborati.

Per informazioni sull’acquisizione degli indirizzi e-mail in Experience Platform, leggi la sezione [panoramica dell’acquisizione batch](/help/ingestion/batch-ingestion/overview.md).

Se scegli di eseguire l’hash degli indirizzi e-mail da solo, assicurati di soddisfare i seguenti requisiti:

* Rimuovere gli spazi iniziali e finali.
* Converte tutti i caratteri ASCII in minuscolo.
* In entrata `gmail.com` indirizzi e-mail, rimuovi i seguenti caratteri dalla parte del nome utente dell’indirizzo e-mail:
   * Il punto (. (codice ASCII 46). Ad esempio, normalizza `jane.doe@gmail.com` a `janedoe@gmail.com`.
   * Il segno più (+ (codice ASCII 43)) e tutti i caratteri successivi. Ad esempio, normalizza `janedoe+home@gmail.com` a `janedoe@gmail.com`.

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (e-mail o e-mail con hash) utilizzati nella destinazione Trade Desk. |
| Frequenza di esportazione | **[!UICONTROL Batch giornaliero]** | Poiché un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il profilo (identità) viene aggiornato una volta al giorno a valle della piattaforma di destinazione. Ulteriori informazioni su [esportazioni batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Connetti alla destinazione {#connect}

### Autentica nella destinazione {#authenticate}

[!DNL The Trade Desk] La destinazione CRM è un caricamento di file batch giornaliero e non richiede l’autenticazione da parte dell’utente.

### Inserisci i dettagli della destinazione {#fill-in-details}

Prima di poter inviare o attivare i dati sul pubblico a una destinazione, devi impostare una connessione alla tua piattaforma di destinazione. Mentre [configurazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) in questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Tipo di account]**: scegli la **[!UICONTROL Account esistente]** opzione.
* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID inserzionista]**: il tuo [!DNL Trade Desk Advertiser ID], che può essere condiviso dal tuo [!DNL Trade Desk] Account Manager o in [!DNL Advertiser Preferences] nel [!DNL Trade Desk] UI.

![Schermata dell’interfaccia utente di Platform che mostra come compilare i dettagli della destinazione.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

Quando ci si connette alla destinazione, l’impostazione di un criterio di governance dei dati è completamente facoltativa. Rivedi l’Experience Platform [panoramica sulla governance dei dati](/help/data-governance/policies/overview.md) per ulteriori dettagli.

## Attiva il pubblico in questa destinazione {#activate}

Letto [attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](/help/destinations/ui/activate-batch-profile-destinations.md) per istruzioni sull’attivazione di tipi di pubblico in una destinazione.

In **[!UICONTROL Pianificazione]** , puoi configurare la pianificazione e i nomi dei file per ogni pubblico da esportare. La configurazione della pianificazione è obbligatoria, ma il nome del file è facoltativo.

![Schermata dell’interfaccia utente di Platform per pianificare l’attivazione del pubblico.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Tutti i tipi di pubblico attivati in [!DNL The Trade Desk] La destinazione CRM viene impostata automaticamente su una frequenza giornaliera e su un&#39;esportazione di file completa.

![Schermata dell’interfaccia utente di Platform per pianificare l’attivazione del pubblico.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

In **[!UICONTROL Mappatura]** , è necessario selezionare attributi o spazi dei nomi di identità dalla colonna di origine e mappare alla colonna di destinazione.

![Schermata dell’interfaccia utente di Platform per mappare l’attivazione del pubblico.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

Di seguito è riportato un esempio di corretta mappatura identità durante l’attivazione di tipi di pubblico su [!DNL The Trade Desk] Destinazione CRM.

>[!IMPORTANT]
>
> [!DNL The Trade Desk] La destinazione CRM non accetta indirizzi e-mail non elaborati e con hash come identità nello stesso flusso di attivazione. Crea flussi di attivazione separati per gli indirizzi e-mail non elaborati e con hash.

Selezione dei campi di origine:

* Seleziona la `Email` spazio dei nomi o attributo come identità di origine se si utilizza l’indirizzo e-mail non elaborato al momento dell’acquisizione dei dati.
* Seleziona la `Email_LC_SHA256` spazio dei nomi o attributo come identità di origine se esegui l’hashing degli indirizzi e-mail dei clienti al momento dell’inserimento dei dati in Platform.

Selezione dei campi di destinazione:

* Input  `email` come identità di destinazione quando lo spazio dei nomi o l’attributo di origine è `Email`.
* Input  `hashed_email` come identità di destinazione quando lo spazio dei nomi o l’attributo di origine è `Email_LC_SHA256`.

## Convalida esportazione dati {#validate}

Per verificare che i dati vengano esportati correttamente da Experience Platform e in [!DNL The Trade Desk], i tipi di pubblico sono disponibili nella sezione dati di Adobe 1PD in [!DNL The Trade Desk] Piattaforma di gestione dati (DMP, Data Management Platform). Di seguito sono riportati i passaggi per trovare l’ID corrispondente all’interno di [!DNL Trade Desk] Interfaccia utente:

1. Innanzitutto, fai clic su **[!UICONTROL Dati]** Scheda e revisione **[!UICONTROL Prime parti]**.
2. Scorri la pagina verso il basso, sotto **[!UICONTROL Dati importati]**, troverai il **[!UICONTROL Adobe 1PD Tile]**.
3. Fai clic su**[!UICONTROL Adobe 1PD]** e elencherà tutti i tipi di pubblico attivati per il [!DNL Trade Desk] destinazione per l&#39;inserzionista. È inoltre possibile utilizzare la funzione di ricerca.
4. L’ID segmento # dell’Experience Platform verrà visualizzato come Nome segmento nel [!DNL Trade Desk] UI.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, consulta la sezione [Panoramica sulla governance dei dati](/help/data-governance/home.md).
