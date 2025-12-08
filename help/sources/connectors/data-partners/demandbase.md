---
title: Intento Demandbase
description: Scopri l’origine di Intento Demandbase su Experience Platform.
last-substantial-update: 2025-03-26T00:00:00Z
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Edizione B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: 62dd27e0-b846-4c04-977f-8a3ab99bc464
source-git-commit: e223ea754a250956e65c3f526119a3ebd7bb067c
workflow-type: tm+mt
source-wordcount: '1504'
ht-degree: 1%

---

# [!DNL Demandbase Intent]

[!DNL Demandbase] è una piattaforma di marketing basata sull&#39;account che è possibile utilizzare per il successo di vendite e marketing B2B. [!DNL Demandbase Intent] è un&#39;origine Adobe Experience Platform che puoi utilizzare per collegare il tuo account [!DNL Demandbase] ad Experience Platform e integrare i dati di intento dell&#39;account.

Con l&#39;origine [!DNL Demandbase], è possibile identificare account con interessi elevati in base a impegni in tempo reale. Assegnando priorità ai segnali di intento più forti, puoi creare segmenti precisi e distribuire campagne iper-mirate, garantendo che le attività di marketing si concentrino sugli account che hanno più probabilità di conversione. L’attivazione di strategie basate sulle intenzioni consente di ottimizzare la spesa pubblicitaria, aumentare il coinvolgimento e aumentare il ROI.

Per informazioni sui prerequisiti nell&#39;origine [!DNL Demandbase], leggere questo documento.

## Prerequisiti {#prerequisites}

Leggere le sezioni seguenti per i passaggi preliminari prima di connettere [!DNL Demandbase] ad Experience Platform.

### Indirizzo IP inserisco nell&#39;elenco Consentiti

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un inserisco nell&#39;elenco Consentiti di. La mancata aggiunta di indirizzi IP specifici per l’area geografica al elenco Consentiti può causare errori o non prestazioni durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [Indirizzo IP/inserisco nell&#39;elenco Consentiti di](../../ip-address-allow-list.md).

### Configurare le autorizzazioni su Experience Platform

Per connettere l&#39;account **[!UICONTROL View Sources]** ad Experience Platform, è necessario che per l&#39;account siano abilitate sia le autorizzazioni **[!UICONTROL Manage Sources]** che quelle [!DNL Demandbase]. Contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie. Per ulteriori informazioni, leggere la [guida all&#39;interfaccia utente per il controllo degli accessi](../../../access-control/abac/ui/permissions.md).

### Vincoli di denominazione per file e directory

Quando si assegna un nome al file o alla directory di archiviazione cloud, è necessario tenere presenti le restrizioni elencate di seguito:

* I nomi dei componenti di directory e file non possono superare i 255 caratteri.
* I nomi di file e directory non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
* I seguenti caratteri URL riservati devono essere correttamente preceduti dall&#39;escape: `! ' ( ) ; @ & = + $ , % # [ ]`
* I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
* Non sono consentiti caratteri di percorso URL non validi. I punti di codice come `\uE000`, sebbene validi nei nomi di file NTFS, non sono caratteri Unicode validi. Inoltre, alcuni caratteri ASCII o Unicode, come i caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.), non sono consentiti. Per le regole che regolano le stringhe Unicode in HTTP/1.1, vedere [RFC 2616, Sezione 2.2: Regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
* Non sono consentiti i seguenti nomi di file: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carattere punto (.) e due caratteri punto (..).

### Raccogli le credenziali richieste

[!DNL Demandbase] su Experience Platform è ospitato da [!DNL Google Cloud Storage]. Per autenticare correttamente l&#39;account [!DNL Demandbase], è necessario fornire i valori appropriati per le credenziali seguenti:

| Credenziali | Descrizione |
| --- | --- |
| ID chiave di accesso | ID della chiave di accesso [!DNL Demandbase]. Si tratta di una stringa alfanumerica di 61 caratteri necessaria per autenticare l’account in Experience Platform. |
| Chiave di accesso segreta | Chiave di accesso segreta [!DNL Demandbase]. Si tratta di una stringa con codifica base 64 di 40 caratteri necessaria per autenticare l’account in Experience Platform. |
| Nome del bucket | Il bucket [!DNL Demandbase] da cui verranno estratti i dati. |
| Percorso della cartella | Percorso della cartella a cui desideri fornire l’accesso. |

Per ulteriori informazioni su queste credenziali, leggere la [[!DNL Google Cloud Storage] Guida delle chiavi HMAC](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Per i passaggi su come generare la propria chiave di accesso, leggere la [guida ai prerequisiti nella [!DNL Google Cloud Storage] panoramica origine](../cloud-storage/google-cloud-storage.md#prerequisite-setup-for-connecting-your-google-cloud-storage-account).

## Schema [!DNL Demandbase]

>[!IMPORTANT]
>
>Durante la creazione di uno schema B2B per gli intenti dell’account Demandbase nell’interfaccia utente di Experience Platform, assicurati di abilitare l’acquisizione del profilo per lo schema. Per ulteriori informazioni, leggere la guida su [creazione e modifica di schemi nell&#39;interfaccia utente](../../../xdm/ui/resources/schemas.md).

Leggere questa sezione per informazioni sullo schema [!DNL Demandbase] e sulla struttura dei dati.

Lo schema [!DNL Demandbase] è denominato **Intento account Demandbase B2B**. Si tratta delle informazioni di intento settimanali (ricerca dell’acquirente B2B anonimo e consumo di contenuti) su un account e parole chiave specifici. I dati sono in formato parquet.

* Classe - XDM [!DNL Demandbase Account Intent]
* Spazio dei nomi - B2B [!DNL Demandbase Account Intent]
* Identità primaria - `intentID`
* Relazioni - Account B2B

| Nome campo | Tipo di dati | Descrizione |
|--------------------------|-----------|-------------------------------------------------------------------------------------------------------------|
| `extSourceSystemAudit` | OGGETTO | Questo campo contiene informazioni sul controllo del sistema provenienti da una fonte esterna. |
| `_id` | STRINGA | Questo è l’identificatore di sistema univoco del record. |
| `accountDomain` | STRINGA | Questo campo contiene il dominio dell’account. |
| `accountID` | STRINGA | Questo è l’ID account B2B a cui è associato il record intento. |
| `demandbaseAccountID` | STRINGA | Questo è l&#39;ID società in [!DNL Demandbase]. |
| `durationType` | STRINGA | Questo campo specifica il tipo di periodo di validità dell’intento, ad esempio &quot;settimana&quot;. |
| `endDate` | DATA | Data di fine del periodo di validità dell&#39;intento. |
| `intentID` | STRINGA | Si tratta di un valore univoco generato dal sistema per il record intento. |
| `intentStrength` | STRINGA | Questo campo specifica il tipo di periodo di validità dell’intento, ad esempio &quot;DAY&quot;, &quot;WEEK&quot; o &quot;MONTH&quot;. |
| `isTrending` | BOOLEANO | Questo campo indica se la parola chiave ha tendenza, con valori possibili come Basso, Medium o Alto. |
| `keyword` | STRINGA | Questo campo contiene la parola chiave o la frase che indica l&#39;intento da [!DNL Demandbase]. |
| `keywordSetID` | STRINGA | Identificatore del set di parole chiave. |
| `keywordSetName` | STRINGA | Nome del set di parole chiave. |
| `numTrendingDays` | NUMERO INTERO | Questo campo indica il numero di giorni in cui la parola chiave ha avuto una tendenza. |
| `partitionDate` | DATA | Data di partizione del record. |
| `peopleResearchingCount` | NUMERO INTERO | Questo campo indica il numero di persone che ricercano la parola chiave. |
| `startDate` | DATA | Data di inizio del periodo di validità dell&#39;intento. |
| `trendingScore` | NUMERO INTERO | Questo campo contiene il punteggio di tendenza per la parola chiave. |

{style="table-layout:auto"}

>[!TIP]
>
>Eventuali modifiche allo schema vengono comunicate in anticipo ad Adobe. Per supportare un’evoluzione dello schema fluida, è essenziale mantenere la compatibilità con le versioni precedenti. Experience Platform applica un approccio di controllo delle versioni di sola aggiunta, garantendo che gli aggiornamenti allo schema non siano distruttivi. Ciò significa che le modifiche che causano interruzioni sono severamente vietate e sono consentite solo le modifiche che migliorano o estendono lo schema esistente.

## Connetti il tuo account [!DNL Demandbase] ad Experience Platform nell&#39;interfaccia utente

Dopo aver completato la configurazione dei prerequisiti, leggi l&#39;esercitazione su [connessione dell&#39;account [!DNL Demandbase] ad Experience Platform](../../tutorials/ui/create/data-partners/demandbase.md) per avviare l&#39;integrazione.

## Domande frequenti {#faq}

Leggere questa sezione per le risposte alle domande frequenti relative all&#39;origine [!DNL Demandbase].

### È necessario disporre di un contratto esistente con [!DNL Demandbase] per utilizzare i dati di intento dell&#39;account in Real-Time CDP B2B edition?

+++Risposta

Sì, è necessario disporre di un contratto attivo con [!DNL Demandbase] per accedere e utilizzare i dati di intento in Experience Platform e Real-Time CDP B2B edition. L&#39;integrazione sfrutta il contratto esistente con [!DNL Demandbase] per acquisire e attivare i segnali di intento dell&#39;account in Experience Platform e Real-Time CDP.

+++

### I campi personalizzati di [!DNL Demandbase] sono supportati in questa integrazione?

+++Risposta

Al momento, è possibile utilizzare solo i campi standard [!DNL Demandbase] per l&#39;acquisizione e l&#39;attivazione. Per visualizzare l&#39;elenco dei campi supportati, leggere la [[!DNL Demandbase] guida allo schema](#schema) per i dettagli sulla disponibilità dei campi.

+++

### È possibile acquisire dati da [!DNL Demandbase] ad Experience Platform su base ad hoc?

+++Risposta

Sì, è possibile acquisire dati da [!DNL Demandbase] su base ad hoc. Puoi creare un nuovo flusso di dati per acquisire i dati di intento più recenti, purché siano presenti nuovi dati da [!DNL Demandbase]. Tuttavia, puoi avere un solo flusso di dati attivo alla volta. Assicurati quindi di eliminare il flusso di dati esistente, prima di crearne uno nuovo.

+++

### Qual è il processo di convalida per i dati intento e come posso verificare quali dati intento sono collegati a un account specifico?

+++Risposta

Per convalidare i dati di intento e determinare quali segnali di intento sono collegati ad account specifici, utilizzare [Adobe Experience Platform Query Service](../../../query-service/home.md) per AccountID.

+++

### Come posso cercare un intento per una società specifica?

+++Risposta

Eseguire una query SQL in [Query Service](../../../query-service/home.md) per cercare i dati di intento utilizzando il nome della società o l&#39;ID account. Per visualizzare tutti i dati di intento per una società specifica, è possibile eseguire una query SQL in Query Service utilizzando il nome della società o l&#39;ID account per recuperare tutti i segnali di intento associati.

+++


### Ho riscontrato un problema nel processo di corrispondenza dell’account in Experience Platform. Come procedere?

+++Risposta

La risoluzione dipende dal problema specifico:

* **Dominio società errato o mancante in Experience Platform**: se il problema deriva da un valore del dominio società errato nei dati dell&#39;account, aggiorna il campo del dominio società in Experience Platform per garantire una corrispondenza accurata.
* **Mappatura campo non corretta nel flusso di dati**: se il problema è dovuto a un percorso di campo del dominio della società non corretto nel flusso di dati, aggiorna la configurazione del flusso di dati in modo che faccia riferimento al percorso di campo corretto.

+++

### Come si eliminano i dati di intento in Experience Platform?

+++Risposta

È necessario [eliminare il set di dati](../../../catalog/datasets/user-guide.md#delete-a-dataset) per eliminare i dati intento in Experience Platform.

+++

### Quale campo viene utilizzato per associare gli account da [!DNL Demandbase] ad Experience Platform?

+++Risposta

Il campo `accountOrganization.domain` viene utilizzato per gli account corrispondenti. Se la tua organizzazione utilizza un campo personalizzato diverso per memorizzare il nome del sito web, assicurati di fornire il percorso del campo corretto per una mappatura accurata.

+++

### Cosa succede quando il dominio di un’azienda viene aggiornato in Experience Platform?

+++Risposta

Quando un dominio della società viene aggiornato, il nuovo valore del dominio viene applicato nella successiva esecuzione del flusso di dati. Ciò garantisce che:

* Per l’acquisizione di dati con intento futuro, utilizza il dominio aggiornato per la corrispondenza dell’account.
* Eventuali segnali di intento precedentemente non corrispondenti ora possono essere allineati correttamente con l’account previsto.
* Non vengono apportate modifiche retroattive ai dati acquisiti precedenti; i dati nuovi e in arrivo rispecchieranno l’aggiornamento.

+++

### Qual è il processo di corrispondenza del dominio?

+++Risposta

La corrispondenza del dominio in Experience Platform si basa su una corrispondenza esatta del valore del campo di dominio sottoposto a scorrimento. Experience Platform rimuove automaticamente i prefissi (ad esempio, https:/<span>/www.) e mantiene il dominio di primo livello (ad esempio, adobe.com). La corrispondenza richiede un valore di dominio esatto, senza supporto per corrispondenza fuzzy o sottodomini.

+++

### Dove posso usare i dati intento?

+++Risposta

I dati sulle finalità possono essere utilizzati in [Tipi di pubblico dell&#39;account](../../../segmentation/types/account-audiences.md) per migliorare il targeting, la segmentazione e la personalizzazione. Sfruttando i segnali di intento, le aziende possono identificare e interagire con gli account che mostrano un forte interesse per argomenti specifici, ottimizzando il marketing e la portata delle vendite

+++
