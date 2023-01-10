---
keywords: Experience Platform;home;argomenti popolari;schema;schema;XDM;campi;schemi;schemi;dispositivo;tipo di dati;tipo di dati;tipo di dati;tipo di dati;
solution: Experience Platform
title: Tipo di dati dispositivo
description: Questo documento fornisce una panoramica del tipo di dati Device XDM.
exl-id: 049a2ca1-6bc3-4b9c-832a-77102e8a0ed2
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 6%

---

# [!UICONTROL Dispositivo] tipo di dati

[!UICONTROL Dispositivo] è un tipo di dati XDM standard che descrive un dispositivo identificato. Un dispositivo è un&#39;applicazione o un&#39;istanza del browser che può essere monitorata attraverso le sessioni, normalmente tramite i cookie.

<img src="../images/data-types/device.png" width="450" /><br />

| Proprietà | Tipo di dati | Descrizione |
| --- | --- | --- |
| `colorDepth` | Intero | Il numero di colori che il display è in grado di rappresentare. |
| `manufacturer` | Stringa | Nome dell’organizzazione a cui appartiene la progettazione e la creazione del dispositivo. |
| `model` | Stringa | Nome del modello del dispositivo. Questo è il nome comune, leggibile dall’utente o di marketing del dispositivo. Ad esempio, &quot;iPhone 6S&quot; è un particolare modello di telefono cellulare. |
| `modelNumber` | Stringa | La designazione univoca del numero di modello assegnata dal costruttore per questo dispositivo. I numeri di modello non sono versioni, ma identificatori univoci che identificano una particolare configurazione di modello. |
| `screenHeight` | Intero | Il numero di pixel verticali della visualizzazione attiva del dispositivo nell&#39;orientamento predefinito. |
| `screenOrientation` | Stringa | L&#39;orientamento dello schermo corrente. I valori accettati includono `portrait` e `landscape`. |
| `screenWidth` | Stringa | Il numero di pixel orizzontali della visualizzazione attiva del dispositivo nell&#39;orientamento predefinito. |
| `type` | Stringa | Il tipo di dispositivo di cui tenere traccia. I valori accettati includono: <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | Stringa | Identificatore del dispositivo. Può trattarsi di un identificatore di DeviceAtlas o di un altro servizio che identifica l&#39;hardware in uso. |
| `typeIDService` | Stringa | Spazio dei nomi del servizio utilizzato per identificare il tipo di dispositivo. Consulta la sezione [appendice](#typeIDService) per informazioni dettagliate sui valori accettati. |

{style=&quot;table-layout:auto&quot;}

Per ulteriori dettagli sul gruppo di campi, consulta l’archivio XDM pubblico:

* [Esempio popolato](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## Appendice

La sezione seguente contiene informazioni aggiuntive su [!UICONTROL Dispositivo] tipo di dati.

## Valori accettati per typeIDService {#typeIDService}

La tabella seguente illustra i valori accettati per `typeIDService` e loro significati associati:

| Valore | Descrizione |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | Il dispositivo è stato identificato utilizzando DeviceAtlas. |
| `https://ns.adobe.com/xdm/external/adobecampaign` | Il dispositivo è stato identificato tramite Adobe Campaign. |
