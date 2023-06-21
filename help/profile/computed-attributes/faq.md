---
title: Domande frequenti sugli attributi calcolati
description: Risposte alle domande frequenti sull’utilizzo degli attributi calcolati.
badge: "Beta"
source-git-commit: 3b4e1e793a610c9391b3718584a19bd11959e3be
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---


# Domande frequenti

>[!IMPORTANT]
>
>Gli attributi calcolati sono attualmente in **beta** ed è **non** disponibile per tutti gli utenti.

In Adobe Experience Platform, gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento in attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate in segmentazione, attivazione e personalizzazione. Di seguito è riportato un elenco delle domande frequenti relative agli attributi calcolati.

## Quali set di dati contribuiscono ai calcoli degli attributi calcolati?

Attributi calcolati considera i set di dati Experience Event abilitati per il profilo cliente in tempo reale per il calcolo degli attributi calcolati.

## Quali campi Experience Data Model (XDM) possono essere utilizzati per creare attributi calcolati?

Tutti i campi XDM nello schema di unione eventi esperienza possono essere utilizzati per creare attributi calcolati.

## Cosa rappresenta l’&quot;ora dell’ultima valutazione&quot;?

L&#39;ora dell&#39;ultima valutazione indica che gli eventi **precedente** a quella marca temporale sono stati considerati nell’ultimo aggiornamento riuscito dell’attributo calcolato.

## È possibile scegliere la frequenza di aggiornamento? Come si decide?

La frequenza di aggiornamento viene determinata automaticamente in base al periodo di lookback dell’attributo calcolato. Per ulteriori informazioni, leggere la [sezione periodo di lookback](./overview.md#lookback-periods) della panoramica degli attributi calcolati.

## In che modo i calcoli sono influenzati dalle scadenze dei dati di Experience Event?

I calcoli degli attributi calcolati si basano sul periodo di lookback definito e sugli eventi esperienza che rientrano in tale periodo di tempo. Di conseguenza, questi calcoli sono **non** interessati dalle scadenze dei dati dell’evento esperienza. Tuttavia, per garantire la precisione degli attributi calcolati, il periodo di lookback deve rimanere **entro** i limiti delle scadenze dei dati.

## È possibile creare un attributo calcolato basato su un altro attributo calcolato?

Poiché gli attributi calcolati vengono creati utilizzando i campi Evento esperienza e si trovano in un campo Profilo, non è possibile utilizzare direttamente un attributo calcolato per crearne un altro.

## Esistono limiti al numero di attributi calcolati che è possibile creare?

Il numero massimo corrente di **pubblicato** gli attributi calcolati sono 25.

## Esistono implicazioni a valle per la disabilitazione di un attributo calcolato?

Prima di disabilitare l’attributo calcolato, **dovrebbe** rimuovile dai sistemi a valle (ad esempio segmentazione, percorsi o destinazioni), in quanto potrebbero verificarsi complicazioni se non vengono rimosse.

## Cosa succede quando disattivi un attributo calcolato? {#inactive-status}

Quando un attributo calcolato viene disabilitato o reso inattivo, non viene più aggiornato. Di conseguenza, questo attributo calcolato **non può** essere utilizzati nella ricerca di profili o in altri utilizzi a valle.

## In che modo gli attributi calcolati aiutano a stimolare il coinvolgimento?

Gli attributi calcolati favoriscono l’arricchimento del profilo aggregando gli attributi dell’evento a livello di profilo unito. Ad esempio, puoi personalizzare le e-mail di marketing con l’ultimo prodotto visualizzato.
