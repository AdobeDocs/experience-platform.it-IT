---
source-git-commit: 1ab56cf2495238385d726277f6409d2e0c0cb017
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 3%

---
# Snippet

## Quote e timeline di elaborazione {#quotas}

Registra Le richieste di cancellazione sono soggette ai limiti di invio giornalieri e mensili degli identificatori, determinati in base al diritto alla licenza della tua organizzazione. Questi limiti si applicano sia alle richieste di eliminazione basate su API che su interfaccia utente.

>[!NOTE]
>
>Puoi inviare fino a **1.000.000 identificatori al giorno**, ma solo se lo consente la quota mensile rimanente. Se il limite mensile è inferiore a 1 milione, le richieste giornaliere non possono superare tale limite.

### Diritto invio mensile per prodotto {#quota-limits}

La tabella seguente illustra i limiti di invio degli identificatori per prodotto e livello di adesione. Per ogni prodotto, il limite mensile è il minore tra due valori: un limite fisso di identificazione o una soglia basata su percentuale associata al volume di dati concesso in licenza.

| Prodotto | Descrizione diritto | Limite mensile (scegliendo il valore minore) |
|----------|-------------------------|---------------------------------|
| REAL-TIME CDP o ADOBE JOURNEY OPTIMIZER | Senza il componente aggiuntivo Privacy and Security Shield o Healthcare Shield | 2.000.000 identificatori o il 5% del pubblico indirizzabile |
| REAL-TIME CDP o ADOBE JOURNEY OPTIMIZER | Con il componente aggiuntivo Privacy and Security Shield o Healthcare Shield | 15.000.000 identificatori o il 10% del pubblico indirizzabile |
| Customer Journey Analytics | Senza il componente aggiuntivo Privacy and Security Shield o Healthcare Shield | 2.000.000 identificatori o 100 identificatori per milione di righe CJA di diritto |
| Customer Journey Analytics | Con il componente aggiuntivo Privacy and Security Shield o Healthcare Shield | 15.000.000 identificatori o 200 identificatori per milione di righe CJA di diritto |

>[!NOTE]
>
> La maggior parte delle organizzazioni avrà limiti mensili inferiori in base al proprio pubblico indirizzabile effettivo o ai diritti di riga di CJA.

Le quote vengono reimpostate il primo giorno di ogni mese di calendario. La quota non utilizzata **non** viene riportata.

>[!NOTE]
>
>Le quote si basano sui diritti mensili concessi in licenza dalla tua organizzazione per **identificatori inviati**. Queste non vengono applicate dai guardrail di sistema, ma possono essere monitorate e riviste.
>
>Eliminazione record è un **servizio condiviso**. Il limite mensile riflette il diritto più alto tra Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics ed eventuali componenti aggiuntivi Shield applicabili.

### Elaborazione dei timeline per l’invio degli identificatori {#sla-processing-timelines}

Dopo l’invio, le richieste di eliminazione dei record vengono messe in coda ed elaborate in base al livello di adesione.

| Descrizione del prodotto e della licenza | Durata coda | Tempo di elaborazione massimo (SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| Senza il componente aggiuntivo Privacy and Security Shield o Healthcare Shield | Fino a 15 giorni | 30 giorni |
| Con il componente aggiuntivo Privacy and Security Shield o Healthcare Shield | In genere 24 ore | 15 giorni |

Se l’organizzazione richiede limiti più elevati, contatta il rappresentante Adobe per una revisione dell’adesione.
