---
title: Panoramica degli host gestiti da Adobe
description: Scopri l’opzione di hosting predefinita per la distribuzione delle build della libreria di tag in Adobe Experience Platform.
exl-id: 9042c313-b0d3-4f6e-963d-0051d760fd16
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 88%

---

# Panoramica degli host gestiti da Adobe

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

L’impostazione predefinita per la distribuzione delle build delle librerie di tag in Adobe Experience Platform prevede l’utilizzo di host gestiti da Adobe. Quando si crea una nuova proprietà tramite l’interfaccia utente di Data Collection, viene creato automaticamente un host predefinito gestito da Adobe.

Con gli host gestiti da Adobe, le build delle librerie vengono distribuite a una rete per la distribuzione di contenuti (CDN) di terze parti con cui Adobe ha stipulato un contratto. Essendo indipendenti da Adobe, tali CDN funzionano anche quando Platform è in manutenzione o non disponibile, e il codice distribuito continuerà a funzionare normalmente sui tuoi siti e sulle tue applicazioni. Il codice da incorporare per un host gestito da Adobe fa riferimento al file della libreria principale sulla rete CDN, in modo che un dispositivo client possa recuperare i file in fase di esecuzione.

Questo documento fornisce una panoramica sugli host gestiti da Adobe in Platform e descrive come creare un nuovo host gestito da Adobe.

## Akamai

Attualmente, il fornitore CDN principale per Adobe è [Akamai](https://www.akamai.com/it). La solida rete CDN di Akamai è stata realizzata per distribuire i contenuti a un pubblico globale e per elevati volumi di visitatori web. Comprende reti ridondanti di nodi con bilanciamento del carico e ottimizzati in base alla posizione geografica, al fine di fornire i contenuti il più rapidamente possibile ai visitatori da ogni parte del mondo.

Nello specifico, Akamai esegue più di 137.000 server in 87 paesi in oltre 1150 reti. In termini di ridondanza, la rete CDN non solo effettua l’instradamento da un server all’altro, ma può anche essere indirizzata da un nodo di server a un altro, a seconda delle necessità. In altre parole, ogni nodo è costituito da più server; nell’eventualità in cui un server non sia disponibile, subentrano altri server dello stesso nodo in modo da evitare che si verifichino problemi.

Qualora non sia disponibile un intero nodo, Akamai utilizza il nodo successivo più vicino con gli stessi contenuti già memorizzati nella cache. I nodi vengono selezionati in modo dinamico in base alla posizione del visitatore, al carico del traffico e ad altri fattori. In tal modo i contenuti vengono distribuiti in modo coerente dal nodo locale migliore per ogni visitatore.

I file in hosting su Akamai hanno un dominio `assets.adobedtm.com`. Questo può essere utilizzato come riferimento sicuro o meno (`http://` o `https://`) in base al modo in cui viene richiamato nel codice `<script>` incorporato.

>[!WARNING]
>
>Se la libreria non è disponibile dalla rete Akamai, Platform non è in grado di evitare eventuali errori di rete che potrebbero verificarsi.

## Memorizzazione nella cache delle build delle librerie

Quando si utilizzano gli host gestiti da Adobe, le build delle librerie sono memorizzate nella cache in due posizioni:

* [Cache perimetrale](#edge)
* [Memorizzazione nella cache del browser](#browser)

### Cache perimetrale {#edge}

Lo scopo principale di una rete CDN è quello di distribuire in modo intelligente i contenuti ai server geograficamente più vicini agli utenti finali, per velocizzarne la trasmissione ai dispositivi client. A tal fine, le CDN rendono disponibili copie dei contenuti su server distribuiti geograficamente in tutto il mondo, o “nodi perimetrali”.

Una volta che la build è stata implementata nell&#39;host gestito da Adobe, la rete CDN la distribuisce ai vari server centralizzati (origini). Questi a loro volta inviano copie della build a numerosi nodi perimetrali in tutto il mondo, dove vengono memorizzate nella cache. Le versioni cache della build memorizzate nei nodi perimetrali vengono quindi trasmesse ai dispositivi client.

![](../images/cdn-diagram.png)

>[!NOTE]
>
>Per gli host gestiti da Adobe, la prima libreria pubblicata in un nuovo ambiente può impiegare fino a cinque minuti per propagarsi nella rete CDN globale.

Quando un nodo perimetrale riceve una richiesta per un file specifico (ad esempio la build della libreria), viene innanzitutto verificato il tempo di scadenza del file. Se il tempo non è scaduto, il nodo perimetrale trasmette la versione cache. Se il tempo è scaduto, il nodo perimetrale richiede una nuova copia dall’origine più vicina, distribuisce la copia aggiornata e quindi memorizza nella cache la copia aggiornata con una nuova scadenza.

>[!NOTE]
>
>Oltre ai nodi perimetrali, la memorizzazione nella cache può essere eseguita anche in eventuali reti intermedie, come le reti aziendali o mobili. Se le build non vengono memorizzate nella cache come previsto, il problema potrebbe risiedere in queste ultime reti.

#### Annullamento della validità della cache perimetrale {#invalidation}

Quando carichi una nuova build della libreria, le cache su tutti i nodi edge applicabili vengono invalidate. Questo significa che ogni nodo considera non valida la propria versione cache, indipendentemente da quanto recentemente abbia recuperato una nuova copia. Alla successiva richiesta del file, il nodo perimetrale recupera una nuova copia dall’origine.

Poiché Akamai dispone di più server di origine che replicano i file tra di loro e non è possibile sapere quale origine ha ottenuto il file per prima, le nuove richieste potrebbero pervenire a un’origine che non dispone della versione più recente. La versione precedente verrebbe quindi memorizzata di nuovo nella cache. Per evitare che ciò si verifichi, vengono avviati più annullamenti di validità della cache per ogni nuova build, secondo gli intervalli seguenti:

* Immediatamente dopo il caricamento
* 5 minuti dopo il caricamento
* 60 minuti dopo il caricamento

I gruppi del server di origine hanno quindi il tempo necessario per replicare tra loro la versione più recente del file, affinché tutti dispongano della versione più recente al momento del recupero del file.

### Memorizzazione nella cache del browser {#browser}

Le build delle librerie vengono anche memorizzate nella cache del browser tramite l’intestazione HTTP `cache-control`. Quando utilizzi gli host gestiti da Adobe, non puoi intervenire sulle intestazioni restituite nelle risposte API e vengono quindi utilizzate le impostazioni di cache predefinite di Adobe. In altre parole, non è possibile utilizzare intestazioni personalizzate per gli host gestiti da Adobe. Se hai l’esigenza di usare un’intestazione `cache-control` personalizzata, puoi ricorrere al [self-hosting](self-hosting-libraries.md).

Il tempo di scadenza della build della libreria memorizzata nella cache del browser (determinato dall&#39;intestazione `cache-control`) varia a seconda dell&#39;ambiente di tag in uso:

| Ambiente | Valore `cache-control` |
| --- | --- |
| Sviluppo | `max-age=0, no-cache, no-store` |
| Staging | `max-age=0, no-cache, no-store` |
| Produzione | `max-age=3600` |

Come riportato in questa tabella, la memorizzazione nella cache del browser non è supportata negli ambienti di sviluppo e di staging. Evita quindi di utilizzare i codici da incorporare a scopo di sviluppo o staging in contesti di produzione o con traffico elevato.

Le intestazioni per il controllo della cache sono applicabili solo alla build della libreria principale. Le risorse secondarie rispetto alla libreria principale sono sempre considerate nuove e quindi non è necessario memorizzarle nella cache del browser.

## Utilizzo dell’hosting gestito da Adobe nell’interfaccia utente di

La prima volta che crei una proprietà nell’interfaccia utente di Platform o di Data Collection, viene automaticamente creato un host gestito da Adobe. Anche tutti gli ambienti disponibili con proprietà immediatamente utilizzabili vengono assegnati per impostazione predefinita all’host gestito da Adobe.

>[!NOTE]
>
>Se l’host gestito da Adobe predefinito viene rimosso da tutti gli ambienti, sarà possibile eliminarlo. Se in un secondo tempo desideri ripristinarlo, puoi creare un nuovo host come descritto di seguito:
>
>1. Seleziona la scheda **[!UICONTROL Host]** nella tua proprietà, quindi seleziona **[!UICONTROL Aggiungi host]**.
>1. Specifica un nome per l’host, seleziona **[!UICONTROL Gestito da Adobe]** come tipo di host, quindi seleziona **[!UICONTROL Salva]**.
>
>A questo punto puoi riassegnare gli ambienti all’host gestito da Adobe, in base alle tue esigenze.

## Passaggi successivi

Questo documento fornisce una panoramica dell’hosting gestito da Adobe per le librerie di tag in Adobe Experience Platform. Per informazioni su altre opzioni di hosting, consulta la seguente documentazione:

* [Hosting SFTP](./sftp-host.md)
* [Self-hosting delle librerie](./self-hosting-libraries.md)

Per informazioni sulla gestione degli host per i tuoi ambienti, consulta la [guida degli ambienti](../environments.md).
