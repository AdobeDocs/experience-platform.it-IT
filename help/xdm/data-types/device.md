---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;dispositivo;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati dispositivo
description: Scopri il tipo di dati XDM per dispositivo.
exl-id: 049a2ca1-6bc3-4b9c-832a-77102e8a0ed2
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 17%

---

# Tipo di dati [!UICONTROL Dispositivo]

[!UICONTROL Il dispositivo] è un tipo di dati XDM standard che descrive un dispositivo identificato. Un dispositivo è un’applicazione o un’istanza del browser tracciabile nelle sessioni, normalmente tramite i cookie.

![](../images/data-types/device.png){width=450}

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `colorDepth` | Intero | Il numero di colori che il display è in grado di rappresentare. |
| `manufacturer` | Stringa | Il nome dell’organizzazione proprietaria del design e della creazione del dispositivo. |
| `model` | Stringa | Nome del modello del dispositivo. Questo è il nome comune, leggibile o commerciale del dispositivo. Ad esempio, &quot;iPhone 6S&quot; è un particolare modello di telefono cellulare. |
| `modelNumber` | Stringa | La designazione univoca del numero di modello assegnata dal fabbricante a questo dispositivo. I numeri di modello non sono versioni, ma identificatori univoci che identificano una particolare configurazione del modello. |
| `screenHeight` | Intero | Il numero di pixel verticali del display attivo del dispositivo nell’orientamento predefinito. |
| `screenOrientation` | Stringa | L&#39;orientamento corrente dello schermo. I valori accettati includono `portrait` e `landscape`. |
| `screenWidth` | Stringa | Il numero di pixel orizzontali del display attivo del dispositivo nell’orientamento predefinito. |
| `type` | Stringa | Tipo di dispositivo tracciato. I valori accettati includono: <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | Stringa | Identificatore del dispositivo. Può trattarsi di un identificatore di DeviceAtlas o di un altro servizio che identifica l’hardware in uso. |
| `typeIDService` | Stringa | Spazio dei nomi del servizio utilizzato per identificare il tipo di dispositivo. Per informazioni dettagliate sui valori accettati, vedere [appendice](#typeIDService). |

{style="table-layout:auto"}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## Appendice

La sezione seguente contiene informazioni aggiuntive sul tipo di dati [!UICONTROL Device].

## Valori accettati per typeIDService {#typeIDService}

Nella tabella seguente vengono illustrati i valori accettati per `typeIDService` e i relativi significati associati:

| Valore | Descrizione |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | Il dispositivo è stato identificato tramite DeviceAtlas. |
| `https://ns.adobe.com/xdm/external/adobecampaign` | Il dispositivo è stato identificato tramite Adobe Campaign. |
