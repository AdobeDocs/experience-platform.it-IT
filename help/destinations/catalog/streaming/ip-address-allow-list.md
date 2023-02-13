---
keywords: Indirizzo IP, intervallo IP, destinazioni di elenco consentiti, inserire nell'elenco Consentiti, destinazioni di streaming inserire nell'elenco Consentiti
title: inserire nell'elenco Consentiti dell’indirizzo IP per le destinazioni di streaming
type: Documentation
description: Questa pagina fornisce intervalli IP che è possibile aggiungere all’elenco consentiti per esportare in modo sicuro i dati dall’Experience Platform all’endpoint API REST HTTP, all’istanza Kinesis Amazon o Hubs evento di Azure.
exl-id: f41303bd-c886-4c67-9e39-21efc3f5b768
source-git-commit: 4d71e246c8ce92cbdae4d248568cf32ab44ac82a
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# inserire nell&#39;elenco Consentiti dell’indirizzo IP per le destinazioni di streaming {#ip-address-allowlist}

>[!IMPORTANT]
>
> * Adobe consiglia di aggiungere un segnalibro a questa pagina e di rivisitarla ogni tre mesi per verificare la presenza degli indirizzi IP più recenti. Adobe non fornisce notifiche sui nuovi intervalli IP.
> * Elenco degli IP documentati qui *non* applica a tutte le destinazioni create utilizzando [[!DNL Destination SDK]](/help/destinations/destination-sdk/overview.md).


## Panoramica {#overview}

Gli intervalli IP qui documentati si applicano alle seguenti destinazioni:

* [Destinazione API HTTP](./http-destination.md)
* [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)

Il traffico in uscita dall’Experience Platform a queste destinazioni passa sempre attraverso gli IP elencati in questa pagina.

Questa pagina fornisce intervalli IP che puoi aggiungere al tuo inserire nell&#39;elenco Consentiti, per esportare in modo sicuro i dati dall’Experience Platform all’endpoint HTTP, [!DNL Amazon Kinesis]oppure [!DNL Azure Event Hubs] istanza. Questa funzionalità è particolarmente utile se l’endpoint HTTP si trova dietro un firewall aziendale o se gli standard di sicurezza e conformità aziendali richiedono la inserisce nell&#39;elenco Consentiti di un elenco di intervalli IP.

È possibile definire controlli di accesso alla rete tramite il firewall di rete. Specificando l’intervallo IP appropriato, puoi consentire il traffico per il servizio di trasferimento dati.

Adobe consiglia di aggiungere i seguenti intervalli IP a un inserire nell&#39;elenco Consentiti prima di lavorare con le destinazioni sopra menzionate in questa pagina. Se non aggiungi l’intervallo IP specifico per l’area geografica al tuo inserire nell&#39;elenco Consentiti, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l’utilizzo di queste destinazioni di streaming.

## VA7: Clienti USA e America {#us-americas}

`20.186.185.239`
`40.70.154.136/29`
`52.254.106.160/28`
`52.254.106.176/28`
`52.254.105.192/28`
`20.186.185.181`
`52.254.107.64/28`
`52.254.107.80/28`
`52.254.106.144/28`
`52.254.106.0/28`
`52.254.107.16/28`
`52.254.107.32/28`
`52.254.106.224/28`
`20.186.185.227`
`52.254.106.192/28`
`52.254.107.128/28`
`52.254.106.208/28`
`52.254.106.240/28`
`52.254.107.0/28`
`52.254.107.144/28`

## NLD2: Clienti EMEA {#emea}

`40.74.4.160/28`
`40.74.6.128/28`
`40.74.7.128/28`
`40.74.4.176/28`
`51.144.184.248/29`
`40.74.7.208/28`
`52.142.236.87`
`20.50.23.153`
`20.101.246.9`
`40.74.4.144/28`
`40.74.7.160/28`
`40.74.3.176/28`
`40.74.6.144/28`
`40.74.6.80/28`
`40.74.5.128/28`
`40.74.7.144/28`
`40.74.7.176/28`
`40.74.6.96/28`
`40.74.6.112/28`
`51.105.144.1`
`40.74.7.192/28`
`51.105.144.81`
`51.124.70.4`

## AUS5: Clienti APAC {#apac}

`20.43.104.80/28`
`20.43.104.16/28`
`20.43.104.128/28`
`20.40.188.166`
`20.40.191.224/28`
`20.43.104.176/28`
`20.43.104.0/28`
`20.43.105.0/28`
`20.43.105.48/28`
`20.40.191.240/28`
`20.43.104.192/28`
`20.40.188.227`
`20.40.188.194`
`20.43.104.144/28`
`20.43.104.160/28`
`20.43.104.96/28`
`20.43.105.32/28`
`20.43.104.112/28`
`20.43.105.16/28`
`20.43.104.48/28`
`20.40.191.96/28`
`20.43.104.32/28`
`20.43.104.64/28`