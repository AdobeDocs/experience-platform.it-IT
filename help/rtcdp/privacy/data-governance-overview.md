---
title: Panoramica sulla governance dei dati
seo-title: Governance dei dati in tempo reale della piattaforma dati del cliente
description: 'Data Governance consente di gestire i dati dei clienti e di garantire la conformità a normative, restrizioni e criteri applicabili all''uso dei dati. '
seo-description: 'Data Governance consente di gestire i dati dei clienti e di garantire la conformità a normative, restrizioni e criteri applicabili all''uso dei dati. '
translation-type: tm+mt
source-git-commit: f5fbb1434b7154dcdbef12de7882ecd3d2f18d52

---


# Governance dei dati in CDP in tempo reale

Real-time Customer Data Platform (CDP in tempo reale) riunisce i dati di più sistemi aziendali, consentendo agli esperti di marketing di identificare, comprendere e coinvolgere meglio i clienti. Questi dati possono essere soggetti a restrizioni d&#39;uso definite dalla tua organizzazione o dalle normative legali. Pertanto, è importante assicurarsi che la CDP in tempo reale sia conforme ai criteri di utilizzo quando si gestiscono i dati.

Adobe Experience Platform Data Governance consente di gestire i dati dei clienti e di garantire la conformità a normative, restrizioni e criteri applicabili all&#39;uso dei dati. Questo svolge un ruolo chiave all’interno di CDP in tempo reale, consentendo di definire criteri di utilizzo, classificare i dati in base a tali criteri e verificare la presenza di violazioni dei criteri durante l’esecuzione di determinate azioni di marketing.

CDP in tempo reale è basato su Adobe Experience Platform e pertanto la maggior parte delle funzionalità di governance dei dati è trattata nella documentazione della piattaforma. Questo documento è destinato a completare la panoramica [sulla governance dei](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/technical_overview/data_governance/dule_overview.md) dati per Experience Platform e illustra le funzioni di governance disponibili in Real-time CDP. Vengono trattati i seguenti argomenti:

* [Applicazione di etichette di utilizzo ai dati](#apply-usage-labels-to-your-data)
* [Gestire i criteri di utilizzo dei dati](#manage-data-usage-policies)
* [Applica conformità all&#39;utilizzo dei dati](#enforce-data-usage-compliance)

## Applicazione di etichette di utilizzo ai dati

Governance dei dati consente di applicare etichette di utilizzo ai dati, a livello di dataset o di dataset. Le etichette di utilizzo dei dati consentono di classificare i dati in base ai criteri di utilizzo applicati a tali dati.

Per informazioni dettagliate sull&#39;utilizzo delle etichette di utilizzo dei dati, consultate la guida [utente delle etichette di utilizzo dei](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/tutorials/dule/dule_working_with_labels.md) dati per Adobe Experience Platform.

## Imposta limitazioni sulle destinazioni

Puoi impostare restrizioni di utilizzo dei dati su una destinazione definendo i casi di utilizzo marketing per tale destinazione. La definizione dei casi di utilizzo per le destinazioni consente di verificare la presenza di violazioni dei criteri di utilizzo e di verificare che i profili o i segmenti inviati a tale destinazione siano compatibili con le regole di governance dei dati.

I casi di utilizzo del marketing possono essere definiti durante la fase di _configurazione_ del flusso di lavoro _Modifica destinazione_ . Per ulteriori informazioni, consulta la documentazione di destinazione.


## Gestire i criteri di utilizzo dei dati

Affinché le etichette di utilizzo dei dati supportino efficacemente la conformità dei dati, è necessario definire e abilitare i criteri di utilizzo dei dati. I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing consentite o con cui è consentito eseguire attività sui dati all’interno di un CDP in tempo reale. Per ulteriori informazioni, consulta la sezione &quot;Criteri di utilizzo dei dati&quot; nella panoramica [sulla governance dei](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/technical_overview/data_governance/dule_overview.md) dati della piattaforma esperienza.

Adobe Experience Platform fornisce diversi criteri **** fondamentali per i casi di utilizzo più comuni dell&#39;esperienza cliente. Tali criteri possono essere visualizzati eseguendo una richiesta all&#39;API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)DULE Policy Service, come mostrato nella sezione &quot;Elenca tutti i criteri&quot; della guida [per gli sviluppatori di](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html#!api-specification/markdown/narrative/technical_overview/data_governance/dule_policy_service_developer_guide.md)Policy Service. Potete anche creare criteri **** personalizzati per modellare le restrizioni di utilizzo personalizzate, come illustrato nella sezione &quot;Crea un criterio&quot; della guida per gli sviluppatori.

## (Beta) Applica la conformità all&#39;utilizzo dei dati {#enforce-data-usage-compliance}

>[!IMPORTANT]
>Al momento questa funzione è in versione beta e non è disponibile per tutti gli utenti. Può essere attivato su richiesta. La documentazione e la funzionalità sono soggette a modifiche.

Una volta etichettati i dati e definiti i criteri di utilizzo, potete applicare la conformità dell&#39;utilizzo dei dati ai criteri. Quando si attivano i segmenti di pubblico verso destinazioni in CDP in tempo reale, la governance dei dati applica automaticamente i criteri di utilizzo in caso di violazioni.

Il diagramma seguente illustra come l&#39;implementazione dei criteri è integrata nel flusso di dati dell&#39;attivazione dei segmenti:

![](assets/enforcement-flow.png)

Quando un segmento viene attivato per la prima volta, il servizio Criteri DULE verifica la presenza di violazioni dei criteri in base ai seguenti fattori:

* Le etichette di utilizzo dei dati applicate ai campi e ai set di dati all’interno del segmento da attivare.
* Scopo di marketing della destinazione.

### Messaggi sulle violazioni dei criteri

Se si verifica una violazione del criterio durante il tentativo di attivare un segmento (o di [apportare modifiche a un segmento](#policy-enforcement-for-activated-segments)già attivato), l&#39;azione viene impedita e viene visualizzato un puntatore che indica che sono stati violati uno o più criteri. Selezionate una violazione di criterio nella colonna a sinistra del puntatore per visualizzare i dettagli relativi a tale violazione.

![](assets/violation-popover.png)

La scheda *Dettagli* del puntatore indica l&#39;azione che ha attivato la violazione il motivo della violazione e fornisce suggerimenti per la possibile risoluzione del problema.

Fare clic su **Data Lineage** per tenere traccia delle destinazioni, dei segmenti, dei criteri di unione o dei set di dati le cui etichette dati hanno attivato la violazione.

![](assets/data-lineage.png)

Dopo l&#39;attivazione di una violazione, il pulsante **Salva** viene disattivato per l&#39;attivazione fino a quando i componenti appropriati non vengono aggiornati in conformità ai criteri di utilizzo dei dati.

### Applicazione dei criteri per i segmenti attivati

L&#39;applicazione dei criteri continua a essere applicata ai segmenti dopo che questi sono stati attivati, limitando le modifiche a un segmento o alla sua destinazione che si tradurrebbero in una violazione dei criteri. A causa dei numerosi componenti coinvolti nell&#39;attivazione dei segmenti alle destinazioni, una delle seguenti azioni può potenzialmente determinare una violazione:

* Aggiornamento delle etichette di utilizzo dei dati
* Modifica dei set di dati per un segmento
* Modifica dei predicati dei segmenti
* Modifica delle configurazioni di destinazione

Se una delle azioni di cui sopra genera una violazione, tale azione non viene salvata e viene visualizzato un messaggio di violazione dei criteri, garantendo che i segmenti attivati continuino a rispettare i criteri di utilizzo dei dati quando vengono modificati.

## Passaggi successivi

Ora che hai introdotto le funzioni chiave di governance dei dati su CDP in tempo reale e come Experience Platform le consente, continua a consultare la [documentazione per la governance dei dati su Adobe Experience Platform](https://www.adobe.io/apis/experienceplatform/home/dule/duleservices.html). La documentazione fornisce panoramiche dei concetti fondamentali di governance dei dati, nonché flussi di lavoro dettagliati per la gestione delle etichette e dei criteri di utilizzo dei dati.