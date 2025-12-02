---
solution: Experience Platform
title: Panoramica sulla raccolta dati
description: Scopri come inviare dati a Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 3d51f01d314587510d900d335dc92fedb8ac31e8
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---

# Panoramica sulla raccolta dati

Adobe Experience Platform fornisce una suite di tecnologie che consente di raccogliere i dati sull’esperienza del cliente da varie origini e inviarli all’Edge Network di Adobe Experience Platform. Tali dati possono quindi essere arricchiti, trasformati e distribuiti a destinazioni Adobe o non Adobe.

Adobe supporta i seguenti linguaggi di codice con librerie dedicate per la raccolta dati:

* **JavaScript**: per siti Web e applicazioni basate su Web
* **Cotlin**: per dispositivi Android
* **Swift**: per dispositivi iOS
* **Brightscript**: per dispositivi Roku
* **Flutter**: per applicazioni Android + iOS che utilizzano Flutter
* **React Native**: per applicazioni Android + iOS che utilizzano React Native

L’interfaccia utente dei tag in Raccolta dati di Adobe Experience Platform include un’estensione per SDK web e SDK mobile.

Se nessuno degli SDK di cui sopra soddisfa le esigenze del progetto, puoi utilizzare l&#39;[API Edge Network di Adobe Experience Platform](https://developer.adobe.com/data-collection-apis/docs/) per inviare dati direttamente ad Adobe.

## Processo di raccolta dati

Invece di installare e implementare singole librerie per ciascun prodotto Adobe, puoi implementare uno degli SDK o delle estensioni di tag sopra riportati per aggregare tutti i dati desiderati in un singolo payload. Il payload viene inviato a uno [stream di dati](/help/datastreams/overview.md) nell&#39;Edge Network di Adobe Experience Platform.

![Diagramma raccolta dati](assets/tags-sdks.png)

Adobe Experience Platform Edge Network è una rete di server distribuita a livello globale, veloce e affidabile in grado di ricevere ed elaborare dati su una scala straordinaria. Quando un flusso di dati riceve dei dati, questi vengono distribuiti a ciascuna soluzione configurata dall’utente. I dati vengono trasmessi in un formato comprensibile a ogni singolo prodotto.

![Diagramma soluzioni Adobe](assets/adobe-solutions.png)

È inoltre possibile utilizzare [inoltro eventi](/help/tags/ui/event-forwarding/overview.md) per trasformare, arricchire e inviare dati a qualsiasi destinazione non Adobe con latenza ridotta e senza alcun codice di implementazione lato client.

![Diagramma inoltro eventi](assets/event-forwarding.png)
