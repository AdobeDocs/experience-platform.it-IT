---
title: Informazioni riservate e personali in XDM
description: Scopri le considerazioni chiave relative alle informazioni personali sensibili (SPI) e alle informazioni personali identificabili (PII) in Experience Data Model (XDM).
exl-id: 92a8b6ad-3c45-4772-8178-60f857ab13e2
source-git-commit: 302dca9a9f834dba1fd3fdac15284ea4e2fba282
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Informazioni riservate e personali in XDM

Experience Data Model (XDM) fornisce strutture di dati standard da utilizzare in Adobe Experience Platform, che consentono di raccogliere dati sulle esperienze dei clienti. Questi dati possono includere informazioni personali sensibili (SPI) e informazioni personali identificabili (PII) come l’indirizzo e-mail, il nome, l’ID account di un cliente e altri campi di dati.

Le regole organizzative e le normative legali sulla privacy, come il Regolamento generale sulla protezione dei dati (RGPD), impongono restrizioni su come SPI e PII possono essere raccolti, memorizzati, utilizzati e condivisi. Di conseguenza, è importante considerare quali campi rappresentano informazioni riservate o personali nel modello di dati e assicurarsi che le operazioni rientrino in linee guida organizzative e legali.

Questo documento tratta considerazioni chiave relative ai dati sensibili e personali in XDM.

## Determinare quali campi contengono dati sensibili o personali

I concetti di SPI e PII sono molto specifici per il contesto. Spetta quindi a te comprendere il modello di dati, le operazioni aziendali e le normative applicabili, al fine di determinare quali campi dello schema rappresentano dati sensibili o personali.

Ad esempio, la giurisdizione legale dei tuoi clienti ha un effetto diretto su quali informazioni sono considerate sensibili. Il RGPD fornisce definizioni solide per SPI e PII, ma i clienti al di fuori dello Spazio economico europeo (SEE) possono essere soggetti a definizioni e restrizioni diverse.

## Trattamento di dati sensibili e personali

Analogamente alle definizioni per i dati sensibili e personali stessi, anche le restrizioni per il trattamento di tali dati sono specifiche del contesto.

Il consenso del cliente è spesso un fattore critico in termini di quali dati possono essere raccolti ed elaborati e per quali scopi. A seconda della giurisdizione legale in cui si trovano i tuoi clienti, per raccogliere i loro dati sensibili e personali potrebbe essere necessario il consenso esplicito. Anche nei casi in cui non è richiesto il consenso esplicito, le restrizioni alla gestione dei dati sono ancora applicabili a seconda di ciò che l’informativa sulla privacy dice al cliente.

Consulta il team legale per determinare quanto dati sensibili e personali devono essere gestiti per i tuoi casi d&#39;uso aziendali.

## Limitare l’uso di dati sensibili e personali

XDM fornisce una varietà di gruppi di campi e tipi di dati standard per descrivere strutture di dati rilevanti e di uso comune per migliorare le esperienze dei clienti. Tuttavia, se una risorsa standard consigliata contiene campi con restrizioni che non desideri includere negli schemi, non è necessario utilizzare tale risorsa.

Platform consente di definire gruppi di campi e tipi di dati personalizzati, garantendo il controllo completo sulla struttura dei dati nel caso in cui le risorse standard disponibili non soddisfino le tue esigenze. Per ulteriori informazioni su come definire queste risorse personalizzate, consulta la seguente documentazione:

* [Creare un gruppo di campi personalizzato](../ui/resources/field-groups.md#create)
* [Creare un tipo di dati personalizzato](../ui/resources/data-types.md#create)

<!-- (To include once features are available)
* Marking fields as sensitive
* Remove fields from standard field groups pre-ingestion
* Deprecate fields post-ingestion
-->

>[!IMPORTANT]
>
>SPI e PII devono essere salvati solo nel [Profilo individuale XDM](../classes/individual-profile.md) e [XDM ExperienceEvent](../classes/experienceevent.md) classi. Come best practice per l’eliminazione dei dati e per scopi di privacy e governance, non salvare SPI e PII in altre classi XDM personalizzate o standard.

## Passaggi successivi

Questo documento tratta le considerazioni chiave relative ai dati sensibili e personali in XDM. Per ulteriori informazioni su come modellare gli schemi per soddisfare al meglio i casi d’uso aziendali, consulta la guida su [best practice per la modellazione dei dati](./best-practices.md).

Per ulteriori informazioni sulla governance dei dati e sulle funzionalità per la privacy in Experienci Platform, consulta la panoramica su [governance, privacy e sicurezza](../../landing/governance-privacy-security/overview.md).
