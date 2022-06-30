---
keywords: Experience Platform;home;argomenti popolari;etichette identità
title: Etichettare un campo come identità nell’interfaccia utente
description: I campi che contengono informazioni personali (PII) possono essere etichettati come campi di identità. Un valore fornito in un campo di identità viene interpretato come identità dal servizio Identity. Lo spazio dei nomi dell’identità viene specificato come parte dell’etichettatura del campo.
source-git-commit: ae51c9bd07944f26be2809a6d15f9d9e8c2fd5a1
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Etichettare un campo come identità nell’interfaccia utente

I campi che contengono informazioni personali (PII) possono essere etichettati come campi di identità. Un valore fornito in un campo di identità viene interpretato come identità da [!DNL Identity Service]. Lo spazio dei nomi dell’identità viene specificato come parte dell’etichettatura del campo.

Affinché un campo sia etichettato come identità, è necessario soddisfare i seguenti criteri:

* È possibile utilizzare solo i campi di tipo stringa per l&#39;identità
* Le identità sono riconosciute solo nei dati relativi a record e serie temporali
* Solo i campi PII devono essere contrassegnati come identità. La scelta di un campo che rappresenta dati più generici comporterebbe relazioni meno precise e potenziali errori nell&#39;accesso alle identità correlate dal grafico dell&#39;identità

Per istruzioni su come etichettare i campi di identità nell’interfaccia utente, consulta la guida su [definizione dei campi di identità nell’interfaccia utente](../../xdm/ui/fields/identity.md).

## Passaggi successivi

Per ulteriori informazioni su [!DNL Identity Service], vedi [[!DNL Identity Service] panoramica](../home.md).
