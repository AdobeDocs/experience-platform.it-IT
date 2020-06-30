---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Servizio Adobe Experience Platform Identity
topic: overview
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 0%

---


# [!DNL Identity Service]panoramica

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Ciò è reso più difficile quando i dati del cliente sono frammentati in sistemi diversi, causando l&#39;apparenza di più &quot;identità&quot; per ogni singolo cliente.  Adobe Experience Platform [!DNL Identity Service] consente di acquisire una visione migliore del cliente e del suo comportamento, collegando le identità tra dispositivi e sistemi, per offrire esperienze digitali personali e di forte impatto in tempo reale.

## Informazioni [!DNL Identity Service]

Ogni giorno, i clienti interagiscono con il tuo business e creano una relazione in continua crescita con il tuo marchio. Un cliente tipico può essere attivo in un numero qualsiasi di sistemi all&#39;interno dell&#39;infrastruttura dati dell&#39;azienda, come i sistemi di eCommerce, fedeltà e help desk. Lo stesso cliente può anche impegnarsi anonimamente su qualsiasi numero di dispositivi. [!DNL Identity Service] consente di mettere insieme un quadro completo del cliente, aggregando dati correlati che altrimenti potrebbero essere silenziati tra sistemi diversi.

Considera un esempio quotidiano della relazione tra un consumatore e il tuo marchio:

Mary ha un account sul tuo sito di eCommerce dove ha completato alcuni ordini in passato. Di solito usa il suo portatile personale per fare acquisti, dove accede ogni volta. Tuttavia, durante una delle sue visite utilizza il suo tablet per acquistare sandali, ma non effettua un ordine e non effettua l&#39;accesso.

A questo punto, l&#39;attività di Mary viene visualizzata come due profili separati: login eCommerce e dispositivo tablet, forse identificati dall&#39;ID dispositivo.

Mary riprende in seguito la sessione per tablet e fornisce il suo indirizzo e-mail durante la sottoscrizione alla newsletter. In questo modo, l&#39;assimilazione in streaming aggiunge una nuova identità come dati di record all&#39;interno del suo profilo. Di conseguenza, [!DNL Identity Service] ora collega l&#39;attività di Mary per i dispositivi tablet con la cronologia del suo account eCommerce.

Per il clic successivo sul tablet, il contenuto di destinazione potrebbe riflettere il profilo completo e la storia di Mary, piuttosto che un semplice tablet utilizzato da un acquirente sconosciuto.

Le relazioni di identità che [!DNL Identity Service] definiscono e mantengono sono sfruttate [!DNL Real-time Customer Profile] per creare un quadro completo di un cliente e delle sue interazioni con il tuo marchio. Per ulteriori informazioni, consulta la panoramica [Profilo cliente](../profile/home.md)in tempo reale.

### Identità

Un&#39;identità è un dato univoco per un&#39;entità, in genere una singola persona. Un&#39;identità, ad esempio un ID di login, un ECID o un ID fedeltà, viene definita identità **** nota.

Informazioni quali indirizzo e-mail e numero di telefono, utili per identificare direttamente un cliente. Di conseguenza, i dati PII vengono utilizzati per far corrispondere le identità multiple di un cliente ai diversi sistemi.

**Identità** sconosciute o anonime che separano un dispositivo senza identificare la persona che lo utilizza. Questa categoria include informazioni quali l&#39;indirizzo IP del visitatore e l&#39;ID del cookie. Anche se i dati comportamentali possono essere raccolti da un dispositivo utilizzando identità sconosciute, l&#39;associazione di tali identità tra dispositivi o supporti è limitata fino a quando il cliente non fornisce i dati PII durante il suo viaggio.

Come mostrato nell&#39;immagine seguente, le identità conosciute e anonime sono entrambe componenti importanti dei grafici [di](#identity-graphs)identità, che vengono discussi più avanti in questo documento.

![Cuciture di identità su Platform](./images/identity-service-stitching.png)

Esempi di [!DNL Identity Service] implementazioni:

- Un&#39;azienda di telecomunicazioni può basarsi sul valore &quot;numero di telefono&quot;, dove un numero di telefono fa riferimento allo stesso individuo di interesse sia per i set di dati offline che online.
- Una società retail può utilizzare &quot;indirizzo e-mail&quot; nei set di dati offline e l&#39;ECID nei set di dati online a causa dell&#39;alta percentuale di visitatori anonimi.
- Una banca potrebbe preferire il &quot;numero di conto&quot; nei set di dati offline, come le transazioni di ramo. Possono dipendere dall&#39;&quot;ID di accesso&quot; nei set di dati online, perché la maggior parte dei visitatori viene autenticata durante la visita.
- I clienti possono anche avere ID proprietari univoci, come GUID o altri identificatori univoci universalmente.

### Dati identità

Se hai chiesto a una persona &quot;Qual è il tuo ID?&quot; senza un ulteriore contesto, sarebbe difficile per loro fornire una risposta utile. Nella stessa logica, un valore di stringa che rappresenta un valore di identità, sia che si tratti di un ID generato dal sistema che di un indirizzo e-mail, è completo solo se viene fornito con un qualificatore che fornisce il contesto del valore stringa: lo spazio dei nomi dell&#39;identità.

## Spazi dei nomi e grafici di identità

I clienti possono interagire con il tuo marchio attraverso una combinazione di canali online e offline, il che ti permette di trovare il modo di conciliare queste interazioni frammentate in un&#39;unica identità cliente.

[!DNL Experience Platform] affronta questa sfida attraverso due concetti: [spazi dei nomi](#identity-namespaces) e grafici [di](#identity-graphs)identità.

### Spazi dei nomi delle identità

Quando il cliente interagisce con il tuo marchio su più canali, tra cui web, applicazioni mobili, call center o un negozio, può essere difficile comprenderlo e servirlo se non riesci a osservare e monitorare la loro attività su più canali.

Comprendere il cliente su più dispositivi e canali inizia riconoscendolo in ciascun canale.  Adobe Experience Platform ottiene questo risultato utilizzando spazi dei nomi di identità.
Uno spazio nomi identità è un identificatore, ad esempio l&#39;ID dispositivo o l&#39;ID e-mail, utilizzato per fornire il contesto da cui provengono i dati. Gli spazi dei nomi delle identità vengono utilizzati per cercare o collegare identità singole e forniscono contesto per i valori delle identità per evitare conflitti tra i dati. Ad esempio, l’ID &quot;123456&quot; può fare riferimento a una persona nel sistema eCommerce e a una persona diversa nel sistema di help desk. Per ulteriori informazioni, consultate la panoramica [dello spazio nomi](./namespaces.md)identità.

### Grafici di identità

Un grafico di identità è una mappa di relazioni tra diversi spazi dei nomi di identità, che fornisce una rappresentazione visiva di come il cliente interagisce con il proprio marchio tra canali diversi.

Tutti i grafici dell&#39;identità del cliente sono gestiti collettivamente e aggiornati [!DNL Identity Service] in tempo quasi reale, in risposta all&#39;attività del cliente.

[!DNL Identity Service] gestisce un grafico di identità visibile solo dalla tua organizzazione e basato sui dati, detto grafico privato. [!DNL Identity Service] amplia il grafico privato quando un record di dati assimilato contiene più identità, aggiungendo una relazione tra le identità trovate.

Come esempio dei potenziali tipi di fattori da considerare quando si forniscono ed etichettano i dati di identità, l&#39;uso di numeri di telefono come &quot;telefono di lavoro&quot; potrebbe portare a più relazioni di quanto si intende nel grafico di identità. Molti dipendenti fanno riferimento allo stesso numero di posti di lavoro, e che &quot;casa&quot; e &quot;mobile&quot; servono meglio a mantenere le relazioni il più possibile precise.

## Invio dei dati di identità a [!DNL Identity Service]

In questa sezione viene illustrato come i dati forniti al Adobe Experience Platform  vengono elaborati prima di essere utilizzati per [!DNL Identity Service] creare un grafico dell&#39;identità per ciascun cliente.

### Decidere sui campi di identità

A seconda della strategia aziendale di raccolta dei dati, i campi dati etichettati come identità determinano quali dati vengono inclusi nella mappa di identità. Per ottenere il massimo vantaggio  Adobe Experience Platform e le identità cliente più complete possibili, è necessario caricare sia i dati online che offline.

- I dati online sono dati che descrivono la presenza e il comportamento online, ad esempio nomi utente e indirizzi e-mail.

- I dati offline si riferiscono a dati che non sono direttamente correlati alla presenza online, come ID dai sistemi CRM. Questo tipo di dati rende le identità più solide e supporta la coesione dei dati tra i diversi sistemi.

### Creare spazi dei nomi di identità aggiuntivi

Anche se [!DNL Experience Platform] offre diversi spazi dei nomi standard, potrebbe essere necessario creare spazi di nomi aggiuntivi per classificare correttamente le identità. Per ulteriori informazioni, consultate la sezione sulla [visualizzazione e la creazione di spazi dei nomi per la vostra organizzazione](./namespaces.md) nella panoramica dello spazio dei nomi delle identità.

>[!NOTE] Gli spazi dei nomi delle identità sono un qualificatore per le identità. Di conseguenza, una volta creato uno spazio nomi, non può essere eliminato.

### Includi dati di identità in [!DNL Experience Data Model] (XDM)

Come framework standard per l&#39; [!DNL Platform] organizzazione dei dati dei clienti, [!DNL Experience Data Model] (XDM) consente di condividere e comprendere i dati tra [!DNL Experience Platform] e altri servizi che interagiscono con [!DNL Platform]. Per ulteriori informazioni, vedere la panoramica [del sistema](../xdm/home.md)XDM.

Gli schemi di record e di serie temporali forniscono i mezzi per includere i dati di identità. Durante l&#39;assimilazione dei dati, il grafico dell&#39;identità creerà nuove relazioni tra i frammenti di dati provenienti da spazi dei nomi diversi se questi vengono trovati a condividere dati di identità comuni.

### Contrassegnazione dei campi XDM come identità

Qualsiasi campo di tipo `string` negli schemi che implementa classi XDM di record o serie temporale può essere etichettato come campo di identità. Di conseguenza, tutti i dati immessi in quel campo saranno considerati dati di identità.

I campi di identità consentono inoltre il collegamento di identità se condividono dati PII comuni.
Ad esempio, etichettando i campi dei numeri di telefono come campi di identità, [!DNL Identity Service] traccia automaticamente le relazioni con gli altri individui che utilizzano lo stesso numero di telefono.

>[!NOTE] Lo spazio dei nomi delle identità risultanti viene fornito al momento in cui il campo è etichettato.

### Configurare un dataset per [!DNL Identity Service]

Durante il processo di assimilazione in streaming, estrae [!DNL Identity Service ]automaticamente i dati di identità dai dati dei record e delle serie temporali. Tuttavia, prima di poter acquisire i dati, questi devono essere attivati per [!DNL Identity Service]. Per ulteriori informazioni, consulta l’esercitazione sulla [configurazione di un set di dati per il profilo cliente e il servizio identità in tempo reale mediante l’utilizzo delle API](../profile/tutorials/dataset-configuration.md) .

### Assegna dati a [!DNL Identity Service]

[!DNL Identity Service] consuma i dati conformi a XDM inviati [!DNL Experience Platform] tramite caricamento [batch](../ingestion/batch-ingestion/overview.md) o caricamento [in streaming](../ingestion/streaming-ingestion/overview.md).

## Governance dei dati

 Adobe Experience Platform è stato creato tenendo presente la privacy e include un framework di governance dei dati per proteggere i dati PII del cliente. I dati di identità nello spazio dei nomi &quot;email&quot; o &quot;phone&quot; sono crittografati per impostazione predefinita, ma per garantire che i dati riservati siano crittografati prima che vengano memorizzati, le etichette di utilizzo dei dati possono essere applicate ai dati durante l&#39;assimilazione o al loro arrivo [!DNL Platform]. Per ulteriori informazioni, consulta la panoramica [sulla governance dei](../data-governance/home.md)dati.

## Passaggi successivi

Ora che hai compreso i concetti chiave di [!DNL Identity Service] e il suo ruolo all&#39;interno [!DNL Experience Platform], puoi iniziare a imparare come lavorare con il grafico di identità utilizzando il [!DNL Identity Service API](./api/getting-started.md).