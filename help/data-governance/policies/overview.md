---
keywords: Experience Platform;home;argomenti popolari;dule;DULE
solution: Experience Platform
title: Panoramica dei criteri di utilizzo dei dati
description: I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing che possono essere eseguiti o meno sui dati in Adobe Experience Platform.
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 4%

---

# Panoramica sui criteri di utilizzo dei dati {#policies-overview}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_restrictusage"
>title="Limitare l’utilizzo dei dati"
>abstract="Il tipo di criterio di utilizzo dei dati valuta azioni di marketing specifiche applicate alle etichette di governance dei dati per limitare l’utilizzo dei dati nelle attività di marketing."

Affinché le etichette di utilizzo dei dati supportino in modo efficace la conformità, è necessario implementare i criteri di utilizzo dei dati. I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing che possono essere eseguiti o meno sui dati in [!DNL Experience Platform].

Sono disponibili due tipi di criteri:

* **[!UICONTROL Criteri di governance dei dati]**: limita l’attivazione dei dati in base all’azione di marketing che viene eseguita e alle etichette di utilizzo dei dati presenti nei dati in questione.
* **[!UICONTROL Criterio di consenso]**: filtra i profili che possono essere attivati in [destinazioni](../../destinations/home.md) in base al consenso o alle preferenze dei clienti

>[!NOTE]
>
>I criteri di utilizzo dei dati non devono essere confusi con [criteri di controllo dell’accesso](../../access-control/abac/end-to-end-guide.md#policy), che determinano se alcuni utenti di Platform nella tua organizzazione possono accedere a determinati campi di dati e sono configurati tramite [!UICONTROL Autorizzazioni] scheda.

Questo documento fornisce una panoramica di alto livello dei criteri di utilizzo dei dati e fornisce collegamenti a ulteriore documentazione sull’utilizzo dei criteri nell’interfaccia utente o nell’API.

## Azioni di marketing {#marketing-actions}

Le azioni di marketing (o casi di utilizzo di marketing) nel contesto del framework di governance dei dati sono azioni che [!DNL Experience Platform] il consumatore di dati può accettare, per il quale l’organizzazione desidera limitare l’utilizzo dei dati. Di conseguenza, i criteri di utilizzo dei dati sono definiti dai seguenti elementi:

1. Un’azione di marketing specifica
2. Le condizioni alle quali tale azione è limitata

Un esempio di azione di marketing potrebbe essere il desiderio di esportare un set di dati in un servizio di terze parti. Se esiste una policy che indica che non è possibile esportare tipi specifici di dati (ad esempio dati personali) e tenti di esportare un set di dati che contiene un’etichetta &quot;I&quot; (dati di identità), riceverai una risposta da [!DNL Policy Service] che segnala la violazione di un criterio di utilizzo dati.

>[!NOTE]
>
>Le azioni di marketing di per sé non limitano l’utilizzo dei dati. Devono essere inclusi nei criteri di utilizzo dei dati abilitati affinché tali azioni possano essere valutate per le violazioni dei criteri.

Quando si verifica un utilizzo dei dati nel servizio dell’organizzazione, è necessario indicare le azioni di marketing pertinenti in modo da poter identificare eventuali violazioni dei criteri. È quindi possibile utilizzare [API del servizio criteri](https://www.adobe.io/experience-platform-apis/references/policy-service/) per verificare la presenza di violazioni dei criteri nell’integrazione.

>[!NOTE]
>
>Puoi impostare casi di utilizzo di marketing sulle destinazioni per automatizzare l’applicazione dei criteri. Consulta la [documentazione sulle destinazioni](../../destinations/home.md) per ulteriori informazioni sulle opzioni di configurazione per la destinazione specifica.

Per un elenco delle opzioni disponibili, vedere l&#39;appendice del presente documento. [azioni di marketing definite dall’Adobe disponibili](#core-actions). Puoi anche definire azioni di marketing personalizzate utilizzando [!DNL Policy Service] API o [!DNL Experience Platform] dell&#39;utente. Ulteriori informazioni sull’utilizzo delle azioni e dei criteri di marketing sono disponibili nella sezione successiva.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## Gestione dei criteri di utilizzo dei dati {#manage}

Una volta applicate le etichette di utilizzo dei dati, gli amministratori dei dati possono utilizzare [!DNL Policy Service] API o [!DNL Experience Platform] Interfaccia utente per gestire e valutare i criteri relativi alle azioni di marketing eseguite sui dati contenenti le etichette di utilizzo dei dati. È possibile creare e aggiornare i criteri, determinare lo stato di un criterio e utilizzare le azioni di marketing per valutare se una specifica azione viola un criterio di utilizzo dei dati.

>[!IMPORTANT]
>
>Tutti i criteri di utilizzo dei dati (inclusi i criteri principali forniti da Adobe) sono disabilitati per impostazione predefinita. Affinché un singolo criterio possa essere preso in considerazione per l’applicazione, devi abilitarlo manualmente tramite l’API o l’interfaccia utente.

Per istruzioni dettagliate sull’utilizzo delle azioni di marketing e dei criteri di utilizzo dei dati nell’API, consulta l’esercitazione su [creazione e valutazione dei criteri di utilizzo dei dati](create.md). Per ulteriori informazioni, consulta le operazioni chiave fornite [!DNL Policy Service] API, consulta [Guida per gli sviluppatori di Policy Service](../api/getting-started.md).

Per informazioni su come utilizzare le azioni e i criteri di marketing in [!DNL Platform] UI, consulta la [guida utente sui criteri di utilizzo dei dati](./user-guide.md).

## Passaggi successivi

Questo documento fornisce un’introduzione ai criteri di utilizzo dei dati all’interno del framework di governance dei dati. Per ulteriori informazioni su come utilizzare i criteri nell’API e nell’interfaccia utente, ora puoi continuare a leggere la documentazione del processo collegata a in questa guida.

## Appendice

La sezione seguente fornisce informazioni aggiuntive sui criteri di utilizzo dei dati.

### Azioni di marketing definite dall’Adobe {#core-actions}

La tabella seguente descrive le azioni di marketing di base fornite per Adobe e pronte all’uso.

>[!NOTE]
>
>Le azioni di marketing di base devono essere considerate come punto di partenza per identificare i criteri di utilizzo da creare e verificare le violazioni. Le definizioni e il modo in cui vengono interpretate dipendono dalle esigenze e dai criteri dell’organizzazione.

| Azione di marketing | Descrizione |
| --- | --- |
| Analytics | Azione che utilizza i dati a scopo di analisi, ad esempio per misurare, analizzare e generare rapporti sull’utilizzo da parte dei clienti dei siti o delle app della tua organizzazione. |
| Combinare con dati direttamente identificabili | Azione che combina qualsiasi PII (Personally Identifiable Information) con dati anonimi. I contratti per i dati provenienti da reti di annunci, server di annunci e fornitori di dati di terze parti spesso includono divieti contrattuali specifici sull’utilizzo di tali dati con dati direttamente identificabili. |
| Targeting tra siti | Azione che utilizza i dati per il targeting di annunci tra siti. La combinazione di dati provenienti da diversi siti, compresa una combinazione di dati nel sito e dati esterni al sito o una combinazione di dati provenienti da diverse fonti esterne al sito, è definita dati intersito. I dati tra siti vengono generalmente raccolti ed elaborati per trarre conclusioni sugli interessi degli utenti. |
| Data Science | Azione che utilizza i dati per i flussi di lavoro di data science. Alcuni contratti includono divieti espliciti sull’uso dei dati per la scienza dei dati. A volte queste sono formulate in termini che vietano l’uso di dati per l’intelligenza artificiale (IA), l’apprendimento automatico (ML) o la modellazione. |
| Targeting e-mail | Azione che utilizza i dati nelle campagne di targeting e-mail. |
| Esporta a terze parti | Azione che esporta dati a processori ed entità che non hanno relazioni dirette con i clienti. Molti fornitori di dati hanno clausole nei contratti che vietano l&#39;esportazione di dati da dove sono stati raccolti originariamente. Ad esempio, i contratti per social network spesso limitano il trasferimento dei dati che ricevi da loro. |
| Pubblicità on-site | Azione che utilizza i dati per gli annunci nel sito, inclusa la selezione e la consegna di annunci sui siti web o sulle app della tua organizzazione, o per misurare la consegna e l’efficacia di tali annunci. |
| Personalizzazione nel sito | Azione che utilizza i dati per la personalizzazione del contenuto nel sito. Per personalizzazione nel sito si intende qualsiasi dato utilizzato per trarre conclusioni sugli interessi degli utenti e per selezionare i contenuti o gli annunci da distribuire in base a tali conclusioni. |
| Corrispondenza segmento | Azione che utilizza i dati per Adobe Experience Platform Segment Match, che consente a due o più utenti di Platform di scambiarsi i dati dei segmenti. Attivando i criteri che fanno riferimento a questa azione, puoi limitare i dati utilizzati per Segment Match. Ad esempio, se il criterio principale &quot;Limita la condivisione dei dati&quot; è abilitato, tutti i dati con un [Etichetta C11](../labels/reference.md#c11) non può essere utilizzato per Segment Match. |
| Personalizzazione di una singola identità | Azione che richiede che una singola identità sia utilizzata a scopo di personalizzazione invece di unire le identità da più origini. |
