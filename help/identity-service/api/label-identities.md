---
keywords: Experience Platform;home;argomenti popolari;etichette identità
solution: Experience Platform
title: Etichettare un campo come identità
topic-legacy: api guide
description: I campi che contengono informazioni personali (PII) possono essere etichettati come campi di identità. Un valore fornito in un campo di identità viene interpretato come identità dal servizio Identity. Lo spazio dei nomi dell’identità viene specificato come parte dell’etichettatura del campo.
exl-id: f0b3f18b-7302-4a0b-b444-2d4b59787681
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---

# Etichettare un campo come identità

I campi che contengono informazioni personali (PII) possono essere etichettati come campi di identità. Un valore fornito in un campo di identità viene interpretato come un&#39;identità da [!DNL Identity Service]. Lo spazio dei nomi dell’identità viene specificato come parte dell’etichettatura del campo.

Affinché un campo sia etichettato come identità, è necessario soddisfare i seguenti criteri:

- È possibile utilizzare solo i campi di tipo stringa per l&#39;identità
- Le identità sono riconosciute solo nei dati relativi a record e serie temporali
- Solo i campi PII devono essere contrassegnati come identità. La scelta di un campo che rappresenta dati più generici comporterebbe relazioni meno precise e potenziali errori nell&#39;accesso alle identità correlate dal grafico dell&#39;identità

Per istruzioni su come utilizzare l&#39;API del Registro di sistema dello schema per etichettare un campo come identità, visita la [guida all&#39;endpoint dei descrittori](../../xdm/api/descriptors.md#create).

## Passaggi successivi

Procedi all&#39;esercitazione successiva su [elencare le identità del cluster](./list-cluster-identites.md)
