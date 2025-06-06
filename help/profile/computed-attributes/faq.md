---
title: Domande frequenti sugli attributi calcolati
description: Risposte alle domande frequenti sull’utilizzo degli attributi calcolati.
exl-id: a4d3c06a-d135-453b-9637-4f98e62737a7
source-git-commit: 7d515401eb49ffd2ad5cf0bd074896b274c4fb05
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 0%

---

# Domande frequenti

In Adobe Experience Platform, gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento in attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate in segmentazione, attivazione e personalizzazione. Di seguito è riportato un elenco delle domande frequenti relative agli attributi calcolati.

## Come posso accedere agli attributi calcolati?

Per accedere agli attributi calcolati, devi disporre delle autorizzazioni appropriate (**Visualizza attributi calcolati** e **Gestisci attributi calcolati**). Per ulteriori informazioni sulle autorizzazioni richieste, leggere la [documentazione sul controllo degli accessi](../../access-control/home.md). Per informazioni su come applicare queste autorizzazioni, leggere la [guida alla gestione delle autorizzazioni](../../access-control/ui/permissions.md).

## Quali set di dati contribuiscono ai calcoli degli attributi calcolati?

Attributi calcolati considera i set di dati Experience Event abilitati per il profilo cliente in tempo reale per il calcolo degli attributi calcolati.

## Quali campi Experience Data Model (XDM) possono essere utilizzati per creare attributi calcolati?

Tutti i campi XDM nello schema di unione eventi esperienza possono essere utilizzati per creare attributi calcolati.

## Cosa rappresentano &quot;ultima valutazione&quot; e &quot;ultimo stato di valutazione&quot;?

L’ultima valutazione si riferisce alla marca temporale fino alla quale gli eventi vengono considerati nell’ultima esecuzione riuscita. Lo stato dell’ultima valutazione indica se l’ultima esecuzione della valutazione è stata eseguita correttamente o meno.

## È possibile scegliere la frequenza di aggiornamento? Come si decide?

La frequenza di aggiornamento viene determinata automaticamente in base al periodo di lookback dell’attributo calcolato. Per ulteriori informazioni, consulta la [sezione Periodo di lookback](./overview.md#lookback-periods) della panoramica degli attributi calcolati.

## In che modo i calcoli sono influenzati dalle scadenze dei dati di Experience Event?

I calcoli degli attributi calcolati vengono recuperati per la durata del lookback definita nella prima valutazione e aggiornati in base agli eventi incrementali per gli aggiornamenti successivi. Di conseguenza, questi calcoli sono **non** interessati dalle scadenze dei dati Experience Event dei vecchi dati dopo la prima valutazione.

Ad esempio, se crei un attributo calcolato valutato mensilmente con un periodo di lookback di tre mesi, per la prima valutazione l’attributo calcolato calcolerà tutti gli eventi entro tale periodo di lookback di tre mesi. Anche se la scadenza dei dati del set di dati Experience Event è un mese, questa scadenza dei dati **non** influirà sull&#39;aggiornamento mensile degli attributi calcolati, poiché l&#39;esecuzione della valutazione del mese successivo aggregherà in modo incrementale gli eventi e aggiornerà il calcolo.

>[!NOTE]
>
>I dati scaduti **non possono** essere recuperati in un secondo momento da un attributo calcolato. La scadenza dei dati del set di dati dell&#39;evento **maggio** ha limitato la possibilità di convalidare il valore dell&#39;attributo calcolato in un momento successivo. Per convalidare il valore dell&#39;attributo calcolato, il periodo di lookback deve rimanere **entro** i limiti delle scadenze dei dati.

## È possibile creare un attributo calcolato basato su un altro attributo calcolato?

Poiché gli attributi calcolati vengono creati utilizzando i campi Evento esperienza e si trovano in un campo Profilo, non è possibile utilizzare direttamente un attributo calcolato per crearne un altro.

## Esistono limiti al numero di attributi calcolati che è possibile creare?

Sì, esiste un limite al numero di attributi calcolati che è possibile creare. Questo limite si applica solo agli attributi calcolati **active**. Fai riferimento alla descrizione del prodotto o contatta l’Account Team di Adobe per ulteriori informazioni.

## Esistono implicazioni a valle per la disabilitazione di un attributo calcolato?

Prima di disabilitare l&#39;attributo calcolato, **devi** rimuoverlo dai sistemi a valle (come segmentazione, percorsi o destinazioni), poiché potrebbero verificarsi complicazioni se non viene rimosso.

## Cosa succede quando disattivi un attributo calcolato? {#inactive-status}

Quando un attributo calcolato viene disabilitato o reso inattivo, non viene più aggiornato. Di conseguenza, questo attributo calcolato **non può** essere utilizzato nella ricerca di profili o in altri utilizzi a valle.

## In che modo gli attributi calcolati aiutano a stimolare il coinvolgimento?

Gli attributi calcolati favoriscono l’arricchimento del profilo aggregando gli attributi dell’evento a livello di profilo unito. Ad esempio, puoi personalizzare le e-mail di marketing con l’ultimo prodotto visualizzato.

## Con quale frequenza vengono valutati gli attributi calcolati? È correlato alla pianificazione di valutazione del pubblico?

Gli attributi calcolati vengono valutati in una frequenza **batch** **indipendente** rispetto alla pianificazione della valutazione del pubblico, della destinazione e del percorso. Ciò significa che indipendentemente dal tipo di segmentazione (segmentazione batch o segmentazione in streaming), l’attributo calcolato verrà valutato sulla propria pianificazione (oraria, giornaliera, settimanale o mensile).

La prima valutazione dell&#39;attributo calcolato viene eseguita entro le 24 ore successive alla sua **creazione**. Le valutazioni batch successive vengono eseguite su base oraria, giornaliera, settimanale o mensile a seconda del periodo di lookback definito.

Ad esempio, se la prima valutazione si verifica alle 12:00 UTC del 9 ottobre, le valutazioni successive si verificheranno nei seguenti orari:

- Prossimo aggiornamento giornaliero: 10 ottobre alle 12 UTC
- Prossimo aggiornamento settimanale: 12:00 UTC del 15 ottobre
- Prossimo aggiornamento mensile: 12:00 UTC del 1° novembre

>[!IMPORTANT]
>
>Questo accade solo se l&#39;aggiornamento rapido è abilitato per **not**. Per informazioni sulle modifiche del periodo di lookback quando è abilitato l&#39;aggiornamento rapido, leggere la [sezione sull&#39;aggiornamento rapido](./overview.md#fast-refresh).

Entrambi gli aggiornamenti di **weekly** e **month** hanno luogo all&#39;inizio della **settimana** del calendario (la domenica della nuova settimana) o all&#39;inizio del **mese** del calendario (il primo del nuovo mese), anziché esattamente una settimana o un mese dopo la prima data di valutazione.

>[!NOTE]
>
>Il valore dell&#39;attributo calcolato è **not** aggiornato immediatamente nel profilo dopo ogni esecuzione della valutazione. Per garantire che il valore aggiornato sia presente nei profili, è necessario considerare un buffer di alcune ore tra il tempo di valutazione e l’utilizzo degli attributi calcolati. La pianificazione dell&#39;aggiornamento degli attributi calcolati è **determinata dal sistema** e **non può** essere modificata. Per ulteriori informazioni, contatta l’Assistenza clienti di Adobe.

## Come interagiscono gli attributi calcolati con i tipi di pubblico valutati utilizzando la segmentazione in streaming?

Se un pubblico valutato mediante segmentazione in streaming utilizza un attributo calcolato, durante la valutazione del pubblico verrà utilizzato il **valore più recente** dell&#39;attributo calcolato. Ad esempio, se il pubblico cerca eventi di acquisto, al momento dell’evento di acquisto farà riferimento all’ultimo valore dell’attributo calcolato valutato.

## Posso utilizzare attributi calcolati su Edge?

Come qualsiasi altro attributo di profilo, gli attributi calcolati sono disponibili e possono essere utilizzati sugli spigoli. Si noti che gli attributi calcolati sono **non** calcolati sul server Edge.

## Come vengono applicate le etichette di utilizzo dei dati sugli attributi calcolati?

Gli attributi calcolati derivano automaticamente le etichette di utilizzo dei dati dai campi e dai set di dati di origine utilizzati per definire gli attributi calcolati. In questo modo i dati comportamentali verranno utilizzati in modo appropriato.

## Come si utilizzano gli attributi calcolati con Adobe Journey Optimizer?

Per utilizzare gli attributi calcolati nei percorsi, è necessario aggiungere il gruppo di campi `SystemComputedAttributes` all&#39;origine dati Experience Platform. Per ulteriori informazioni sulla configurazione dell&#39;origine dati Experience Platform, leggere la [guida all&#39;origine dati di Adobe Experience Platform](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configure-journeys/data-source-journeys/adobe-experience-platform-data-source.html?lang=it).
