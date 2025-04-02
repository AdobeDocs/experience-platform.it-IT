---
title: ELENCO CONSENTITI di indirizzo IP per destinazioni di archiviazione cloud basata su file
type: Documentation
description: Questa pagina fornisce intervalli IP che puoi aggiungere al tuo elenco consentiti per esportare in modo sicuro i dati da Experience Platform alle destinazioni dell’archiviazione cloud.
exl-id: 0b8086aa-786e-4244-b2a5-a3f57ad59a8b
source-git-commit: 7cf15550d7619e247052efc4d9b4c72c5d32641a
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---

# Indirizzi IP di cui è stato eseguito il inserisco nell&#39;elenco Consentiti per le destinazioni di archiviazione cloud basate su file {#ip-address-allow-list-cloud-storage}

>[!IMPORTANT]
>
> * Adobe consiglia di applicare un segnalibro a questa pagina e di visitarla nuovamente ogni tre mesi per verificare la presenza degli indirizzi IP più recenti. Adobe non fornisce la notifica dei nuovi intervalli IP.
> * Sebbene Adobe supporti le esportazioni di dati ai server SFTP, i percorsi consigliati per l&#39;archiviazione cloud per l&#39;esportazione dei dati sono [!DNL Amazon S3] e [!DNL Azure Blob].

## Applicabilità {#applicability}

Le informazioni sull’intervallo IP in questa pagina si applicano ai seguenti connettori di archiviazione cloud basati su file nel catalogo delle destinazioni:

* [[!UICONTROL Amazon S3]](./amazon-s3.md)
* [[!UICONTROL Google Cloud Storage]](google-cloud-storage.md)
* [SFTP](./sftp.md)

>[!IMPORTANT]
>
>Gli intervalli IP documentati in questa pagina sono *non* supportati per le seguenti destinazioni di archiviazione cloud basata su file: [!UICONTROL BLOB di Azure], [!UICONTROL Archiviazione Azure Data Lake Gen2] e [!UICONTROL Area di destinazione dati].

## Panoramica {#overview}

Questa pagina fornisce intervalli IP che puoi aggiungere al tuo inserisco nell&#39;elenco Consentiti di per esportare in modo sicuro i dati da Experience Platform in diverse destinazioni di archiviazione cloud.

È possibile definire i controlli di accesso alla rete tramite il firewall di rete. Specificando l’intervallo IP appropriato, puoi consentire il traffico per il servizio di trasferimento dati.

Adobe consiglia di aggiungere i seguenti intervalli IP a un inserisco nell&#39;elenco Consentiti di prima di utilizzare le connessioni di destinazione dell’archiviazione cloud. Se non si aggiunge l’intervallo IP specifico per l’area geografica al inserisco nell&#39;elenco Consentiti di, si potrebbero verificare errori o prestazioni quando si utilizzano le connessioni di destinazione dell’archiviazione cloud.

## Obbligatorio per tutti i clienti {#all-customers}

* `52.247.108.70`

## Clienti statunitensi in esecuzione su AWS {#aws}

L’intervallo IP riportato di seguito si applica ai clienti di Experience Platform che eseguono su Amazon Web Services (AWS). Per ulteriori informazioni, consulta [Panoramica di Experience Platform Multi-Cloud](../../../landing/multi-cloud.md).

>[!NOTE]
>
>Questo intervallo IP non è supportato per i clienti che eseguono su AWS e utilizzano destinazioni basate su file per esportare dati in Amazon S3.

* `66.117.18.0/24`

## Clienti USA {#us-customers}

* `52.252.71.64/29`

## Clienti Canada {#canada-customers}

* `20.220.135.16/29`

## Clienti EMEA {#emea-customers}

* `51.137.8.208/29`

## Clienti britannici {#uk-customers}

* `20.26.133.96/29`

## Clienti APAC {#apac-customers}

* `20.53.201.168/29`
