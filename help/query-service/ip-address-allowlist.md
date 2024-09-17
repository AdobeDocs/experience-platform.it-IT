---
keywords: Indirizzo IP, intervallo IP, elenco consentiti, inserisco nell'elenco Consentiti di, servizio query, accesso alla rete
title: INSERIRE NELL'ELENCO CONSENTITI Indirizzo IP per Query Service
description: Questa pagina fornisce intervalli IP aggiornati che è possibile aggiungere al elenco Consentiti di per un accesso sicuro a Query Service.
exl-id: f6745e0f-d387-45f2-9f72-054e721016ff
source-git-commit: 029d0ad63460a71770e5ba3cd75a29cb04c0cb9c
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Indirizzo IP inserisco nell&#39;elenco Consentiti {#ip-address-allow-list}

>[!IMPORTANT]
>
> * L’Adobe consiglia di aggiungere un segnalibro a questa pagina e di visitarla nuovamente ogni tre mesi per verificare la presenza degli indirizzi IP più recenti. L’Adobe non fornisce la notifica dei nuovi intervalli IP.
> * Sebbene Adobe supporti le esportazioni di dati ai server SFTP, i percorsi consigliati per l&#39;archiviazione cloud per l&#39;esportazione dei dati sono [!DNL Amazon S3] e [!DNL Azure Blob].
> * Dal 15 ottobre 2024 i nuovi intervalli IP hanno sostituito quelli esistenti. Inserire nell&#39;elenco Consentiti Per evitare interruzioni del servizio, assicurati che gli IP vecchi e nuovi vengano aggiunti al tuo prima di questa data.

## Panoramica {#overview}

Questa pagina fornisce indirizzi IP che puoi aggiungere al tuo inserisco nell&#39;elenco Consentiti di esportazione dei dati da Experience Platform al tuo [server SFTP](../destinations/catalog/cloud-storage/sftp.md) in modo sicuro.

È possibile definire i controlli di accesso alla rete tramite il firewall di rete. Specificando l’intervallo IP appropriato, puoi consentire il traffico per il servizio di trasferimento dati.

Come parte dei miglioramenti in corso, Adobe ha aggiornato gli intervalli IP utilizzati per l’accesso di rete a Query Service il 15 ottobre 2024. Gli indirizzi IP esistenti diventeranno obsoleti e i nuovi indirizzi IP sostituiranno quelli esistenti. Per garantire la continuità del servizio, è fondamentale aggiungere sia il vecchio che il nuovo intervallo IP al inserisco nell&#39;elenco Consentiti di.

L’Adobe consiglia di aggiungere i seguenti intervalli IP specifici per area geografica a un inserisco nell&#39;elenco Consentiti di a seconda della tua area geografica. La mancata aggiunta di intervalli IP specifici per l’area geografica al inserisco nell&#39;elenco Consentiti di può causare errori o non prestazioni.

## VA7: clienti USA e America {#us-americas}

**IP precedente:** 20.14.241.153\
**Nuovo IP:** 4.152.211.251

## NLD2: clienti EMEA {#emea}

**IP precedente:** 20.101.233.128\
**Nuovo IP:** 108.141.12.47

## AUS5: clienti APAC {#apac}

**IP precedente:** 20.248.220.69\
**Nuovo IP:** 40.82.220.111

## CAN2: clienti canadesi {#can2}

**IP precedente:** 4.172.1.139\
**Nuovo IP:** 4.172.28.20

## GBR9: clienti Regno Unito {#gbr9}

**IP precedente:** 20.108.200.9\
**Nuovo IP:** 20.254.80.141

