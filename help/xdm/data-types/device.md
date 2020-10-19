---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;device;datatype;data-type;data type;
solution: Experience Platform
title: Tipo di dati dispositivo
topic: overview
description: Questo documento fornisce una panoramica del tipo di dati XDM dispositivo.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 4%

---


# [!UICONTROL Device] tipo di dati

[!UICONTROL Device] è un tipo di dati XDM standard che descrive un dispositivo identificato. Un dispositivo è un&#39;istanza di applicazione o browser che può essere tracciata tra le sessioni, normalmente tramite cookie.

<img src="../images/data-types/device.png" width="450" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `colorDepth` | Intero | Il numero di colori che il display è in grado di rappresentare. |
| `manufacturer` | Stringa | Nome dell&#39;organizzazione proprietaria della progettazione e della creazione del dispositivo. |
| `model` | Stringa | Nome del modello per il dispositivo. Questo è il nome comune, leggibile dall&#39;uomo o di marketing del dispositivo. Ad esempio, &quot;iPhone 6S&quot; è un modello particolare di telefono cellulare. |
| `modelNumber` | Stringa | La designazione univoca del numero del modello assegnata dal produttore per questo dispositivo. I numeri dei modelli non sono versioni, ma identificatori univoci che identificano una particolare configurazione del modello. |
| `screenHeight` | Intero | Il numero di pixel verticali della visualizzazione attiva del dispositivo nell&#39;orientamento predefinito. |
| `screenOrientation` | Stringa | L&#39;orientamento dello schermo corrente. I valori accettati includono `portrait` e `landscape`. |
| `screenWidth` | Stringa | Il numero di pixel orizzontali della visualizzazione attiva del dispositivo nell&#39;orientamento predefinito. |
| `type` | Stringa | Tipo di dispositivo di cui tenere traccia. I valori accettati includono: <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | Stringa | Identificatore del dispositivo. Può trattarsi di un identificatore di DeviceAtlas o di un altro servizio che identifica l&#39;hardware utilizzato. |
| `typeIDService` | Stringa | Spazio dei nomi del servizio utilizzato per identificare il tipo di dispositivo. Per informazioni dettagliate sui valori accettati, consultare l&#39; [appendice](#typeIDService) . |

Per ulteriori dettagli sul mixin, fare riferimento al repository XDM pubblico:

* [Esempio compilato](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## Appendice

La sezione seguente contiene informazioni aggiuntive sul tipo di [!UICONTROL Device] dati.

## Valori accettati per typeIDService {#typeIDService}

Nella tabella seguente sono riportati i valori accettati per `typeIDService` e i significati associati:

| Valore | Descrizione |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | Il dispositivo è stato identificato tramite DeviceAtlas. |
| `https://ns.adobe.com/xdm/external/adobecampaign` | Il dispositivo è stato identificato tramite  Adobe Campaign. |