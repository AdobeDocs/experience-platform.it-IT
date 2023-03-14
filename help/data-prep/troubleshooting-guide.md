---
keywords: Experience Platform;home;argomenti popolari;
title: Guida alla risoluzione dei problemi della preparazione dati
description: Questo documento fornisce le risposte alle domande più frequenti sulla preparazione dati di Adobe Experience Platform.
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%

---

# [!DNL Data Prep] guida alla risoluzione dei problemi

Questo documento fornisce le risposte alle domande più frequenti su Adobe Experience Platform [!DNL Data Prep], nonché una guida alla risoluzione dei problemi relativi agli errori più comuni. Per domande e informazioni sulla risoluzione di problemi relativi alle API di Platform in generale, consulta [Guida alla risoluzione dei problemi API di Adobe Experience Platform](../landing/troubleshooting.md).

## Domande frequenti

Di seguito è riportato un elenco di domande frequenti su [!DNL Data Prep] e le loro risposte.

### Come vengono risolti gli errori di trasformazione?

[!DNL Data Prep] localizza tutti gli errori di trasformazione nella colonna in cui si sono verificati. Di conseguenza, tale colonna viene annullata e il resto della riga continua a essere elaborato. Questi problemi di trasformazione vengono registrati come **Avvisi**. È consigliabile rivedere periodicamente gli avvisi e modificare la logica di trasformazione per tenere conto dei problemi di trasformazione. Questo aumenterà la qualità dei dati acquisiti in Experience Platform.

Se le colonne sono contrassegnate come **Obbligatorio** vengono annullati a causa di problemi di trasformazione, la riga non verrà acquisita. Quando è abilitata l’acquisizione parziale dei dati, puoi impostare la soglia di tali rifiuti prima che l’intero flusso non riesca. Se l’attributo nullified non influisce su alcuna convalida a livello di schema, la riga continua a essere acquisita.

Verranno rifiutate anche tutte le righe non valide anche senza errori di trasformazione. Ad esempio, un flusso di acquisizione dati può avere una mappatura pass-through (nessuna logica di trasformazione) a un campo obbligatorio e non esiste un valore in ingresso per tale attributo. Questa riga verrà rifiutata.

### Come posso eliminare i caratteri speciali in un campo?

È possibile utilizzare caratteri speciali in un campo `${...}`. Tuttavia, i file JSON che contengono campi con un punto (`.`) non sono supportati da questo meccanismo. Quando si interagisce con le gerarchie, se un attributo figlio ha un punto (`.`), è necessario utilizzare una barra rovesciata (`\`) per eliminare i caratteri speciali. Ad esempio: `address` è un oggetto che contiene l’attributo `street.name`, può quindi essere indicato come `address.street\.name` invece di `address.street.name`.

### Qual è la lunghezza massima dei campi calcolati?

I campi calcolati hanno una lunghezza massima di 4096 caratteri.