---
title: Standard di compatibilità con le versioni precedenti
description: Scopri lo standard di compatibilità con le versioni precedenti di Adobe Experience Platform che garantisce la compatibilità delle versioni aggiornate delle estensioni dei tag con le versioni precedenti.
exl-id: 325390f1-88c7-4b9e-a484-5442ca649bdf
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 97%

---

# Standard di compatibilità con le versioni precedenti

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Gli aggiornamenti a un’estensione tag in Adobe Experience Platform devono essere compatibili con le versioni precedenti dell’estensione. Ciò significa che:

* Qualsiasi modifica ai componenti primari delle estensioni deve essere compatibile con le versioni precedenti. Ciò include la configurazione dell’estensione, i tipi di evento, i tipi di condizione, i tipi di azione, i tipi di elemento dati e i moduli condivisi.
* I componenti creati da un utente con la versione precedente dell’estensione devono poter superare la convalida rispetto agli schemi forniti nella nuova versione.
* Un utente di Adobe Experience Platform deve essere in grado di installare una versione aggiornata dell’estensione e tutto ciò che ha già fatto deve continuare a funzionare nello stesso modo, fino a quando non apporterà modifiche intenzionali.

## Modifiche consentite

Sono consentiti i seguenti tipi di modifiche all’estensione:

1. È possibile aggiungere nuovi componenti (tipi di evento, tipi di condizione, ecc.).
1. È possibile aggiungere nuovi campi facoltativi alle impostazioni di configurazione dell’estensione.
1. È possibile convertire i campi obbligatori in campi facoltativi.

## Modifiche non consentite

I seguenti tipi di modifiche all’estensione non sono consentiti:

1. Non è possibile rinominare un componente.
1. Non è possibile rimuovere un componente.
1. Non è possibile rimuovere un campo da un componente.
1. Non è possibile trasformare i campi facoltativi in campi obbligatori.
1. Non è possibile aggiungere nuovi campi obbligatori.
1. Non è possibile modificare l’API dei moduli condivisi esistenti.

Se si apporta una di queste modifiche, chiunque abbia installato l’estensione nella propria proprietà inizierà immediatamente ad avere problemi come quelli descritti di seguito:

* Le regole nonn funzioneranno più correttamente perché uno dei componenti della regola è alla ricerca di un componente che non esiste più.
* Tutte le build danno errore perché la libreria include una risorsa upstream che non esiste più nell’estensione.
* Tutte le build non vanno a buon fine perché la libreria include una risorsa con impostazioni che non superano la convalida rispetto al nuovo schema.

In particolare, in questo secondo caso, gli utenti possono restare senza un rimedio e non possono correggere le loro proprietà per poter pubblicare di nuovo.

## Rimozione delle funzionalità

Potrebbero verificarsi situazioni in cui si ha una ragione di business valida e si ritiene necessario apportare una delle modifiche vietate (elencate sopra). Anche se non è possibile, esistono delle alternative:

1. Per rimuovere un componente => Creare un nuovo componente e rendere obsoleto il precedente
1. Per rimuovere un campo da un componente => Creare un nuovo componente senza quel campo e rendere obsoleto il precedente
1. Per rendere obbligatorio un campo facoltativo => Creare un nuovo componente che richieda il campo desiderato e rendere obsoleto il precedente
1. Per modificare l’API di un modulo condiviso => Creare un nuovo modulo condiviso e rendere obsoleto il precedente

Come vedi, le alternative seguono uno schema comune. Bene. Quando dichiari obsoleto un componente, avvisa gli utenti che l’estensione è ora obsoleta e che è necessario passare a una nuova.  Alcuni suggerimenti sulla comunicazione con gli utenti:

* Aggiorna il nome visualizzato del vecchio componente, aggiungendo “(Obsoleto)”.
* Aggiungi alla vista del vecchio componente un testo di avviso rosso e ben visibile, che informi l’utente del fatto che il componente è diventato obsoleto e che si deve passare al nuovo componente.
* Aggiorna il codice del modulo in modo che vengano registrate le notifiche di obsolescenza nella console. Tieni presente che queste informazioni saranno visibili agli utenti finali, quindi è importante mantenerle chiare e non troppo tecniche.
* Invia messaggi e-mail informativi dal sistema di gestione delle relazioni con i clienti.

Nei casi in cui la vecchia funzionalità non sia solo indesiderata ma anche non più presente nella soluzione, puoi compiere un passo ulteriore, ma solo dopo aver informato preventivamente gli utenti dando loro il tempo di aggiornare.

* Aggiorna il contenuto del modulo in modo che non funzioni più. Così facendo, nella versione successiva la funzionalità risulterà rimossa dalla libreria implementata dell’utente, senza interrompere il funzionamento di alcuna regola o versione.

### Ripristino delle funzionalità rimosse

Se la funzionalità è già stata rimossa e gli utenti lamentano dei malfunzionamenti, è necessario rilasciare una nuova versione dell’estensione che ripristini i componenti rimossi.

Puoi anche ripristinarli in uno stato obsoleto, come descritto sopra; l’importante è che esistano.

Ad esempio, supponiamo che sia presente una versione 1.0 con il componente XYZ utilizzato dagli utenti. Viene poi rilasciata la versione 1.1, priva del componente XYZ. Ora gli utenti segnalano che le proprietà non funzionano più con l’estensione e che è necessario correggerla. Dovrai quindi rilasciare una versione 1.2 che ripristini il componente XYZ (eventualmente in uno stato obsoleto) e chiedere agli utenti di eseguire l’aggiornamento alla versione 1.2 affinché tutto torni a funzionare.
