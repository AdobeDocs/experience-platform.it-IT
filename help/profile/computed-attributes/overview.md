---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API
title: Introduzione agli attributi calcolati
type: Documentation
description: Gli attributi calcolati sono funzioni per aggregare dati a livello di evento in attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate tra segmentazione, attivazione e personalizzazione.
exl-id: 13878363-589d-4a3c-811c-21d014a5f3c2
hide: true
hidefromtoc: true
source-git-commit: 5ae7ddbcbc1bc4d7e585ca3e3d030630bfb53724
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 1%

---

# Panoramica degli attributi calcolati (alfa)

>[!IMPORTANT]
>
>La funzionalità dell&#39;attributo calcolato è attualmente in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Gli attributi calcolati sono funzioni utilizzate per aggregare dati a livello di evento in attributi a livello di profilo. Queste funzioni vengono calcolate automaticamente in modo che possano essere utilizzate tra segmentazione, attivazione e personalizzazione.

Ogni attributo calcolato contiene un&#39;espressione, o &quot;regola&quot;, che valuta i dati in arrivo e memorizza il valore risultante in un attributo di profilo. Questi calcoli consentono di rispondere facilmente a domande relative a fattori quali il valore di acquisto a vita, il tempo tra gli acquisti o il numero di aperture di applicazioni, senza che sia necessario eseguire manualmente calcoli complessi ogni volta che le informazioni sono necessarie. Questi valori di attributi calcolati possono quindi essere visualizzati in un profilo, utilizzati per creare un segmento o a cui è possibile accedere tramite diversi pattern di accesso.

Questa guida ti aiuterà a comprendere meglio il ruolo degli attributi calcolati all’interno di Adobe Experience Platform.

## Informazioni sugli attributi calcolati

Adobe Experience Platform consente di importare e unire facilmente i dati da più origini per generare [!DNL Real-Time Customer Profiles]. Ogni profilo contiene informazioni importanti relative a un individuo, come le informazioni di contatto, le preferenze e la cronologia degli acquisti, fornendo una vista a 360 gradi del cliente.

Alcune delle informazioni raccolte nel profilo sono facilmente comprensibili quando si leggono direttamente i campi di dati (ad esempio, &quot;nome&quot;), mentre altri dati richiedono l’esecuzione di calcoli multipli o l’utilizzo di altri campi e valori per generare le informazioni (ad esempio, &quot;totale dell’acquisto nel corso della vita&quot;). Per semplificare la comprensione di questi dati, [!DNL Platform] consente di creare attributi calcolati che eseguono automaticamente tali riferimenti e calcoli, restituendo il valore nel campo appropriato.

Gli attributi calcolati includono la creazione di un&#39;espressione, o &quot;regola&quot;, che opera sui dati in arrivo e memorizza il valore risultante in un attributo di profilo. Le espressioni possono essere definite in diversi modi, consentendo di specificare che una regola valuta solo gli eventi in arrivo, un evento in entrata e i dati di profilo o un evento in arrivo, i dati di profilo e gli eventi storici.

### Casi d’uso

I casi di utilizzo per gli attributi calcolati possono variare da calcoli semplici a riferimenti molto complessi. Di seguito sono riportati alcuni esempi di casi d’uso per gli attributi calcolati:

1. **[!UICONTROL Percentuali]:** Un attributo calcolato semplice può comprendere l&#39;acquisizione di due campi numerici in un record e la suddivisione di tali campi per creare una percentuale. Ad esempio, puoi prendere il numero totale di e-mail inviate a un singolo utente e dividerlo per il numero di e-mail aperte dal singolo utente. Osservare il campo dell’attributo calcolato risultante mostrerebbe rapidamente la percentuale di e-mail totali aperte dal singolo utente.
1. **[!UICONTROL Uso dell&#39;applicazione]:** Un altro esempio include la possibilità di aggregare il numero di volte in cui un utente apre l&#39;applicazione. Tracciando il numero totale di aperture di applicazioni, sulla base di singoli eventi aperti, puoi offrire offerte o messaggi speciali agli utenti sul loro 100° open, incoraggiando un maggiore coinvolgimento con il tuo marchio.
1. **[!UICONTROL Valori del ciclo di vita]:** La raccolta dei totali correnti, ad esempio un valore di acquisto a vita per un cliente, può essere molto difficile. È necessario aggiornare il totale storico ogni volta che si verifica un nuovo evento di acquisto. Un attributo calcolato ti consente di farlo molto più facilmente mantenendo il valore del ciclo di vita in un singolo campo che viene aggiornato automaticamente dopo ogni evento di acquisto riuscito relativo al cliente.

## Limitazioni note

### Disponibilità ritardata di nuovi attributi calcolati

La disponibilità di nuovi attributi calcolati può essere ritardata fino a 2 ore dopo l&#39;aggiunta dell&#39;attributo di schema corrispondente allo schema dell&#39;unione.

Questo ritardo è dovuto alla configurazione di memorizzazione in cache corrente. Dopo l’alfa la frequenza di aggiornamento della cache potrebbe essere aumentata.

### Tracciamento della dipendenza nei segmenti

Gli attributi dello schema già utilizzati in un’espressione di definizione del segmento, ma successivamente trasformati in un attributo calcolato, non verranno tracciati come una dipendenza di quel segmento.

Poiché non è stata rilevata alcuna dipendenza, Experience Platform non valuterà automaticamente l’attributo calcolato associato ogni volta che viene valutata la definizione del segmento.

In alternativa, la creazione di attributi calcolati può essere gestita tramite un gruppo di campi schema specifico che aggiunge nuovi attributi calcolati che non sono in conflitto con gli attributi esistenti. Un’altra alternativa è quella di ricreare il segmento con il tracciamento corretto della dipendenza per i nuovi attributi calcolati.
