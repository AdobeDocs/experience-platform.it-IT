---
title: Usa i dati meteo da DNL The Weather Channel
description: Utilizza i dati meteo da DNL The Weather Channel per migliorare i dati raccolti attraverso gli stream di dati.
exl-id: 548dfca7-2548-46ac-9c7e-8190d64dd0a4
source-git-commit: 4c9abcefb279c6e8a90744b692d86746a4896d0a
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 3%

---

# Utilizza i dati meteo da [!DNL The Weather Channel]

L’Adobe ha collaborato con [!DNL [The Weather Company]](https://www.ibm.com/weather) per portare il contesto aggiuntivo del meteo americano ai dati raccolti tramite flussi di dati. Puoi utilizzare questi dati per l’analisi, il targeting e la creazione di segmenti in Experience Platform.

Sono disponibili 3 tipi di dati da [!DNL The Weather Channel]:

* **[!UICONTROL Condizioni meteorologiche attuali]**: le condizioni meteo correnti dell’utente, in base alla sua posizione. Ciò include la temperatura corrente, le precipitazioni, la copertura nuvolosa e altro ancora.
* **[!UICONTROL Tempo previsto]**: la previsione include le previsioni a 1,2,3,5,7 e 10 giorni per l’ubicazione utente.
* **[!UICONTROL Triggers]**: gli attivatori sono combinazioni specifiche che si associano a diverse condizioni meteo semantiche. Esistono tre diversi tipi di fattori scatenanti:

   * **[!UICONTROL Attivatori meteo]**: condizioni semanticamente significative, come tempo freddo o piovoso. Questi possono differire nelle loro definizioni tra i vari climi.
   * **[!UICONTROL Attivatori prodotto]**: condizioni che porterebbero all’acquisto di diversi tipi di prodotti. Ad esempio: le previsioni del freddo potrebbero indicare che gli acquisti di impermeabili sono più probabili.
   * **[!UICONTROL Condizioni Meteorologiche Avverse]**: Avvisi meteorologici severi, come tempeste invernali o avvertenze di uragani.

## Prerequisiti {#prerequisites}

Prima di utilizzare i dati meteo, è necessario soddisfare i seguenti prerequisiti:

* Devi ottenere la licenza per i dati meteo che userai, da [!DNL The Weather Channel]. Quindi lo abiliteranno sul tuo account.
* I dati meteo sono disponibili solo attraverso flussi di dati. Per utilizzare i dati meteo, è necessario utilizzare [!DNL Web SDK], [!DNL Mobile Edge Extension] o [API server](../../server-api/overview.md) per sfruttare questi dati.
* Lo stream di dati deve avere [[!UICONTROL Geolocalizzazione]](../configure.md#advanced-options) abilitato.
* Aggiungi il [gruppo di campi meteo](#schema-configuration) allo schema in uso.

## Provisioning {#provisioning}

Dopo aver concesso la licenza ai dati da [!DNL The Weather Channel], consentiranno al tuo account di accedere ai dati. Successivamente, devi contattare l’Assistenza clienti Adobe per far sì che i dati siano abilitati nel flusso di dati. Una volta abilitati, i dati verranno aggiunti automaticamente.

Puoi convalidarne l’aggiunta eseguendo una traccia Edge con il debugger o utilizzando Assurance per tracciare un hit attraverso [!DNL Edge Network].

### Configurazione dello schema {#schema-configuration}

Devi aggiungere i gruppi di campi meteo allo schema di Experience Platform corrispondente al set di dati dell’evento che stai utilizzando nel flusso di dati. Sono disponibili cinque gruppi di campi:

* [!UICONTROL Tempo previsto]
* [!UICONTROL Condizioni meteorologiche attuali]
* [!UICONTROL Attivatori prodotto]
* [!UICONTROL Trigger relativi]
* [!UICONTROL Condizioni Meteorologiche Avverse]

## Accedere ai dati meteo {#access-weather-data}

Una volta che i dati sono concessi in licenza e disponibili, puoi accedervi in diversi modi in tutti i servizi Adobe.

### Adobe Analytics {#analytics}

In entrata [!DNL Adobe Analytics], i dati meteo sono disponibili per la mappatura tramite regole di elaborazione, insieme al resto [!DNL XDM] schema.

Puoi trovare l’elenco dei campi che puoi mappare in [riferimento meteo](weather-reference.md) pagina. Come per tutti [!DNL XDM] negli schemi, le chiavi hanno il prefisso `a.x`. Ad esempio, un campo denominato `weather.current.temperature.farenheit` verrebbe visualizzato in [!DNL Analytics] as `a.x.weather.current.temperature.farenheit`.

![Interfaccia regola di elaborazione](../assets/data-enrichment/weather/processing-rules.png)

### Adobe Customer Journey Analytics {#cja}

In entrata [!DNL Adobe Customer Journey Analytics], i dati meteo sono disponibili nel set di dati specificato nel flusso di dati. Se gli attributi meteo sono [aggiunto allo schema](#prerequisites-prerequisites), saranno disponibili per [aggiungere a una visualizzazione dati](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=it) in [!DNL Customer Journey Analytics].

### Real-Time Customer Data Platform {#rtcdp}

I dati meteorologici sono disponibili nel [Real-time Customer Data Platform](../../rtcdp/overview.md), per l’utilizzo in segmenti. I dati meteo sono allegati agli eventi.

![Generatore di segmenti che mostra gli eventi meteo](../assets/data-enrichment/weather/schema-builder.png)

Poiché le condizioni meteorologiche cambiano spesso, Adobe consiglia di impostare vincoli di tempo sui segmenti, come illustrato nell’esempio precedente. Avere un giorno freddo nell&#39;ultimo giorno o due è molto più importante che avere un giorno freddo 6 mesi fa.

Consulta la [riferimento meteo](weather-reference.md) per i campi disponibili.

### Adobe Target {#target}

In entrata [!DNL Adobe Target], puoi utilizzare i dati meteo per promuovere la personalizzazione in tempo reale. I dati meteo vengono trasmessi a [!DNL Target] as [!UICONTROL mBox] e puoi accedervi tramite un [!UICONTROL mBox] parametro.

![Generatore di pubblico di Target](../assets/data-enrichment/weather/target-audience-builder.png)

Il parametro è [!DNL XDM] percorso di un campo specifico. Consulta la [riferimento meteo](weather-reference.md) per i campi disponibili e i percorsi corrispondenti.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora hai una migliore comprensione di come utilizzare i dati meteo nelle varie soluzioni di Adobe. Per ulteriori informazioni sulla mappatura dei campi dei dati meteo, vedi [riferimento mappatura campo](weather-reference.md).
