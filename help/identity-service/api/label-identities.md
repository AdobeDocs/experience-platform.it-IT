---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Etichettare un campo come identità
topic: api guide
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 1%

---


# Etichettare un campo come identità

I campi che contengono informazioni personali (PII) possono essere etichettati come campi di identità. Un valore fornito in un campo identità viene interpretato come identità da [!DNL Identity Service]. Lo spazio dei nomi dell&#39;identità è specificato come parte dell&#39;etichettatura del campo.

Affinché un campo sia etichettato come identità, è necessario soddisfare i seguenti criteri:

- Per l&#39;identità è possibile utilizzare solo i campi di tipo stringa
- Le identità sono riconosciute solo nei dati relativi a record e serie temporali
- Solo i campi PII devono essere contrassegnati come identità. La scelta di un campo che rappresenta più dati generici comporterebbe relazioni meno precise e potenziali errori nell&#39;accesso alle identità correlate dal grafico di identità

Per istruzioni sull&#39;utilizzo dell&#39;API del Registro di sistema dello schema per etichettare un campo come identità, vedere [Creazione di un descrittore](../../xdm/api/descriptors.md).

## Passaggi successivi

Passate all&#39;esercitazione successiva per [elencare le identità del cluster](./list-cluster-identites.md)