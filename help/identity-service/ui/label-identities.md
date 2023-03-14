---
keywords: Experience Platform;home;argomenti popolari;label identities
title: Etichettare un campo come identità nell’interfaccia utente
description: I campi che contengono informazioni personali (PII, personally identifiable information) possono essere etichettati come campi di identità. Un valore fornito in un campo di identità viene interpretato come un’identità dal servizio Identity. Lo spazio dei nomi dell’identità è specificato come parte dell’etichettatura del campo.
exl-id: c3097030-0242-404f-9e4c-72a7fa574011
source-git-commit: 44e056407f5089c927752f00cc6bf173d7640b83
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Etichettare un campo come identità nell’interfaccia utente

I campi che contengono informazioni personali (PII, personally identifiable information) possono essere etichettati come campi di identità. Un valore fornito in un campo di identità viene interpretato come un’identità da [!DNL Identity Service]. Lo spazio dei nomi dell’identità è specificato come parte dell’etichettatura del campo.

Affinché un campo sia etichettato come identità devono essere soddisfatti i seguenti criteri:

* Solo i campi di tipo stringa possono essere utilizzati per l’identità
* Le identità sono riconosciute solo nei dati delle serie temporali e dei record
* Solo i campi PII devono essere contrassegnati come identità. La scelta di un campo che rappresenta dati più generici determinerebbe relazioni meno precise e potenziali errori di accesso alle identità correlate dal grafico delle identità

Per istruzioni su come etichettare i campi di identità nell’interfaccia utente, consulta la guida su [definizione dei campi di identità nell’interfaccia utente](../../xdm/ui/fields/identity.md).

## Passaggi successivi

Per ulteriori informazioni su [!DNL Identity Service], vedere [[!DNL Identity Service] panoramica](../home.md).
