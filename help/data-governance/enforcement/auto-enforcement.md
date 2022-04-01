---
keywords: Experience Platform;home;argomenti popolari;applicazione dei criteri;applicazione automatica;applicazione basata su API;governance dei dati
solution: Experience Platform
title: Applicazione automatica dei criteri
topic-legacy: guide
description: Questo documento illustra come i criteri di utilizzo dei dati vengono applicati automaticamente quando si attivano segmenti nelle destinazioni in Experience Platform.
exl-id: c6695285-77df-48c3-9b4c-ccd226bc3f16
source-git-commit: 63705bdcf102ff01b4d67ce5955d8e23b32dbfe6
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 0%

---

# Applicazione automatica delle regole

Una volta etichettati i dati e definiti i criteri di utilizzo, puoi applicare la conformità dell’utilizzo dei dati ai criteri. Quando si attivano i segmenti di pubblico nelle destinazioni, Adobe Experience Platform applica automaticamente i criteri di utilizzo in caso di violazioni.

## Prerequisiti

Questa guida richiede una buona comprensione dei servizi Platform coinvolti nell’applicazione automatica. Per ulteriori informazioni, consulta la seguente documentazione prima di continuare con questa guida:

* [Governance dei dati di Adobe Experience Platform](../home.md): Il framework tramite il quale Platform applica la conformità all’utilizzo dei dati tramite l’uso di etichette e criteri.
* [Profilo cliente in tempo reale](../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Servizio di segmentazione di Adobe Experience Platform](../../segmentation/home.md): Il motore di segmentazione in [!DNL Platform] utilizzato per creare segmenti di pubblico dai profili cliente in base ai comportamenti e agli attributi dei clienti.
* [Destinazioni](../../destinations/home.md): Le destinazioni sono integrazioni predefinite con applicazioni comunemente utilizzate che consentono l’attivazione senza soluzione di continuità dei dati da Platform per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e altro ancora.

## Flusso di applicazione {#flow}

Il diagramma seguente illustra come l’implementazione dei criteri viene integrata nel flusso di dati dell’attivazione dei segmenti:

![](../images/enforcement/enforcement-flow.png)

Quando un segmento viene attivato per la prima volta, [!DNL Policy Service] verifica le politiche applicabili in base ai seguenti fattori:

* Le etichette di utilizzo dei dati applicate ai campi e ai set di dati all’interno del segmento da attivare.
* Scopo di marketing della destinazione.
<!-- * (Beta) The profiles that have consented to be included in the segment activation, based on your configured consent policies. -->

>[!NOTE]
>
>Se esistono etichette di utilizzo dei dati che sono state applicate solo a determinati campi all’interno di un set di dati (anziché all’intero set di dati), l’applicazione di tali etichette a livello di campo all’attivazione si verifica solo nelle seguenti condizioni:
>
>* I campi vengono utilizzati nella definizione del segmento.
>* I campi sono configurati come attributi proiettati per la destinazione di destinazione.


## Linea di dati {#lineage}

La derivazione dei dati svolge un ruolo chiave nel modo in cui i criteri vengono applicati in Platform. In termini generali, la derivazione di dati si riferisce all&#39;origine di un insieme di dati e a ciò che gli accade (o a dove si muove) nel tempo.

Nel contesto della governance dei dati, la derivazione consente alle etichette di utilizzo dei dati di propagarsi dai set di dati ai servizi a valle che utilizzano i loro dati, ad esempio Profilo cliente in tempo reale e destinazioni. Questo consente di valutare e applicare i criteri in diversi punti chiave del percorso di dati tramite Platform e fornisce contesto ai consumatori di dati sul motivo per cui si è verificata una violazione dei criteri.

Ad Experience Platform, l&#39;applicazione delle politiche riguarda la seguente linea di demarcazione:

1. I dati vengono acquisiti in Platform e memorizzati in **set di dati**.
1. I profili dei clienti sono identificati e costruiti a partire da tali set di dati unendo frammenti di dati in base alla **criterio di unione**.
1. I gruppi di profili sono suddivisi in **segmenti** basati su attributi comuni.
1. I segmenti vengono attivati a valle **destinazioni**.

Ogni fase nella timeline di cui sopra rappresenta un’entità che può contribuire alla violazione di un criterio, come descritto nella tabella seguente:

| Fase di derivazione dei dati | Ruolo nell&#39;applicazione delle politiche |
| --- | --- |
| Set di dati | I set di dati contengono etichette di utilizzo dei dati (applicate a livello di set di dati o di campo) che definiscono per quali casi d’uso può essere utilizzato l’intero set di dati o campi specifici. Le violazioni dei criteri si verificano se un set di dati o un campo contenente determinate etichette viene utilizzato per uno scopo limitato da un criterio. |
<!-- | Dataset | Datasets contain data usage labels (applied at the dataset or field level) that define which use cases the entire dataset or specific fields can be used for. Policy violations will occur if a dataset or field containing certain labels is used for a purpose that a policy restricts.<br><br>Any consent attributes collected from your customers are also stored in datasets. If you have access to [consent policies](../policies/user-guide.md#consent-policy) (currently in beta), any profiles that do not meet the consent attribute requirements of your policies will be excluded from segments that are activated to a destination. | -->
| Criteri di unione | I criteri di unione sono le regole utilizzate da Platform per determinare la priorità dei dati durante l’unione di frammenti da più set di dati. Le violazioni dei criteri si verificano se i criteri di unione sono configurati in modo che i set di dati con etichette limitate vengano attivati in una destinazione. Consulta la sezione [panoramica dei criteri di unione](../../profile/merge-policies/overview.md) per ulteriori informazioni. | | Segmento | Le regole del segmento definiscono quali attributi includere dai profili cliente. A seconda dei campi inclusi nella definizione di un segmento, il segmento eredita eventuali etichette di utilizzo applicate a tali campi. Le violazioni dei criteri si verificano se attivi un segmento le cui etichette ereditate sono limitate dai criteri applicabili della destinazione di destinazione, in base al relativo caso d’uso di marketing. |
<!-- | Segment | Segment rules define which attributes should be included from customer profiles. Depending on which fields a segment definition includes, the segment will inherit any applied usage labels for those fields. Policy violations will occur if you activate a segment whose inherited labels are restricted by the target destination's applicable policies, based on its marketing use case. | -->
| Destinazione | Quando si imposta una destinazione, è possibile definire un’azione di marketing (talvolta denominata caso d’uso di marketing). Questo caso d’uso è correlato a un’azione di marketing definita in un criterio. In altre parole, il caso di utilizzo marketing definito per una destinazione determina quali criteri di utilizzo dei dati e i criteri di consenso sono applicabili a tale destinazione. Le violazioni dei criteri si verificano se attivi un segmento le cui etichette di utilizzo sono limitate dai criteri applicabili della destinazione di destinazione. |

>[!IMPORTANT]
>
>Alcuni criteri di utilizzo dei dati possono specificare due o più etichette con una relazione AND. Ad esempio, un criterio potrebbe limitare un’azione di marketing se le etichette `C1` E `C2` sono presenti entrambi, ma non limitano la stessa azione se è presente solo una di queste etichette.
>
>Quando si tratta di applicazione automatica, il framework per la governance dei dati non considera l’attivazione di segmenti separati a una destinazione come una combinazione di dati. Pertanto, l&#39;esempio `C1 AND C2` policy **NOT** applicata se queste etichette sono incluse in segmenti separati. Al contrario, questo criterio viene applicato solo quando entrambe le etichette sono presenti nello stesso segmento al momento dell’attivazione.

Quando si verificano violazioni dei criteri, i messaggi risultanti visualizzati nell’interfaccia utente forniscono strumenti utili per esplorare la linea di dati che contribuiscono alla violazione per risolvere il problema. Ulteriori dettagli sono forniti nella sezione successiva.

## Messaggi di violazione dei criteri {#enforcement}

<!-- (TO INCLUDE FOR PHASE 2)
The sections below outline the different policy enforcement messages that appear in the Platform UI:

* [Data usage policy violation](#data-usage-violation)
* [Consent policy evaluation](#consent-policy-evaluation)

### Data usage policy violation {#data-usage-violation} -->

Se si verifica una violazione di criteri durante il tentativo di attivare un segmento (o [apportare modifiche a un segmento già attivato](#policy-enforcement-for-activated-segments)) l&#39;azione viene impedita e viene visualizzato un manifesto che indica che uno o più criteri sono stati violati. Una volta attivata la violazione, la **[!UICONTROL Salva]** viene disattivato per l’entità che stai modificando fino a quando i componenti appropriati non vengono aggiornati in conformità ai criteri di utilizzo dei dati.

Seleziona una violazione di criteri nella colonna a sinistra del puntatore per visualizzare i dettagli relativi a tale violazione.

![](../images/enforcement/violation-policy-select.png)

Il messaggio di violazione fornisce un riepilogo del criterio violato, incluse le condizioni che il criterio è configurato per controllare, l&#39;azione specifica che ha attivato la violazione e un elenco di possibili risoluzioni del problema.

![](../images/enforcement/violation-summary.png)

Sotto il riepilogo delle violazioni viene visualizzato un grafico della derivazione di dati che consente di visualizzare quali set di dati, criteri di unione, segmenti e destinazioni sono stati coinvolti nella violazione dei criteri. L’entità che stai modificando viene evidenziata nel grafico, indicando quale punto del flusso sta causando la violazione. Puoi selezionare un nome di entità all’interno del grafico per aprire la pagina dei dettagli dell’entità in questione.

![](../images/enforcement/data-lineage.png)

È inoltre possibile utilizzare **[!UICONTROL Filtro]** icona (![](../images/enforcement/filter.png)) per filtrare le entità visualizzate per categoria. Affinché i dati possano essere visualizzati, è necessario selezionare almeno due categorie.

![](../images/enforcement/lineage-filter.png)

Seleziona **[!UICONTROL Vista a elenco]** per visualizzare la derivazione dati come elenco. Per tornare al grafico visivo, seleziona **[!UICONTROL Vista a percorso]**.

![](../images/enforcement/list-view.png)

<!-- (TO INCLUDE FOR PHASE 2)
### Consent policy evaluation (Beta) {#consent-policy-evaluation}

>[!IMPORTANT]
>
>Consent policies are currently in beta and your organization may not have access to them yet.

If you have [created consent policies](../policies/user-guide.md#consent-policy) and are activating a segment to a destination, you can see how your consent policies will affect the percentage of profiles that will be included in the activation.

Once you reach at the **[!UICONTROL Review]** step in the [activation workflow](../../destinations/ui/activation-overview.md), select **[!UICONTROL View applied policies]**.

A policy check dialog appears, showing you a preview of how your consent policies affect the addressable audience of the activated segment.
 -->

## Applicazione dei criteri per i segmenti attivati {#policy-enforcement-for-activated-segments}

L’applicazione dei criteri si applica ancora ai segmenti dopo che sono stati attivati, limitando le modifiche a un segmento o alla sua destinazione che si traducono in una violazione dei criteri. A causa di come [derivazione dati](#lineage) agisce nell&#39;applicazione dei criteri; una delle seguenti azioni può potenzialmente determinare una violazione:

* Aggiornamento delle etichette di utilizzo dei dati
* Modifica dei set di dati per un segmento
* Modifica dei predicati dei segmenti
* Modifica delle configurazioni di destinazione

Se una delle azioni precedenti causa una violazione, tale azione non viene salvata e viene visualizzato un messaggio di violazione dei criteri, garantendo che i segmenti attivati continuino a rispettare i criteri di utilizzo dei dati in fase di modifica.

## Passaggi successivi

In questo documento è stato illustrato il funzionamento, ad Experience Platform, dell&#39;applicazione automatica delle regole. Per informazioni su come integrare programmaticamente l’applicazione dei criteri nelle applicazioni utilizzando le chiamate API, consulta la guida su [Implementazione basata su API](./api-enforcement.md).
