---
keywords: ' Experience Platform;home;argomenti popolari;identità etichetta'
solution: Experience Platform
title: Etichettare un campo come identità
topic: api guide
description: I campi che contengono informazioni personali (PII) possono essere etichettati come campi di identità. Un valore fornito in un campo di identità viene interpretato come identità dal servizio identità. Lo spazio dei nomi dell'identità è specificato come parte dell'etichettatura del campo.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---


# Etichettare un campo come identità

I campi che contengono informazioni personali (PII) possono essere etichettati come campi di identità. Un valore fornito in un campo di identità viene interpretato come identità da [!DNL Identity Service]. Lo spazio dei nomi dell&#39;identità è specificato come parte dell&#39;etichettatura del campo.

Affinché un campo sia etichettato come identità, è necessario soddisfare i seguenti criteri:

- Per l&#39;identità è possibile utilizzare solo i campi di tipo stringa
- Le identità sono riconosciute solo nei dati relativi a record e serie temporali
- Solo i campi PII devono essere contrassegnati come identità. La scelta di un campo che rappresenta più dati generici comporterebbe relazioni meno precise e potenziali errori nell&#39;accesso alle identità correlate dal grafico di identità

Per istruzioni sull&#39;utilizzo dell&#39;API del Registro di sistema dello schema per etichettare un campo come identità, vedere la [guida dell&#39;endpoint dei descrittori](../../xdm/api/descriptors.md#create).

## Passaggi successivi

Passare all&#39;esercitazione successiva per [elencare le identità del cluster](./list-cluster-identites.md)