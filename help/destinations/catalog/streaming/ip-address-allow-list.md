---
keywords: Indirizzo IP, intervallo IP, destinazioni di elenco consentiti, di elenco Consentiti inserì nell'elenco Consentiti, destinazioni di streaming di
title: INSERIRE NELL'ELENCO CONSENTITI Indirizzo IP per le destinazioni di streaming
type: Documentation
description: Questa pagina fornisce intervalli IP che è possibile aggiungere all’elenco consentiti per esportare in modo sicuro i dati da Experience Platform all’endpoint API REST HTTP, Amazon Kinesis o all’istanza dei Azure Event Hubs.
exl-id: f41303bd-c886-4c67-9e39-21efc3f5b768
source-git-commit: 851565b4c40452d102eff134533c9d44ea19ca76
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---


# INSERIRE NELL&#39;ELENCO CONSENTITI Indirizzo IP per le destinazioni basate su API in streaming {#ip-address-allowlist}

>[!IMPORTANT]
>
> * Adobe consiglia di applicare un segnalibro a questa pagina e di visitarla nuovamente ogni tre mesi per verificare la presenza degli indirizzi IP più recenti. Adobe non fornisce la notifica dei nuovi intervalli IP.

## Panoramica {#overview}

Gli intervalli IP documentati in questa pagina si applicano alle seguenti destinazioni:

* [Destinazioni enterprise avanzate](../../destination-types.md#advanced-enterprise-destinations): [Destinazione API HTTP](./http-destination.md), [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md)
* [Destinazioni di esportazione del pubblico in streaming](../../destination-types.md#streaming-destinations), ad esempio [Pubblico in tempo reale CDH Pega](/help/destinations/catalog/personalization/pega-v2.md), integrazioni basate su API con [Salesforce Marketing Cloud](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md) e [Oracle Eloqua](/help/destinations/catalog/email-marketing/oracle-eloqua-api.md)
* Destinazioni pubbliche o private generate tramite [Destination SDK](../../destination-sdk/getting-started.md)

Il traffico in uscita da Experience Platform verso queste destinazioni passa sempre attraverso gli IP elencati in questa pagina.

Questa pagina fornisce intervalli IP che puoi aggiungere al tuo inserisco nell&#39;elenco Consentiti di per esportare in modo sicuro i dati da Experience Platform alle destinazioni elencate in precedenza. Questa funzionalità è particolarmente utile se l’endpoint HTTP si trova dietro un firewall aziendale o se gli standard di sicurezza e conformità dell’azienda richiedono la inserisce nell&#39;elenco Consentiti di un elenco di intervalli IP.

È possibile definire i controlli di accesso alla rete tramite il firewall di rete. Specificando l’intervallo IP appropriato, puoi consentire il traffico per il servizio di trasferimento dati.

## Inserire nell&#39;elenco Consentiti Quando gli IP in questa pagina {#when-to-allowlist}

Se il criterio organizzativo richiede di inserire nell&#39;elenco Consentiti gli IP per il traffico in entrata, è necessario aggiungere al elenco Consentiti gli intervalli IP delle seguenti categorie prima di utilizzare le destinazioni sopra menzionate in questa pagina:

1. Tutti i [indirizzi IP globali](#global)
2. Oltre agli indirizzi IP globali, aggiungi gli indirizzi IP corrispondenti all’area in cui hai effettuato il provisioning, dall’elenco più in basso nella pagina. La mancata aggiunta dell’intervallo IP specifico per la tua regione al inserisco nell&#39;elenco Consentiti di potrebbe causare errori o non prestazioni durante l’utilizzo di queste destinazioni di streaming.

## Indirizzi IP globali {#global}

* `3.209.222.108`
* `3.211.230.204`
* `35.169.227.49`
* `66.117.18.133`
* `66.117.18.134`
* `66.117.18.135`

Oltre a questi indirizzi IP globali, è necessario inserire nell&#39;elenco Consentiti gli indirizzi IP per l’area in cui è stato eseguito il provisioning della tua organizzazione dall’elenco seguente.

## VA7: clienti USA e America {#us-americas}

* `4.152.211.251`
* `20.22.83.112`
* `20.186.185.181`
* `20.186.185.227`
* `20.186.185.239`
* `40.70.154.136/29`
* `52.254.105.192/28`
* `52.254.106.0/28`
* `52.254.106.144/28`
* `52.254.106.160/28`
* `52.254.106.176/28`
* `52.254.106.192/28`
* `52.254.106.208/28`
* `52.254.106.224/28`
* `52.254.106.240/28`
* `52.254.107.0/28`
* `52.254.107.16/28`
* `52.254.107.32/28`
* `52.254.107.64/28`
* `52.254.107.80/28`
* `52.254.107.128/28`
* `52.254.107.144/28`

## VA6: clienti americani e americani in esecuzione su AWS {#aws}

L’intervallo IP riportato di seguito si applica ai clienti di Experience Platform che eseguono su Amazon Web Services (AWS). Per ulteriori informazioni, consulta [Panoramica di Experience Platform Multi-Cloud](../../../landing/multi-cloud.md).

* `3.209.222.108`
* `3.211.230.204`
* `35.169.227.49`
* `66.117.18.133`
* `66.117.18.134`
* `66.117.18.135`

## NLD2: clienti EMEA {#emea}

* `20.50.23.153`
* `20.101.246.9`
* `40.74.3.176/28`
* `40.74.4.144/28`
* `40.74.4.160/28`
* `40.74.4.176/28`
* `40.74.5.128/28`
* `40.74.6.80/28`
* `40.74.6.96/28`
* `40.74.6.112/28`
* `40.74.6.128/28`
* `40.74.6.144/28`
* `40.74.7.128/28`
* `40.74.7.144/28`
* `40.74.7.160/28`
* `40.74.7.176/28`
* `40.74.7.192/28`
* `40.74.7.208/28`
* `51.105.144.1`
* `51.105.144.81`
* `51.124.70.4`
* `51.144.184.248/29`
* `52.142.236.87`
* `108.141.12.47`

## AUS5: clienti APAC {#apac}

* `20.40.188.166`
* `20.40.188.194`
* `20.40.188.227`
* `20.40.191.96/28`
* `20.40.191.224/28`
* `20.40.191.240/28`
* `20.43.104.0/28`
* `20.43.104.16/28`
* `20.43.104.32/28`
* `20.43.104.48/28`
* `20.43.104.64/28`
* `20.43.104.80/28`
* `20.43.104.96/28`
* `20.43.104.112/28`
* `20.43.104.128/28`
* `20.43.104.144/28`
* `20.43.104.160/28`
* `20.43.104.176/28`
* `20.43.104.192/28`
* `20.43.105.0/28`
* `20.43.105.16/28`
* `20.43.105.32/28`
* `20.43.105.48/28`
* `20.227.35.177`
* `20.53.206.128`

## CAN2: clienti Canada {#can}

* `20.104.46.64/28`
* `20.104.46.80/28`
* `20.104.46.128/28`
* `20.104.46.160/28`
* `20.116.145.94`
* `20.116.147.168`
* `20.200.70.192/28`
* `20.200.70.208/28`
* `20.200.70.224/28`
* `20.200.70.240/28`
* `20.200.71.0/28`
* `20.200.71.16/28`
* `20.200.71.32/28`
* `20.200.71.48/28`
* `20.200.71.64/28`
* `20.200.71.80/28`
* `20.200.71.96/28`
* `20.200.71.112/28`
* `20.200.71.128/28`
* `20.200.71.144/28`
* `20.200.71.160/28`
* `20.200.71.176/28`
* `20.200.93.180`
* `20.200.94.83`
* `20.200.94.116`

## GBR9: clienti in Gran Bretagna {#gbr}

* `20.26.64.112/28`
* `20.26.64.208/28`
* `20.26.64.240/28`
* `20.26.65.0/28`
* `20.26.128.247`
* `20.26.130.226`
* `20.26.131.71`
* `20.108.119.100`
* `20.108.202.84`
* `20.254.1.128/28`
* `20.254.2.32/28`
* `20.254.2.128/28`
* `20.254.2.208/28`
* `20.254.3.32/28`
* `20.254.3.48/28`
* `20.254.3.112/28`
* `20.254.3.144/28`
* `20.254.3.176/28`
* `20.254.3.192/28`
* `20.254.3.240/28`
* `20.254.4.0/28`
* `20.254.4.16/28`
* `20.254.4.32/28`
* `20.254.4.64/28`
* `20.254.4.96/28`

## IND2: clienti India {#india}

* `4.188.4.11`
* `4.188.4.99`
* `4.188.4.138`
* `4.188.4.154`
* `4.188.4.167`
* `4.213.40.145`
* `4.224.74.0/28`
* `4.224.74.64/28`
* `4.224.74.80/28`
* `4.224.74.96/28`
* `20.244.74.112/28`
* `20.244.77.0/28`
* `20.244.77.16/28`
* `20.244.77.160/28`
* `20.244.77.208/28`
* `20.244.78.0/28`
* `20.244.78.208/28`
* `20.244.79.0/28`
* `20.244.79.16/28`
* `20.244.79.48/28`
* `20.244.79.80/28`
* `20.244.79.128/28`
* `20.244.79.144/28`
* `20.244.79.192/28`
* `20.244.79.208/28`
* `20.244.79.224/28`

