---
title: Il Trade Desk - Connessione CRM
description: Attiva i profili nel tuo account di Trade Desk per il targeting e l’eliminazione del pubblico in base ai dati CRM.
last-substantial-update: 2025-01-16T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 47d4078acc73736546d4cbb2d17b49bf8945743a
workflow-type: tm+mt
source-wordcount: '1643'
ht-degree: 2%

---

# Connessione [!DNL Trade Desk] - CRM

>[!IMPORTANT]
>
>Nel [catalogo destinazioni](/help/destinations/catalog/overview.md) sono presenti due destinazioni di CRM di The Trade Desk.
>
>* Se i dati vengono originati nell&#39;UE, utilizzare la destinazione **[!DNL The Trade Desk - CRM (EU)]**.
>* Se i dati vengono originati nelle aree APAC o NAMER, utilizzare la destinazione **[!DNL The Trade Desk - CRM (NAMER & APAC)]**.
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team *[!DNL Trade Desk]*. Per richieste di informazioni o richieste di aggiornamento, contatta il tuo rappresentante [!DNL Trade Desk].

## Panoramica {#overview}

Scopri come attivare i profili nell&#39;account [!DNL Trade Desk] per il targeting e l&#39;eliminazione del pubblico in base ai dati CRM.

Questo connettore invia dati a [!DNL The Trade Desk] per l&#39;attivazione di dati di prime parti. [!DNL The Trade Desk] memorizza le e-mail e i numeri di telefono non elaborati (senza hash).

>[!TIP]
>
>Utilizza la destinazione [!DNL The Trade Desk - CRM] per inviare dati CRM (ad esempio e-mail e numeri di telefono) e altri identificatori di dati di prime parti come cookie e ID dispositivo. Puoi continuare a utilizzare la [destinazione Trade Desk](/help/destinations/catalog/advertising/tradedesk.md) nel catalogo Experience Platform per i cookie e le mappature degli ID dispositivo.

## Prerequisiti {#prerequisites}

>[!IMPORTANT]
>
>Prima di poter attivare i tipi di pubblico per il Trade Desk, è necessario contattare l&#39;account manager [!DNL Trade Desk] per abilitare la funzione. Se invii e-mail, numeri di telefono e UID2/EUID, devi condividere l&#39;accordo UID2/EUID firmato con [!DNL The Trade Desk].

## Requisiti di corrispondenza ID {#id-matching-requirements}

A seconda del tipo di ID inseriti in Adobe Experience Platform, devi rispettare i requisiti corrispondenti. Per ulteriori informazioni, consulta la [panoramica dello spazio dei nomi delle identità](/help/identity-service/features/namespaces.md).

## Identità supportate {#supported-identities}

[!DNL The Trade Desk] supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

Adobe Experience Platform supporta sia indirizzi e-mail con hash che numeri di telefono. Segui le istruzioni riportate nella sezione sui requisiti di corrispondenza ID e utilizza gli spazi dei nomi appropriati rispettivamente per gli indirizzi e-mail in testo normale e con hash.

| Identità di destinazione | Descrizione |
|---|---|
| E-mail | Indirizzi e-mail (testo non crittografato) |
| Email_LC_SHA256 | Gli indirizzi e-mail devono avere un hash utilizzando SHA256 e lettere minuscole. Non potrai modificare questa impostazione in un secondo momento. |
| Telefono (E.164) | Numeri di telefono che devono essere normalizzati nel formato E.164. Il formato E.164 include un segno più (+), un codice internazionale di chiamata del paese, un prefisso locale e un numero di telefono. Ad esempio: (+)(prefisso del paese)(prefisso dell&#39;area)(numero di telefono). Questo identificatore non è disponibile per The Trade Desk - First-Party Data (EU). |
| Telefono (SHA256_E.164) | Numeri di telefono che sono già stati normalizzati al formato E.164 e quindi sottoposti a hashing utilizzando SHA-256, con l’hash risultante codificato in Base64. Questo identificatore non è disponibile per The Trade Desk - First-Party Data (EU). |
| TDID | ID cookie nel Trade Desk |
| GAID | GOOGLE ADVERTISING ID |
| IDFA | Apple ID per inserzionisti |
| UID2 | Valore UID2 non elaborato |
| UID2Token | Il token UID2 crittografato, noto anche come token pubblicitario. |
| EUID | Valore ID Unione Europea non elaborato |
| EUIDToken | Il token EUID crittografato, noto anche come token pubblicitario. |
| RampID | RampID di 49 o 70 caratteri (precedentemente noto come IdentityLink o IDL). Deve essere un RampID da LiveRamp mappato specificamente per The Trade Desk. |
| netID | NetID dell&#39;utente come stringa con codifica base64 a 70 caratteri. Questo ID è supportato solo in Europa. |
| FirstID | Il First-id dell’utente, un cookie di prima parte generalmente impostato dagli editori in Francia. Questo ID è supportato solo in Europa. |

{style="table-layout:auto"}

## Requisiti di hashing delle e-mail {#email-hashing}

Puoi eseguire l’hashing degli indirizzi e-mail prima di acquisirli in Adobe Experience Platform o utilizzare indirizzi e-mail non elaborati.

Per informazioni sull&#39;acquisizione di indirizzi e-mail in Experience Platform, consulta la [panoramica sull&#39;acquisizione batch](/help/ingestion/batch-ingestion/overview.md).

Se scegli di eseguire l’hash degli indirizzi e-mail da solo, assicurati di soddisfare i seguenti requisiti:

* Rimuovere gli spazi iniziali e finali.
* Converte tutti i caratteri ASCII in minuscolo.
* In `gmail.com` indirizzi e-mail, rimuovi i seguenti caratteri dalla parte del nome utente dell&#39;indirizzo e-mail:

      * Il periodo (`.`) (codice ASCII 46). Ad esempio, normalizzare &quot;jane.doe@gmail.com&quot; in &quot;janedoe@gmail.com&quot;.
     * Il segno più (`+`) (codice ASCII 43) e tutti i caratteri successivi. Ad esempio, normalizzare `janedoe+home@gmail.com` in `janedoe@gmail.com`.
  
## Requisiti di normalizzazione e hashing dei numeri di telefono {#phone-hashing}

Ecco cosa devi sapere sul caricamento dei numeri di telefono:

* È necessario normalizzare i numeri di telefono prima di inviarli in una richiesta, indipendentemente dal fatto che in una richiesta vengano inviati con hash o senza hash.
* Per caricare dati normalizzati, con hash e codificati, devi inviare numeri di telefono come hash SHA-256 con codifica Base64 dei numeri di telefono normalizzati.

Per caricare numeri di telefono non elaborati o con hash, è necessario normalizzarli.

>[!IMPORTANT]
>
>La normalizzazione prima dell’hashing garantisce che il valore ID generato sia sempre lo stesso e che i dati possano essere associati con precisione.

Ecco cosa devi sapere sui requisiti di normalizzazione dei numeri di telefono:

* L&#39;operatore UID2 accetta i numeri di telefono nel formato E.164, che è il formato dei numeri di telefono internazionali che garantisce l&#39;univocità globale.
* I numeri di telefono E.164 possono avere un massimo di 15 cifre.
* I numeri di telefono E.164 normalizzati utilizzano la seguente sintassi: `[+][country code][subscriber number including area code]` senza spazi, trattini, parentesi o altri caratteri speciali. Di seguito sono riportati alcuni esempi:

      * US: 1 (234) 567-8901 è normalizzato a +12345678901.
     * Singapore: 65 1243 5678 è normalizzato a +6512345678.
     * Australia: il numero di telefono cellulare 0491 570 006 è normalizzato per aggiungere il codice del paese e rilasciare lo zero iniziale: +61491570006.
     * Regno Unito: il numero di telefono cellulare 07812 345678 è normalizzato per aggiungere il codice del paese e rilasciare lo zero iniziale: +447812345678.
  
Verificare che il numero telefonico normalizzato sia UTF-8, non un altro sistema di codifica come UTF-16.

Un hash del numero di telefono è un hash SHA-256 con codifica Base64 di un numero di telefono normalizzato. Il numero di telefono viene prima normalizzato, quindi viene eseguito l’hashing utilizzando l’algoritmo di hashing SHA-256 e quindi i byte risultanti del valore hash vengono codificati utilizzando la codifica Base64. La codifica Base64 viene applicata ai byte del valore hash, non alla rappresentazione di stringa con codifica esadecimale.
La tabella seguente mostra un esempio di numero di telefono di input semplice e il risultato di ogni passaggio viene applicato per ottenere un valore sicuro e opaco.

| Tipo | Esempio | Commenti e utilizzo |
|---|---|---|
| Numero di telefono non elaborato | 1 (234) 567-8901 | Questo è il punto di partenza. |
| Numero di telefono normalizzato | +12345678901 | La normalizzazione è sempre il primo passo. |
| Hash SHA-256 del numero di telefono normalizzato | 10e6f0b47054a83359477dcb35231db6de5c69fb1816e1a6b98e192de9e5b9ee | Questa stringa di 64 caratteri è una rappresentazione con codifica esadecimale del SHA-256 a 32 byte. |
| Codifica esadecimale a Base64 SHA-256 del numero di telefono normalizzato e con hash | EObwtHBUqDNZR33LNSMdtt5cafsYFuGmuY4ZLenlue4 | Questa stringa di 44 caratteri è una rappresentazione con codifica Base64 del SHA-256 a 32 byte. L’hash SHA-256 è un valore esadecimale. È necessario utilizzare un codificatore Base64 che accetta un valore esadecimale come input. Utilizza questa codifica per i valori phone_hash inviati nel corpo della richiesta. |

>[!IMPORTANT]
>
>Quando si applica la codifica Base64, assicurarsi di utilizzare una funzione che accetta un valore esadecimale come input. Se utilizzi una funzione che accetta testo come input, il risultato è una stringa più lunga che non è valida ai fini di UID2.

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Audience export]** | Stai esportando tutti i membri di un pubblico con gli identificatori (e-mail o e-mail con hash) utilizzati nella destinazione Trade Desk. |
| Frequenza di esportazione | **[!UICONTROL Daily Batch]** | Poiché un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il profilo (identità) viene aggiornato una volta al giorno a valle della piattaforma di destinazione. Ulteriori informazioni sulle [esportazioni batch](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

### Autentica nella destinazione {#authenticate}

La destinazione CRM [!DNL The Trade Desk] è un caricamento di file batch giornaliero e non richiede l&#39;autenticazione da parte dell&#39;utente.

### Inserisci i dettagli della destinazione {#fill-in-details}

Prima di poter inviare o attivare i dati sul pubblico a una destinazione, devi impostare una connessione alla tua piattaforma di destinazione. Durante la [configurazione](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Account Type]**: scegliere l&#39;opzione **[!UICONTROL Existing Account]**.
* **[!UICONTROL Name]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Description]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Advertiser ID]**: [!DNL Trade Desk Advertiser ID], che può essere condiviso dal tuo Account Manager [!DNL Trade Desk] o essere trovato in [!DNL Advertiser Preferences] nell&#39;interfaccia utente [!DNL Trade Desk].

![Schermata dell&#39;interfaccia utente di Experience Platform che mostra come compilare i dettagli della destinazione.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

Quando ci si connette alla destinazione, l’impostazione di un criterio di governance dei dati è completamente facoltativa. Per ulteriori dettagli, consulta la [panoramica sulla governance dei dati](/help/data-governance/policies/overview.md) di Experience Platform.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, sono necessarie le **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL View Identity Graph]** [per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](/help/destinations/ui/activate-batch-profile-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in una destinazione.

Nella pagina **[!UICONTROL Scheduling]** è possibile configurare la pianificazione e i nomi dei file per ogni pubblico da esportare. La configurazione della pianificazione è obbligatoria, ma il nome del file è facoltativo.

![Schermata dell&#39;interfaccia utente di Experience Platform per pianificare l&#39;attivazione del pubblico.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>Tutti i tipi di pubblico attivati nella destinazione CRM [!DNL The Trade Desk] vengono automaticamente impostati su una frequenza giornaliera e su un&#39;esportazione di file completa.

![Schermata dell&#39;interfaccia utente di Experience Platform per pianificare l&#39;attivazione del pubblico.](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

Nella pagina **[!UICONTROL Mapping]** è necessario selezionare attributi o spazi dei nomi di identità dalla colonna di origine e mappare alla colonna di destinazione.

![Schermata dell&#39;interfaccia utente di Experience Platform per mappare l&#39;attivazione del pubblico.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

Di seguito è riportato un esempio di mapping di identità corretto durante l&#39;attivazione di tipi di pubblico nella destinazione CRM [!DNL The Trade Desk].

Selezione dei campi di origine e di destinazione:

| Campo di origine | Campo di destinazione |
|---|---|
| E-mail | e-mail |
| Email_LC_SHA256 | hash_email |
| Telefono (E.164) | telefono |
| Telefono (SHA256_E.164) | hash_phone |
| TDID | tdid |
| GAID | daid |
| IDFA | idfa |
| UID2 | uid2 |
| UID2Token | uid2_token |
| EUID | euid |
| EUIDToken | euid_token |
| RampID | idl |
| ID5 | id5 |
| netID | net_id |
| FirstID | first_id |


## Convalida esportazione dati {#validate}

Per verificare che i dati siano stati esportati correttamente da Experience Platform in [!DNL The Trade Desk], trovare i tipi di pubblico nella scheda Adobe 1PD nella libreria [!DNL The Trade Desk] &quot;Dati e identità inserzionista&quot;. Di seguito sono riportati i passaggi per trovare l&#39;ID corrispondente nell&#39;interfaccia utente [!DNL Trade Desk]:

1. Selezionare innanzitutto la scheda **[!UICONTROL Libraries]** e rivedere la sezione **[!UICONTROL Advertiser data and identity]**.
2. Fai clic su **[!UICONTROL Adobe 1PD]** per elencare tutti i tipi di pubblico attivati in [!DNL The Trade Desk].
3. Il Nome segmento o l&#39;ID segmento di Experience Platform verrà visualizzato come Nome segmento nell&#39;interfaccia utente [!DNL Trade Desk].

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).
