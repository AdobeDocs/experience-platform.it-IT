---
title: Panoramica dell’estensione Common Analytics
description: Scopri l’estensione tag Common Analytics in Adobe Experience Platform.
exl-id: 9eeb4589-df90-4356-b927-b2c29c32370b
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 82%

---

# Panoramica dell’estensione Common Analytics Plugins

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Questo articolo contiene informazioni su come configurare l’estensione Common Analytics Plugins e sulle opzioni disponibili quando si usa questa estensione per potenziare l’estensione [!DNL Adobe Analytics].

## Configurare l’estensione Common Analytics Plugins

Questa sezione descrive le opzioni disponibili per configurare l’estensione Common Analytics Plugins.

>[!IMPORTANT]
>
>L’estensione Common Analytics Plugins potenzia l’estensione [!DNL Adobe Analytics]. Per funzionare è necessario che l’estensione [!DNL Adobe Analytics] sia installata nella tua proprietà. Inoltre, la funzione di tracciamento deve essere accessibile a livello globale nell’estensione [!DNL Adobe Analytics].

Non è richiesta alcuna configurazione aggiuntiva a livello di estensione.

## Aggiunta di plug-in all’estensione [!DNL Adobe Analytics]

Per utilizzare i plug-in forniti in questa estensione, devi innanzitutto inizializzare quelli che intendi utilizzare nella rispettiva regola.

1. Crea una nuova regola.
1. Aggiungi l’evento Core - Library Loaded (Page Top) (Core - Libreria caricata (Inizio pagina)).
1. Utilizza uno dei metodi di inizializzazione indicati di seguito.

## Tipi di azioni dell’estensione Common Analytics Plugins

In questa sezione sono descritti i tipi di azioni disponibili nell’estensione Common Analytics Plugins.

L’estensione Common Analytics Plugins fornisce le azioni seguenti:

* [Inizializza](#initialize)
* [Inizializza plug-in](#initialize-plugin)

### Inizializza

>[!IMPORTANT]
>
>Anche se questa azione è la più semplice da implementare, Adobe Consulting consiglia di non utilizzarla in quanto aumenta il peso del plug-in.

Con questa azione puoi selezionare ogni plug-in da includere nell’implementazione e salvare le modifiche. Seleziona tutti i componenti che intendi utilizzare durante l’implementazione.

### Inizializza plug-in

Queste azioni inizializzano il plug-in specifico che intendi utilizzare singolarmente. Per inizializzare tutti i plug-in che intendi usare nella tua proprietà, è sufficiente aggiungere l’azione corrispondente alla regola e salvare la regola. Questa configurazione dell’estensione richiede un po&#39; più di tempo, ma genera un codice più efficiente. È quindi l’approccio consigliato da Adobe.

## Elementi dati dell’estensione Common Analytics Plugins

Nell’estensione Common Analytics Plugins sono disponibili i seguenti elementi dati che sfruttano le funzionalità tag per impostare e configurare i plug-in corrispondenti in Analytics:

* `getGeoCoordinates`
* `getNewRepeat`
* `getPageName`
* `getResponsiveLayout`
* `getTimeParting`
* `getTimeSinceLastVisit`
* `getVisitDuration`
* `getVisitNum`

>[!NOTE]
>
>Per ulteriori informazioni sui plug-in di cui sopra, consulta la [documentazione di Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/impl-plugins.html?lang=it).
