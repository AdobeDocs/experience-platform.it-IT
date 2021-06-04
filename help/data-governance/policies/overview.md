---
keywords: Experience Platform;casa;argomenti popolari;modulo;DULE
solution: Experience Platform
title: Panoramica dei criteri di utilizzo dei dati
topic-legacy: policies
description: Affinché le etichette per l’utilizzo dei dati supportino efficacemente la conformità dei dati, è necessario implementare i criteri per l’utilizzo dei dati. I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing che sono consentite o a cui è consentita l’esecuzione di dati all’interno di un Experience Platform.
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: 4aeb12aec026ab2dc29133dd44e54b453fb71fe3
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 0%

---

# Panoramica dei criteri di utilizzo dei dati

Affinché le etichette per l’utilizzo dei dati supportino efficacemente la conformità dei dati, è necessario implementare i criteri per l’utilizzo dei dati. I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing consentite o a cui è stata limitata l’esecuzione di dati all’interno di [!DNL Experience Platform].

Questo documento fornisce una panoramica di alto livello dei criteri di utilizzo dei dati e collegamenti ad ulteriore documentazione per l’utilizzo dei criteri nell’interfaccia utente o API.

## Azioni di marketing {#marketing-actions}

Le azioni di marketing (o casi d’uso di marketing) nel contesto del framework di governance dei dati sono azioni che un consumatore di dati [!DNL Experience Platform] può intraprendere, per le quali la tua organizzazione desidera limitare l’utilizzo dei dati. Di conseguenza, un criterio di utilizzo dei dati è definito come segue:

1. Un’azione di marketing specifica
2. Le etichette di utilizzo dei dati su cui è limitata l’esecuzione dell’azione

Un esempio di azione di marketing potrebbe essere il desiderio di esportare un set di dati in un servizio di terze parti. Se è in vigore un criterio che indica che tipi specifici di dati (come PII (Personally Identifiable Information)) non possono essere esportati e si tenta di esportare un set di dati che contiene un’etichetta &quot;I&quot; (Dati identità), riceverai una risposta da [!DNL Policy Service] che informa che è stata violata una policy di utilizzo dei dati.

>[!NOTE]
>
>Le azioni di marketing da sole non limitano l’utilizzo dei dati. Devono essere inclusi nei criteri di utilizzo dei dati abilitati per poter valutare tali azioni in caso di violazioni dei criteri.

Quando si verifica un utilizzo dei dati nel servizio dell’organizzazione, è necessario indicare le azioni di marketing rilevanti in modo da identificare eventuali violazioni dei criteri. Puoi quindi utilizzare l&#39; [API del servizio criteri](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) per verificare la presenza di violazioni dei criteri nell&#39;integrazione.

>[!NOTE]
>
>Se utilizzi [!DNL Real-time Customer Data Platform], puoi impostare casi di utilizzo del marketing sulle destinazioni per automatizzare l’applicazione dei criteri. Per ulteriori informazioni, consulta il documento sulla [governance dei dati in Real-time CDP](../../rtcdp/privacy/data-governance-overview.md) .

Vedi l&#39;appendice di questo documento per un elenco delle [azioni di marketing definite dall&#39;Adobe disponibili](#core-actions). Puoi anche definire azioni di marketing personalizzate utilizzando l’ API [!DNL Policy Service] o l’ interfaccia utente [!DNL Experience Platform ]. Ulteriori informazioni sull’utilizzo delle azioni e dei criteri di marketing sono disponibili nella sezione successiva.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## Gestione dei criteri di utilizzo dei dati {#manage}

Una volta applicate le etichette di utilizzo dei dati, gli amministratori dei dati possono utilizzare l’ API [!DNL Policy Service] o l’ interfaccia utente [!DNL Experience Platform] per gestire e valutare i criteri relativi alle azioni di marketing da eseguire sui dati contenenti etichette di utilizzo dei dati. Puoi creare e aggiornare i criteri, determinare lo stato di un criterio e utilizzare le azioni di marketing per valutare se un&#39;azione specifica viola un criterio di utilizzo dei dati.

>[!IMPORTANT]
>
>Per impostazione predefinita, tutti i criteri di utilizzo dei dati (inclusi i criteri principali forniti da Adobe) sono disabilitati. Affinché un singolo criterio possa essere preso in considerazione per l’implementazione, devi abilitare manualmente tale criterio tramite l’API o l’interfaccia utente.

Per istruzioni dettagliate sull’utilizzo delle azioni di marketing e dei criteri di utilizzo dei dati nell’API, consulta l’esercitazione su [creazione e valutazione dei criteri di utilizzo dei dati](create.md). Per ulteriori informazioni sulle operazioni chiave fornite dall&#39;API [!DNL Policy Service], consulta la [Guida per gli sviluppatori di Policy Service](../api/getting-started.md).

Per informazioni su come utilizzare le azioni e i criteri di marketing nell’ interfaccia utente di [!DNL Platform], consulta la [guida utente relativa ai criteri di utilizzo dei dati](./user-guide.md).

## Passaggi successivi

Questo documento fornisce un&#39;introduzione ai criteri di utilizzo dei dati all&#39;interno del framework [!DNL Data Governance]. Per ulteriori informazioni su come utilizzare i criteri nelle API e nell’interfaccia utente, consulta la documentazione sul processo collegata a in questa guida.

## Appendice

La sezione seguente fornisce informazioni aggiuntive sui criteri di utilizzo dei dati.

### Azioni di marketing definite in Adobe {#core-actions}

La tabella seguente descrive le azioni di marketing di base fornite out-of-the-box per Adobe.

>[!NOTE]
>
>Le azioni di marketing di base devono essere viste come un punto di partenza per aiutarti a identificare i criteri di utilizzo per creare e verificare la presenza di violazioni. Le definizioni e le modalità di interpretazione dipendono dalle esigenze e dai criteri della tua organizzazione.

| Azione di marketing | Descrizione |
| --- | --- |
| Analytics | Un’azione che utilizza i dati a scopo di analisi, ad esempio per misurare, analizzare e generare rapporti sull’utilizzo dei siti o delle app da parte dei clienti dell’organizzazione. |
| Combinare con dati direttamente identificabili | Un’azione che combina qualsiasi informazione identificabile dalla persona (PII) con dati anonimi. I contratti per i dati provenienti da reti di annunci, server di annunci e fornitori di dati di terze parti spesso includono specifici divieti contrattuali sull&#39;uso di tali dati con dati direttamente identificabili. |
| Targeting tra siti | Un’azione che utilizza i dati per il targeting degli annunci tra siti. La combinazione di dati provenienti da più siti, compresa una combinazione di dati in loco e dati fuori sito o una combinazione di dati provenienti da più fonti esterne al sito, è definita dati intersito. I dati intersito vengono in genere raccolti ed elaborati per fare deduzioni sugli interessi degli utenti. |
| Data Science | Azione che utilizza i dati per i flussi di lavoro di scienza dei dati. Alcuni contratti includono divieti espliciti sull&#39;uso dei dati per la scienza dei dati. A volte tali termini sono formulati in termini che vietano l’uso di dati per l’intelligenza artificiale (AI), l’apprendimento automatico (ML) o la modellazione. |
| Targeting e-mail | Un’azione che utilizza i dati nelle campagne di targeting e-mail. |
| Esportazione verso terzi | Un’azione che esporta i dati a processori ed entità che non hanno relazioni dirette con i clienti. Molti fornitori di dati hanno termini nei contratti che vietano l&#39;esportazione di dati da dove sono stati originariamente raccolti. Ad esempio, i contratti di social network spesso limitano il trasferimento dei dati che ricevi da loro. |
| Pubblicità on-site | Un’azione che utilizza i dati per gli annunci onsite, inclusa la selezione e la consegna di annunci pubblicitari sui siti web o sulle app della tua organizzazione, o per misurare la consegna e l’efficacia di tali annunci pubblicitari. |
| Personalizzazione on-site | Un’azione che utilizza i dati per la personalizzazione dei contenuti sul sito. Per personalizzazione in sito si intende qualsiasi dato utilizzato per fare deduzioni sugli interessi degli utenti e utilizzato per selezionare quali contenuti o annunci vengono serviti in base a tali deduzioni. |
| Corrispondenza segmento | Un’azione che utilizza i dati per Adobe Experience Platform Segment Match (Corrispondenza segmento), che consente a due o più utenti di Platform di scambiare i dati dei segmenti. Attivando i criteri che fanno riferimento a questa azione, puoi limitare i dati utilizzati per la corrispondenza dei segmenti. Ad esempio, se il criterio principale &quot;Limita la condivisione dei dati&quot; è abilitato, non è possibile utilizzare dati con un&#39;etichetta [C11](../labels/reference.md#c11) per Segment Match. |
| Personalizzazione a identità singola | Un’azione che richiede l’utilizzo di una singola identità a scopo di personalizzazione anziché unire identità da più sorgenti. |
