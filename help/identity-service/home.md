---
keywords: Experience Platform;home;argomenti popolari;identità;identità;grafici XDM;servizio identità;servizio Identity
solution: Experience Platform
title: Panoramica del servizio Identity
topic: ' - Panoramica'
description: Il servizio Adobe Experience Platform Identity consente di acquisire una visione migliore del cliente e del suo comportamento attraverso il collegamento di identità tra dispositivi e sistemi, consentendo di fornire in tempo reale esperienze digitali personali e di forte impatto.
translation-type: tm+mt
source-git-commit: bb218fc0cca6fe74693e99747963058bd0dc962a
workflow-type: tm+mt
source-wordcount: '1718'
ht-degree: 0%

---


# [!DNL Identity Service]panoramica

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Ciò è reso più difficile quando i dati dei clienti sono frammentati in diversi sistemi, il che fa sì che ogni singolo cliente sembri avere più &quot;identità&quot;. Adobe Experience Platform [!DNL Identity Service] ti aiuta a ottenere una visione migliore del cliente e del suo comportamento attraverso il collegamento di identità tra dispositivi e sistemi, consentendoti di offrire esperienze digitali personali di grande impatto in tempo reale.

## Comprensione di [!DNL Identity Service]

Ogni giorno i clienti interagiscono con il tuo business e instaurano una relazione in continuo aumento con il tuo marchio. Un cliente tipico può essere attivo in un numero qualsiasi di sistemi all’interno dell’infrastruttura dati della tua organizzazione, come i sistemi eCommerce, loyalty e help-desk. Lo stesso cliente può anche impegnarsi in modo anonimo su qualsiasi numero di dispositivi. [!DNL Identity Service] consente di creare un quadro completo del cliente, aggregando dati correlati che altrimenti potrebbero essere memorizzati in più sistemi diversi.

Considera un esempio quotidiano del rapporto di un consumatore con il tuo marchio:

Mary ha un account sul tuo sito di eCommerce dove ha completato alcuni ordini in passato. Di solito usa il suo portatile personale per fare acquisti, dove accede ogni volta. Tuttavia, durante una delle sue visite utilizza il suo tablet per comprare sandali, ma non effettua un ordine e non effettua l&#39;accesso.

A questo punto, l’attività di Mary viene visualizzata come due profili separati: il suo accesso eCommerce e il suo dispositivo tablet, forse identificato dall’ID dispositivo.

Mary riprende in seguito la sessione del tablet e fornisce il suo indirizzo e-mail durante l&#39;iscrizione alla newsletter. In questo modo, l’acquisizione in streaming aggiunge una nuova identità come dati di record all’interno del suo profilo. Di conseguenza, [!DNL Identity Service] ora relaziona l’attività per dispositivi tablet di Mary con la cronologia del suo account eCommerce.

Al prossimo clic sul suo tablet, il tuo contenuto di destinazione potrebbe riflettere l&#39;intero profilo e la storia di Mary, piuttosto che un semplice tablet utilizzato da un acquirente sconosciuto.

Le relazioni di identità che [!DNL Identity Service] definisce e mantiene sono sfruttate da [!DNL Real-time Customer Profile] per creare un quadro completo di un cliente e delle sue interazioni con il tuo marchio. Per ulteriori informazioni, consulta la [Panoramica sul profilo cliente in tempo reale](../profile/home.md).

### Identità

Un’identità è un dato univoco per un’entità, in genere una singola persona. Un&#39;identità, ad esempio un ID di accesso, un ECID o un ID fedeltà, viene definita identità nota.

PII come indirizzo e-mail e numero di telefono, serve per identificare direttamente un cliente. Di conseguenza, i dati PII vengono utilizzati per far corrispondere le identità multiple di un cliente tra i vari sistemi.

Identità sconosciute o anonime che separano un dispositivo senza identificare la persona effettiva che lo utilizza. Questa categoria include informazioni quali l’indirizzo IP del visitatore e l’ID cookie. Anche se i dati comportamentali possono essere raccolti da un dispositivo utilizzando identità sconosciute, l&#39;associazione di tali identità tra dispositivi o supporti è limitata fino a quando il cliente non fornisce dati PII durante il proprio percorso.

Come mostrato nell&#39;immagine seguente, le identità note e anonime sono entrambe componenti importanti dei [grafici di identità](#identity-graphs), discussi in seguito in questo documento.

![Unione delle identità su Platform](./images/identity-service-stitching.png)

Esempi di implementazioni [!DNL Identity Service] includono:

- Un&#39;azienda di telecomunicazioni può basarsi sul valore &quot;numero di telefono&quot;, dove un numero di telefono fa riferimento allo stesso individuo di interesse sia per i set di dati offline che online.
- Una società di vendita al dettaglio può utilizzare &quot;indirizzo e-mail&quot; nei set di dati offline e ECID nei set di dati online a causa dell&#39;alta percentuale di visitatori anonimi.
- Una banca può preferire il &quot;numero di conto&quot; nei set di dati offline, ad esempio le transazioni di ramo. Possono dipendere dall’&quot;ID di accesso&quot; nei set di dati online, perché la maggior parte dei visitatori verrebbe autenticata durante la visita.
- I clienti possono inoltre disporre di ID proprietari univoci, ad esempio GUID o altri identificatori univoci universalmente.

### Dati identità

Se hai chiesto a una persona &quot;Qual è il tuo ID?&quot; senza ulteriore contesto, sarebbe difficile per loro fornire una risposta utile. Per la stessa logica, un valore stringa che rappresenta un valore di identità, sia che si tratti di un ID generato dal sistema o di un indirizzo e-mail, è completo solo se viene fornito con un qualificatore che fornisce il contesto del valore stringa: lo spazio dei nomi identity.

## Namespace e grafici di identità

I clienti possono interagire con il tuo marchio tramite una combinazione di canali online e offline, per cui è difficile riconciliare queste interazioni frammentate in un’unica identità del cliente.

[!DNL Experience Platform] affronta questa sfida attraverso due concetti:  [spazi ](#identity-namespaces) dei nomi delle identità e grafici  [delle identità](#identity-graphs).

Il seguente video è pensato per supportare la tua comprensione di identità e grafici di identità. Il video seguente illustra le tre funzionalità di raccolta identità, grafici identità e API. Descrive inoltre come gli algoritmi deterministici e probabilistici vengono utilizzati per creare grafici di identità privata e discute il ruolo dei grafici di identità privata, il grafico Co-op del servizio Adobe Experience Platform Identity e i grafici di terze parti.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

### Namespace Identity

Quando il cliente interagisce con il tuo marchio su più canali, inclusi web, applicazioni mobili, call center o una vetrina, può essere difficile comprenderli e distribuirli se non riesci a osservarne e monitorarne l’attività tra i vari canali.

Per comprendere il cliente su più dispositivi e canali, è innanzitutto necessario riconoscerlo in ciascun canale. Per ottenere questo risultato, Adobe Experience Platform utilizza i namespace di identità.
Uno spazio dei nomi di identità è un identificatore, ad esempio ID dispositivo o ID e-mail, utilizzato per fornire il contesto da cui provengono i dati. I namespace di identità vengono utilizzati per cercare o collegare singole identità e forniscono il contesto dei valori di identità per evitare conflitti tra dati. Ad esempio, l’ID &quot;123456&quot; può fare riferimento a una persona nel sistema eCommerce e a una persona diversa nel sistema di help desk. Per ulteriori informazioni, consulta la [panoramica dello spazio dei nomi identità](./namespaces.md).

### Grafici di identità

Un grafico di identità è una mappa delle relazioni tra diversi namespace di identità, che fornisce una rappresentazione visiva del modo in cui il cliente interagisce con il tuo marchio attraverso diversi canali.

Tutti i grafici di identità dei clienti vengono gestiti e aggiornati collettivamente da [!DNL Identity Service] in tempo quasi reale, in risposta all&#39;attività dei clienti.

[!DNL Identity Service] gestisce un grafico delle identità visibile solo dalla tua organizzazione e generato in base ai tuoi dati, denominato grafico privato. [!DNL Identity Service] potenzia il grafico privato quando un record di dati acquisito contiene più di un’identità, aggiungendo una relazione tra le identità trovate.

Come esempio dei potenziali tipi di fattori da considerare quando si forniscono ed etichettano i dati di identità, l&#39;uso di numeri di telefono come &quot;telefono di lavoro&quot; può comportare più relazioni di quanto si intende nel grafico di identità. Si può trovare che molti dipendenti si riferiscono allo stesso numero di lavoro, e che &quot;casa&quot; e &quot;mobile&quot; meglio servire a mantenere le relazioni il più preciso possibile.

Per ulteriori informazioni, consulta l’esercitazione sull’ [accesso al visualizzatore del grafico delle identità](./ui/identity-graph-viewer.md)

## Fornitura di dati di identità a [!DNL Identity Service]

Questa sezione descrive come vengono elaborati i dati forniti a Adobe Experience Platform prima di essere utilizzati da [!DNL Identity Service] per creare un grafico delle identità per ciascun cliente.

### Decidere sui campi di identità

A seconda della strategia di raccolta dati aziendale, i campi dati etichettati come identità determinano quali dati vengono inclusi nella mappa di identità. Per ottenere il massimo vantaggio da Adobe Experience Platform e le identità cliente più complete possibili, è necessario caricare sia i dati online che offline.

- I dati online sono dati che descrivono la presenza e il comportamento online, ad esempio nomi utente e indirizzi e-mail.

- I dati offline si riferiscono a dati che non sono direttamente correlati alla presenza online, come gli ID dai sistemi CRM. Questo tipo di dati rende le identità più solide e supporta la coesione dei dati tra i diversi sistemi.

### Creare spazi dei nomi di identità aggiuntivi

Anche se [!DNL Experience Platform] offre diversi namespace standard, potrebbe essere necessario creare altri namespace per suddividere in categorie le identità in modo appropriato. Per ulteriori informazioni, consulta la sezione relativa alla [visualizzazione e creazione di spazi dei nomi per la tua organizzazione](./namespaces.md) nella panoramica dello spazio dei nomi delle identità.

>[!NOTE]
>
>Gli spazi dei nomi di identità sono un qualificatore per le identità. Di conseguenza, una volta creato uno spazio dei nomi, non può essere eliminato.

### Includi dati di identità in [!DNL Experience Data Model] (XDM)

In qualità di framework standard con cui [!DNL Platform] organizza i dati dei clienti, [!DNL Experience Data Model] (XDM) consente la condivisione e comprensione dei dati tra [!DNL Experience Platform] e altri servizi che interagiscono con [!DNL Platform]. Per ulteriori informazioni, consulta la [Panoramica del sistema XDM](../xdm/home.md).

Gli schemi di record e serie temporali forniscono i mezzi per includere i dati di identità. Durante l’acquisizione dei dati, il grafico dell’identità crea nuove relazioni tra frammenti di dati provenienti da namespace diversi se questi condividono i dati di identità comuni.

### Contrassegno dei campi XDM come identità

Qualsiasi campo di tipo `string` negli schemi che implementano classi XDM di record o serie temporali può essere etichettato come campo di identità. Di conseguenza, tutti i dati acquisiti in quel campo saranno considerati dati di identità.

I campi di identità consentono anche il collegamento di identità se condividono dati PII comuni.
Ad esempio, etichettando i campi del numero di telefono come campi di identità, [!DNL Identity Service] esegue automaticamente il grafico delle relazioni con gli altri utenti che utilizzano lo stesso numero di telefono.

>[!NOTE]
>
>Lo spazio dei nomi delle identità risultanti viene fornito al momento dell’etichettatura del campo.

### Configura un set di dati per [!DNL Identity Service]

Durante il processo di acquisizione in streaming, [!DNL Identity Service ]estrae automaticamente i dati di identità dai dati di record e dalle serie temporali. Tuttavia, prima di poter acquisire i dati, questi devono essere abilitati per [!DNL Identity Service]. Per ulteriori informazioni, consulta l’esercitazione su [configurazione di un set di dati per il profilo cliente in tempo reale e il servizio Identity utilizzando le API](../profile/tutorials/dataset-configuration.md) .

### Inserire dati in [!DNL Identity Service]

[!DNL Identity Service] utilizza dati conformi a XDM inviati a  [!DNL Experience Platform] tramite  [acquisizione ](../ingestion/batch-ingestion/overview.md) batch o  [acquisizione in streaming](../ingestion/streaming-ingestion/overview.md).

Il video seguente è pensato per comprendere meglio il servizio Identity. Questo video illustra come etichettare i campi dati come identità, acquisire i dati di identità e verificare che siano stati inseriti nei grafici privati del servizio Adobe Experience Platform Identity.

>[!WARNING]
>
>L’ [!DNL Platform] interfaccia utente mostrata nel video seguente è obsoleta. Consulta la documentazione per le ultime schermate e funzionalità dell’interfaccia utente .

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## Governance dei dati

Adobe Experience Platform è stato creato tenendo presente la privacy e include un framework di governance dei dati per proteggere i dati PII dei clienti. I dati di identità nello spazio dei nomi &quot;e-mail&quot; o &quot;telefono&quot; sono crittografati per impostazione predefinita, ma per garantire che i dati sensibili vengano crittografati prima che vengano mantenuti, le etichette di utilizzo dei dati possono essere applicate ai dati così come vengono acquisiti o una volta che arrivano in [!DNL Platform]. Per ulteriori informazioni, consulta la [Panoramica sulla governance dei dati](../data-governance/home.md).

## Passaggi successivi

Ora che conosci i concetti chiave di [!DNL Identity Service] e il relativo ruolo all’interno di [!DNL Experience Platform], puoi iniziare a imparare a lavorare con il grafico delle identità utilizzando [[!DNL Identity Service API]](./api/getting-started.md).
