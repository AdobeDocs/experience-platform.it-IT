---
title: Indirizzo IP in fase di Inserire nell'elenco Consentiti per l’API Streaming Ingestion
description: Scopri come proteggere l’accesso all’API Streaming Ingestion consentendo solo indirizzi IP specifici tramite l’inserisce nell'elenco Consentiti di. Questa guida spiega come impostare, abilitare e gestire le restrizioni basate su indirizzi IP per la sicurezza API.
hide: true
hidefromtoc: true
badge: beta
source-git-commit: f1d851afae5ad271e3c7d9d887f614058a262874
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# INSERIRE NELL&#39;ELENCO CONSENTITI dell’indirizzo IP in attesa dell’API Streaming Ingestion

>[!AVAILABILITY]
>
>Il supporto per l’indirizzo IP da inserire nell&#39;elenco Consentiti per l’API Streaming Ingestion è disponibile in versione beta e la tua organizzazione potrebbe non averne ancora accesso. La funzionalità e la documentazione sono soggette a modifiche.

Inserire nell&#39;elenco Consentiti Ora puoi gli indirizzi IP per l’API Streaming Ingestion. Utilizza questa funzione per proteggere gli endpoint di acquisizione limitando l’accesso solo agli indirizzi IP specificati.

## Funzionamento della inserire nell&#39;elenco Consentiti dell’indirizzo IP

La funzione di inserire nell&#39;elenco Consentiti IP funziona come segue:

1. **Invia indirizzi IP:** Fornisci un elenco di indirizzi IP attendibili, mappati alle tue sandbox.
2. **Configurazione:** Adobe configura il inserisco nell&#39;elenco Consentiti di a livello di organizzazione e sandbox per la tua organizzazione.
3. **Imposizione:** Le richieste in arrivo vengono valutate in base al inserisco nell&#39;elenco Consentiti di fornito:
   * Se l’indirizzo IP corrisponde al inserisco nell&#39;elenco Consentiti di, la richiesta viene elaborata normalmente.
   * Se l’indirizzo IP non si trova nel inserisco nell&#39;elenco Consentiti di, la richiesta viene bloccata e viene ricevuto un errore HTTP 403 senza corpo di risposta.

## Considerazioni chiave

* La funzionalità di inserire nell&#39;elenco Consentiti dell&#39;indirizzo IP si applica solo all&#39;API [Streaming Ingestion](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) (`dcs.adobedc.net`) e **not** si applica a `server.adobedc.net` o `edge.adobedc.net`.
* Le nuove sandbox sono aperte per impostazione predefinita fino a quando non viene abilitata l’opzione di inserire nell&#39;elenco Consentiti di un’istanza di.
* Se si rimuove una sandbox dal inserisco nell&#39;elenco Consentiti di, questa verrà riaperta su Internet.
* Devi mantenere l’elenco completo delle mappature sandbox-indirizzo IP sul tuo lato e inviare sempre l’elenco completo nel modulo di inserire nell&#39;elenco Consentiti dell’indirizzo IP. Gli aggiornamenti incrementali non sono supportati.

## Abilita inserire nell&#39;elenco Consentiti indirizzo IP

Per abilitare l’indirizzo IP alla inserisce nell&#39;elenco Consentiti per la tua organizzazione, segui la procedura riportata di seguito:

1. Scarica e completa il modulo di inserisce nell&#39;elenco Consentiti dell&#39;indirizzo IP [](../images/assets/ip_allowlisting_aep.xlsx.zip).
2. Apri un ticket di supporto e crea un file con l&#39;oggetto **AEP DCS &amp; Streaming Ingestion - IP richiesta di Inserire nell&#39;elenco Consentiti**. Allega il modulo compilato a questo ticket.
3. Dopo aver inviato il ticket, l’Assistenza clienti di Adobe inoltrerà la richiesta al team di progettazione.
4. Gli ingegneri abilitano la inserire nell&#39;elenco Consentiti dell&#39;e confermano l&#39;installazione.
5. Quindi, convalida l’accesso e conferma l’utilizzo del ticket di supporto.

| Organizzazione | Nome sandbox | Indirizzi IP consentiti |
| --- | --- | --- |
| ACME | Prod | 203.0.113.42, 198.51.100.25, 192.0.2.10 |
| ACME | Dev | 203.0.113.43, 198.51.100.26, 192.0.2.11 |
| LUMA | Prod | 203.0.113.46, 198.51.100.29, 192.0.2.14 |

## Domande frequenti

Di seguito sono riportate le risposte alle domande più frequenti sull’indirizzo IP in attesa di inserire nell&#39;elenco Consentiti per l’API Streaming Ingestion.

### Quali API sono coperte?

Solo gli endpoint dell&#39;API Streaming Ingestion `dcs.adobedc.net`.

## Cosa succede se la mia richiesta proviene da un indirizzo IP non elencato?

È bloccato con un errore HTTP 403.

### Le nuove sandbox sono protette automaticamente?

No. Sono aperti fino a quando non fornisci mappature di indirizzi IP tramite il modulo di inserire nell&#39;elenco Consentiti di.

### Posso inviare solo indirizzi IP aggiornati quando il mio inserisce nell&#39;elenco Consentiti modifiche?

No. Devi sempre inviare l’elenco completo delle mappature sandbox e indirizzi IP. Non sono accettati aggiornamenti parziali (incrementali).