---
title: Panoramica degli host gestiti da Adobe
description: Scopri l’opzione di hosting predefinita per la distribuzione delle build delle librerie di tag in Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 66%

---

# Panoramica degli host gestiti da Adobe

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Gli host gestiti da Adobe sono l’impostazione host predefinita per la distribuzione delle build della libreria di tag in Adobe Experience Platform. Quando crei una nuova proprietà tramite l’interfaccia utente Raccolta dati, viene creato automaticamente un host predefinito gestito da Adobe.

Con gli host gestiti da Adobe, le build delle librerie vengono distribuite a una rete per la distribuzione di contenuti (CDN) di terze parti con cui Adobe ha stipulato un contratto. Essendo indipendenti da Adobe, tali CDN funzionano anche quando Platform è in manutenzione o non disponibile, e il codice distribuito continuerà a funzionare normalmente sui tuoi siti e sulle tue applicazioni. Il codice da incorporare per un host gestito da Adobe fa riferimento al file della libreria principale sulla rete CDN, in modo che un dispositivo client possa recuperare i file in fase di esecuzione.

Questo documento fornisce una panoramica degli host gestiti da Adobe in Platform e descrive come creare un nuovo host gestito da Adobe nell’interfaccia utente di .

## Akamai

Attualmente, il fornitore CDN principale per Adobe è [Akamai](https://www.akamai.com/it). La solida rete CDN di Akamai è stata realizzata per distribuire i contenuti a un pubblico globale e per elevati volumi di visitatori web. Comprende reti ridondanti di nodi con bilanciamento del carico e ottimizzati in base alla posizione geografica, al fine di fornire i contenuti il più rapidamente possibile ai visitatori da ogni parte del mondo.

Nello specifico, Akamai esegue più di 137.000 server in 87 paesi in oltre 1150 reti. In termini di ridondanza, la rete CDN non solo effettua l’instradamento da un server all’altro, ma può anche essere indirizzata da un nodo di server a un altro nodo di server in base alle esigenze. In altre parole, ogni nodo è costituito da più server; nell’eventualità in cui un server non sia disponibile, subentrano altri server dello stesso nodo in modo da evitare che si verifichino problemi.

Se un intero nodo è inattivo, Akamai utilizza dal nodo successivo più vicino con lo stesso contenuto memorizzato nella cache. I nodi vengono selezionati in modo dinamico in base alla posizione del visitatore, al carico del traffico e ad altri fattori. In tal modo i contenuti vengono distribuiti in modo coerente dal nodo locale migliore per ogni visitatore.

I file in hosting su Akamai hanno un dominio `assets.adobedtm.com`. Questo può essere utilizzato come riferimento sicuro o meno (`http://` o `https://`) in base al modo in cui viene richiamato nel codice `<script>` incorporato.

>[!WARNING]
>
>Se la libreria non è disponibile dalla rete Akamai, Platform non è in grado di evitare eventuali errori di rete che potrebbero verificarsi.

## Memorizzazione nella cache delle build delle librerie

Quando si utilizzano gli host gestiti da Adobe, le build delle librerie sono memorizzate nella cache in due posizioni:

* [Cache perimetrale](#edge)
* [Memorizzazione nella cache del browser](#browser)

### Cache perimetrale {#edge}

Lo scopo principale di una rete CDN è quello di distribuire in modo intelligente i contenuti ai server geograficamente più vicini agli utenti finali, in modo che i contenuti possano essere recuperati più rapidamente dai dispositivi client. A tal fine, le CDN rendono disponibili copie dei contenuti su server distribuiti geograficamente in tutto il mondo, o “nodi perimetrali”.

Una volta che la build è stata implementata nell&#39;host gestito da Adobe, la rete CDN la distribuisce ai vari server centralizzati (origini). Questi a loro volta inviano copie della build a numerosi nodi perimetrali in tutto il mondo, dove vengono memorizzate nella cache. Le versioni cache della build memorizzate nei nodi perimetrali vengono quindi trasmesse ai dispositivi client.

![](../images/cdn-diagram.png)

>[!NOTE]
>
>Per gli host gestiti da Adobe, la prima libreria pubblicata in un nuovo ambiente può impiegare fino a cinque minuti per propagarsi nella rete CDN globale.

Quando un nodo perimetrale riceve una richiesta per un file specifico (come la build della libreria), il nodo controlla prima il valore TTL (time-to-live) sul file. Se tale valore non è scaduto, il nodo perimetrale trasmette la versione cache. Se invece è scaduto, viene richiesta una nuova copia dall’origine più vicina. La copia aggiornata viene trasmessa e viene quindi memorizza nella cache con un nuovo valore TTL.

>[!NOTE]
>
>Oltre ai nodi perimetrali, la memorizzazione nella cache può essere eseguita anche in eventuali reti intermedie, come le reti aziendali o mobili. Se le build non vengono memorizzate nella cache come previsto, il problema potrebbe risiedere in queste ultime reti.

#### Annullamento della validità della cache perimetrale {#invalidation}

Quando carichi una nuova build della libreria, le cache su tutti i nodi edge applicabili vengono invalidate. Questo significa che ogni nodo considera non valida la propria versione cache, indipendentemente da quanto recentemente abbia recuperato una nuova copia. Alla successiva richiesta del file, il nodo perimetrale recupera una nuova copia dall’origine.

Poiché Akamai dispone di più server di origine che replicano i file tra loro e non è possibile sapere quale origine ha ricevuto per prima il file, queste richieste di nodo possono colpire un&#39;origine che non dispone della versione più recente. In questo modo la versione precedente verrebbe nuovamente memorizzata nella cache. Per evitare che ciò si verifichi, vengono eseguiti più invalidamenti dati cache per ogni nuova build, secondo gli intervalli seguenti:

* Immediatamente dopo il caricamento
* 5 minuti dopo il caricamento
* 60 minuti dopo il caricamento

I gruppi del server di origine hanno quindi il tempo necessario per replicare tra loro la versione più recente del file, affinché tutti dispongano della versione più recente al momento del recupero del file.

### Memorizzazione nella cache del browser {#browser}

Le build delle librerie vengono anche memorizzate nella cache del browser tramite l’intestazione HTTP `cache-control`. Quando utilizzi gli host gestiti da Adobe, non puoi intervenire sulle intestazioni restituite nelle risposte API e vengono quindi utilizzate le impostazioni di cache predefinite di Adobe. In altre parole, non è possibile utilizzare intestazioni personalizzate per gli host gestiti da Adobe. Se hai l’esigenza di usare un’intestazione `cache-control` personalizzata, puoi ricorrere al [self-hosting](self-hosting-libraries.md).

Il valore TTL (time-to-live) della build della libreria memorizzata nella cache del browser (determinato dall’ intestazione `cache-control` ) varia a seconda dell’ambiente tag utilizzato:

| Ambiente | Valore `cache-control` |
| --- | --- |
| Sviluppo | `max-age=0, no-cache, no-store` |
| Staging | `max-age=0, no-cache, no-store` |
| Produzione | `max-age=3600` |

Come riportato in questa tabella, la memorizzazione nella cache del browser non è supportata negli ambienti di sviluppo e di staging. Evita quindi di utilizzare i codici da incorporare a scopo di sviluppo o staging in contesti di produzione o con traffico elevato.

Le intestazioni di controllo cache sono applicate solo alla build della libreria principale. Le risorse secondarie rispetto alla libreria principale sono sempre considerate nuove e quindi non è necessario memorizzarle nella cache del browser.

## Utilizzo dell’hosting gestito da Adobe nell’interfaccia utente di raccolta dati

La prima volta che crei una proprietà nell&#39; [Interfaccia di raccolta dati](http://launch.adobe.com/it), viene automaticamente creato un host gestito da Adobe. Anche tutti gli ambienti disponibili con proprietà immediatamente utilizzabili vengono assegnati per impostazione predefinita all’host gestito da Adobe.

>[!NOTE]
>
>Se l’host gestito da Adobe predefinito viene rimosso da tutti gli ambienti, sarà possibile eliminarlo. Se in un secondo tempo desideri ripristinarlo, puoi creare un nuovo host come descritto di seguito:
>
>1. Seleziona la scheda **[!UICONTROL Host]** nella tua proprietà, quindi seleziona **[!UICONTROL Aggiungi host]**.
>1. Specifica un nome per l’host, seleziona **[!UICONTROL Gestito da Adobe]** come tipo di host, quindi seleziona **[!UICONTROL Salva]**.

>
>
A questo punto puoi riassegnare gli ambienti all’host gestito da Adobe, in base alle tue esigenze.

## Passaggi successivi

Questo documento fornisce una panoramica dell’hosting gestito da Adobi per le librerie di tag in Adobe Experience Platform. Per informazioni su altre opzioni di hosting, consulta la seguente documentazione:

* [Hosting SFTP](./sftp-host.md)
* [Self-hosting delle librerie](./self-hosting-libraries.md)

Per informazioni sulla gestione degli host per i tuoi ambienti, consulta la [guida degli ambienti](../environments.md).
