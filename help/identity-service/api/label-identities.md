---
keywords: Experience Platform;home;argomenti popolari;label identities
solution: Experience Platform
title: Etichettare un campo come identità
description: I campi che contengono informazioni personali (PII, personally identifiable information) possono essere etichettati come campi di identità. Un valore fornito in un campo di identità viene interpretato come un’identità dal servizio Identity. Lo spazio dei nomi dell’identità è specificato come parte dell’etichettatura del campo.
role: Developer
exl-id: f0b3f18b-7302-4a0b-b444-2d4b59787681
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---

# Etichettare un campo come identità

I campi che contengono informazioni personali (PII, personally identifiable information) possono essere etichettati come campi di identità. Un valore fornito in un campo di identità viene interpretato come un’identità da [!DNL Identity Service]. Lo spazio dei nomi dell’identità è specificato come parte dell’etichettatura del campo.

Affinché un campo sia etichettato come identità devono essere soddisfatti i seguenti criteri:

- Solo i campi di tipo stringa possono essere utilizzati per l’identità
- Le identità sono riconosciute solo nei dati delle serie temporali e dei record
- Solo i campi PII devono essere contrassegnati come identità. La scelta di un campo che rappresenta dati più generici determinerebbe relazioni meno precise e potenziali errori di accesso alle identità correlate dal grafico delle identità

Per istruzioni su come utilizzare l’API Schema Registry per etichettare un campo come identità, visita [guida dell’endpoint &quot;descriptors&quot;](../../xdm/api/descriptors.md#create).

## Passaggi successivi

Procedi all’esercitazione successiva per [elenca identità cluster](./list-cluster-identites.md)
