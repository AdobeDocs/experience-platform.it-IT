---
title: Guardrail Real-Time CDP
description: Scopri i guardrail dei dati nei vari servizi e aree di Real-Time CDP.
feature: Guardrails, Data Management, Data Ingestion, Data Export
exl-id: 377499b4-5707-4d50-94e3-02f88ad5bf2c
source-git-commit: 5d6b70e397a252e037589c3200053ebcb7eb8291
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---

# Guardrail Real-Time CDP

I guardrail sono soglie che forniscono indicazioni per l’utilizzo dei dati e del sistema, l’ottimizzazione delle prestazioni e la prevenzione di errori o risultati imprevisti in Real-Time CDP. I guardrail possono fare riferimento all’utilizzo o al consumo di dati e all’elaborazione in relazione alle licenze concesse.

>[!IMPORTANT]
>
>Controllare i diritti di licenza nell&#39;ordine di vendita e i corrispondenti [Descrizione del prodotto](https://helpx.adobe.com/it/legal/product-descriptions.html) sui limiti di utilizzo effettivi oltre a questa pagina di guardrail.

Inizia qui e segui i collegamenti riportati di seguito per comprendere tutti i guardrail nei vari servizi e aree di Real-Time CDP:

* [Guardrail per l’acquisizione dei dati](/help/ingestion/guardrails.md)
* [Guardrail per il [!DNL Edge Network Server API]](/help/server-api/guardrails.md)
* [Guardrail per [!DNL Real-Time Customer Profile] dati e segmentazione](/help/profile/guardrails.md)
* [Guardrail per [!DNL Identity Service] dati](/help/identity-service/guardrails.md)
* [Guardrail per [!DNL Query Service]](/help/query-service/guardrails.md)
* [Guardrail per l’attivazione dei dati tramite destinazioni](/help/destinations/guardrails.md)
* [Guardrail per Real-Time CDP B2B](/help/rtcdp/b2b-guardrails.md)

>[!TIP]
>
>Inoltre, visita [blueprint dell’esperienza digitale](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html) per ulteriori informazioni quali [diagrammi di latenza end-to-end](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=en#end-to-end-latency-diagrams) per vari servizi di Experience Platform.

## Tipi di guardrail {#guardrail-types}

I due tipi di guardrail in tutte le aree e i servizi di Real-Time CDP sono:

| Tipo di guardrail | Descrizione |
|----------|---------|
| **Guardrail delle prestazioni (limite morbido)** | I guardrail di prestazioni sono limiti di utilizzo relativi all’ambito dei tuoi casi d’uso. Quando si superano i guardrail delle prestazioni, è possibile che si verifichi un peggioramento delle prestazioni e della latenza. L’Adobe non è responsabile di tale degrado delle prestazioni. I clienti che superano costantemente il limite di prestazioni possono scegliere di concedere licenze aggiuntive per evitare il degrado delle prestazioni. |
| **Guardrail applicati dal sistema (limite rigido)** | I guardrail applicati dal sistema vengono applicati dall’interfaccia utente o dall’API di Real-Time CDP. Questi sono i limiti che non puoi superare, poiché l’interfaccia utente e l’API ti impediranno di farlo o restituiranno un errore. |

{style="table-layout:auto"}

## Informazioni su licenze e licenze Real-Time CDP {#product-descriptions}

Inoltre, fare riferimento ai collegamenti di descrizione del prodotto riportati di seguito per informazioni su licenze e adesione in base all&#39;edizione e al livello Real-Time CDP acquistati:

* [Tutte le descrizioni dei prodotti Adobe](https://helpx.adobe.com/it/legal/product-descriptions.html)
* [Real-time Customer Data Platform (versione B2C - Pacchetti Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (B2P Edition - Pacchetti Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-time Customer Data Platform (Edizione B2B - Pacchetti Prime e Ultimate)](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)

## Guardrail per altre applicazioni Experienci Platform  {#guardrails-other-aep-apps}

Guardrail simili esistono per altre applicazioni Experienci Platform. Per ulteriori informazioni, visitare i collegamenti riportati di seguito:

* [Guardrail Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/guardrails.html?lang=en)
* [Guardrail del Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html)

## Passaggi successivi

Dopo aver compreso le protezioni che si applicano alle varie aree e servizi di Real-Time CDP, puoi seguire la procedura [caso di utilizzo di esempio di un’implementazione di Real-Time CDP](/help/rtcdp/get-started.md).
