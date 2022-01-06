---
title: Informazioni riservate e personali in XDM
description: Scopri le considerazioni principali relative alle informazioni personali sensibili (SPI) e alle informazioni personali (PII) in Experience Data Model (XDM).
source-git-commit: 76815389a1c87fbf908e499c50594a4b356a11a9
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# Informazioni riservate e personali in XDM

Experience Data Model (XDM) fornisce strutture di dati standard da utilizzare in Adobe Experience Platform, che consentono di raccogliere dati sulle esperienze dei clienti. Questi dati possono includere dati personali sensibili (SPI) e informazioni personali identificabili (PII) come l’indirizzo e-mail, il nome, l’ID account e altri campi di dati di un cliente.

Le regole organizzative e le normative legali sulla privacy, come il Regolamento generale sulla protezione dei dati (RGPD), impongono restrizioni sulle modalità di raccolta, archiviazione, utilizzo e condivisione di SPI e PII. Di conseguenza, è importante considerare quali campi rappresentano informazioni sensibili o personali nel modello dati e assicurarsi che le operazioni rientrino nelle linee guida organizzative e legali.

Questo documento tratta considerazioni chiave relative ai dati personali e sensibili in XDM.

## Determinare quali campi contengono dati sensibili o personali

Ciò che costituisce SPI e PII è molto specifico per il contesto e spetta quindi a te comprendere il tuo modello di dati, le operazioni aziendali e le normative applicabili al fine di determinare quali campi dello schema rappresentano dati sensibili o personali.

Ad esempio, la giurisdizione legale dei clienti ha un effetto diretto su quali informazioni sono considerate sensibili. Il RGPD fornisce solide definizioni per i requisiti SPI e PII, ma i clienti al di fuori dello Spazio economico europeo (SEE) possono essere soggetti a definizioni e restrizioni diverse.

## Gestione dei dati sensibili e personali

Analogamente alle definizioni dei dati personali e sensibili, anche le restrizioni per la gestione di tali dati sono specifiche per il contesto.

Il consenso dei clienti è spesso un fattore critico in termini di quali dati possono essere raccolti ed elaborati e per quali scopi. A seconda della giurisdizione legale in cui si trovano i clienti, può essere richiesto un consenso esplicito per la raccolta dei loro dati personali e sensibili. Anche nei casi in cui non è richiesto un consenso esplicito, le restrizioni di gestione dei dati sono ancora applicabili a seconda di quanto indicato dall’avviso sulla privacy al cliente.

Consulta il tuo team legale per determinare come devono essere gestiti i dati personali e sensibili per i tuoi casi d’uso aziendali.

## Limitazione dell&#39;uso di dati sensibili e personali

XDM fornisce una varietà di gruppi di campi e tipi di dati standard per descrivere strutture di dati pertinenti e di uso comune per migliorare le esperienze dei clienti. Se una risorsa standard consigliata contiene campi con restrizioni che non si desidera includere negli schemi, non è tuttavia necessario utilizzare tale risorsa.

Platform ti consente di definire gruppi di campi e tipi di dati personalizzati e di controllare in modo completo la struttura dei dati nel caso in cui le risorse standard disponibili non soddisfino le tue esigenze. Per ulteriori informazioni su come definire queste risorse personalizzate, consulta la seguente documentazione:

* [Creare un gruppo di campi personalizzato](../ui/resources/field-groups.md#create)
* [Creare un tipo di dati personalizzato](../ui/resources/data-types.md#create)

<!-- (To include once features are available)
* Marking fields as sensitive
* Remove fields from standard field groups pre-ingestion
* Deprecate fields post-ingestion
-->

## Passaggi successivi

Questo documento tratta considerazioni chiave relative ai dati personali e sensibili in XDM. Per ulteriori informazioni su come modellare gli schemi per soddisfare al meglio i casi d’uso aziendali, consulta la guida su [best practice per la modellazione dei dati](./best-practices.md).

Per ulteriori informazioni sulla governance dei dati e sulle funzionalità per la privacy in Experience Platform, consulta la panoramica su [governance, privacy e sicurezza](../../landing/governance-privacy-security/overview.md).
