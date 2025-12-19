---
title: Estensione Nextdoor Conversion API
description: Scopri come utilizzare l’estensione Nextdoor Conversion API per inviare eventi di conversione per monitorare le prestazioni delle campagne pubblicitarie.
last-substantial-update: 2025-12-18T00:00:00Z
source-git-commit: 56c69696300dd9de8c0e98ecc71cafc7328f1620
workflow-type: tm+mt
source-wordcount: '1772'
ht-degree: 8%

---


# Estensione dell&#39;API di conversione [!DNL Nextdoor] - Guida utente

## Panoramica

[!DNL Nextdoor] è un servizio di social networking per i quartieri che connette le persone alle loro comunità locali. È una piattaforma in cui i vicini possono comunicare, condividere informazioni, essere aggiornati su eventi locali e notizie, e comprare e vendere oggetti con altri nella loro zona.

Utilizzare l&#39;estensione [[!DNL Nextdoor] Conversion API](https://help.nextdoor.com/s/article/About-the-Nextdoor-Conversion-API) per inviare eventi di conversione direttamente all&#39;API di conversione [!DNL Nextdoor's]. Questa estensione consente di monitorare e misurare le prestazioni delle campagne pubblicitarie [!DNL Nextdoor] inviando dati di conversione lato server.

Questa guida illustra come installare, configurare e utilizzare l&#39;estensione API di conversione [!DNL Nextdoor] nell&#39;inoltro degli eventi [rules](https://experienceleague.adobe.com/en/docs/experience-platform/tags/ui/rules).

## Prerequisiti {#prerequisites}

Per utilizzare questa estensione è necessario un account [!DNL Nextdoor] Ads Manager valido. Se non ne hai già uno, vai alla [[!DNL Nextdoor Ads] pagina di registrazione](https://ads.nextdoor.com/v2/signup) per registrarti e creare il tuo account.

### Raccogliere i dettagli di configurazione richiesti {#configuration-details}

Per connettere Experience Platform a [!DNL Nextdoor], sono necessarie le seguenti informazioni:

| Credenziali | Descrizione | Note sulla sicurezza |
| --- | --- | --- |
| ID Data Source | L&#39;identificatore univoco dell&#39;origine dati da [!DNL Nextdoor], disponibile nell&#39;account [!DNL Nextdoor Ads Manager] accedendo alla pagina Assets > Pixel e generando un pixel Nextdoor. | Puoi condividerlo all’interno della tua organizzazione in tutta sicurezza. |
| Token di accesso | Il token di accesso per l’autenticazione API per una comunicazione sicura. Puoi generare questo token accedendo al tuo account [!DNL Nextdoor Ads Manager] e alle impostazioni API. | Mantieni sicuro questo token, in quanto fornisce l’accesso al tuo account. |

## Installa e configura l&#39;estensione [!DNL Nextdoor] {#install}

Per installare l&#39;estensione, seleziona **[!UICONTROL Extensions]** nel menu di navigazione a sinistra. Nella scheda **[!UICONTROL Catalog]**, selezionare **[!UICONTROL Nextdoor Conversion API Extension]**, quindi selezionare **[!UICONTROL Install]**.

![Il catalogo delle estensioni mostra la scheda delle estensioni [!DNL Nextdoor] che evidenzia l&#39;installazione.](../../../images/extensions/server/nextdoor/install-extension.png)

Nella schermata successiva, immettere i valori di configurazione generati da [!DNL Nextdoor Ads Manager]:

* **[!UICONTROL Data Source ID]**
* **[!UICONTROL Access Token]**

Al termine, selezionare **[!UICONTROL Save]**.

Schermata di configurazione ![[!DNL Nextdoor] per l&#39;estensione dell&#39;API di conversione [!DNL Nextdoor].](../../../images/extensions/server/nextdoor/configure.png)

## Configurare una regola di inoltro degli eventi {#config-rule}

Una volta configurati tutti gli elementi dati, puoi creare regole di inoltro degli eventi che determinano quando e come inviare gli eventi a [!DNL Nextdoor].

Crea una nuova [regola](../../../ui/managing-resources/rules.md) nella proprietà di inoltro eventi. In **[!UICONTROL Actions]**, aggiungere una nuova azione e impostare l&#39;estensione su **[!UICONTROL Nextdoor Conversion API Extension]**. Per inviare eventi Edge Network a [!DNL Nextdoor], impostare **[!UICONTROL Action Type]** su **[!UICONTROL Report Web Conversions]**.

![Tipo di azione [!UICONTROL Report Web Conversions] selezionato per una regola [!DNL Nextdoor] nell&#39;interfaccia utente di Data Collection.](../../../images/extensions/server/nextdoor/select-action.png)

Dopo aver effettuato questa selezione, vengono visualizzati controlli aggiuntivi che consentono di configurare ulteriormente l’evento, come descritto di seguito. Al termine, selezionare **[!UICONTROL Keep Changes]** per salvare la regola.

**Parametri corpo principale**

Questi parametri di base definiscono l’evento di conversione:

| Parametro | Descrizione | Tipo di dati | Obbligatorio | Opzioni/Formato | Esempio |
| ------------------------------------ | -------------- | -------------- | -------------- | -------------- | -------------- |
| [!UICONTROL Event Name] | Specifica il tipo di evento di conversione tracciato. | Stringa (a discesa) | Obbligatorio | <ul><li>Acquisto</li><li>Lead</li><li>Registrati</li><li>Aggiungi al carrello</li><li>Avvia estrazione</li><li>Visualizzazione pagina</li><li>Ricerca</li><li>Visualizza contenuto</li><li>Aggiungi alla lista dei desideri</li><li>Abbonati</li><li>Personalizzato</li></li>Conversione 1-10</li></ul> | `Purchase` |
| [!UICONTROL Event ID] | Identificatore univoco per impedire la generazione di rapporti sugli eventi duplicati. Se questo campo viene lasciato vuoto, viene generato automaticamente. | Stringa | Facoltativo | Identificatore di stringa univoco | `order_12345` |
| [!UICONTROL Event Time (Unix Epoch)] | Timestamp in cui si è verificato l’evento di conversione. Se non specificato, viene utilizzata l&#39;ora corrente. | Intero | Facoltativo | Timestamp Unix in secondi | `1703980800` (30 dicembre 2023) |
| [!UICONTROL Action Source] | Canale o piattaforma in cui si è verificata la conversione. | Stringa (a discesa) | Obbligatorio | <ul><li>sito web</li><li>e-mail</li><li>app</li><li>phone_call</li><li>chat</li><li>physical_store</li><li>system_generated</li><li>altro</li></ul> | `website` |
| [!UICONTROL Data Source ID] | Sostituisci l’ID dell’origine dati globale per eventi specifici. Se lasciato vuoto, eredita dalla configurazione. | Stringa | Facoltativo | Stringa alfanumerica | `12345` |
| [!UICONTROL Action Source URL] | L’URL specifico in cui si è verificata la conversione. | Stringa | Facoltativo | URL completo comprensivo di protocollo | https://example.com/checkout/success |

**Parametri di privacy e conformità**

Utilizza questi parametri per garantire la conformità alla privacy:

| Parametro | Descrizione | Tipo di dati | Obbligatorio | Valori/Formato | Esempio |
| -------------------------------------------- | ---------------------------------------------------  | --------- | -------- | ---------------------------------------------------------- | ---------- |
| [!UICONTROL Restricted Data Usage] | Contrassegno flag per limitare l’utilizzo dei dati per rispettare la privacy. | Intero | Facoltativo | <ul><li>0 = Nessuna restrizione</li><li>1 = Restrict</li></ul> | `0` |
| [!UICONTROL Restricted Data Usage (Country)] | Limitazioni di elaborazione dei dati specifiche per paese. | Intero | Facoltativo | 1 = Stati Uniti (possono essere supportati altri codici) | `1` |
| [!UICONTROL Restricted Data Usage (State)] | Restrizioni specifiche per gli Stati Uniti. | Intero | Facoltativo | 1000 = CA, 1001 = CO, ecc. | `1000` |
| [!UICONTROL Test Event] | Contrassegna l&#39;evento come test per lo sviluppo/il debug. | Stringa | Facoltativo | Qualsiasi stringa non vuota | `test` |

**Parametri informazioni cliente**

>[!IMPORTANT]
>
>Devi fornire almeno un parametro di informazioni sul cliente per l’attribuzione e la corrispondenza corrette degli eventi.

| Parametro | Descrizione | Tipo di dati | Obbligatorio | Formato | Esempio |
| ------------------------------ | ----------------------------------------------- | --------- | ------------------------------------ | ------------------------------------ | -------------------------- |
| [!UICONTROL Email] | Indirizzo e-mail del cliente per la corrispondenza delle identità. | Stringa | È necessario almeno un campo cliente | Testo normale o hash SHA-256 | `user@example.com` |
| [!UICONTROL Phone Number] | Numero di telefono del cliente per la corrispondenza delle identità. | Stringa | È necessario almeno un campo cliente | Formato E.164 (con hash SHA-256) | `+15551234567` |
| [!UICONTROL First Name] | Nome del cliente per una corrispondenza migliorata. | Stringa | È necessario almeno un campo cliente | Testo normale o hash SHA-256 | `John` |
| [!UICONTROL Last Name] | Cognome del cliente per corrispondenza avanzata. | Stringa | È necessario almeno un campo cliente | Testo normale o hash SHA-256 | `Smith` |
| [!UICONTROL Date of Birth] | Data di nascita del cliente per la corrispondenza demografica. | Stringa | Facoltativo | AAAAMMGG (SHA-256 con hash) | `19900115` |
| [!UICONTROL Gender] | Sesso del cliente per il targeting demografico. | Stringa | Facoltativo | M/F/O (sha-256 con hash) | `M` |
| [!UICONTROL External ID] | L’identificatore cliente interno. | Stringa | Facoltativo | Qualsiasi stringa univoca | `customer_12345` |
| [!UICONTROL Street Address] | Indirizzo del cliente. | Stringa | Facoltativo | SHA-256 con hash | `123 Main Street` (con hash) |
| [!UICONTROL City] | Città del cliente. | Stringa | Facoltativo | SHA-256 con hash | `San Francisco` (con hash) |
| [!UICONTROL State] | Provincia del cliente. | Stringa | Facoltativo | Codice a due lettere (con hash SHA-256) | `CA` (con hash) |
| [!UICONTROL Zip Code] | Codice postale del cliente. | Stringa | Facoltativo | Prime 5 cifre US (SHA-256 con hash) | `94102` (con hash) |
| [!UICONTROL Country] | Paese del cliente. | Stringa | Facoltativo | ISO-3166-1 alpha-2 (con hash SHA-256) | `US` (con hash) |
| [!UICONTROL Click ID] | Identificatore di clic NextPort per l’attribuzione. | Stringa | Facoltativo | Acquisito dal parametro URL `ndclid` | `nd_click_12345abcdef` |
| [!UICONTROL Client IP Address] | Indirizzo IP del dispositivo dell’utente. | Stringa | Facoltativo | Indirizzo IPv4 o IPv6 | `192.168.1.1` |
| [!UICONTROL Client User Agent] | Stringa dell’agente utente del browser. | Stringa | Facoltativo | Stringa agente utente del browser non elaborata | `Mozilla/5.0 (Windows...)` |

**Parametri personalizzati**

Questi parametri forniscono contesto aggiuntivo sull’evento di conversione:

| Parametro | Descrizione | Tipo di dati | Obbligatorio | Formato | Esempio |
| ------------------------------ | ---------------------------------------------- | ------------------- | -------------------------------- | --------------------------------------- | ----------------------- |
| [!UICONTROL Order Value] | Valore totale della transazione di acquisto. | Stringa | **OBBLIGATORIO per gli eventi di acquisto** | Valuta ISO 4217 + Importo (senza spazi) | `USD123.45` |
| [!UICONTROL Order ID] | Identificatore univoco di transazione o ordine. | Stringa | Facoltativo | Qualsiasi stringa univoca | `order_12345` |
| [!UICONTROL Delivery Category] | Metodo di consegna del prodotto/servizio. | Stringa | Facoltativo | <ul><li>`in_store`</li><li>`curbside`</li><li>`home_delivery`</li></ul> | `home_delivery` |
| [!UICONTROL Product Context] | Informazioni dettagliate sui prodotti acquistati. | Stringa (array JSON) | Facoltativo | Array JSON di oggetti prodotto | `[{"id":"SKU123","content_name":"Widget","item_price":29.99,"quantity":1}]` |

**Parametri app mobile**

È necessario includere questi parametri quando `Action Source = 'APP'`:

| Parametro | Descrizione | Tipo di dati | Obbligatorio | Formato | Esempio |
| --------------------------------- | --------------------------------------------- | --------- | --------------------------- | ----------------------------------------- | ----------------- |
| [!UICONTROL App ID*] | Identificatore dell’applicazione mobile. | Stringa | **OBBLIGATORIO per gli eventi APP** | <ul><li>ID bundle (iOS)</li><li>Nome pacchetto (Android)</li></ul> | `com.company.app` |
| [!UICONTROL App Tracking Enabled] | Stato del consenso per la trasparenza del tracciamento delle app di iOS. | Stringa | **OBBLIGATORIO per gli eventi APP** | Stringa booleana | `true` |
| [!UICONTROL Platform] | Sistema operativo mobile. | Stringa | **OBBLIGATORIO per gli eventi APP** | <ul><li>`iOS`</li><li>`Android`</li></ul> | `Android` |
| [!UICONTROL App Version] | Versione dell’app mobile. | Stringa | **OBBLIGATORIO per gli eventi APP** | Stringa di versione definita dall’app | `2.0.0-beta` |

## Tipi di evento {#event-types}

I seguenti tipi di evento sono supportati per diversi scenari di conversione:

| Nome evento | Tipo evento | Descrizione | Caso d’uso | Campi obbligatori | Note |
| ------------------------ | ---------- | -------------------------------------- | --------------------------------------- | -------------------------------------- | ------------------------------------- |
| [!UICONTROL Purchase] | Standard | Transazione di acquisto completata. | Conversioni e-commerce | <ul><li>Nome evento</li><li>Valore ordine</li><li>Informazioni Cliente</li></ul> | Più importante per l’ottimizzazione ROAS |
| [!UICONTROL Lead] | Standard | Generazione di lead o richiesta di informazioni. | Invio di moduli, richieste di contatto | <ul><li>Nome evento</li><li>Informazioni Cliente</li></ul> | Conversione di alto valore per B2B |
| [!UICONTROL Sign Up] | Standard | Registrazione utente o creazione account. | Iscrizione alla newsletter, registrazione account | <ul><li>Nome evento</li><li>Informazioni Cliente</li></ul> | Tracciamento delle conversioni Top-funnel |
| [!UICONTROL Add to Cart] | Standard | Prodotto aggiunto al carrello. | Tracciamento funnel per e-commerce | <ul><li>Nome evento</li><li>Informazioni Cliente</li></ul> | Segnale di coinvolgimento mid-funnel |
| [!UICONTROL Initiate Checkout] | Standard | Processo di estrazione avviato. | Tracciamento intento di acquisto | <ul><li>Nome evento</li><li>Informazioni Cliente</li></ul> | Indicatore forte intento di acquisto |
| [!UICONTROL Page View] | Standard | Pagina importante visitata. | Coinvolgimento con i contenuti, pagine di destinazione | <ul><li>Nome evento</li><li>Informazioni Cliente</li></ul> | Usa solo per pagine di alto valore |
| [!UICONTROL Search] | Standard | Ricerca eseguita sul sito. | Individuazione di prodotti e contenuti | <ul><li>Nome evento</li><li>Informazioni Cliente</li></ul> | Indica il coinvolgimento attivo dell&#39;utente |
| [!UICONTROL View Content] | Standard | Contenuto o prodotto visualizzato. | Visualizzazioni di pagine di prodotti, coinvolgimento con i contenuti | <ul><li>Nome evento</li><li>Informazioni Cliente</li></ul> | Utile per i tipi di pubblico di remarketing |
| [!UICONTROL Add to Wishlist] | Standard | Prodotto aggiunto alla lista dei desideri. | Intento di acquisto futuro | <ul><li>Nome evento</li><li>Informazioni Cliente</li></ul> | Indica un forte interesse per il prodotto |
| [!UICONTROL Subscribe] | Standard | Iscrizione a servizio/newsletter. | Ricavi ricorrenti, coinvolgimento | <ul><li>Nome evento</li><li>Informazioni Cliente</li></ul> | Indicatore di valore a vita elevata |
| [!UICONTROL Custom Conversion 1 - 10] | Personalizzato | Evento di conversione specifico per l’azienda. | Definisci il tipo di conversione | <ul><li>Nome evento</li><li>Informazioni Cliente</li></ul> | Personalizza per azioni aziendali specifiche |

## Integrazione degli elementi dati {#data-element}

Tutti i campi supportano gli elementi dati di inoltro eventi di Adobe. Seleziona l&#39;icona dell&#39;elemento dati ![elementi dati](../../../images/extensions/server/nextdoor/data-element-icon.png) accanto a qualsiasi campo per:

* **Seleziona elementi dati esistenti**: seleziona gli elementi dati già creati.
* **Aggiungi nuovi elementi dati**: crea e definisci nuovi elementi dati in base alle esigenze.
* **Applica valori dinamici**: popola i campi con il contenuto dinamico ottenuto dal tuo sito Web.

## Best practice {#best-practices}

Segui queste best practice per garantire un tracciamento accurato delle conversioni, migliorare la qualità dei dati e rispettare le normative sulla privacy. Questi consigli consentiranno di massimizzare l&#39;efficacia dell&#39;integrazione dell&#39;API di conversione [!DNL Nextdoor] e di ottimizzare le prestazioni pubblicitarie.

### Qualità dei dati e conformità alla privacy

Una corretta gestione dei dati è essenziale per massimizzare l’accuratezza dell’attribuzione della conversione mantenendo al contempo la privacy degli utenti e la conformità alle normative. Queste procedure garantiscono che i dati dei clienti vengano formattati correttamente, elaborati in modo sicuro e gestiti in conformità alle normative sulla privacy.

* **Formattazione dei dati coerente**: formattazione coerente di e-mail, numeri di telefono e altri dati:

   * **Normalizzazione e-mail**: converti le e-mail in lettere minuscole, taglia gli spazi vuoti e rimuovi i punti dagli indirizzi [!DNL Gmail].
   * **Standardizzazione numero di telefono**: utilizza il formato E.164 (+1234567890) per la compatibilità internazionale.
   * **Normalizzazione degli indirizzi**: standardizzare le abbreviazioni stradali (St., Ave., Rd.) e rimuovere eventuali spazi in più.
   * **Formattazione nome**: converti i nomi in minuscolo, rimuovi gli spazi in eccesso e gestisci i caratteri speciali in modo coerente.

* **Dati sensibili all&#39;hashing**: provare a eseguire l&#39;hashing dei dati sensibili dei clienti prima di inviarli. Normalizza sempre i dati prima dell’hashing per garantire valori di hashing coerenti:

   * Utilizza l’hashing SHA-256 per numeri di telefono, indirizzi e altri dati PII.
   * L’estensione applica automaticamente l’hash alle e-mail in testo normale: puoi inviare entrambi i formati.
   * Hash coerente dei dati in tutte le implementazioni di tracciamento.
      * **Esempio**: normalizzare &quot;John@Example.COM&quot; → &quot;john@example.com&quot; prima dell&#39;hashing.

* **Fornisci informazioni complete**: includi quante più informazioni possibili per una migliore corrispondenza:

   * Includi più identificatori (e-mail + telefono, o e-mail + nome + indirizzo) se disponibili.
   * Utilizza gli ID cliente esterni per collegare eventi di conversione ai tuoi dati di gestione delle relazioni con i clienti.
   * Fornisci dati demografici (età, genere) quando disponibili e conformi alle leggi sulla privacy.

* **Gestione del consenso**: assicurati di disporre del consenso corretto per la raccolta dei dati:

   * Implementa meccanismi di consenso appropriati prima di raccogliere i dati dei clienti.
   * Rispetta le preferenze di rinuncia dell’utente e le richieste di eliminazione dei dati.
   * Utilizza i parametri Limitato all’utilizzo dei dati per gli utenti che hanno rinunciato.
   * **Risorse**:
      * [Guida alla conformità RGPD](https://gdpr.eu/compliance/)
      * [Requisiti per la privacy del CCPA](https://oag.ca.gov/privacy/ccpa)

* **Minimizzazione dati**: invia solo i dati necessari per il tracciamento delle conversioni:

   * Raccogli e invia solo dati essenziali per l’attribuzione e l’ottimizzazione.
   * Esamina e controlla regolarmente i campi di dati che stai inviando.
   * Rimuovi le informazioni non necessarie per ridurre i rischi per la privacy.

* **Utilizza marche temporali precise**: assicurati che le marche temporali dell&#39;evento siano precise per la corretta attribuzione.
   * Utilizza il tempo effettivo in cui si è verificata la conversione, non quando hai elaborato i dati.
   * Assicurati che le marche temporali siano in formato Unix (secondi dal 1° gennaio 1970).
   * Considera le differenze di fuso orario nei calcoli delle marche temporali.

### Deduplicazione degli eventi

Impedisci la duplicazione degli eventi di conversione per garantire una misurazione accurata delle campagne ed evitare metriche di prestazioni eccessive. Implementa la deduplicazione corretta in modo che ogni conversione venga conteggiata una sola volta, fornendo dati affidabili per le decisioni di ottimizzazione.

* **Fornisci ID evento univoci**: utilizza sempre ID evento univoci per evitare conversioni duplicate.
* **Utilizza nomi coerenti**: applica nomi di eventi coerenti nell&#39;implementazione.

### Limitazione di tariffa

L&#39;API di conversione [!DNL Nextdoor] è soggetta a limite di frequenza. Il limite di frequenza corrente è **100 richieste/minuto** per inserzionista. Se superi il limite di velocità, l&#39;API restituirà un codice di errore `HTTP 429 Too Many Requests`.

## Conclusione {#conclusion}

L&#39;estensione dell&#39;API di conversione [!DNL Nextdoor] consente di tenere traccia delle conversioni e misurare l&#39;efficacia delle campagne pubblicitarie [!DNL Nextdoor]. Seguendo questa guida e implementando le best practice, puoi garantire un tracciamento accurato delle conversioni e ottimizzare le prestazioni pubblicitarie.

Per informazioni aggiornate e risorse aggiuntive, visitare [[!DNL Nextdoor Ads Manager]](https://ads.nextdoor.com).

## Passaggi successivi {#next-steps}

In questa guida viene illustrato come inviare dati evento lato server a [!DNL Nextdoor] utilizzando l&#39;estensione API di conversione [!DNL Nextdoor]. Per ulteriori informazioni sulle funzionalità di inoltro eventi in [!DNL Adobe Experience Platform], vedere la [panoramica sull&#39;inoltro eventi](../../../ui/event-forwarding/overview.md).
