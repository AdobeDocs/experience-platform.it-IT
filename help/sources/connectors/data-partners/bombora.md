---
title: Intento Bombora
description: Scopri la fonte dell’Intento di Bombora su Experience Platform.
last-substantial-update: 2025-03-26T00:00:00Z
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="Edizione B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
exl-id: d2e81207-8ef5-4e52-bbac-a2fa262d8d08
source-git-commit: 8a5fdcfcf503df1b9d5aa338ff530181a2d03b5d
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 1%

---

# [!DNL Bombora Intent]

[!DNL Bombora] è una soluzione di pubblico completa specializzata nei dati intento B2B. [!DNL Bombora Intent] è un&#39;origine Adobe Experience Platform che puoi utilizzare per collegare il tuo account [!DNL Bombora] ad Experience Platform e integrare i dati di intento dell&#39;account.

Con l&#39;origine [!DNL Bombora Intent], è possibile integrare i dati di intento di sovraccarico dell&#39;azienda [!DNL Bombora's] per identificare gli account che ricercano attivamente i propri prodotti o servizi. Utilizza [!DNL Bombora] per assegnare la priorità agli account sul mercato, per creare segmenti precisi ed eseguire campagne ABM iper-mirate, in modo che le tue attività di marketing si concentrino sugli account che hanno più probabilità di essere convertiti. Inoltre, puoi sfruttare le strategie basate sulle finalità per ottimizzare la spesa pubblicitaria, aumentare il coinvolgimento e massimizzare il ROI.

Per informazioni sui prerequisiti nell&#39;origine [!DNL Bombora], leggere questo documento.

## Casi d’uso {#use-cases}

Leggere i seguenti esempi di casi d&#39;uso applicabili all&#39;origine [!DNL Bombora].

### Integrazione con Demand-Side Platform (DSP)

In qualità di esperto di marketing B2B, puoi creare un elenco di account in Real-Time CDP, identificare aziende che mostrano un intento elevato per i tuoi prodotti, quindi attivare questo elenco in [!DNL Bombora], che si integra direttamente con le DSP, consentendo di eseguire campagne pubblicitarie programmatiche mirate utilizzando i dati di [!DNL Bombora's]. In questo modo la spesa pubblicitaria si concentra sulle aziende che hanno più probabilità di convertire.

### Funzionalità Account-Based Marketing (ABM)

In qualità di esperto di marketing B2B, puoi creare un elenco di account basato su segnali di intento di prime e terze parti. Puoi quindi attivare questo elenco in [!DNL Bombora], dove le funzionalità ABM consentono di rivolgerti specificamente ai dipendenti di questi account, garantendo che gli annunci raggiungano i responsabili delle decisioni anziché un pubblico ampio.

### Attivazione ABM multicanale

In qualità di esperto di marketing B2B, puoi creare un elenco di account in Real-Time CDP, identificando le aziende con intento elevato e attivarlo in [!DNL Bombora] per eseguire campagne mirate su più canali. Sui social media a pagamento, puoi distribuire annunci personalizzati ai professionisti negli account di destinazione su piattaforme come [!DNL Linkedin] e [!DNL Facebook].

Utilizzando piattaforme di annunci native, puoi assicurarti che i contenuti raggiungano i responsabili decisionali in contesti rilevanti. Puoi anche estendere le campagne alla TV avanzata, distribuendo annunci agli account chiave. Questo approccio multicanale garantisce la coerenza dei messaggi tra le piattaforme, massimizzando i tassi di coinvolgimento e conversione.

## Prerequisiti {#prerequisites}

Leggere le sezioni seguenti per i passaggi preliminari prima di connettere [!DNL Bombora] ad Experience Platform.

### Indirizzo IP inserisco nell&#39;elenco Consentiti

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un inserisco nell&#39;elenco Consentiti di. La mancata aggiunta di indirizzi IP specifici per l’area geografica al elenco Consentiti può causare errori o non prestazioni durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [Indirizzo IP/inserisco nell&#39;elenco Consentiti di](../../ip-address-allow-list.md).

### Configurare le autorizzazioni su Experience Platform

Per connettere l&#39;account **[!UICONTROL ad Experience Platform, è necessario che per l&#39;account siano abilitate le autorizzazioni]** Visualizza origini **[!UICONTROL e]** Gestisci origini[!DNL Bombora]. Contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie. Per ulteriori informazioni, leggere la [guida all&#39;interfaccia utente per il controllo degli accessi](../../../access-control/abac/ui/permissions.md).

### Vincoli di denominazione per file e directory

Quando si assegna un nome al file o alla directory di archiviazione cloud, è necessario tenere presenti le restrizioni elencate di seguito:

* I nomi dei componenti di directory e file non possono superare i 255 caratteri.
* I nomi di file e directory non possono terminare con una barra (`/`). Se fornito, verrà rimosso automaticamente.
* I seguenti caratteri URL riservati devono essere correttamente preceduti dall&#39;escape: `! ' ( ) ; @ & = + $ , % # [ ]`
* I seguenti caratteri non sono consentiti: `" \ / : | < > * ?`.
* Non sono consentiti caratteri di percorso URL non validi. I punti di codice come `\uE000`, sebbene validi nei nomi di file NTFS, non sono caratteri Unicode validi. Inoltre, alcuni caratteri ASCII o Unicode, come i caratteri di controllo (da 0x00 a 0x1F, \u0081, ecc.), non sono consentiti. Per le regole che regolano le stringhe Unicode in HTTP/1.1, vedere [RFC 2616, Sezione 2.2: Regole di base](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
* Non sono consentiti i seguenti nomi di file: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carattere punto (.) e due caratteri punto (..).

### Raccogli le credenziali richieste

[!DNL Bombora] su Experience Platform è ospitato da [!DNL Google Cloud Storage]. Per autenticare correttamente l&#39;account [!DNL Bombora], è necessario fornire i valori appropriati per le credenziali seguenti:

| Credenziali | Descrizione |
| --- | --- |
| ID chiave di accesso | ID della chiave di accesso [!DNL Bombora]. Si tratta di una stringa alfanumerica di 61 caratteri necessaria per autenticare l’account in Experience Platform. |
| Chiave di accesso segreta | Chiave di accesso segreta [!DNL Bombora]. Si tratta di una stringa con codifica base 64 di 40 caratteri necessaria per autenticare l’account in Experience Platform. |
| Nome del bucket | Il bucket [!DNL Bombora] da cui verranno estratti i dati. |

Per ulteriori informazioni su queste credenziali, leggere la [[!DNL Google Cloud Storage] Guida delle chiavi HMAC](https://cloud.google.com/storage/docs/authentication/hmackeys#overview). Per i passaggi su come generare la propria chiave di accesso, leggere la [guida ai prerequisiti nella [!DNL Google Cloud Storage] panoramica origine](../cloud-storage/google-cloud-storage.md#prerequisite-setup-for-connecting-your-google-cloud-storage-account).

## Schema [!DNL Bombora] {#schema}

Leggere questa sezione per informazioni sullo schema [!DNL Bombora] e sulla struttura dei dati.

Lo schema [!DNL Bombora] è denominato **Intento account Bombora B2B**. Si tratta di informazioni di intento settimanali (ricerca di acquirenti B2B anonimi e consumo di contenuti) su account e argomenti specifici. I dati sono in formato parquet.

* Classe - XDM [!DNL Bombora Account Intent]
* Spazio dei nomi - B2B [!DNL Bombora Account Intent]
* Identità primaria - `intentID`
* Relazioni - Account B2B

| Nome campo | Tipo di dati | Descrizione |
|------------------------|-----------|----------------------------------------------------------------------------------------|
| `extSourceSystemAudit` | OGGETTO | Questo campo viene utilizzato dal sistema per il controllo del sistema di origine. |
| `_id` | STRINGA | Questo campo viene utilizzato dal sistema come identificatore univoco. |
| `accountDomain` | STRINGA | Questo campo contiene il dominio dell’account. |
| `accountID` | STRINGA | Questo campo contiene l’ID account B2B a cui è associato questo record intento. |
| `bomboraAccountName` | STRINGA | Questo campo contiene l&#39;ID azienda di Bombora. |
| `clusterID` | STRINGA | Questo campo contiene l&#39;ID cluster. |
| `clusterName` | STRINGA | Questo campo contiene il nome del cluster. |
| `compositeScore` | NUMERO INTERO | Questo campo contiene il punteggio composito dell’intento. |
| `intentID` | STRINGA | Questo campo contiene un valore univoco generato dal sistema. |
| `partitionDate` | DATA | Questo campo contiene la data di partizione. Questa operazione viene eseguita settimanalmente, alla fine della settimana, nel formato `mm/dd/yyyy`. |
| `topicID` | STRINGA | Questo campo contiene l&#39;ID argomento intento di Bombora. |
| `topicName` | STRINGA | Questo campo contiene il nome dell&#39;argomento intento di Bombora. |

{style="table-layout:auto"}

>[!TIP]
>
>Eventuali modifiche allo schema vengono comunicate in anticipo ad Adobe. Per supportare un’evoluzione dello schema fluida, è essenziale mantenere la compatibilità con le versioni precedenti. Experience Platform applica un approccio di controllo delle versioni di sola aggiunta, garantendo che gli aggiornamenti allo schema non siano distruttivi. Ciò significa che le modifiche che causano interruzioni sono severamente vietate e sono consentite solo le modifiche che migliorano o estendono lo schema esistente.

## Connetti il tuo account [!DNL Bombora] ad Experience Platform nell&#39;interfaccia utente

Dopo aver completato la configurazione dei prerequisiti, leggi l&#39;esercitazione su [connessione dell&#39;account [!DNL Bombora] ad Experience Platform](../../tutorials/ui/create/data-partners/bombora.md) per avviare l&#39;integrazione.

## Domande frequenti {#faq}

Leggere questa sezione per le risposte alle domande frequenti relative all&#39;origine [!DNL Bombora].

### È necessario disporre di un contratto esistente con [!DNL Bombora] per utilizzare i dati di intento dell&#39;account in Real-Time CDP B2B edition?

+++Risposta

Sì, è necessario disporre di un contratto attivo con [!DNL Bombora] per accedere e utilizzare i dati di intento in Experience Platform e Real-Time CDP B2B edition. L&#39;integrazione sfrutta il contratto esistente con [!DNL Bombora] per acquisire e attivare i segnali di intento dell&#39;account in Experience Platform e Real-Time CDP.

+++

### I campi personalizzati di [!DNL Bombora] sono supportati in questa integrazione?

+++Risposta

Al momento, è possibile utilizzare solo i campi standard [!DNL Bombora] per l&#39;acquisizione e l&#39;attivazione. Per visualizzare l&#39;elenco dei campi supportati, leggere la [[!DNL Bombora] guida allo schema](#schema) per i dettagli sulla disponibilità dei campi.

+++

### È possibile acquisire dati da [!DNL Bombora] ad Experience Platform su base ad hoc?

+++Risposta

Sì, è possibile acquisire dati da [!DNL Bombora] su base ad hoc. Puoi creare un nuovo flusso di dati per acquisire i dati di intento più recenti, purché siano presenti nuovi dati da [!DNL Bombora]. Tuttavia, puoi avere un solo flusso di dati attivo alla volta. Assicurati quindi di eliminare il flusso di dati esistente, prima di crearne uno nuovo.

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

### Quale campo viene utilizzato per associare gli account da [!DNL Bombora] ad Experience Platform?

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

I dati sulle finalità possono essere utilizzati in [Tipi di pubblico dell&#39;account](../../../segmentation/types/account-audiences.md) per migliorare il targeting, la segmentazione e la personalizzazione. Sfruttando i segnali di intento, le aziende possono identificare e interagire con gli account che mostrano un elevato interesse per argomenti specifici, ottimizzando il marketing e la portata delle vendite.

+++
