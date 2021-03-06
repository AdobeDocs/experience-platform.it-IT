---
keywords: Experience Platform;home;argomenti popolari;
title: Guida alla risoluzione dei problemi di preparazione dei dati
topic-legacy: troubleshooting
description: Questo documento fornisce le risposte alle domande più frequenti sulla preparazione dei dati di Adobe Experience Platform.
source-git-commit: e96263847f53ea2c884c273fd7986855d4c478c1
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# [!DNL Data Prep] guida alla risoluzione dei problemi

Questo documento fornisce le risposte alle domande frequenti su Adobe Experience Platform [!DNL Data Prep], nonché una guida alla risoluzione dei problemi relativi agli errori comuni. Per domande e informazioni sulla risoluzione dei problemi relativi alle API di Platform in generale, vedi [Guida alla risoluzione dei problemi dell’API Adobe Experience Platform](../landing/troubleshooting.md).

## Domande frequenti

Di seguito è riportato un elenco delle domande frequenti su [!DNL Data Prep] e le loro risposte.

### Come vengono risolti gli errori di trasformazione?

[!DNL Data Prep] localizza tutti gli errori di trasformazione nella colonna in cui si sono verificati. Di conseguenza, tale colonna viene annullata e il resto della riga continuerà a essere elaborato. Questi problemi di trasformazione vengono registrati come **Avvisi**. È consigliabile esaminare periodicamente gli avvisi e regolare la logica di trasformazione per tenere conto dei problemi di trasformazione. Ciò aumenterà la qualità dei dati acquisiti in Experience Platform.

Se le colonne sono contrassegnate come **Obbligatorio** sono annullati a causa di problemi di trasformazione, quindi la riga non verrà assimilata. Quando l’acquisizione parziale dei dati è abilitata, puoi impostare la soglia di tali rifiuti prima che l’intero flusso non riesca. Se l’attributo nullizzato non ha influito sulle convalide a livello di schema, la riga continuerà a essere assimilata.

Vengono rifiutate anche tutte le righe non valide anche senza errori di trasformazione. Ad esempio, un flusso di acquisizione dati potrebbe avere una mappatura pass through (nessuna logica di trasformazione) per un campo obbligatorio e non esiste alcun valore in entrata per tale attributo. Questa riga verrà rifiutata.