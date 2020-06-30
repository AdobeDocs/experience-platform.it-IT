---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Panoramica sui criteri di utilizzo dei dati
topic: policies
translation-type: tm+mt
source-git-commit: d4964231ee957349f666eaf6b0f5729d19c408de
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 0%

---


# Panoramica sui criteri di utilizzo dei dati

Affinché le etichette di utilizzo dei dati supportino efficacemente la conformità dei dati, è necessario implementare dei criteri di utilizzo dei dati. I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing consentite o con cui è consentito eseguire determinate attività sui dati all&#39;interno [!DNL Experience Platform].

Questo documento fornisce una panoramica di alto livello dei criteri di utilizzo dei dati e fornisce collegamenti ad ulteriore documentazione per l&#39;utilizzo dei criteri nell&#39;interfaccia utente o nell&#39;API.

## Azioni di marketing {#marketing-actions}

**Le azioni** di marketing (o casi **di utilizzo** marketing) nel contesto del framework di governance dei dati sono azioni che un consumatore di [!DNL Experience Platform] dati può intraprendere, per le quali l&#39;organizzazione intende limitare l&#39;utilizzo dei dati. Di conseguenza, un criterio di utilizzo dei dati è definito come segue:

1. Un&#39;azione di marketing specifica
2. Le etichette di utilizzo dei dati a cui è stata limitata l&#39;esecuzione dell&#39;azione

Un esempio di un&#39;azione di marketing potrebbe essere il desiderio di esportare un dataset in un servizio di terze parti. Se è presente un criterio che indica che tipi specifici di dati (come Informazioni personali (PII)) non possono essere esportati e si tenta di esportare un set di dati contenente un&#39;etichetta &quot;I&quot; (Dati identità), si riceverà una risposta dalla [!DNL Policy Service] notifica che un criterio di utilizzo dei dati è stato violato.

>[!NOTE] Le azioni di marketing di per sé non limitano l&#39;utilizzo dei dati. Devono essere inclusi nei criteri di utilizzo dei dati abilitati per poter valutare tali azioni in caso di violazioni dei criteri.

Quando si verifica l&#39;utilizzo dei dati nel servizio dell&#39;azienda, è necessario indicare le azioni di marketing rilevanti in modo da identificare eventuali violazioni dei criteri. Potete quindi utilizzare [DULE Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) per verificare la presenza di violazioni dei criteri nell&#39;integrazione.

>[!NOTE] Se utilizzi Real-time Customer Data Platform, puoi impostare casi di utilizzo del marketing sulle destinazioni per automatizzare l&#39;applicazione dei criteri. Per ulteriori informazioni, consulta il documento sulla governance dei [dati in CDP](../../rtcdp/privacy/data-governance-overview.md) in tempo reale.

Vedi l&#39;appendice di questo documento per un elenco delle azioni [di marketing definite da Adobe](#core-actions)disponibili. Puoi anche definire azioni di marketing personalizzate utilizzando l&#39;API di DULE Policy Service o l&#39;interfaccia utente Experience Platform . Ulteriori informazioni sull&#39;utilizzo delle azioni e dei criteri di marketing sono disponibili nella sezione successiva.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/data-export-controls.html).
-->

## Gestione dei criteri di utilizzo dei dati {#manage}

Una volta applicate le etichette di utilizzo dei dati, gli amministratori dei dati possono utilizzare l&#39;API DULE Policy Service o l&#39;interfaccia  Experience Platform per gestire e valutare i criteri relativi alle azioni di marketing eseguite sui dati contenenti etichette di utilizzo dei dati. Puoi creare e aggiornare i criteri, determinare lo stato di un criterio e utilizzare azioni di marketing per valutare se un&#39;azione specifica viola un criterio di utilizzo dei dati.

>[!IMPORTANT] Tutti i criteri di utilizzo dei dati (inclusi i criteri di base forniti da Adobe) sono disattivati per impostazione predefinita. Affinché un singolo criterio venga preso in considerazione per l&#39;implementazione, è necessario attivarlo manualmente tramite l&#39;API o l&#39;interfaccia utente.

Per istruzioni dettagliate sull&#39;utilizzo delle azioni di marketing e dei criteri di utilizzo dei dati nell&#39;API, consulta l&#39;esercitazione sulla [creazione e la valutazione dei criteri](create.md)di utilizzo dei dati. Per ulteriori informazioni sulle operazioni chiave fornite dall&#39;API di Servizio criteri, consultate la guida [per gli sviluppatori di Servizio](../api/getting-started.md)criteri.

Per informazioni su come utilizzare le azioni e i criteri di marketing nell&#39;interfaccia utente di Platform, consulta la guida [utente relativa ai criteri di utilizzo dei](./user-guide.md)dati.

## Passaggi successivi

Questo documento ha fornito un&#39;introduzione ai criteri di utilizzo dei dati all&#39;interno del framework DULE. È ora possibile continuare a leggere la documentazione del processo collegata a questa guida per ulteriori informazioni sull&#39;utilizzo dei criteri nell&#39;API e nell&#39;interfaccia utente.

## Appendice

La sezione seguente fornisce informazioni aggiuntive sui criteri di utilizzo dei dati.

### Azioni di marketing definite da Adobe {#core-actions}

La tabella seguente descrive le azioni di marketing di base fornite out-of-the-box da Adobe.

>[!NOTE] Le azioni di marketing di base dovrebbero essere viste come punto di partenza per aiutarti a identificare quali criteri di utilizzo creare e verificare la presenza di violazioni. Le definizioni e il modo in cui vengono interpretate dipendono dalle esigenze e dalle politiche aziendali.

| Azione marketing | Descrizione |
| --- | --- |
| Analytics | Un&#39;azione che utilizza i dati a scopo di analisi, come la misurazione, l&#39;analisi e il reporting sull&#39;utilizzo da parte dei clienti dei siti o delle app dell&#39;organizzazione. |
| Combinazione con PII | Un&#39;azione che combina qualsiasi informazione personale (PII) con dati anonimi. I contratti per i dati originati da reti pubblicitarie, server di annunci e provider di dati di terze parti spesso includono specifici divieti contrattuali sull&#39;uso di tali dati con dati direttamente identificabili. |
| Targeting tra siti | Un&#39;azione che utilizza i dati per il targeting degli annunci tra siti. La combinazione di dati provenienti da diversi siti, inclusa una combinazione di dati sul sito e dati fuori sede o una combinazione di dati provenienti da più fonti esterne al sito, è definita dati intersito. I dati intersito vengono in genere raccolti ed elaborati per trarre conclusioni sugli interessi degli utenti. |
| Scienza dei dati | Azione che utilizza i dati per i flussi di lavoro di analisi dei dati. Alcuni contratti includono divieti espliciti sull&#39;uso dei dati per la scienza dei dati. Talvolta tali termini sono formulati in termini che vietano l&#39;uso di dati per l&#39;intelligenza artificiale (AI), l&#39;apprendimento automatico (ML) o la modellazione. |
| Targeting e-mail | Azione che utilizza i dati nelle campagne di targeting delle e-mail. |
| Esportazione verso terzi | Un&#39;azione che esporta dati a processori ed entità che non hanno relazioni dirette con i clienti. Molti provider di dati hanno termini nei contratti che vietano l&#39;esportazione di dati da dove è stato originariamente raccolto. Ad esempio, i contratti con i social network spesso limitano il trasferimento dei dati che ricevi da loro. |
| Pubblicità on-site | Un&#39;azione che utilizza i dati per gli annunci onsite, inclusa la selezione e la consegna di annunci pubblicitari sui siti Web o sulle app dell&#39;organizzazione, o per misurare la consegna e l&#39;efficacia di tali pubblicità. |
| Personalizzazione on-site | Azione che utilizza i dati per la personalizzazione dei contenuti on-site. Per personalizzazione in sito si intende qualsiasi dato utilizzato per fare deduzioni sugli interessi degli utenti e utilizzato per selezionare quali contenuti o annunci vengono serviti in base a tali inferenze. |
| Personalizzazione identità singola | Un&#39;azione che richiede l&#39;uso di un&#39;unica identità a scopo di personalizzazione invece di cucire identità da più origini. |
