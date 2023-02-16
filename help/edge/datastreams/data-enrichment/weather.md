---
title: Usa i dati meteo da DNL The Weather Channel
description: Utilizza i dati meteo da DNL The Weather Channel per migliorare i dati raccolti attraverso i datastreams.
source-git-commit: b53be9f2f2d55d5f9e8081fb0ca6732dcc2a8c11
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 3%

---


# Usa dati meteo da [!DNL The Weather Channel]

L&#39;Adobe ha collaborato con [!DNL [The Weather Company]](https://www.ibm.com/weather) portare il contesto aggiuntivo del meteo degli Stati Uniti ai dati raccolti tramite datastreams. Puoi utilizzare questi dati per analisi, targeting e creazione di segmenti in Experience Platform.

Sono disponibili 3 tipi di dati da [!DNL The Weather Channel]:

* **[!UICONTROL Tempo attuale]**: Le condizioni meteorologiche correnti dell&#39;utente, in base alla loro posizione. Ciò include la temperatura attuale, la percipitazioni, la copertura del cloud e altro ancora.
* **[!UICONTROL Tempo previsto]**: La previsione include la previsione di 1,2,3,5,7 e 10 giorni per la posizione dell&#39;utente.
* **[!UICONTROL Triggers]**: Triggers sono combinazioni specifiche che si associano a diverse condizioni meteo semantiche. Ci sono tre diversi tipi di trigger del tempo:

   * **[!UICONTROL Trigger del tempo]**: Condizioni semanticamente significative, come il freddo o il tempo piovoso. Questi possono differire nelle loro definizioni tra i vari climi.
   * **[!UICONTROL Trigger dei prodotti]**: Condizioni che condurrebbero all&#39;acquisto di diversi tipi di prodotti. Ad esempio: le previsioni del tempo freddo potrebbero significare che gli acquisti di giacche piovane sono più probabili.
   * **[!UICONTROL Gravi condizioni meteorologiche]**: Avvertenze meteorologiche gravi, come le tempeste d&#39;inverno o gli avvertimenti di uragani.

## Prerequisiti {#prerequisites}

Prima di utilizzare i dati meteo, assicurati di soddisfare i seguenti prerequisiti:

* È necessario richiedere la licenza per i dati meteo che verranno utilizzati, da [!DNL The Weather Channel]. L&#39;attiveranno quindi sul tuo account.
* I dati meteo sono disponibili solo tramite datastreams. Per utilizzare i dati meteo, è necessario utilizzare [!DNL Web SDK], [!DNL Mobile Edge Extension] o [API server](../../../server-api/overview.md) per sfruttare questi dati.
* Il tuo datastream deve avere [[!UICONTROL Posizione geografica]](../configure.md#advanced-options) abilitato.
* Aggiungi il [gruppo meteo](#schema-configuration) allo schema in uso.

## Provisioning {#provisioning}

Dopo aver concesso la licenza per i dati da [!DNL The Weather Channel], consentiranno al tuo account di accedere ai dati. Successivamente, devi contattare l’Assistenza clienti Adobe per far sì che i dati siano abilitati sul tuo datastream. Una volta abilitati, i dati vengono aggiunti automaticamente.

Puoi verificare che venga aggiunto eseguendo una traccia Edge con il debugger o utilizzando Assurance per tracciare un hit tramite [!DNL Edge Network].

### Configurazione dello schema {#schema-configuration}

È necessario aggiungere i gruppi di campi meteo allo schema Experience Platform corrispondente al set di dati dell’evento utilizzato nel datastream. Sono disponibili cinque gruppi di campi:

* [!UICONTROL Tempo previsto]
* [!UICONTROL Tempo attuale]
* [!UICONTROL Trigger dei prodotti]
* [!UICONTROL Trigger relativi]
* [!UICONTROL Gravi condizioni meteorologiche]

## Accedere ai dati meteo {#access-weather-data}

Una volta che i dati sono concessi in licenza e disponibili, puoi accedervi in diversi modi in tutti i servizi Adobe.

### Adobe Analytics {#analytics}

In [!DNL Adobe Analytics], i dati meteo sono disponibili per la mappatura tramite regole di elaborazione, insieme al resto del [!DNL XDM] schema.

Puoi trovare l’elenco dei campi che puoi mappare nella sezione [riferimento meteo](weather-reference.md) pagina. Come per tutti [!DNL XDM] schemi, le chiavi hanno il prefisso `a.x`. Ad esempio, un campo denominato `weather.current.temperature.farenheit` si presentava [!DNL Analytics] come `a.x.weather.current.temperature.farenheit`.

![Interfaccia delle regole di elaborazione](../../assets/datastreams/data-enrichment/weather/processing-rules.png)

### Adobe Customer Journey Analytics {#cja}

In [!DNL Adobe Customer Journey Analytics], i dati meteo sono disponibili nel set di dati specificato nel datastream . Se gli attributi meteo sono [aggiunto allo schema](#prerequisites-prerequisites), saranno disponibili per [aggiunta a una visualizzazione dati](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=it) in [!DNL Customer Journey Analytics].

### Real-Time Customer Data Platform {#rtcdp}

I dati meteo sono disponibili nella sezione [Real-time Customer Data Platform](../../../rtcdp/overview.md), da utilizzare nei segmenti. I dati meteo sono allegati agli eventi.

![Generatore di segmenti che mostra gli eventi meteo](../../assets/datastreams/data-enrichment/weather/schema-builder.png)

Poiché le condizioni meteo cambiano spesso, Adobe consiglia di impostare vincoli di tempo sui segmenti, come illustrato nell’esempio precedente. Avere un giorno freddo nell&#39;ultimo giorno o due è molto più incisivo che avere un giorno freddo 6 mesi fa.

Consulta la sezione [riferimento meteo](weather-reference.md) per i campi disponibili.

### Adobe Target {#target}

In [!DNL Adobe Target], puoi utilizzare i dati meteo per favorire la personalizzazione in tempo reale. I dati meteo vengono trasmessi a [!DNL Target] come [!UICONTROL mBox] e puoi accedervi tramite un [!UICONTROL mBox] parametro .

![Target Audience Builder](../../assets/datastreams/data-enrichment/weather/target-audience-builder.png)

Il parametro è il [!DNL XDM] percorso di un campo specifico. Consulta la sezione [riferimento meteo](weather-reference.md) per i campi disponibili e i percorsi corrispondenti.

## Passaggi successivi {#next-steps}

Dopo aver letto questo documento, ora hai una migliore comprensione di come utilizzare i dati meteo tra varie soluzioni di Adobe. Per ulteriori informazioni sulla mappatura dei campi dati meteo, consulta la sezione [riferimento alla mappatura dei campi](weather-reference.md).