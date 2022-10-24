---
keywords: Experience Platform;interfaccia utente;interfaccia utente;personalizzazione;dashboard utilizzo licenza;dashboard;utilizzo licenza;adesione;consumo
title: Guida al dashboard per l’utilizzo delle licenze
description: Adobe Experience Platform fornisce un dashboard tramite il quale è possibile visualizzare informazioni importanti sull’utilizzo delle licenze dell’organizzazione.
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: e67b3a6f9f57a3971a5bfa755db3b1043bebc96b
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 1%

---

# Dashboard di utilizzo licenze {#license-usage-dashboard}

L’interfaccia utente di Adobe Experience Platform fornisce un dashboard attraverso il quale è possibile visualizzare informazioni importanti sull’utilizzo delle licenze dell’organizzazione, acquisite durante un’istantanea giornaliera. Questa guida illustra come accedere e utilizzare il dashboard per l’utilizzo delle licenze nell’interfaccia utente e fornisce ulteriori informazioni sulle visualizzazioni visualizzate nel dashboard.

Per una panoramica generale dell’interfaccia utente di Platform, visita [Guida all’interfaccia utente di Experience Platform](../../landing/ui-guide.md).

## Dati del dashboard per l’utilizzo della licenza

Nel dashboard sull’utilizzo delle licenze viene visualizzata un’istantanea dei dati relativi alle licenze dell’organizzazione, ad Experience Platform. I dati nel dashboard vengono visualizzati esattamente come vengono visualizzati nel momento specifico in cui è stata scattata l&#39;istantanea. In altre parole, lo snapshot non è un&#39;approssimazione o un esempio dei dati e il dashboard non viene aggiornato in tempo reale.

>[!NOTE]
>
>Eventuali modifiche o aggiornamenti apportati ai dati dall&#39;acquisizione dello snapshot non verranno visualizzati nel dashboard fino all&#39;acquisizione dello snapshot successivo.

## Esplorazione del dashboard di utilizzo della licenza

Per passare al dashboard dell’utilizzo della licenza nell’interfaccia utente di Platform, seleziona **[!UICONTROL Utilizzo della licenza]** nella barra a sinistra. Viene aperta la **[!UICONTROL Panoramica]** scheda che mostra il dashboard.

>[!NOTE]
>
>Il dashboard di utilizzo della licenza non è abilitato per impostazione predefinita. Per poter visualizzare il dashboard, è necessario concedere agli utenti l’autorizzazione &quot;Visualizza dashboard di utilizzo licenze&quot;. Per i passaggi sulla concessione delle autorizzazioni di accesso per visualizzare il dashboard di utilizzo della licenza, fare riferimento al [guida alle autorizzazioni del dashboard](../permissions.md).

![](../images/license-usage/dashboard-overview.png)

### Selezionare una sandbox

Per scegliere una sandbox da visualizzare nel dashboard, selezionate una delle seguenti opzioni [!UICONTROL Produzione] o [!UICONTROL Sviluppo]. La sandbox selezionata è indicata dal pulsante di scelta accanto al nome della sandbox.

La generazione di rapporti sui consumi per le sandbox è cumulativa per tutte le sandbox dello stesso tipo. In altre parole, seleziona [!UICONTROL Produzione] o [!UICONTROL Sviluppo] fornisce rapporti sui consumi per tutte le sandbox di produzione o di sviluppo, rispettivamente.

![](../images/license-usage/select-sandbox.png)

>[!WARNING]
>
>È necessario specificare le autorizzazioni per visualizzare il dashboard di utilizzo della licenza a livello di sandbox. È quindi necessario aggiungere a ogni singolo sandbox l’autorizzazione per visualizzare il dashboard. Questa limitazione verrà affrontata in una versione futura. Nel frattempo, è disponibile la seguente soluzione alternativa:
>
>1. Crea un profilo di prodotto in Adobe Admin Console.
>2. In Autorizzazione nella categoria Sandbox , aggiungi tutte le sandbox che desideri visualizzare nel dashboard di utilizzo della licenza.
>3. Nella categoria Autorizzazione dashboard utente, aggiungi l&#39;autorizzazione &quot;Visualizza dashboard utilizzo licenza&quot;.


### Selezionare un intervallo di date

Dopo aver selezionato una sandbox, puoi utilizzare il menu a discesa dell’intervallo di date per selezionare il periodo di tempo da visualizzare nel dashboard. Sono disponibili più opzioni, tra cui il valore predefinito degli ultimi 30 giorni.

![](../images/license-usage/select-date-range.png)

Puoi anche selezionare **[!UICONTROL Data personalizzata]** per scegliere il periodo di tempo visualizzato.

![](../images/license-usage/select-custom-date.png)

## Widget

Il dashboard per l&#39;utilizzo delle licenze è composto da widget che visualizzano metriche di sola lettura che forniscono informazioni importanti sull&#39;utilizzo delle licenze dell&#39;organizzazione. Le metriche visibili dipendono dalle licenze specifiche della tua organizzazione (consulta la sezione [metriche disponibili](#available-metrics) sezione per i dettagli).

Ogni widget visualizza un grafico a linee che confronta i numeri effettivi per la tua organizzazione con il totale disponibile con le licenze della tua organizzazione e fornisce una percentuale dell&#39;utilizzo totale.

![](../images/license-usage/widgets.png)

## Metriche disponibili

Il dashboard di utilizzo della licenza riporta quattro metriche chiave, con ulteriori metriche da aggiungere nelle versioni successive. Le metriche disponibili sono:

* [!UICONTROL Pubblico indirizzabile]
* [!UICONTROL Ricchezza media del profilo]
* [!UICONTROL Rapporto dati analizzati per segmentazione]
* [!UICONTROL Memoria totale consumata]

La disponibilità di queste metriche e la definizione specifica di ciascuna di esse variano a seconda della licenza acquistata dalla tua organizzazione. Per le definizioni dettagliate di ciascuna metrica, fare riferimento alla documentazione appropriata relativa alla descrizione del prodotto:

| Licenza | Descrizione del prodotto |
|---|---|
| <ul><li>Adobe Experience Platform:OD LITE</li><li>Adobe Experience Platform:OD STANDARD</li><li>Adobe Experience Platform:BUONA PESANTE</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>Adobe Experience Platform:OD</li></ul> | [Experience Platform, servizi app e servizi intelligenti](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>PIATTAFORMA DATI CLIENTE RT:OD</li><li>PIATTAFORMA DATI DEL CLIENTE RT:BUON PRFL A 10M</li><li>PIATTAFORMA DATI DEL CLIENTE RT:DA BUON PRFL A 50M</li></ul> | [Adobe Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP:BUONA ATTIVAZIONE</li><li>AEP:BUONA ATTIVAZIONE PRFL A 10M</li><li>AEP:BUONA ATTIVAZIONE PRFL FINO A 50 M</li></ul> | [Attivazione Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD INTELLIGENCE</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>SELEZIONE Journey Optimizer:OD</li><li>PRIME Journey Optimizer:OD</li><li>Journey Optimizer ULTIMATE:OD</li><li>UNP AJO PRIME STARTER:OD</li><li>UNP AJO ULTIMATE STARTER:OD</li><li>UNP Real-Time CDP:BUONA ORCHESTRAZIONE PROFILO</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>Il dashboard di utilizzo delle licenze riporta solo l’ultima licenza per la quale è stato effettuato il provisioning per la tua organizzazione. Se la licenza più recente fornita per la tua organizzazione non viene visualizzata nella tabella precedente, il dashboard di utilizzo della licenza potrebbe non essere visualizzato correttamente. Il supporto per licenze aggiuntive e licenze multiple in un&#39;unica organizzazione è pianificato per una versione futura.

## Passaggi successivi

Dopo aver letto questo documento, è possibile individuare il dashboard di utilizzo della licenza e selezionare una sandbox da visualizzare. Puoi anche trovare ulteriori informazioni sulle metriche disponibili per la tua organizzazione, in base alla licenza acquistata dalla tua organizzazione.

Per ulteriori informazioni sulle altre funzioni disponibili nell’interfaccia utente di Experience Platform, consulta [Guida all’interfaccia utente di Platform](../../landing/ui-guide.md).
