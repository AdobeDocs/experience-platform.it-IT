---
title: Panoramica dell’estensione Common Analytics
description: Scopri l’estensione tag di Analytics comune in Adobe Experience Platform.
source-git-commit: 5f810ada57eeb12a56de603d974a091b888dc9d2
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 70%

---

# Panoramica dell’estensione Common Analytics Plugins

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

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
1. Aggiungi l’evento Core - Library Loaded (Page Top) (Core - Libreria caricato (parte superiore della pagina)).
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

Con questa azione puoi selezionare ogni plug-in da includere nell’implementazione e salvare le modifiche. Seleziona tutti i plug-in che intendi usare nell’implementazione. Puoi trovare collegamenti alla documentazione sull’utilizzo di ciascun plug-in e una breve descrizione nella [panoramica dei plug-in di Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/impl-plugins.html?lang=it).

### Inizializza plug-in

Queste azioni inizializzano il plug-in specifico che intendi utilizzare singolarmente. Per inizializzare tutti i plug-in che intendi usare nella tua proprietà, è sufficiente aggiungere l’azione corrispondente alla regola e salvare la regola. Questa configurazione dell’estensione richiede un po&#39; più di tempo, ma genera un codice più efficiente. È quindi l’approccio consigliato da Adobe.

## Elementi dati dell’estensione Common Analytics Plugins

In questa sezione sono descritti gli elementi dati disponibili nell’estensione Common Analytics Plugins.

### getGeoCoordinates

Consente agli utenti di sfruttare l’interfaccia utente nativa di raccolta dati in Adobe Experience Platform per configurare e configurare il plug-in getGeoCoordinates.

### getNewRepeat

Consente agli utenti di sfruttare l’interfaccia utente nativa di raccolta dati per configurare e configurare il plug-in getNewRepeat.

### getPageName

Consente agli utenti di sfruttare l’interfaccia utente nativa di raccolta dati per configurare e configurare il plug-in getPageName.

### getResponsiveLayout

Consente agli utenti di sfruttare l’interfaccia utente nativa di raccolta dati per configurare e configurare il plug-in getResponsiveLayout .

### getTimeParting

Consente agli utenti di sfruttare l’interfaccia utente nativa di raccolta dati per configurare e configurare il plug-in getTimeParting.

### getTimeSinceLastVisit

Consente agli utenti di sfruttare l’interfaccia utente nativa di raccolta dati per configurare e configurare il plug-in getTimeSinceLastVisit.

### getVisitDuration

Consente agli utenti di sfruttare l’interfaccia utente nativa di raccolta dati per configurare e configurare il plug-in getVisitDuration.

### getVisitNum

Consente agli utenti di sfruttare l’interfaccia utente nativa di raccolta dati per configurare e configurare il plug-in getVisitNum.
