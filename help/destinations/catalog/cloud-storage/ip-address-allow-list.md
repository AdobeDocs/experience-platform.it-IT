---
keywords: Indirizzo IP, intervallo IP, destinazioni elenco consentiti, inserisce nell'elenco Consentiti di
title: ELENCO CONSENTITI di indirizzo IP per le destinazioni di archiviazione cloud
type: Documentation
description: Questa pagina fornisce intervalli IP che puoi aggiungere all’elenco consentiti per esportare in modo sicuro i dati da Experience Platform al server SFTP, all’archiviazione Amazon S3 o Azure Blob.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: c4d8ae6de2e1bbf23a25a66bde5dc88c13a13402
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# INSERISCO NELL&#39;ELENCO CONSENTITI di indirizzi IP per le destinazioni di archiviazione cloud {#ip-address-allow-list}

>[!IMPORTANT]
>
> * L’Adobe consiglia di aggiungere un segnalibro a questa pagina e di visitarla nuovamente ogni tre mesi per verificare la presenza degli indirizzi IP più recenti. L’Adobe non fornisce la notifica dei nuovi intervalli IP.
> * Sebbene Adobe supporti le esportazioni di dati ai server SFTP, le posizioni di archiviazione cloud consigliate per l’esportazione dei dati sono [!DNL Amazon S3] e [!DNL Azure Blob].


## Panoramica {#overview}

Questa pagina fornisce intervalli IP che puoi aggiungere al tuo inserisco nell&#39;elenco Consentiti di, per esportare in modo sicuro i dati da Experience Platform al tuo [Server SFTP](./sftp.md).

È possibile definire i controlli di accesso alla rete tramite il firewall di rete. Specificando l’intervallo IP appropriato, puoi consentire il traffico per il servizio di trasferimento dati.

L’Adobe consiglia di aggiungere i seguenti intervalli IP a un inserisco nell&#39;elenco Consentiti di prima di utilizzare le connessioni di destinazione dell’archiviazione cloud. La mancata aggiunta dell’intervallo IP specifico per l’area geografica al inserisco nell&#39;elenco Consentiti di può causare errori o non prestazioni quando si utilizzano le connessioni di destinazione dell’archiviazione cloud.

## Obbligatorio per tutti i clienti

* `52.247.108.70`

## Clienti USA

* `52.252.71.64/29`

## Clienti EMEA

* `51.137.8.208/29`

## Clienti APAC

* `20.53.201.168/29`
