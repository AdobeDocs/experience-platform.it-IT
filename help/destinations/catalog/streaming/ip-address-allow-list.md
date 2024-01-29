---
keywords: Indirizzo IP, intervallo IP, destinazioni di elenco consentiti, inserisce nell'elenco Consentiti di , destinazione di streaming di, destinazione di streaming di un elenco Consentiti
title: INSERIRE NELL'ELENCO CONSENTITI Indirizzo IP per le destinazioni di streaming
type: Documentation
description: Questa pagina fornisce intervalli IP che è possibile aggiungere all’elenco consentiti per esportare in modo sicuro i dati da Experienci Platform all’endpoint API REST HTTP, all’istanza di Amazon Kinesis o all’istanza di Azure Event Hubs.
exl-id: f41303bd-c886-4c67-9e39-21efc3f5b768
source-git-commit: d4833821105433518ee30415fe08f281effa5616
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# INSERIRE NELL&#39;ELENCO CONSENTITI Indirizzo IP per le destinazioni di streaming {#ip-address-allowlist}

>[!IMPORTANT]
>
> * L’Adobe consiglia di aggiungere un segnalibro a questa pagina e di visitarla nuovamente ogni tre mesi per verificare la presenza degli indirizzi IP più recenti. L’Adobe non fornisce la notifica dei nuovi intervalli IP.
> * L’elenco degli IP qui documentato *non* applica a tutte le destinazioni create utilizzando [[!DNL Destination SDK]](/help/destinations/destination-sdk/overview.md).

## Panoramica {#overview}

Gli intervalli IP qui documentati si applicano alle seguenti destinazioni:

* [Destinazione API HTTP](./http-destination.md)
* [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md)
* [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)

Il traffico in uscita da Experienci Platform a queste destinazioni passa sempre attraverso gli IP elencati in questa pagina.

Questa pagina fornisce intervalli IP che è possibile aggiungere al inserisco nell&#39;elenco Consentiti di per esportare in modo sicuro i dati da Experienci Platform all’endpoint HTTP. [!DNL Amazon Kinesis], o [!DNL Azure Event Hubs] dell&#39;istanza. Questa funzionalità è particolarmente utile se l’endpoint HTTP si trova dietro un firewall aziendale o se gli standard di sicurezza e conformità dell’azienda richiedono la inserisce nell&#39;elenco Consentiti di un elenco di intervalli IP.

È possibile definire i controlli di accesso alla rete tramite il firewall di rete. Specificando l’intervallo IP appropriato, puoi consentire il traffico per il servizio di trasferimento dati.

L’Adobe consiglia di aggiungere i seguenti intervalli IP a un inserisco nell&#39;elenco Consentiti di prima di lavorare con le destinazioni menzionate in precedenza in questa pagina. La mancata aggiunta dell’intervallo IP specifico per la tua regione al inserisco nell&#39;elenco Consentiti di può causare errori o non prestazioni durante l’utilizzo di queste destinazioni di streaming.

## VA7: clienti USA e America {#us-americas}

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
`20.22.83.112`

## NLD2: clienti EMEA {#emea}

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
`20.101.233.128`

## AUS5: clienti APAC {#apac}

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
`20.53.206.128`
`20.227.35.177`

## CAN2: clienti Canada {#can}

`20.104.46.128/28`
`20.104.46.160/28`
`20.104.46.64/28`
`20.104.46.80/28`
`20.116.145.94`
`20.116.147.168`
`20.200.70.192/28`
`20.200.70.208/28`
`20.200.70.224/28`
`20.200.70.240/28`
`20.200.71.0/28`
`20.200.71.112/28`
`20.200.71.128/28`
`20.200.71.144/28`
`20.200.71.16/28`
`20.200.71.160/28`
`20.200.71.176/28`
`20.200.71.32/28`
`20.200.71.48/28`
`20.200.71.64/28`
`20.200.71.80/28`
`20.200.71.96/28`
`20.200.93.180`
`20.200.94.116`
`20.200.94.83`
