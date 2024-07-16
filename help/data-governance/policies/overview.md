---
keywords: Experience Platform;home;argomenti popolari;dule;DULE
solution: Experience Platform
title: Panoramica dei criteri di utilizzo dei dati
description: I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing che possono essere eseguiti o meno sui dati in Adobe Experience Platform.
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: e5d90b24dad7faa9aa31c3b0670f8efa69cf0334
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 17%

---

# Panoramica dei criteri di utilizzo dei dati {#policies-overview}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_restrictusage"
>title="Limitare l’utilizzo dei dati"
>abstract="Il tipo di criterio di utilizzo dei dati valuta azioni di marketing specifiche applicate alle etichette di governance dei dati per limitare l’utilizzo dei dati nelle attività di marketing."

Affinché le etichette di utilizzo dei dati supportino in modo efficace la conformità, è necessario implementare i criteri di utilizzo dei dati. I criteri di utilizzo dei dati sono regole che descrivono i tipi di azioni di marketing che possono essere eseguiti o meno sui dati in [!DNL Experience Platform].

Sono disponibili due tipi di criteri:

* **[!UICONTROL Criteri di governance dei dati]**: limita l&#39;attivazione dei dati in base all&#39;azione di marketing in esecuzione e alle etichette di utilizzo dei dati presenti nei dati in questione.
* **[!UICONTROL Criteri di consenso]**: filtra i profili che possono essere attivati in [destinazioni](../../destinations/home.md) in base al consenso o alle preferenze dei tuoi clienti

>[!NOTE]
>
>I criteri di utilizzo dei dati non devono essere confusi con i [criteri di controllo dell&#39;accesso](../../access-control/abac/end-to-end-guide.md#policy), che determinano se alcuni utenti di Platform nella tua organizzazione possono accedere a determinati campi di dati, e sono configurati tramite la scheda [!UICONTROL Autorizzazioni].

Questo documento fornisce una panoramica di alto livello dei criteri di utilizzo dei dati e fornisce collegamenti a ulteriore documentazione sull’utilizzo dei criteri nell’interfaccia utente o nell’API.

## Azioni marketing {#marketing-actions}

Le azioni di marketing, dette anche casi di utilizzo di marketing, nel contesto del framework di governance dei dati, sono azioni che un consumatore di dati [!DNL Experience Platform] può intraprendere, per le quali l&#39;organizzazione desidera limitare l&#39;utilizzo dei dati. Di conseguenza, i criteri di utilizzo dei dati sono definiti dai seguenti elementi:

1. Un’azione di marketing specifica
2. Le condizioni alle quali tale azione è limitata

Un esempio di azione di marketing potrebbe essere il desiderio di esportare un set di dati in un servizio di terze parti. Se è presente un criterio che indica che non è possibile esportare tipi specifici di dati (ad esempio dati personali) e si tenta di esportare un set di dati che contiene un&#39;etichetta &quot;I&quot; (dati di identità), verrà inviata una risposta da [!DNL Policy Service] in cui si informa che un criterio di utilizzo dati è stato violato.

>[!NOTE]
>
>Le azioni di marketing di per sé non limitano l’utilizzo dei dati. Devono essere inclusi nei criteri di utilizzo dei dati abilitati affinché tali azioni possano essere valutate per le violazioni dei criteri.

Quando si verifica un utilizzo dei dati nel servizio dell’organizzazione, è necessario indicare le azioni di marketing pertinenti in modo da poter identificare eventuali violazioni dei criteri. È quindi possibile utilizzare l&#39;[API del servizio criteri](https://www.adobe.io/experience-platform-apis/references/policy-service/) per verificare la presenza di violazioni dei criteri nell&#39;integrazione.

>[!NOTE]
>
>Puoi impostare casi di utilizzo di marketing sulle destinazioni per automatizzare l’applicazione dei criteri. Per ulteriori informazioni sulle opzioni di configurazione per la destinazione specifica, consulta la [documentazione sulle destinazioni](../../destinations/home.md).

Consulta l&#39;appendice di questo documento per un elenco delle [azioni di marketing disponibili definite dall&#39;Adobe](#core-actions). È inoltre possibile definire azioni di marketing personalizzate utilizzando l&#39;API [!DNL Policy Service] o l&#39;interfaccia utente [!DNL Experience Platform]. Ulteriori informazioni sull’utilizzo delle azioni e dei criteri di marketing sono disponibili nella sezione successiva.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share audiences with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager audiences are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## Gestione dei criteri di utilizzo dei dati {#manage}

Dopo aver applicato le etichette di utilizzo dei dati, gli amministratori dei dati possono utilizzare l&#39;API [!DNL Policy Service] o l&#39;interfaccia utente [!DNL Experience Platform] per gestire e valutare i criteri relativi alle azioni di marketing eseguite sui dati contenenti le etichette di utilizzo dei dati. È possibile creare e aggiornare i criteri, determinare lo stato di un criterio e utilizzare le azioni di marketing per valutare se una specifica azione viola un criterio di utilizzo dei dati.

>[!IMPORTANT]
>
>Tutti i criteri di utilizzo dei dati (inclusi i criteri principali forniti da Adobe) sono disabilitati per impostazione predefinita. Affinché un singolo criterio possa essere preso in considerazione per l’applicazione, devi abilitarlo manualmente tramite l’API o l’interfaccia utente.

Per istruzioni dettagliate sull&#39;utilizzo delle azioni di marketing e dei criteri di utilizzo dei dati nell&#39;API, consulta il tutorial su [creazione e valutazione dei criteri di utilizzo dei dati](create.md). Per ulteriori informazioni sulle operazioni chiave fornite dall&#39;API [!DNL Policy Service], vedere la [Guida per gli sviluppatori del servizio criteri](../api/getting-started.md).

Per informazioni su come utilizzare le azioni e i criteri di marketing nell&#39;interfaccia utente di [!DNL Platform], vedere la [guida utente dei criteri di utilizzo dei dati](./user-guide.md).

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
| Combinare con dati direttamente identificabili | Azione che combina qualsiasi informazione che consenta l’identificazione delle persone (PII) con dati anonimi. I contratti per dati provenienti da reti di annunci, server di annunci e fornitori di dati di terze parti spesso includono divieti contrattuali specifici sull’uso di tali dati direttamente identificabili. |
| Targeting tra siti | Azione che utilizza i dati per il targeting di annunci tra siti. La combinazione di dati provenienti da diversi siti, compresa una combinazione di dati nel sito e dati esterni al sito o una combinazione di dati provenienti da diverse fonti esterne al sito, è definita dati intersito. I dati tra siti vengono generalmente raccolti ed elaborati per trarre conclusioni sugli interessi degli utenti. |
| Data science | Azione che utilizza i dati per i flussi di lavoro di data science. Alcuni contratti includono divieti espliciti sull’uso dei dati per la data science. A volte tali condizioni sono formulate in termini che vietano l’uso di dati per l’intelligenza artificiale (IA), l’apprendimento automatico (ML) o la modellazione. |
| Esportazione dati | Azione che esporta dati in qualsiasi posizione o destinazione al di fuori di prodotti e servizi di Adobe. Ad esempio, puoi scaricare i dati nel computer locale, copiarli dalla schermata, pianificare la consegna dei dati a una posizione esterna a Adobe, progetti pianificati dal Customer Journey Analytics, scaricare rapporti, API di reporting e così via. |
| Targeting via e-mail | Azione che utilizza i dati nelle campagne di targeting e-mail. |
| Esporta a terze parti | Azione che esporta dati a processori ed entità che non hanno relazioni dirette con i clienti. Molti fornitori di dati hanno clausole nei contratti che vietano l’esportazione di dati da dove sono stati raccolti originariamente. Ad esempio, i contratti per social network spesso limitano il trasferimento dei dati che ricevi da essi. |
| Advertising on-site | Azione che utilizza i dati per gli annunci nel sito, inclusa la selezione e la consegna di annunci sui siti web o sulle app della tua organizzazione, o per misurare la consegna e l’efficacia di tali annunci. |
| Personalization on-site | Azione che utilizza i dati per la personalizzazione del contenuto nel sito. Per personalizzazione nel sito si intende qualsiasi dato utilizzato per trarre conclusioni sugli interessi degli utenti e per selezionare i contenuti o gli annunci da distribuire in base a tali conclusioni. |
| Corrispondenza segmento | Azione che utilizza i dati per Adobe Experience Platform Segment Match, che consente a due o più utenti di Platform di scambiarsi i dati sul pubblico. Attivando i criteri che fanno riferimento a questa azione, puoi limitare i dati utilizzati per Segment Match. Ad esempio, se il criterio principale &quot;Limita condivisione dati&quot; è abilitato, tutti i dati con un&#39;etichetta [C11](../labels/reference.md#c11) non possono essere utilizzati per Segment Match. |
| Personalization a identità singola | Azione che richiede che una singola identità sia utilizzata a scopo di personalizzazione anziché unire le identità da più sorgenti. |
