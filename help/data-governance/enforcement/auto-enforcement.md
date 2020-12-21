---
keywords: Experience Platform;home;popular topics;Policy enforcement;Automatic enforcement;API-based enforcement;data governance
solution: Experience Platform
title: Panoramica dell'applicazione dei criteri
topic: enforcement
description: Questo documento illustra come vengono applicati automaticamente i criteri di utilizzo dei dati quando si attivano segmenti per destinazioni in  Experience Platform.
translation-type: tm+mt
source-git-commit: 385084f3de2ebfcbee94d6b0c116dae82f5df764
workflow-type: tm+mt
source-wordcount: '1109'
ht-degree: 0%

---


# Applicazione automatica delle regole

Una volta etichettati i dati e definiti i criteri di utilizzo, potete applicare la conformità dell&#39;utilizzo dei dati ai criteri. Quando si attivano i segmenti di pubblico alle destinazioni, Adobe Experience Platform applica automaticamente i criteri di utilizzo in caso di violazioni.

## Prerequisiti

Questa guida richiede una buona conoscenza dei servizi della piattaforma coinvolti nell&#39;applicazione automatica. Per ulteriori informazioni, consulta la seguente documentazione prima di continuare con questa guida:

* [Governance](../home.md) dei dati Adobe Experience Platform: Il framework tramite il quale la piattaforma applica la conformità all&#39;utilizzo dei dati tramite l&#39;uso di etichette e criteri.
* [Profilo](../../profile/home.md) cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Servizio](../../segmentation/home.md) di segmentazione Adobe Experience Platform: Il motore di segmentazione  [!DNL Platform] utilizzato per creare segmenti di pubblico dai profili cliente in base ai comportamenti e agli attributi del cliente.
* [Destinazioni](../../destinations/home.md): Le destinazioni sono integrazioni predefinite con applicazioni comunemente utilizzate che consentono l&#39;attivazione senza soluzione di continuità dei dati dalla piattaforma per campagne di marketing multicanale, campagne e-mail, pubblicità mirata e altro ancora.

## Flusso di applicazione {#flow}

Il diagramma seguente illustra come l&#39;implementazione dei criteri è integrata nel flusso di dati dell&#39;attivazione dei segmenti:

![](../images/enforcement/enforcement-flow.png)

Quando un segmento viene attivato per la prima volta, [!DNL Policy Service] verifica la presenza di violazioni dei criteri in base ai seguenti fattori:

* Le etichette di utilizzo dei dati applicate ai campi e ai set di dati all’interno del segmento da attivare.
* Scopo di marketing della destinazione.

>[!NOTE]
>
>Se esistono etichette di utilizzo dei dati che sono state applicate solo a determinati campi all’interno di un set di dati (anziché all’intero set di dati), l’applicazione di tali etichette a livello di campo all’attivazione avviene solo alle seguenti condizioni:
>
>* I campi vengono utilizzati nella definizione del segmento.
>* I campi sono configurati come attributi proiettati per la destinazione di destinazione.


## Linea di dati {#lineage}

La linea di dati svolge un ruolo chiave nel modo in cui i criteri vengono applicati in Piattaforma. In termini generali, la linea di dati si riferisce all&#39;origine di un insieme di dati e a cosa gli accade (o dove si sposta) nel tempo.

Nel contesto di [!DNL Data Governance], la linea consente alle etichette di utilizzo dei dati di propagarsi dai set di dati ai servizi a valle che utilizzano i loro dati, come Profilo cliente in tempo reale e le destinazioni. Questo consente di valutare e applicare le politiche in diversi punti chiave del percorso dei dati attraverso la piattaforma e fornisce contesto ai consumatori di dati in merito al motivo per cui si è verificata una violazione della politica.

In  Experience Platform, l&#39;applicazione delle politiche riguarda la seguente linea di prodotti:

1. I dati vengono trasferiti nella piattaforma e memorizzati in **dataset**.
1. I profili dei clienti sono identificati e costruiti a partire da tali set di dati unendo i frammenti di dati in base al **criterio di unione**.
1. I gruppi di profili sono suddivisi in **segmenti** in base agli attributi comuni.
1. I segmenti sono attivati nelle **destinazioni a valle**.

Ogni fase nella timeline di cui sopra rappresenta un&#39;entità che può contribuire alla violazione di un criterio, come indicato nella tabella seguente:

| Fase di lineamento dei dati | Ruolo nell&#39;applicazione della politica |
| --- | --- |
| Set di dati | I set di dati contengono etichette di utilizzo dei dati (applicate a livello di set di dati o di campi) per le quali è possibile utilizzare l&#39;intero set di dati o campi specifici. Le violazioni dei criteri si verificheranno se un set di dati o un campo contenente determinate etichette viene utilizzato per uno scopo limitato da un criterio. |
| Unisci criterio | I criteri di unione sono regole utilizzate dalla piattaforma per determinare in che modo i dati verranno assegnati priorità durante l&#39;unione di frammenti da più set di dati. Le violazioni dei criteri si verificheranno se i criteri di unione sono configurati in modo che i set di dati con etichette limitate siano attivati a una destinazione. Per ulteriori informazioni, vedere la guida relativa alle [policy di unione](../../profile/ui/merge-policies.md). |
| Segmento | Le regole di segmento definiscono quali attributi devono essere inclusi dai profili cliente. A seconda dei campi inclusi nella definizione di un segmento, il segmento erediterà tutte le etichette di utilizzo applicate a tali campi. Le violazioni dei criteri si verificheranno se attivi un segmento le cui etichette ereditate sono limitate dai criteri applicabili della destinazione di destinazione, in base al relativo caso di utilizzo di marketing. |
| Destinazione | Quando si configura una destinazione, è possibile definire un&#39;azione di marketing (talvolta denominata caso di utilizzo del marketing). Questo caso di utilizzo è correlato a un&#39;azione di marketing come definita in un criterio di utilizzo dei dati. In altre parole, il caso di utilizzo del marketing definito per una destinazione determina quali criteri di utilizzo dei dati sono applicabili a tale destinazione. Le violazioni dei criteri si verificheranno se attivi un segmento le cui etichette di utilizzo sono limitate dai criteri applicabili alla destinazione di destinazione. |

Quando si verificano violazioni dei criteri, i messaggi risultanti visualizzati nell&#39;interfaccia utente forniscono strumenti utili per esplorare la linea di dati che contribuiscono alla violazione per risolvere il problema. Ulteriori dettagli sono forniti nella sezione successiva.

## Messaggi di violazione dei criteri {#enforcement}

Se si verifica una violazione del criterio durante il tentativo di attivare un segmento (o [apportare modifiche a un segmento già attivato](#policy-enforcement-for-activated-segments)), l&#39;azione viene impedita e viene visualizzato un puntatore che indica che uno o più criteri sono stati violati. Dopo l&#39;attivazione di una violazione, il pulsante **[!UICONTROL Save]** viene disabilitato per l&#39;entità che si sta modificando fino a quando i componenti appropriati non vengono aggiornati in modo da rispettare i criteri di utilizzo dei dati.

Selezionate una violazione di criterio nella colonna a sinistra del puntatore per visualizzare i dettagli relativi a tale violazione.

![](../images/enforcement/violation-policy-select.png)

Il messaggio di violazione fornisce un riepilogo del criterio che è stato violato, incluse le condizioni che il criterio è configurato per verificare, l&#39;azione specifica che ha attivato la violazione e un elenco delle possibili risoluzioni del problema.

![](../images/enforcement/violation-summary.png)

Sotto il riepilogo delle violazioni viene visualizzato un grafico della linea di dati che consente di visualizzare quali set di dati, criteri di unione, segmenti e destinazioni sono stati coinvolti nella violazione del criterio. L&#39;entità che si sta modificando è evidenziata nel grafico, indicando quale punto del flusso sta causando la violazione. Potete selezionare un nome entità all&#39;interno del grafico per aprire la pagina dei dettagli per l&#39;entità in questione.

![](../images/enforcement/data-lineage.png)

È inoltre possibile utilizzare l&#39;icona **[!UICONTROL Filter]** (![](../images/enforcement/filter.png)) per filtrare le entità visualizzate per categoria. Affinché i dati possano essere visualizzati, è necessario selezionare almeno due categorie.

![](../images/enforcement/lineage-filter.png)

Selezionare **[!UICONTROL List view]** per visualizzare la linea di dati come elenco. Per tornare al grafico visivo, selezionare **[!UICONTROL Path view]**.

![](../images/enforcement/list-view.png)

## Applicazione dei criteri per i segmenti attivati {#policy-enforcement-for-activated-segments}

L&#39;applicazione dei criteri continua a essere applicata ai segmenti dopo che questi sono stati attivati, limitando le modifiche a un segmento o alla sua destinazione che si tradurrebbero in una violazione dei criteri. A causa di come [la linea di dati](#lineage) funziona nell&#39;applicazione dei criteri, una delle seguenti azioni può potenzialmente determinare una violazione:

* Aggiornamento delle etichette di utilizzo dei dati
* Modifica dei set di dati per un segmento
* Modifica dei predicati dei segmenti
* Modifica delle configurazioni di destinazione

Se una delle azioni di cui sopra genera una violazione, tale azione non viene salvata e viene visualizzato un messaggio di violazione dei criteri, garantendo che i segmenti attivati continuino a rispettare i criteri di utilizzo dei dati quando vengono modificati.

## Passaggi successivi

In questo documento veniva illustrato il funzionamento dell&#39;applicazione automatica dei criteri in  Experience Platform. Per informazioni su come integrare a livello di programmazione l&#39;applicazione dei criteri nelle applicazioni mediante le chiamate API, consultate la guida sull&#39; [imposizione basata sulle API](./api-enforcement.md).