---
keywords: Indirizzo IP, intervallo IP, destinazioni elenchi consentiti
title: 'ELENCO CONSENTITI di indirizzi IP per le destinazioni di archiviazione cloud '
type: Documentazione
description: Questa pagina fornisce intervalli IP che è possibile aggiungere all’elenco consentiti per esportare in modo sicuro i dati dall’Experience Platform al server SFTP, all’archiviazione Amazon S3 o Azure Blob.
translation-type: tm+mt
source-git-commit: 648be489aa77870f67564ee350c4d85885673832
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# ELENCO CONSENTITI di indirizzi IP per le destinazioni di archiviazione cloud {#ip-address-allow-list}

>[!IMPORTANT]
>
> Adobe consiglia di aggiungere un segnalibro a questa pagina e di rivisitarla ogni tre mesi per verificare la presenza degli indirizzi IP più recenti. Adobe non fornisce notifiche sui nuovi intervalli IP.

Questa pagina fornisce intervalli IP che è possibile aggiungere all&#39;elenco consentiti per esportare in modo sicuro i dati dall&#39;Experience Platform al server [SFTP](./sftp.md), [Amazon S3](./amazon-s3.md) o all&#39;archiviazione [Azure Blob](./azure-blob.md).

È possibile definire controlli di accesso alla rete tramite il firewall di rete. Specificando l’intervallo IP appropriato, puoi consentire il traffico per il servizio di trasferimento dati.

È possibile aggiungere i seguenti intervalli IP a un elenco consentiti prima di lavorare con le connessioni di destinazione dell&#39;archiviazione cloud. Se non si aggiunge all&#39;elenco consentiti l&#39;intervallo IP specifico per l&#39;area geografica, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l&#39;utilizzo delle connessioni di destinazione dell&#39;archiviazione cloud.

## Clienti statunitensi

* `52.252.71.64/29`

## Clienti EMEA

* `51.137.8.208/29`

## Clienti APAC

* `20.53.201.168/29`