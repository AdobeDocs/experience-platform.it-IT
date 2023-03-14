---
keywords: Experience Platform;home;argomenti popolari;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Panoramica del connettore di origine di Zoho CRM
description: Scopri come collegare Zoho CRM a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# [!DNL Zoho CRM]

Adobe Experience Platform consente di acquisire dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite [!DNL Platform] servizi. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da un sistema CRM di terze parti. Il supporto per i provider CRM include [!DNL Zoho CRM].

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Consulta la [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

## Recupera le credenziali di autenticazione per [!DNL Zoho CRM]

Prima di poter importare i dati dal [!DNL Zoho CRM] a Platform, devi prima recuperare le credenziali per autenticare il tuo [!DNL Zoho CRM] sorgente. Segui i passaggi seguenti per recuperare l’ID client, il segreto client, il token di accesso e il token di aggiornamento.

### Registrare l&#39;applicazione

Il primo passaggio per recuperare le credenziali di autenticazione consiste nel registrare l’applicazione utilizzando [[!DNL Zoho CRM] console per sviluppatori](https://accounts.zoho.com/). Per registrare l’applicazione, devi selezionare il tipo di client tra: Java Script, basato su Web, mobile, applicazioni mobili non basate su browser o self-client. Quindi, fornisci i valori per il nome dell’applicazione, l’URL della pagina web e un URI di reindirizzamento autorizzato che [!DNL Zoho CRM] può quindi utilizzare per reindirizzarti con un token di concessione.

In caso di esito positivo, la registrazione restituisce l’ID client e il segreto client.

### Creare una richiesta di autorizzazione

Successivamente, devi creare un’ [richiesta di autorizzazione](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) utilizzando un&#39;applicazione basata su Web o un client autonomo. La richiesta di autorizzazione restituisce il token di concessione, che a sua volta ti consente di recuperare il token di accesso.

Quando crei una richiesta di autorizzazione, devi inserire i valori per entrambi **ambiti** e **tipo di accesso**. Fai riferimento a questo [[!DNL Zoho CRM] documento](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html) per ulteriori informazioni sugli ambiti, **tipo di accesso** deve essere sempre impostato su `offline`.

### Generare i token di accesso e aggiornamento

Dopo aver recuperato il token di concessione, puoi generare il tuo [accesso e aggiornamento dei token](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) effettuando una richiesta POST a `{ACCOUNTS_URL}/oauth/v2/token` mentre fornisci l’ID client, il segreto client, il token di concessione e l’URI di reindirizzamento. Durante questo passaggio, devi anche includere `grant_type` come parametro e impostate il valore come `"authorization_code"`.

In caso di esito positivo, la richiesta restituisce i token di accesso e di aggiornamento, che puoi quindi utilizzare per l’autenticazione.

Per informazioni dettagliate sull&#39;acquisizione delle credenziali, vedere [[!DNL Zoho CRM] guida all’autenticazione](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Connetti [!DNL Zoho CRM] a [!DNL Platform] utilizzo delle API

La documentazione seguente fornisce informazioni sulle modalità di connessione [!DNL Zoho CRM] in Platform tramite API o l’interfaccia utente:

- [Creare un [!DNL Zoho CRM] connessione di base tramite l’API del servizio Flow](../../tutorials/api/create/crm/zoho.md)
- [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
- [Creare un flusso di dati per un’origine CRM utilizzando l’API del servizio Flusso](../../tutorials/api/collect/crm.md)

## Connetti [!DNL Zoho CRM] a [!DNL Platform] utilizzo dell’interfaccia utente

- [Creare un [!DNL Zoho CRM] connessione sorgente nell’interfaccia utente](../../tutorials/ui/create/crm/zoho.md)
- [Creare un flusso di dati per una connessione di origine CRM nell’interfaccia utente](../../tutorials/ui/dataflow/crm.md)
