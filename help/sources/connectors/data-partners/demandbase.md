---
title: Intento Demandbase
description: Scopri l’origine di Intento Demandbase su Experience Platform.
last-substantial-update: 2025-03-26T00:00:00Z
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Edizione B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: 62dd27e0-b846-4c04-977f-8a3ab99bc464
source-git-commit: a1af85c6b76cc7bded07ab4acaec9c3213a94397
workflow-type: tm+mt
source-wordcount: '1475'
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

Per connettere l&#39;account [!DNL Demandbase] ad Experience Platform, è necessario che per l&#39;account siano abilitate le autorizzazioni **[!UICONTROL Visualizza origini]** e **[!UICONTROL Gestisci origini]**. Contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie. Per ulteriori informazioni, leggere la [guida all&#39;interfaccia utente per il controllo degli accessi](../../../access-control/abac/ui/permissions.md).

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

Leggere questa sezione per informazioni sullo schema [!DNL Demandbase] e sulla struttura dei dati.

Lo schema [!DNL Demandbase] è denominato **Company Intent Weekly**. Si tratta delle informazioni di intento settimanali (ricerca dell’acquirente B2B anonimo e consumo di contenuti) su un account e parole chiave specifici. I dati sono in formato parquet.

| Nome campo | Tipo di dati | Obbligatorio | Chiave business | Note |
| --- | --- | --- | --- | --- |
| `company_id` | STRINGA | TRUE | SÌ | ID canonico dell’azienda. |
| `domain` | STRINGA | TRUE | SÌ | Il dominio identificato dell’account che mostra l’intento. |
| `start_date` | DATA | TRUE | SÌ | Data di inizio in cui si è verificata l’attività di intento nel periodo di durata. |
| `end_date` | DATA | TRUE | SÌ | Data di fine in cui si è verificata l’attività di intento nel periodo di durata. |
| `duration_type` | STRINGA | TRUE | SÌ | Tipo di durata. In genere, questo valore può essere giornaliero, settimanale o mensile a seconda della durata di rollup scelta. Per questo esempio di dati, il valore è `week`. |
| `keyword_set_id` | STRINGA | TRUE | SÌ | ID del set di parole chiave. È univoco per ogni cliente. |
| `keyword_set` | STRINGA | TRUE | SÌ | Nome del set di parole chiave. |
| `is_trending` | STRINGA | TRUE | | Stato corrente di una determinata tendenza. Lo stato di tendenza è misurato come incremento dell’attività intent nell’ultima settimana rispetto alle medie delle sette settimane precedenti. |
| `intent_strength` | ENUM[STRINGA] | TRUE | | Misurazione quantificata della forza dell&#39;intento. I valori accettati includono: `HIGH`, `MED` e `LOW`. |
| `num_people_researching` | NUMERO INTERO | TRUE | | Numero di persone appartenenti a `company_id` che hanno cercato la parola chiave negli ultimi sette giorni. |
| `num_trending_days` | NUMERO INTERO | TRUE | | Il numero di giorni di tendenza della parola chiave in una determinata durata. |
| `trending_score` | NUMERO INTERO | TRUE | | Punteggio di tendenza. |
| `record_id` | STRINGA | TRUE | | ID univoco del record primario. |
| `partition_date` | DATA | TRUE | | Data di calendario dello snapshot. Questa operazione viene eseguita settimanalmente, alla fine della settimana. |

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
