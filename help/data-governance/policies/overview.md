---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica sui criteri di utilizzo dei dati
topic: policies
translation-type: tm+mt
source-git-commit: d08f06b3c2bdb21e0f4935bbcb6f163892ab9842

---


# Panoramica sui criteri di utilizzo dei dati

Affinché le etichette di utilizzo dei dati supportino efficacemente la conformità dei dati, è necessario implementare dei criteri di utilizzo dei dati. I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing consentite o con cui è consentito eseguire determinate limitazioni ai dati in Experience Platform.

Un esempio di un&#39;azione di marketing potrebbe essere il desiderio di esportare un dataset in un servizio di terze parti. Se è presente un criterio che indica che tipi specifici di dati, come Informazioni personali (PII), non possono essere esportati e che al set di dati è stata applicata un&#39;etichetta &quot;I&quot; (Dati identità), riceverete una risposta dal Servizio criteri in cui viene indicato che è stata violata una policy di utilizzo dei dati.

## Come creare e utilizzare i criteri di utilizzo dei dati

Una volta applicate le etichette di utilizzo dei dati, gli amministratori dei dati possono creare criteri tramite l&#39;API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)DULE Policy Service.

Come amministratore dei dati, puoi utilizzare l&#39;API di Policy Service per gestire e valutare i criteri relativi alle azioni di marketing eseguite sui dati contenenti etichette DULE. Utilizzando l&#39;API, puoi creare e aggiornare criteri, determinare lo stato di un criterio e lavorare con azioni di marketing per valutare se un&#39;azione specifica viola un criterio di utilizzo dei dati.

All&#39;interno dell&#39;API del servizio criteri, tutti i criteri e le azioni di marketing sono denominati o `core` `custom` risorse. `core` le risorse sono definite e gestite da Adobe, mentre `custom` le risorse vengono create e gestite dai singoli clienti. Le `custom` risorse sono pertanto uniche e visibili esclusivamente all&#39;organizzazione che le ha create.

Per ulteriori informazioni sull&#39;esecuzione delle operazioni chiave fornite dall&#39;API di DULE Policy Service, consultate la guida [per gli sviluppatori di](../api/getting-started.md)Policy Service. Per istruzioni dettagliate sull&#39;utilizzo dei criteri DULE, vedete l&#39;esercitazione sulla [creazione e la valutazione di criteri](create.md)DULE.