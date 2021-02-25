---
keywords: Experience Platform ;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Introduzione agli attributi calcolati
topic: guida
type: Documentazione
description: Gli attributi calcolati sono funzioni che consentono di aggregare i dati a livello di evento in attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate tra segmentazione, attivazione e personalizzazione.
translation-type: tm+mt
source-git-commit: 08eff53f107549fab0f167a6c206b632f3c8c183
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 1%

---


# (Alfa) Panoramica sugli attributi calcolati

>[!IMPORTANT]
>
>La funzionalità dell&#39;attributo calcolato è attualmente in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Gli attributi calcolati sono funzioni utilizzate per aggregare i dati a livello di evento in attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate tra segmentazione, attivazione e personalizzazione.

Ogni attributo calcolato contiene un&#39;espressione, o &quot;regola&quot;, che valuta i dati in arrivo e memorizza il valore risultante in un attributo di profilo. Questi calcoli consentono di rispondere facilmente a domande relative a cose come il valore di acquisto del ciclo di vita, il tempo tra acquisti o il numero di aperture di applicazioni, senza che sia necessario eseguire manualmente calcoli complessi ogni volta che le informazioni sono necessarie. Questi valori di attributi calcolati possono essere visualizzati in un profilo, utilizzati per creare un segmento o a cui si accede tramite una serie di pattern di accesso diversi.

Questa guida aiuterà a comprendere meglio il ruolo degli attributi calcolati in Adobe Experience Platform.

## Informazioni sugli attributi calcolati

Adobe Experience Platform consente di importare e unire facilmente dati da più origini per generare [!DNL Real-time Customer Profiles]. Ogni profilo contiene informazioni importanti relative a un individuo, come le informazioni di contatto, le preferenze e la cronologia degli acquisti, fornendo una visualizzazione a 360 gradi del cliente.

Alcune delle informazioni raccolte nel profilo sono facilmente comprensibili quando si leggono direttamente i campi di dati (ad esempio, &quot;nome&quot;), mentre altri dati richiedono l&#39;esecuzione di più calcoli o l&#39;utilizzo di altri campi e valori per generare le informazioni (ad esempio, &quot;totale dell&#39;acquisto nel corso del ciclo di vita&quot;). Per semplificare la comprensione dei dati, [!DNL Platform] consente di creare attributi calcolati che eseguono automaticamente tali riferimenti e calcoli, restituendo il valore nel campo appropriato.

Gli attributi calcolati includono la creazione di un&#39;espressione, o &quot;regola&quot;, che opera sui dati in arrivo e memorizza il valore risultante in un attributo di profilo. Le espressioni possono essere definite in diversi modi, consentendo di specificare che una regola valuta solo gli eventi in arrivo, un evento in arrivo e i dati del profilo o un evento in arrivo, i dati del profilo e gli eventi storici.

### Casi di utilizzo

I casi di utilizzo per gli attributi calcolati possono variare da calcoli semplici a riferimenti molto complessi. Di seguito sono riportati alcuni esempi di casi di utilizzo per gli attributi calcolati:

1. **[!UICONTROL Percentages]:** Un semplice attributo calcolato potrebbe includere l&#39;acquisizione di due campi numerici in un record e la suddivisione per creare una percentuale. Ad esempio, potete prendere il numero totale di e-mail inviate a un singolo e dividerlo per il numero di e-mail che l&#39;utente apre. Osservare il campo attributo calcolato risultante mostrerebbe rapidamente la percentuale di e-mail totali aperte dal singolo utente.
1. **[!UICONTROL Application use]:** Un altro esempio include la possibilità di aggregare il numero di volte che un utente apre l&#39;applicazione. Tracciando il numero totale di aperture di applicazioni, in base a singoli eventi aperti, puoi offrire offerte o messaggi speciali agli utenti sul loro 100° evento aperto, incoraggiando un coinvolgimento più profondo con il tuo marchio.
1. **[!UICONTROL Lifetime values]:** Raccogliere i totali in esecuzione, ad esempio un valore di acquisto per un cliente nel corso della vita, può essere molto difficile. Ciò richiede l&#39;aggiornamento del totale storico ogni volta che si verifica un nuovo evento di acquisto. Un attributo calcolato consente di ottenere questo risultato molto più facilmente mantenendo il valore del ciclo di vita in un singolo campo che viene aggiornato automaticamente dopo ogni evento di acquisto relativo al cliente.

## Limitazioni note

### Disponibilità ritardata di nuovi attributi calcolati

La disponibilità di nuovi attributi calcolati potrebbe essere posticipata fino a 2 ore dopo l&#39;aggiunta dell&#39;attributo di schema corrispondente allo schema unione.

Questo ritardo è dovuto alla configurazione corrente della cache. Post-alfa la frequenza di aggiornamento della cache potrebbe essere aumentata.

### Tracciamento della dipendenza nei segmenti

Gli attributi dello schema già utilizzati in un&#39;espressione di definizione del segmento, ma successivamente trasformati in un attributo calcolato, non saranno tracciati come una dipendenza di quel segmento.

Poiché non è stata rilevata alcuna dipendenza,  Experience Platform non valuterà automaticamente l’attributo calcolato associato ogni volta che viene valutata la definizione del segmento.

In alternativa, la creazione di attributi calcolati potrebbe essere gestita tramite un mixin specifico che aggiunge nuovi attributi calcolati che non entrano in conflitto con gli attributi esistenti. Un&#39;altra alternativa consiste nel ricreare semplicemente il segmento con il corretto tracciamento delle dipendenze per i nuovi attributi calcolati.