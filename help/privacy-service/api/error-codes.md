---
title: Codici di errore Privacy Service in Adobe Experience Platform
description: Comprendi i codici di errore di Privacy Service in modo da poter diagnosticare gli errori, gestire i risultati dei processi a livello di programmazione e determinare i passaggi successivi durante l’invio o il monitoraggio dei processi relativi alla privacy.
keywords: servizio di privacy, codici di errore, processi di privacy, errori api
solution: Experience Platform
source-git-commit: a312dabf5b8c3b52af31e2e127cd4bbeb8dd0021
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 4%

---

# Codici di errore Privacy Service {#privacy-service-error-codes}

Utilizzare questo riferimento per identificare i risultati dei processi di Privacy Service, diagnosticare gli errori e determinare i passaggi successivi appropriati durante l&#39;invio o il monitoraggio dei processi relativi alla privacy in **Adobe Experience Platform**. Per informazioni su come creare, inviare e monitorare i processi relativi alla privacy, consulta la [guida dell&#39;endpoint per i processi relativi alla privacy](./privacy-jobs.md) o la [guida utente dell&#39;interfaccia utente di Privacy Service](../ui/user-guide.md).

I codici di errore Privacy Service sono un contratto pubblico stabile. Ogni codice di errore identifica in modo univoco uno stato di errore o completamento su cui puoi fare affidamento per la gestione programmatica e i flussi di lavoro operativi.

Durante la creazione di flussi di lavoro di automazione o monitoraggio si applicano le seguenti garanzie:

* I codici di errore sono stabili dopo la pubblicazione.
* I messaggi di errore possono cambiare per migliorare la chiarezza, ma il valore del codice no.
* Con il passare del tempo è possibile aggiungere nuovi codici di errore, mentre quelli esistenti non vengono riutilizzati.

Utilizza i codici di errore, non il testo del messaggio, per implementare l’automazione o la logica decisionale. Per informazioni sull&#39;elaborazione efficiente dei processi relativi alla privacy, sul monitoraggio dello stato dei processi e sulla gestione degli errori senza affidarsi al polling o alle stringhe di messaggi, consulta [Best practice per Privacy Service](../best-practices.md).

## Formato della risposta di errore {#error-response-format}

Privacy Service restituisce informazioni di errore nelle risposte ai processi e alle richieste. La risposta include un codice di errore numerico e un messaggio leggibile dal mittente nel payload di risposta.

Il codice di errore trasmette il risultato autorevole. Il messaggio fornisce ulteriore contesto per la risoluzione dei problemi.

Questo documento descrive il significato e l’intento di ciascun codice di errore. Per gli schemi di risposta a livello di campo e i dettagli della richiesta, consulta la [documentazione API di Privacy Service](https://developer.adobe.com/experience-platform-apis/references/privacy-service/).

## Domini di errore {#error-domains}

I codici di errore sono raggruppati per dominio funzionale per consentire una diagnosi più rapida dei problemi.

I domini utilizzati in questo documento includono:

* **Convalida richiesta**: la richiesta non è valida o contiene valori non validi. Per informazioni sulla struttura delle richieste e i requisiti di convalida, consulta la [guida dell&#39;endpoint &quot;privacy jobs&quot;](./privacy-jobs.md).
* **Autorizzazione e provisioning**: l&#39;organizzazione o l&#39;utente non dispone dell&#39;accesso richiesto. Consulta [gestire le autorizzazioni](../permissions.md) per rivedere i requisiti delle autorizzazioni basati su ruoli.
* **Identità e applicabilità**: gli identificatori o gli spazi dei nomi non sono applicabili alla richiesta. Per informazioni sui tipi di identità e i requisiti dello spazio dei nomi supportati, consulta [dati di identità per le richieste di privacy](../identity-data.md).
* **Limitazione di frequenza**: il volume di invio supera i limiti della piattaforma. In questo caso, riduci il tasso di invio e riprova.
* **Accesso ai dati ed elaborazione**: il sistema non è in grado di accedere ai dati richiesti o di elaborarli. Consulta la [guida alla risoluzione dei problemi](../troubleshooting-guide.md) per le cause comuni e i passaggi di correzione.
* **Crittografia e gestione chiavi**: le chiavi di crittografia necessarie non sono disponibili. Consulta [Chiavi gestite dal cliente](../../landing/governance-privacy-security/customer-managed-keys/overview.md) per le linee guida per l&#39;accesso, la configurazione e il ripristino delle chiavi.
* **Stato esecuzione processo**: processo completato completamente, parzialmente o con errori. Per le descrizioni delle categorie di stato dei processi e il loro significato, consulta la [guida dell&#39;endpoint &quot;privacy jobs&quot;](./privacy-jobs.md#status-categories).

>[!NOTE]
>
>Le assegnazioni del dominio riflettono l’intento del codice di errore, non i limiti del servizio interno.

## Riferimento codice di errore {#error-code-reference}

Nella tabella seguente sono elencati tutti i codici di errore Privacy Service pubblici.

| Codice errore | Stato HTTP | Titolo | Descrizione |
| ---------- | ----------- | ----------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------| 
| 1000 — 400 | 400 | Errore di formattazione | Uno o più valori di dati per l’applicazione specificata presentano problemi di formattazione. Per ulteriori informazioni, consulta i dettagli del processo. |
| 1001 — 400 | 400 | Non autorizzato | Non è stato eseguito il provisioning della tua organizzazione. Contatta l’amministratore per ulteriori informazioni. |
| 1010 - 400 | 400 | Autorizzazioni mancanti | Non disponi delle autorizzazioni necessarie per eseguire questa azione. Contatta l’amministratore per richiedere l’accesso. |
| 1020 — 400 | 400 | Caricamento e archiviazione non riusciti | Si è verificato un problema durante il caricamento e l’archiviazione dei dati di accesso. Carica i dati di accesso e riprova. |
| 1021 — 400 | 400 | Errore di processo | Uno o più processi di privacy creati dalla richiesta non sono riusciti. Per ulteriori informazioni, esaminare i dettagli dei processi non riusciti. |
| 1022 - 400 | 400 | Accesso ai dati non riuscito | Si è verificato un problema durante l&#39;accesso ai dati specificati. Rivedi i dettagli del processo per ulteriori informazioni. |
| 1023 - 400 | 400 | Accesso ai dati non riuscito | Si è verificato un problema durante l’accesso o l’individuazione degli ID dei set di dati specificati. Verifica che gli ID forniti siano validi, quindi riprova. |
| 1024 - 400 | 400 | Errore imprevisto | Errore imprevisto. Rivedi i dettagli del processo per ulteriori informazioni. |
| 1030 - 400 | 400 | Limite di frequenza documenti superato | Il carico di lavoro ha superato il limite di frequenza dei documenti. Riduci la frequenza di invio, quindi riprova. |
| 1040 - 400 | 400 | Errore di accesso alla crittografia della chiave | Impossibile elaborare i dati perché l&#39;archivio dati è crittografato e l&#39;accesso alle chiavi è stato revocato. Contatta l’amministratore di Key Vault per ripristinare l’accesso alla chiave del cliente. |
| 6000 — 200 | 200 | Completato | Processo completato correttamente. Rivedi i dettagli del processo per confermare i record e i risultati elaborati. |
| 6051 — 200 | 200 | Provisioning non eseguito | Non è stato eseguito il provisioning della tua organizzazione per l’applicazione richiesta. La richiesta non è applicabile. |
| 6052 — 200 | 200 | ID utente non trovati | Alcuni ID utente non sono stati trovati e gli ID utente sconosciuti non sono applicabili a questo prodotto. Verifica che gli ID utente siano validi, quindi riprova. |
| 6053 — 200 | 200 | Spazio dei nomi non valido | Lo spazio dei nomi identità fornito non è valido per questa applicazione. Utilizza uno spazio dei nomi riconosciuto dal sistema. |
| 6054 - 200 | 200 | Parzialmente completato | Processo completato per i dati applicabili, ma alcuni dati non erano applicabili alla richiesta. Rivedi i dettagli del processo per ulteriori informazioni. |

{style="table-layout:auto"}
