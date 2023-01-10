---
keywords: Experience Platform;home;argomenti popolari;Zoho CRM;zoho crm;Zoho;zoho;zoho
solution: Experience Platform
title: Panoramica del connettore di origine di Zoho CRM
description: Scopri come collegare Zoho CRM a Adobe Experience Platform utilizzando API o l’interfaccia utente.
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# [!DNL Zoho CRM]

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo utilizzando [!DNL Platform] servizi. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

Experience Platform fornisce il supporto per l’acquisizione di dati da un sistema CRM di terze parti. Il supporto per i provider di gestione delle relazioni con i clienti include [!DNL Zoho CRM].

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori sorgente, è necessario aggiungere a un elenco consentiti un elenco di indirizzi IP. Se l’utente non aggiunge all’elenco consentiti gli indirizzi IP specifici per l’area geografica, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l’utilizzo delle origini. Consulta la sezione [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

## Recupera le credenziali di autenticazione per [!DNL Zoho CRM]

Prima di poter raccogliere i dati dal tuo [!DNL Zoho CRM] account a Platform, devi prima recuperare le credenziali per autenticare il tuo [!DNL Zoho CRM] sorgente. Segui i passaggi riportati di seguito per recuperare l’ID client, il segreto client, il token di accesso e il token di aggiornamento.

### Registra la tua applicazione

Il primo passo per recuperare le credenziali di autenticazione è quello di registrare l&#39;applicazione utilizzando [[!DNL Zoho CRM] console per sviluppatori](https://accounts.zoho.com/). Per registrare l&#39;applicazione, è necessario selezionare il tipo di client da: Java Script, web-based, mobile, applicazioni mobili non basate su browser o self-client. Quindi, fornisci i valori per il nome dell&#39;applicazione, l&#39;URL della pagina web e un URI di reindirizzamento autorizzato che [!DNL Zoho CRM] può quindi utilizzare per reindirizzarti con un token di sovvenzione.

Una registrazione corretta restituisce l&#39;ID client e il segreto client.

### Creare una richiesta di autorizzazione

Successivamente, devi creare un [richiesta di autorizzazione](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) utilizzando un&#39;applicazione basata sul web o un self-client. La richiesta di autorizzazione restituisce il token di sovvenzione, che a sua volta consente di recuperare il token di accesso.

Quando crei una richiesta di autorizzazione, devi compilare i valori per entrambi **ambiti** e **tipo di accesso**. Fai riferimento a questo [[!DNL Zoho CRM] documento](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html) per ulteriori informazioni sugli ambiti, mentre **tipo di accesso** deve essere sempre impostato su `offline`.

### Generare i token di accesso e aggiornamento

Una volta recuperato il token di sovvenzione, puoi generare il [token di accesso e aggiornamento](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) effettuando una richiesta di POST a `{ACCOUNTS_URL}/oauth/v2/token` fornendo l&#39;ID client, il segreto client, il token di concessione e l&#39;URI di reindirizzamento. Durante questo passaggio, devi anche includere `grant_type` come parametro e imposta il valore come `"authorization_code"`.

Una richiesta corretta restituisce i token di accesso e aggiornamento, che puoi quindi utilizzare per l’autenticazione.

Per i passaggi dettagliati sull&#39;acquisizione delle credenziali, consulta la sezione [[!DNL Zoho CRM] guida all’autenticazione](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Connetti [!DNL Zoho CRM] a [!DNL Platform] utilizzo delle API

La documentazione seguente fornisce informazioni su come connettersi [!DNL Zoho CRM] su Platform utilizzando le API o l’interfaccia utente:

- [Crea un [!DNL Zoho CRM] connessione di base tramite l’API del servizio di flusso](../../tutorials/api/create/crm/zoho.md)
- [Esplorare le tabelle di dati utilizzando l’API del servizio di flusso](../../tutorials/api/explore/tabular.md)
- [Creare un flusso di dati per un’origine CRM utilizzando l’API del servizio di flusso](../../tutorials/api/collect/crm.md)

## Connetti [!DNL Zoho CRM] a [!DNL Platform] utilizzo dell’interfaccia

- [Crea un [!DNL Zoho CRM] connessione sorgente nell’interfaccia utente](../../tutorials/ui/create/crm/zoho.md)
- [Creare un flusso di dati per una connessione sorgente CRM nell&#39;interfaccia utente](../../tutorials/ui/dataflow/crm.md)
