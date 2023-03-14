---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Introduzione agli attributi calcolati
type: Documentation
description: Gli attributi calcolati sono funzioni per aggregare i dati a livello di evento negli attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate in segmentazione, attivazione e personalizzazione.
exl-id: 13878363-589d-4a3c-811c-21d014a5f3c2
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---

# (Alfa) Panoramica degli attributi calcolati

>[!IMPORTANT]
>
>La funzionalità degli attributi calcolati è attualmente in formato alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento negli attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate in segmentazione, attivazione e personalizzazione.

Ogni attributo calcolato contiene un’espressione, o &quot;regola&quot;, che valuta i dati in arrivo e memorizza il valore risultante in un attributo di profilo. Questi calcoli consentono di rispondere facilmente a domande relative ad aspetti quali il valore di acquisto del ciclo di vita, il tempo che intercorre tra un acquisto e l&#39;altro o il numero di aperture dell&#39;applicazione, senza dover eseguire manualmente calcoli complessi ogni volta che sono necessarie le informazioni. Questi valori di attributo calcolati possono quindi essere visualizzati in un profilo, utilizzati per creare un segmento o accessibili tramite diversi modelli di accesso.

Questa guida ti aiuterà a comprendere meglio il ruolo degli attributi calcolati all’interno di Adobe Experience Platform.

## Informazioni sugli attributi calcolati

Adobe Experience Platform consente di importare e unire facilmente i dati provenienti da più origini per generare [!DNL Real-Time Customer Profiles]. Ogni profilo contiene informazioni importanti relative a un individuo, come le informazioni di contatto, le preferenze e la cronologia degli acquisti, fornendo una visualizzazione a 360 gradi del cliente.

Alcune delle informazioni raccolte nel profilo sono facilmente comprensibili durante la lettura diretta dei campi di dati (ad esempio, &quot;nome&quot;), mentre altri dati richiedono l’esecuzione di più calcoli o l’affidamento su altri campi e valori per generare le informazioni (ad esempio, &quot;totale acquisti per tutta la durata della vita&quot;). Per semplificare la comprensione immediata di questi dati, [!DNL Platform] consente di creare attributi calcolati che eseguono automaticamente questi riferimenti e calcoli, restituendo il valore nel campo appropriato.

Gli attributi calcolati includono la creazione di un’espressione, o &quot;regola&quot;, che funziona sui dati in arrivo e memorizza il valore risultante in un attributo di profilo. Le espressioni possono essere definite in più modi diversi, consentendo di specificare che una regola valuta solo gli eventi in arrivo, un evento in arrivo e i dati del profilo oppure un evento in arrivo, i dati del profilo e gli eventi storici.

### Casi d’uso

I casi di utilizzo per gli attributi calcolati possono variare da calcoli semplici a riferimenti molto complessi. Di seguito sono riportati alcuni esempi di casi di utilizzo per attributi calcolati:

1. **[!UICONTROL Percentuali]:** Un semplice attributo calcolato può includere l’inserimento di due campi numerici in un record e la loro divisione per creare una percentuale. Ad esempio, puoi prendere il numero totale di e-mail inviate a un individuo e dividerlo per il numero di e-mail che il singolo individuo apre. Osservando il campo attributo calcolato risultante, verrebbe rapidamente visualizzata la percentuale del totale di e-mail aperte dall’utente.
1. **[!UICONTROL Utilizzo dell’applicazione]:** Un altro esempio include la possibilità di aggregare il numero di volte in cui un utente apre l’applicazione. Tracciando il numero totale di aperture di applicazioni, in base a singoli eventi aperti, puoi offrire offerte o messaggi speciali agli utenti sulla 100a apertura, incoraggiando un coinvolgimento più profondo con il tuo marchio.
1. **[!UICONTROL Valori ciclo di vita]:** Raccogliere i totali correnti, ad esempio il valore di acquisto del ciclo di vita di un cliente, può essere molto difficile. A tal fine è necessario aggiornare il totale storico ogni volta che si verifica un nuovo evento di acquisto. Un attributo calcolato consente di eseguire questa operazione in modo molto più semplice mantenendo il valore &quot;lifetime&quot; del ciclo di vita in un singolo campo che viene aggiornato automaticamente dopo ogni evento di acquisto riuscito correlato al cliente.

## Limitazioni note

### Disponibilità ritardata di nuovi attributi calcolati

La disponibilità dei nuovi attributi calcolati può essere ritardata fino a 2 ore dopo l’aggiunta dell’attributo schema corrispondente allo schema di unione.

Questo ritardo è dovuto alla configurazione di caching corrente. La frequenza di aggiornamento della cache potrebbe essere aumentata dopo l’esecuzione del comando Alpha.

### Tracciamento delle dipendenze nei segmenti

Gli attributi dello schema già utilizzati in un’espressione di definizione di segmento, ma successivamente trasformati in un attributo calcolato, non verranno tracciati come una dipendenza di quel segmento.

Poiché non è stata rilevata alcuna dipendenza, Experience Platform non valuta automaticamente l’attributo calcolato associato ogni volta che viene valutata la definizione del segmento.

In alternativa, la creazione di attributi calcolati può essere gestita tramite un gruppo di campi dello schema specifico che aggiunge nuovi attributi calcolati che non sono in conflitto con gli attributi esistenti. Un’altra alternativa consiste nel ricreare semplicemente il segmento con il tracciamento delle dipendenze corretto per i nuovi attributi calcolati.
