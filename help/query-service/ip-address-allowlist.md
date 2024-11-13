---
keywords: Indirizzo IP, intervallo IP, elenco consentiti, inserisco nell'elenco Consentiti di, servizio query, accesso alla rete
title: INSERIRE NELL'ELENCO CONSENTITI Indirizzo IP per Query Service
description: Questa pagina fornisce intervalli IP aggiornati che è possibile aggiungere al elenco Consentiti di per un accesso sicuro a Query Service.
exl-id: f6745e0f-d387-45f2-9f72-054e721016ff
source-git-commit: e6c148b943c68bff5330c7ff021ffa88ba131639
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Indirizzo IP inserisco nell&#39;elenco Consentiti {#ip-address-allow-list}

>[!IMPORTANT]
>
> * Adobe consiglia di aggiungere un segnalibro a questa pagina e di visitarla nuovamente ogni tre mesi per verificare la presenza degli indirizzi IP più recenti. Adobe non fornisce la notifica dei nuovi intervalli IP.
> * A partire dal 15 ottobre 2024, solo i nuovi intervalli IP sono validi per l’accesso a Query Service. Gli indirizzi IP obsoleti non funzionano più. Assicurati che il tuo inserisco nell&#39;elenco Consentiti di includa solo i nuovi IP per evitare interruzioni del servizio.

## Panoramica {#overview}

È possibile definire i controlli di accesso alla rete tramite il firewall di rete. Specificando l’intervallo IP appropriato, puoi consentire il traffico per l’accesso a Query Service.

Come parte dei miglioramenti in corso, Adobe ha aggiornato gli intervalli IP per l’accesso di rete a Query Service. Gli indirizzi IP precedenti sono ora obsoleti e solo i nuovi indirizzi IP sono validi. Per mantenere ininterrotto il servizio, è essenziale aggiornare il inserisco nell&#39;elenco Consentiti di per includere i seguenti nuovi intervalli IP.

L’Adobe consiglia di aggiungere i seguenti intervalli IP specifici per area geografica a un inserisco nell&#39;elenco Consentiti a seconda dell’area geografica. La mancata aggiunta di questi intervalli IP specifici per l’area geografica può causare errori o interruzioni del servizio.

## VA7: i clienti americani e americani {#us-americas}

**Nuovo IP:** 4.152.211.251

## NLD2: clienti EMEA {#emea}

**Nuovo IP:** 108.141.12.47

## AUS5: clienti APAC {#apac}

**Nuovo IP:** 40.82.220.111

## CAN2: clienti canadesi {#can2}

**Nuovo IP:** 4.172.28.20

## GBR9: clienti Regno Unito {#gbr9}

**Nuovo IP:** 20.254.80.141

## Impostare restrizioni basate su IP {#set-ip-restrictions}

Utilizza le [guide API per l&#39;autorizzazione dei servizi di query](./auth-api/overview.md) per impostare restrizioni basate su IP. Queste restrizioni basate su IP garantiscono che solo le reti e i computer client approvati possano accedere ai dati tramite SQL in Adobe Experience Platform. Scopri come configurare, applicare e monitorare le restrizioni IP per mantenere standard di sicurezza elevati, con funzionalità di tracciamento degli accessi in tempo reale e avvisi.

* [Guida introduttiva](./auth-api/getting-started.md)
* [Guida dell’endpoint di accesso IP](./auth-api/ip-access.md)
* [Guida dell’endpoint di convalida IP](./auth-api/validate.md)
