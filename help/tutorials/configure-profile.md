---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Esercitazioni sul profilo cliente in tempo reale
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---


# Configura [!DNL Real-time Customer Profile] e [!DNL Identity Service]

Per configurare [!DNL Real-time Customer Profile] la tua organizzazione, devi completare più flussi di lavoro separati. Questo documento illustra i passaggi da seguire e fornisce collegamenti alle esercitazioni per completare ogni singolo flusso di lavoro. Per saperne di più, [!DNL Real-time Customer Profile]iniziare leggendo la panoramica [del](../profile/home.md)profilo.

## Abilita schema per [!DNL Profile] e [!DNL Identity]

Prima di poter inserire i dati  Adobe Experience Platform e utilizzarli per la creazione di [!DNL Real-time Customer Profiles], è necessario creare uno schema che fornisca la struttura dei dati che verranno acquisiti e che tale schema debba essere abilitato per l&#39;uso in [!DNL Profile] e  Adobe Experience Platform [!DNL Identity Service]. Per istruzioni dettagliate sulla creazione di uno schema abilitato per entrambi [!DNL Profile] e [!DNL Identity Service], fare riferimento alle esercitazioni per la [creazione di uno schema mediante l&#39;API](../xdm/tutorials/create-schema-api.md) del Registro di sistema dello schema o [la creazione di uno schema mediante l&#39;interfaccia](../xdm/tutorials/create-schema-ui.md)del Generatore di schemi.

## Configurare un dataset per [!DNL Profile] e [!DNL Identity]

Per iniziare l&#39;assimilazione dei dati in [!DNL Profile], è necessario disporre di un set di dati configurato correttamente per l&#39;utilizzo con [!DNL Real-time Customer Profile] e [!DNL Identity Service]. Per iniziare, segui l’esercitazione [](../profile/tutorials/dataset-configuration.md)Configura un dataset per Profilo e Identità.

## Configurare i criteri di unione

 Adobe Experience Platform consente di unire dati provenienti da più origini e combinarli per visualizzare una visione completa di ogni singolo cliente. Quando si uniscono questi dati, i criteri di unione sono le regole che [!DNL Platform] utilizzano per determinare in che modo i dati verranno classificati come priorità e quali dati verranno combinati per creare tale visualizzazione unificata. Utilizzando le API RESTful o l&#39;interfaccia utente, puoi creare nuovi criteri di unione, gestire i criteri esistenti e impostare un criterio di unione predefinito per la tua organizzazione. Per utilizzare i criteri di unione nell&#39; [!DNL Platform] interfaccia utente, consultare la guida [utente dei criteri di](../profile/ui/merge-policies.md)unione. Per lavorare con i criteri di unione utilizzando l&#39;API Profilo cliente in tempo reale, consulta la guida [per gli sviluppatori dei criteri di](../profile/api/merge-policies.md)unione.

## Configurare le proiezioni dei bordi

Al fine di promuovere esperienze coordinate, coerenti e personalizzate per i clienti attraverso più canali in tempo reale, i dati giusti devono essere prontamente disponibili e costantemente aggiornati man mano che si verificano le modifiche.  Adobe [!DNL Experience Platform] consente l&#39;accesso in tempo reale ai dati attraverso l&#39;uso di ciò che sono noti come edge. Un server periferico è un server collocato geograficamente che memorizza i dati e li rende facilmente accessibili alle applicazioni. I dati vengono indirizzati a un bordo da una proiezione, con una destinazione di proiezione che definisce il bordo a cui verranno inviati i dati, e una configurazione di proiezione che definisce le informazioni specifiche che verranno rese disponibili sul bordo. Per ulteriori informazioni e per iniziare a lavorare con i bordi, fate riferimento alla [!DNL Real-time Customer Profile] guida [secondaria API sulle proiezioni](../profile/api/edge-projections.md)edge.

## Passaggi successivi

Dopo aver configurato [!DNL Real-time Customer Profile] la propria organizzazione, puoi iniziare ad aggiungere dati ai profili dei clienti individuali e a creare segmenti di pubblico in base a attributi specifici del cliente. Per iniziare, consulta le seguenti esercitazioni:

* [Aggiungere dati al profilo cliente in tempo reale](../profile/tutorials/add-profile-data.md)
* [Creazione di un segmento](../segmentation/tutorials/create-a-segment.md)