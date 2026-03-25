---
title: Monitorare la segmentazione dei bordi
description: Scopri come utilizzare il dashboard di monitoraggio per osservare la velocità effettiva di segmentazione Edge.
source-git-commit: 809f80c721d6eedf5ee88dbb1cf4bf7e5a413614
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 3%

---


# Monitorare la segmentazione dei bordi

Puoi utilizzare il dashboard di monitoraggio nell’interfaccia utente di Adobe Experience Platform per eseguire il monitoraggio in tempo reale della segmentazione Edge all’interno della tua organizzazione. Utilizza questa funzione per accedere a una maggiore trasparenza nella velocità effettiva dei dati edge.

## Introduzione

Questa guida richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Flussi di dati](../../datastreams/overview.md): i flussi di dati ti consentono di collegare Experience Platform Edge Network al set di dati.
* [Capacità](../../landing/license-usage-and-guardrails/capacity.md): in Experience Platform, le capacità ti informano se la tua organizzazione ha superato uno dei tuoi guardrail e ti forniscono informazioni su come risolvere questi problemi.
* [Segmentazione di Edge](../../segmentation/methods/edge-segmentation.md): la segmentazione di Edge è la capacità di valutare istantaneamente le definizioni dei segmenti in Adobe Experience Platform [sul perimetro](../../landing/edge-and-hub-comparison.md), abilitando casi di utilizzo di personalizzazione della stessa pagina e della pagina successiva.

## Accesso {#access}

Per accedere al dashboard di monitoraggio per la velocità effettiva di segmentazione Edge, selezionare **[!UICONTROL Monitoring]** nella sezione **[!UICONTROL Data management]**, seguito da **[!UICONTROL Edge]**.

![Il metodo per accedere al dashboard di segmentazione dei bordi del monitoraggio è evidenziato.](/help/dataflows/assets/ui/monitor-edge/access.png)

Viene visualizzato il dashboard di monitoraggio. Mostra le metriche di monitoraggio per la velocità effettiva dello streaming Edge, un grafico che mostra la velocità effettiva dello streaming Edge e una vista dello stream di dati. Queste metriche possono essere filtrate per servizio, per edge e per data.

![Le opzioni di filtro all&#39;interno del dashboard di monitoraggio sono evidenziate.](/help/dataflows/assets/ui/monitor-edge/filtering.png)

>[!NOTE]
>
>Se selezioni **, puoi visualizzare solo** 1&rbrace; la visualizzazione dello stream di dati.[!UICONTROL Edge segmentation throughput]

Se si filtra in base al servizio, è possibile scegliere il servizio di cui visualizzare le informazioni sulla velocità effettiva. Ciò include servizi come segmentazione di Edge, raccolta dati, Target, Adobe Journey Optimizer, Offer Decisioning, destinazioni personalizzate personalizzate personalizzate, inoltro eventi, Adobe Analytics e Adobe Audience Manager.

Se si filtra in base al bordo, è possibile scegliere il bordo di cui si desidera visualizzare le informazioni. Gli spigoli supportati sono la costa orientale degli Stati Uniti, la costa occidentale degli Stati Uniti, l&#39;Europa, l&#39;India, Singapore, l&#39;Australia, il Giappone e la Svizzera. Potete selezionare più spigoli da visualizzare contemporaneamente.

Se si filtra per data, è possibile scegliere la scala cronologica per filtrare gli eventi. Questa scala cronologica può essere impostata fino a 30 giorni. In alternativa, è possibile utilizzare una delle seguenti scale temporali preconfigurate: [!UICONTROL Last 6 hours], [!UICONTROL Last 12 hours], [!UICONTROL Last 24 hours], [!UICONTROL Last 7 days] e [!UICONTROL Last 30 days].

## Metriche di monitoraggio per la velocità effettiva Edge

La tabella delle metriche fornisce informazioni specifiche sulla velocità effettiva Edge del servizio selezionato. Per ulteriori informazioni su ciascuna colonna, consulta la tabella seguente.

| Metrica | Descrizione |
| ------ | ----------- |
| Richieste ricevute | Il numero di richieste ricevute dai bordi selezionati entro l’intervallo di tempo. |
| Velocità massima | Il tasso più alto di richieste ricevute dai bordi selezionati nell’arco temporale. |

{style="table-layout:auto"}

## Grafico di monitoraggio per la velocità effettiva di segmentazione Edge

Il grafico di monitoraggio mostra i record ricevuti al secondo dagli spigoli selezionati entro l’intervallo di tempo assegnato, rispetto alla capacità massima consentita.

![Viene visualizzato il grafico della velocità effettiva di segmentazione Edge.](/help/dataflows/assets/ui/monitor-edge/edge-segmentation-throughput.png)

## Vista stream di dati

>[!NOTE]
>
>La visualizzazione dello stream di dati è **solo** disponibile se si sta filtrando la velocità effettiva di segmentazione di Edge.

Nella sezione di visualizzazione dello stream di dati viene visualizzato un elenco degli ultimi stream di dati che hanno attraversato i bordi della sandbox.

![Viene visualizzata la visualizzazione dello stream di dati, con le informazioni sugli stream di dati elencati.](/help/dataflows/assets/ui/monitor-edge/datastream-view.png)

| Campo | Descrizione |
| ----- | ----------- |
| Nome stream di dati | Nome dello stream di dati. |
| Set di dati | Il nome dei set di dati a cui appartiene il flusso di dati. |
| Servizio abilitato | Nomi dei servizi per i quali è abilitato lo stream di dati. |
| Richieste | Il numero di richieste passate attraverso lo stream di dati. |
| Velocità massima | Il più alto tasso di richieste passate attraverso lo stream di dati. |
