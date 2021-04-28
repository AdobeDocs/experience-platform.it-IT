---
keywords: Indirizzo IP, intervallo IP, destinazioni elenchi consentiti, inserire nell'elenco Consentiti
title: 'ELENCO CONSENTITI di indirizzi IP per le destinazioni di archiviazione cloud '
type: Documentation
description: Questa pagina fornisce intervalli IP che è possibile aggiungere all’elenco consentiti per esportare in modo sicuro i dati dall’Experience Platform al server SFTP, all’archiviazione Amazon S3 o Azure Blob.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
translation-type: tm+mt
source-git-commit: 4cc7fb2714f6df8065a0531f7e507983940d662c
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# ELENCO CONSENTITI di indirizzi IP per le destinazioni di archiviazione cloud {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe consiglia di aggiungere un segnalibro a questa pagina e di rivisitarla ogni tre mesi per verificare la presenza degli indirizzi IP più recenti. Adobe non fornisce notifiche sui nuovi intervalli IP.
> * Mentre Adobe supporta le esportazioni di dati verso server SFTP, le posizioni di archiviazione cloud consigliate per l’esportazione di dati sono [!DNL Amazon S3] e [!DNL Azure Blob].


## Panoramica {#overview}

Questa pagina fornisce intervalli IP che puoi aggiungere al tuo elenco consentiti per esportare in modo sicuro i dati dall&#39;Experience Platform al tuo [server SFTP](./sftp.md).

È possibile definire controlli di accesso alla rete tramite il firewall di rete. Specificando l’intervallo IP appropriato, puoi consentire il traffico per il servizio di trasferimento dati.

Adobe consiglia di aggiungere i seguenti intervalli IP a un elenco consentiti prima di utilizzare le connessioni di destinazione dell&#39;archiviazione cloud. Se non si aggiunge all&#39;elenco consentiti l&#39;intervallo IP specifico per l&#39;area geografica, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l&#39;utilizzo delle connessioni di destinazione dell&#39;archiviazione cloud.

## Richiesto per tutti i clienti

* `52.247.108.70`

## Clienti statunitensi

* `52.252.71.64/29`

## Clienti EMEA

* `51.137.8.208/29`

## Clienti APAC

* `20.53.201.168/29`
