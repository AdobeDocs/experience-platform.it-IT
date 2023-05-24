---
keywords: Experience Platform;identità;servizio identità;risoluzione dei problemi;guardrail;linee guida;limite;
title: Guardrail per il servizio Identity
description: Questo documento fornisce informazioni sui limiti di utilizzo e di tariffa per i dati del servizio Identity, utili per ottimizzare l’utilizzo del grafico delle identità.
exl-id: bd86d8bf-53fd-4d76-ad01-da473a1999ab
source-git-commit: f619bbf2c8d313eabc6444b4bd8c09615a00cc42
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 2%

---

# Guardrail per [!DNL Identity Service] dati

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
| Numero di identità in un grafico | 150 | Il limite viene applicato a livello di sandbox. Il grafo delle identità non verrà aggiornato una volta raggiunto il limite. **Nota**: numero massimo di identità in un grafico delle identità **per un singolo profilo unito** è 50. I profili uniti basati su grafici di identità con più di 50 identità sono esclusi dal profilo cliente in tempo reale. Per ulteriori informazioni, consulta la guida su [guardrail per i dati profilo](../profile/guardrails.md). |
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
