---
title: Guardrail per il servizio Identity (con logica di eliminazione)
description: Scopri i guardrail per il servizio Identity.
hide: true
hidefromtoc: true
source-git-commit: db8edbbc3ea5d8fcec3de95b9a37387bea493693
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 2%

---

# Guardrail per [!DNL Identity Service] dati (con logica di eliminazione)

Questo documento fornisce informazioni sui limiti di utilizzo e di tariffa per [!DNL Identity Service] dati per ottimizzare l’utilizzo del grafo delle identità. Durante l’esame dei seguenti guardrail, si presume che i dati siano stati modellati correttamente. In caso di domande su come modellare i dati, contatta il rappresentante del servizio clienti.

## Introduzione

I seguenti servizi di Experience Platform sono coinvolti nella modellazione dei dati di identità:

* [Identità](home.md): collega le identità da diverse origini dati durante l’acquisizione in Platform.
* [[!DNL Real-Time Customer Profile]](../profile/home.md): crea profili di consumatori unificati utilizzando dati provenienti da più origini.

## Limiti del modello dati

Le tabelle seguenti forniscono indicazioni sui guardrail per i limiti statici e sulle regole di convalida da considerare per gli spazi dei nomi di identità.

### Limiti statici

La tabella seguente illustra i limiti statici applicati ai dati di identità.

| Guardrail | Limite | Note |
| --- | --- | --- |
| Numero di identità in un grafico [!BADGE Beta]{type=Informative} | 50 | Quando un grafico con 50 identità collegate viene aggiornato, Identity Service applica un meccanismo &quot;first in first out&quot; ed elimina l’identità più vecchia per fare spazio all’identità più recente. L’eliminazione si basa sul tipo di identità e sulla marca temporale. Il limite viene applicato a livello di sandbox. Leggi le [appendice](#appendix) per ulteriori informazioni su come Identity Service elimina le identità una volta raggiunto il limite. |
| Numero di identità in un record XDM | 20 | Il numero minimo di record XDM richiesti è due. |
| Numero di spazi dei nomi personalizzati | Nessuna | Non esistono limiti al numero di spazi dei nomi personalizzati che è possibile creare. |
| Numero di grafici | Nessuna | Non esistono limiti al numero di grafi di identità che è possibile creare. |
| Numero di caratteri per un nome visualizzato dello spazio dei nomi o un simbolo di identità | Nessuna | Non vi sono limiti al numero di caratteri di un nome visualizzato dello spazio dei nomi o di un simbolo di identità. |

### Convalida del valore identità

La tabella seguente illustra le regole esistenti da seguire per garantire la corretta convalida del valore di identità.

| Namespace | Regola di convalida | Comportamento del sistema quando la regola viene violata |
| --- | --- | --- |
| ECID | <ul><li>Il valore identità di un ECID deve essere esattamente di 38 caratteri.</li><li>Il valore identità di un ECID deve essere costituito solo da numeri.</li></ul> | <ul><li>Se il valore identità di ECID non è esattamente di 38 caratteri, il record viene ignorato.</li><li>Se il valore di identità dell’ECID contiene caratteri non numerici, il record viene ignorato.</li></ul> |
| Non ECID | Il valore identità non può superare i 1024 caratteri. | Se il valore di identità supera i 1024 caratteri, il record viene ignorato. |

### Acquisizione dello spazio dei nomi dell’identità

A partire dal 31 marzo 2023, il servizio Identity bloccherà l’acquisizione di Adobe Analytics ID (AAID) per i nuovi clienti. Questa identità viene generalmente acquisita tramite [Origine Adobe Analytics](../sources/connectors/adobe-applications/analytics.md) e [Origine Adobe Audience Manager](../sources//connectors/adobe-applications/audience-manager.md) ed è ridondante perché l’ECID rappresenta lo stesso browser web. Se desideri modificare questa configurazione predefinita, contatta il team del tuo account di Adobe.

## Passaggi successivi

Per ulteriori informazioni su, consulta la seguente documentazione [!DNL Identity Service]:

* [Panoramica di [!DNL Identity Service]](home.md)
* [Visualizzatore del grafico delle identità](ui/identity-graph-viewer.md)

## Appendice {#appendix}

La sezione seguente contiene informazioni aggiuntive sui guardrail per Identity Service.

### [!BADGE Beta]{type=Informative} Informazioni sulla logica di eliminazione quando viene aggiornato un grafico delle identità alla capacità {#deletion-logic}

Quando un grafo di identità completo viene aggiornato, Identity Service elimina l’identità meno recente nel grafo prima di aggiungere l’identità più recente. Ciò al fine di mantenere l’accuratezza e la pertinenza dei dati di identità. Questo processo di eliminazione segue due regole principali:

#### La regola #1 l’eliminazione ha priorità in base al tipo di identità di uno spazio dei nomi

La priorità di eliminazione è la seguente:

1. ID cookie
2. ID dispositivo
3. ID multi-dispositivo, e-mail e telefono

#### Regola #2 l’eliminazione si basa sulla marca temporale memorizzata sull’identità

Ogni identità collegata in un grafo ha la propria marca temporale corrispondente. Quando si aggiorna un grafico completo, Identity Service elimina l’identità con la marca temporale meno recente.

Quando un grafico completo viene aggiornato con una nuova identità, queste due regole funzionano insieme per designare quale identità precedente verrà eliminata. Identity Service elimina prima l’ID cookie meno recente, quindi l’ID dispositivo meno recente e infine l’ID/e-mail/telefono multidispositivo meno recente.

>[!NOTE]
>
>Se l’identità designata per essere eliminata è collegata a più altre identità nel grafico, verranno eliminati anche i collegamenti che collegano tale identità.

Nell’esempio seguente, prima di poter aggiornare il grafico a sinistra con una nuova identità, Identity Service deve prima eliminare l’identità esistente con la marca temporale più vecchia. Tuttavia, poiché l’identità meno recente è un ID dispositivo, Identity Service ignora tale identità fino a quando non arriva allo spazio dei nomi con un tipo più alto nell’elenco di priorità di eliminazione, che in questo caso è `ecid-3`. Una volta rimossa l’identità meno recente con un tipo di priorità di eliminazione più elevato, il grafico viene quindi aggiornato con un nuovo collegamento, `ecid-51`.

>[!NOTE]
>
>Nel raro caso in cui vi siano due identità con la stessa marca temporale e lo stesso tipo di identità, Identity Service ordinerà gli ID in base a XID e condurrà all’eliminazione.

![Un esempio dell’identità più vecchia che viene eliminata per contenere l’identità più recente](./images/graph-limits-v3.png)