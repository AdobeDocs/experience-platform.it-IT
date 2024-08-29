---
keywords: Experience Platform;home;argomenti popolari;
title: Guida alla risoluzione dei problemi della preparazione dati
description: Questo documento fornisce le risposte alle domande più frequenti sulla preparazione dati di Adobe Experience Platform.
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: ff8f660c2b3a04d8b4b9d4f19891816a44069088
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 0%

---

# Guida alla risoluzione dei problemi di [!DNL Data Prep]

Questo documento contiene le risposte alle domande frequenti su Adobe Experience Platform [!DNL Data Prep] e una guida alla risoluzione dei problemi relativi agli errori più comuni. Per domande e informazioni sulla risoluzione dei problemi relativi alle API di Platform in generale, consulta la [guida alla risoluzione dei problemi API di Adobe Experience Platform](../landing/troubleshooting.md).

## Domande frequenti

Di seguito è riportato un elenco delle domande frequenti su [!DNL Data Prep] e relative risposte.

### Come vengono risolti gli errori di trasformazione?

[!DNL Data Prep] localizza tutti gli errori di trasformazione nella colonna in cui si sono verificati. Di conseguenza, tale colonna viene annullata e il resto della riga continua a essere elaborato. Questi problemi di trasformazione vengono registrati come **Avvisi**. È consigliabile rivedere periodicamente gli avvisi e modificare la logica di trasformazione per tenere conto dei problemi di trasformazione. Questo aumenterà la qualità dei dati acquisiti in Experience Platform.

Se le colonne contrassegnate come **Obbligatorie** vengono annullate a causa di problemi di trasformazione, la riga non verrà acquisita. Quando è abilitata l’acquisizione parziale dei dati, puoi impostare la soglia di tali rifiuti prima che l’intero flusso non riesca. Se l’attributo nullified non influisce su alcuna convalida a livello di schema, la riga continua a essere acquisita.

Verranno rifiutate anche tutte le righe non valide anche senza errori di trasformazione. Ad esempio, un flusso di acquisizione dati può avere una mappatura pass-through (nessuna logica di trasformazione) a un campo obbligatorio e non esiste un valore in ingresso per tale attributo. Questa riga verrà rifiutata.

### Come posso eliminare i caratteri speciali in un campo?

È possibile eliminare i caratteri speciali in un campo utilizzando `${...}`. Tuttavia, i file JSON che contengono campi con un punto (`.`) non sono supportati da questo meccanismo. Quando si interagisce con le gerarchie, se un attributo figlio ha un punto (`.`), è necessario utilizzare una barra rovesciata (`\`) per eliminare i caratteri speciali. Ad esempio, `address` è un oggetto che contiene l&#39;attributo `street.name`, che può quindi essere indicato come `address.street\.name` invece di `address.street.name`.

### Qual è la lunghezza massima dei campi calcolati?

I campi calcolati hanno una lunghezza massima di 4096 caratteri.

### La mia acquisizione non è riuscita a causa della convalida su un attributo, ma tale attributo è presente correttamente nel file. Cos&#39;è esattamente che non va?

Assicurati che il tipo di dati per ogni campo corrisponda al tipo definito nello schema. Inoltre, è necessario rispettare vincoli quali &quot;Obbligatorio&quot;, &quot;enum&quot; e &quot;formato&quot;.

I dati da acquisire devono essere conformi allo schema Experience Data Model (XDM) definito nell’Experience Platform. Se l’attributo non corrisponde al tipo o al formato previsto specificato nello schema, l’acquisizione non riuscirà.

Se vengono utilizzate le funzioni di preparazione dati, assicurati che la trasformazione risulti negli attributi corretti. È possibile esaminare gli attributi durante il processo di impostazione del flusso di lavoro origini. Durante il passaggio di mappatura, selezionare **[!UICONTROL Nuovo tipo di campo]**, quindi selezionare **[!UICONTROL Aggiungi campo calcolato]**. Quindi, utilizza l’interfaccia del campo calcolato per visualizzare in anteprima ogni funzione.

### Come posso rimuovere i valori di dati errati dai record di acquisizione in streaming o batch?

È possibile utilizzare l’interfaccia di mappatura della preparazione dati per eseguire un filtro a livello di colonna solo mappando le colonne che presentano i dati richiesti. Puoi anche utilizzare i campi calcolati per trasformare i dati utilizzando le funzioni di supporto.

Il filtro a livello di riga è attualmente disponibile solo per il [connettore di origine Adobe Analytics](../sources/tutorials/ui/create/adobe-applications/analytics.md#row-level-filtering).

Dopo l’acquisizione, puoi utilizzare il distillatore di dati per pulire, modellare e manipolare i dati utilizzando SQL. Tuttavia, questo processo richiederà l&#39;eliminazione del batch con i record errati e la riacquisizione di un nuovo batch creato dal risultato dell&#39;istruzione SQL.

>[!IMPORTANT]
>
>* Data lake: puoi rimuovere solo i record già acquisiti eliminando e riacquisendo il batch in cui si trova il record.
>
>* Real-Time Customer Profile: è possibile sovrascrivere i record basati su attributi acquisendo nuovi record, ma non è possibile rimuovere i record evento esperienza.
>
>* Servizio identità: non è possibile rimuovere i record in modo definitivo in Identity Service. Dovrai eliminare l’intero profilo e ricaricarlo con i record corretti utilizzando l’API di eliminazione profilo.

### Qual è la best practice per utilizzare i campi calcolati nei dati GIF?

Puoi utilizzare le funzioni di mappatura della preparazione dati durante il passaggio di mappatura dei dati di origine sullo schema XDM per creare un nuovo campo calcolato.

### Quando inserisci i dati di Adobe Analytics come origine, lo schema creato viene abilitato automaticamente per il profilo?

I dati di Analytics non vengono configurati automaticamente per il profilo. Dopo aver configurato il connettore di origine, devi accedere al set di dati e allo schema e abilitarli per l’acquisizione del profilo.

Quando crei un flusso di dati di origine Analytics in una sandbox di produzione, vengono creati due flussi di dati:

* Un flusso di dati che esegue una retrocompilazione di 13 mesi dei dati storici della suite di rapporti nel data lake. Questo flusso di dati termina quando la retrocompilazione è completa.
* Un flusso di dati che invia dati live al data lake e al profilo. Questo flusso di dati viene eseguito in modo continuo.

### Come posso usare lettere minuscole di un valore all’interno di un oggetto mappa utilizzando le funzioni di preparazione dati?

È possibile recuperare il valore utilizzando la funzione `map_get_values` e quindi impostarlo in minuscolo utilizzando la funzione lower:

```shell
lower(map_get_values(mapObject, 'keyName'))
```

È possibile utilizzare la stessa funzione per rendere minuscolo un oggetto mappa. Tuttavia, non è possibile eseguire un ciclo in un&#39;intera mappa e rendere ogni elemento in minuscolo.

### È possibile utilizzare le funzioni di preparazione dati in modo nidificato?

Sì, puoi utilizzare una funzione di preparazione dati all’interno di un’altra funzione per risolvere i problemi relativi a funzionalità di preparazione dati complesse durante l’acquisizione dei dati.

Ad esempio, se desideri definire un campo come nullo in base a una condizione specifica, puoi utilizzare la funzione &quot;iif&quot; per verificare la presenza di tale campo. Se la funzione restituisce `true`, è possibile utilizzare &quot;nullify()&quot; e, se restituisce `false`, è possibile utilizzare il rispettivo campo.

Se il campo era marketing_type, puoi utilizzare &quot;.equals&quot; per controllare il valore nel campo marketing_type e nidificarlo all’interno di una funzione &quot;iif&quot;. Se restituisce `true`, è possibile utilizzare la funzione &quot;nullify()&quot; come illustrato di seguito:

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

Di seguito sono riportati alcuni esempi di come nidificare le funzioni di preparazione dati utilizzando iif, equals e nullify:

| Funzione | Descrizione | Elemento “parameters” | Sintassi | Espressione | Output di esempio |
| --- | --- | --- | --- | --- | --- |
| iif | Valuta una determinata espressione booleana e restituisce il valore specificato in base al risultato. | <ul><li>ESPRESSIONE: **Obbligatoria** L&#39;espressione booleana in fase di valutazione.</li><li>TRUE_VALUE: **Obbligatorio** Il valore restituito se l&#39;espressione restituisce true.</li><li>FALSE_VALUE: **Obbligatorio** Il valore restituito se l&#39;espressione restituisce false.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;Vero&quot; |
| uguale a | Confronta due stringhe per verificare se sono uguali. Questa funzione distingue tra maiuscole e minuscole. | <ul><li>STRING1: **Obbligatorio** La prima stringa da confrontare.</li><li>STRING2: **Obbligatorio** Seconda stringa da confrontare. | STRINGA1.&#x200B;equals(&#x200B;STRING2) | &quot;string1&quot;.&#x200B;equals&#x200B;(&quot;STRING1&quot;) | false |
| annullare | Imposta il valore dell&#39;attributo su null. Da utilizzare quando non si desidera copiare il campo nello schema di destinazione. | | nullify() | nullify() | null |

{style="table-layout:auto"}

Di seguito è riportato un esempio di come è possibile nidificare le funzioni, supponendo che il campo da valutare sia &quot;marketing_type&quot;.

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

Quindi, dato che hai i seguenti tre campi:

* marketing_type: (e-mail, phyMail, push, sms, telefono)
* total_consents: numero compreso tra 4000 e 5500
* data: da feb a marzo 2024

Puoi utilizzare e nidificare le tre funzioni elencate sopra per manipolare i tre campi:

* iif(marketing_type.equals(&quot;email&quot;), nullify(), iif(marketing_type.equals(&quot;push&quot;), &quot;push-notification&quot;, marketing_type)
* iif(marketing_type.equals(&quot;phyMail&quot;), nullify(), iif(marketing_type.equals(&quot;sms&quot;), &quot;text-message&quot;, marketing_type)
* iif(total_consents > 5000, iif(marketing_type.equals(&quot;phone&quot;), nullify(), marketing_type), &quot;insufficiente-consents&quot;)
* iif(date.equals(&quot;3/21/24&quot;), iif(marketing_type.equals(&quot;push&quot;), nullify(), marketing_type), &quot;not-March&quot;)
* iif(total_consents &lt; 4500, iif(marketing_type.equals(&quot;sms&quot;), &quot;low-consent-sms&quot;, marketing_type), &quot;high-consents&quot;)
* iif(marketing_type.equals(&quot;email&quot;), iif(total_consents > 5000, nullify(), &quot;email-low-consents&quot;), marketing_type)
* iif(marketing_type.equals(&quot;push&quot;), iif(total_consents &lt; 4500, &quot;low-consent-push&quot;, nullify()), marketing_type)
* iif(total_consents >= 5500, iif(marketing_type.equals(&quot;phyMail&quot;), nullify(), &quot;high-consents&quot;), marketing_type)