---
keywords: Experience Platform;casa;argomenti popolari;modulo;DULE
solution: Experience Platform
title: Panoramica dei criteri di utilizzo dei dati
description: I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing che possono essere eseguite sui dati in Adobe Experience Platform o da cui sono previste restrizioni.
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 2%

---

# Panoramica dei criteri di utilizzo dei dati {#policies-overview}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_restrictusage"
>title="Limitare l’utilizzo dei dati"
>abstract="Il tipo di criterio di utilizzo dati valuta azioni di marketing specifiche applicate alle etichette di governance dei dati per limitare l’utilizzo dei dati per le attività di marketing."

Affinché le etichette per l’utilizzo dei dati supportino efficacemente la conformità dei dati, è necessario implementare i criteri per l’utilizzo dei dati. I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing che possono essere eseguiti o meno sui dati in [!DNL Experience Platform].

Sono disponibili due tipi di criteri:

* **[!UICONTROL Criteri di governance dei dati]**: Limita l’attivazione dei dati in base all’azione di marketing in corso e alle etichette di utilizzo dei dati in base ai dati in questione.
* **[!UICONTROL Criterio di consenso]**: Filtrare i profili a cui è possibile attivare [destinazioni](../../destinations/home.md) in base al consenso o alle preferenze dei clienti

>[!NOTE]
>
>I criteri di utilizzo dei dati non devono essere confusi con [criteri di controllo accessi](../../access-control/abac/end-to-end-guide.md#policy), che determinano se determinati utenti di Platform della tua organizzazione possono accedere a determinati campi di dati e sono configurati tramite [!UICONTROL Autorizzazioni] scheda .

Questo documento fornisce una panoramica di alto livello dei criteri di utilizzo dei dati e collegamenti ad ulteriore documentazione per l’utilizzo dei criteri nell’interfaccia utente o API.

## Azioni di marketing {#marketing-actions}

Le azioni di marketing (o casi di utilizzo del marketing) nel contesto del framework di governance dei dati sono azioni che [!DNL Experience Platform] il consumatore di dati può utilizzare, per i quali la tua organizzazione desidera limitare l’utilizzo dei dati. Di conseguenza, un criterio di utilizzo dei dati è definito come segue:

1. Un’azione di marketing specifica
2. Le condizioni alle quali tale azione è limitata dall&#39;esecuzione

Un esempio di azione di marketing potrebbe essere il desiderio di esportare un set di dati in un servizio di terze parti. Se è in vigore un criterio che indica che tipi specifici di dati (come PII (Personally Identifiable Information)) non possono essere esportati e si tenta di esportare un set di dati che contiene un’etichetta &quot;I&quot; (Dati di identità), si riceverà una risposta da [!DNL Policy Service] che indica che è stata violata una policy di utilizzo dei dati.

>[!NOTE]
>
>Le azioni di marketing da sole non limitano l’utilizzo dei dati. Devono essere inclusi nei criteri di utilizzo dei dati abilitati per poter valutare tali azioni in caso di violazioni dei criteri.

Quando si verifica un utilizzo dei dati nel servizio dell’organizzazione, è necessario indicare le azioni di marketing rilevanti in modo da identificare eventuali violazioni dei criteri. È quindi possibile utilizzare la [API del servizio criteri](https://www.adobe.io/experience-platform-apis/references/policy-service/) per verificare la presenza di violazioni dei criteri nell&#39;integrazione.

>[!NOTE]
>
>Puoi impostare casi d’uso di marketing sulle destinazioni per automatizzare l’applicazione dei criteri. Consulta la sezione [documentazione sulle destinazioni](../../destinations/home.md) per ulteriori informazioni sulle opzioni di configurazione per la destinazione specifica.

Vedi l&#39;appendice di questo documento per un elenco di [azioni di marketing definite da un Adobe disponibili](#core-actions). Puoi anche definire azioni di marketing personalizzate utilizzando [!DNL Policy Service] o [!DNL Experience Platform] interfaccia utente. Ulteriori informazioni sull’utilizzo delle azioni e dei criteri di marketing sono disponibili nella sezione successiva.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## Gestione dei criteri di utilizzo dei dati {#manage}

Una volta applicate le etichette di utilizzo dei dati, gli amministratori dei dati possono utilizzare [!DNL Policy Service] o [!DNL Experience Platform] Interfaccia utente per gestire e valutare i criteri relativi alle azioni di marketing in corso sui dati contenenti etichette di utilizzo dei dati. Puoi creare e aggiornare i criteri, determinare lo stato di un criterio e utilizzare le azioni di marketing per valutare se un&#39;azione specifica viola un criterio di utilizzo dei dati.

>[!IMPORTANT]
>
>Per impostazione predefinita, tutti i criteri di utilizzo dei dati (inclusi i criteri principali forniti da Adobe) sono disabilitati. Affinché un singolo criterio possa essere preso in considerazione per l’implementazione, devi abilitare manualmente tale criterio tramite l’API o l’interfaccia utente.

Per istruzioni dettagliate sull’utilizzo delle azioni di marketing e dei criteri di utilizzo dei dati nell’API, consulta l’esercitazione su [creazione e valutazione dei criteri di utilizzo dei dati](create.md). Per ulteriori informazioni sulle operazioni chiave fornite dalla [!DNL Policy Service] API, vedi [Guida per gli sviluppatori di Policy Service](../api/getting-started.md).

Per informazioni su come lavorare con le azioni e i criteri di marketing in [!DNL Platform] Interfaccia utente, vedi [guida utente del criterio di utilizzo dati](./user-guide.md).

## Passaggi successivi

Questo documento fornisce un’introduzione ai criteri di utilizzo dei dati all’interno del framework di governance dei dati. Per ulteriori informazioni su come utilizzare i criteri nelle API e nell’interfaccia utente, consulta la documentazione sul processo collegata a in questa guida.

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
| Corrispondenza segmento | Un’azione che utilizza i dati per Adobe Experience Platform Segment Match (Corrispondenza segmento), che consente a due o più utenti di Platform di scambiare i dati dei segmenti. Attivando i criteri che fanno riferimento a questa azione, puoi limitare i dati utilizzati per la corrispondenza dei segmenti. Ad esempio, se il criterio principale &quot;Limita la condivisione dei dati&quot; è abilitato, qualsiasi dato con un [Etichetta C11](../labels/reference.md#c11) non può essere utilizzato per Segment Match (Corrispondenza segmento). |
| Personalizzazione a identità singola | Un’azione che richiede l’utilizzo di una singola identità a scopo di personalizzazione anziché unire identità da più sorgenti. |
