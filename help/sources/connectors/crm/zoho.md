---
keywords: Experience Platform;home;argomenti popolari;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Panoramica del connettore Source di Zoho CRM
description: Scopri come collegare Zoho CRM a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: 0781d04af12c4c11dfc917adfdec8673cf3be8de
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# [!DNL Zoho CRM]

>[!IMPORTANT]
>
>L&#39;origine [!DNL Zoho CRM] diventerà obsoleta alla fine di giugno 2025. È possibile utilizzare [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md) al posto dell&#39;origine [!DNL Zoho CRM].

Adobe Experience Platform consente di acquisire dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi [!DNL Platform]. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da un sistema CRM di terze parti. Il supporto per i provider di gestione delle relazioni con i clienti include [!DNL Zoho CRM].

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md).

## Recupera le credenziali di autenticazione per [!DNL Zoho CRM]

Prima di poter trasferire i dati dall&#39;account [!DNL Zoho CRM] a Platform, è necessario recuperare le credenziali per autenticare l&#39;origine [!DNL Zoho CRM]. Segui i passaggi seguenti per recuperare l’ID client, il segreto client, il token di accesso e il token di aggiornamento.

### Registrare l&#39;applicazione

Il primo passaggio per recuperare le credenziali di autenticazione consiste nel registrare l&#39;applicazione utilizzando [[!DNL Zoho CRM] Developer Console](https://accounts.zoho.com/). Per registrare l’applicazione, devi selezionare il tipo di client tra: Java Script, basato su Web, mobile, applicazioni mobili non basate su browser o self-client. Fornire quindi i valori per il nome dell&#39;applicazione, l&#39;URL della pagina Web e un URI di reindirizzamento autorizzato che [!DNL Zoho CRM] può utilizzare per reindirizzarti con un token di concessione.

In caso di esito positivo, la registrazione restituisce l’ID client e il segreto client.

### Creare una richiesta di autorizzazione

Successivamente, è necessario creare una [richiesta di autorizzazione](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) utilizzando un&#39;applicazione basata sul Web o un client autonomo. La richiesta di autorizzazione restituisce il token di concessione, che a sua volta ti consente di recuperare il token di accesso.

Durante la creazione di una richiesta di autorizzazione, è necessario compilare i valori per entrambi gli ambiti **ambiti** e **tipo di accesso**. Fare riferimento a questo [[!DNL Zoho CRM] documento](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html) per ulteriori informazioni sugli ambiti, mentre il **tipo di accesso** deve essere sempre impostato su `offline`.

### Generare i token di accesso e aggiornamento

Dopo aver recuperato il token di concessione, puoi generare i [token di accesso e aggiornamento](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) effettuando una richiesta POST a `{ACCOUNTS_URL}/oauth/v2/token` e fornendo al contempo l&#39;ID client, il segreto client, il token di concessione e l&#39;URI di reindirizzamento. Durante questo passaggio, è necessario includere `grant_type` come parametro e impostare il valore come `"authorization_code"`.

In caso di esito positivo, la richiesta restituisce i token di accesso e di aggiornamento, che puoi quindi utilizzare per l’autenticazione.

Per i passaggi dettagliati sull&#39;acquisizione delle credenziali, consulta la [[!DNL Zoho CRM] guida all&#39;autenticazione](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Connetti [!DNL Zoho CRM] a [!DNL Platform] tramite API

La documentazione seguente fornisce informazioni su come connettere [!DNL Zoho CRM] a Platform tramite API o tramite l&#39;interfaccia utente:

- [Crea una connessione di base  [!DNL Zoho CRM]  utilizzando l&#39;API del servizio Flusso](../../tutorials/api/create/crm/zoho.md)
- [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
- [Creare un flusso di dati per un’origine CRM utilizzando l’API del servizio Flusso](../../tutorials/api/collect/crm.md)

## Connetti [!DNL Zoho CRM] a [!DNL Platform] tramite l&#39;interfaccia utente

- [Crea una connessione di origine  [!DNL Zoho CRM]  nell&#39;interfaccia utente](../../tutorials/ui/create/crm/zoho.md)
- [Creare un flusso di dati per una connessione di origine CRM nell’interfaccia utente](../../tutorials/ui/dataflow/crm.md)
