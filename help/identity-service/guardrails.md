---
keywords: Experience Platform;identità;servizio di identità;risoluzione dei problemi;protezioni;linee guida;limite;
title: Guardrail per il servizio Identity
description: Questo documento fornisce informazioni sui limiti di utilizzo e di tasso per i dati del servizio Identity per facilitare l’uso ottimale del grafico di identità.
source-git-commit: b36ace84acdb13b89deb6f77a02c298acade8d8e
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 3%

---

# Guardrail per [!DNL Identity Service] dati

Questo documento fornisce informazioni sui limiti di utilizzo e di tasso per [!DNL Identity Service] per ottimizzare l’utilizzo del grafico di identità. Quando si esaminano le seguenti protezioni, si presume che i dati siano stati modellati correttamente. Se hai domande su come modellare i tuoi dati, contatta il tuo rappresentante del servizio clienti.

## Introduzione

I seguenti servizi di Experience Platform sono coinvolti nella modellazione dei dati di identità:

* [Identità](home.md): Collega le identità di diverse origini dati durante l’acquisizione in Platform.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Crea profili di consumatore unificati utilizzando dati provenienti da più sorgenti.

## Limiti del modello dati

Le tabelle riportate di seguito forniscono indicazioni sulle protezioni per i limiti statici e sulle regole di convalida da considerare per i namespace di identità.

### Limiti statici

La tabella seguente delinea i limiti statici applicati ai dati di identità.

| Guardrail | Limite | Note |
| --- | --- | --- |
| Numero di identità in un grafico | 150 | Il grafico dell’identità non verrà aggiornato una volta raggiunto il limite. |
| Numero di identità in un record XDM | 20 | Il numero minimo di record XDM richiesti è due. |
| Numero di spazi dei nomi personalizzati | Nessuna | Non esistono limiti al numero di spazi dei nomi personalizzati che è possibile creare. |
| Numero di grafici | Nessuna | Non vi sono limiti al numero di grafici di identità che è possibile creare. |
| Numero di caratteri per un nome visualizzato dello spazio dei nomi o un simbolo di identità | Nessuna | Non vi sono limiti al numero di caratteri di un nome visualizzato dello spazio dei nomi o di un simbolo di identità. |

### Convalida del valore dell’identità

La tabella seguente illustra le regole esistenti da seguire per garantire la corretta convalida del valore di identità.

| Namespace | Regola di convalida | Comportamento del sistema quando la regola viene violata |
| --- | --- | --- |
| ECID | <ul><li>Il valore di identità di un ECID deve essere esattamente di 38 caratteri.</li><li>Il valore di identità di un ECID deve essere costituito solo da numeri.</li></ul> | <ul><li>Se il valore di identità di ECID non è esattamente di 38 caratteri, il record viene ignorato.</li><li>Se il valore di identità di ECID contiene caratteri non numerici, il record viene ignorato.</li></ul> |
| Non ECID | Il valore di identità non può superare i 1024 caratteri. | Se il valore di identità supera i 1024 caratteri, il record viene ignorato. |

## Passaggi successivi

Per ulteriori informazioni, consulta la seguente documentazione [!DNL Identity Service]:

* [[!DNL Identity Service] panoramica](home.md)
* [Visualizzatore grafico di identità](ui/identity-graph-viewer.md)
