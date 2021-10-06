---
keywords: profilo rtcdp;profili rtcdp;identità rtcdp;criteri di unione rtcdp;profilo cliente in tempo reale
title: Guida all’interfaccia utente del profilo account
description: Utilizzando i profili account, Real-time Customer Data Platform B2B Edition consente di unificare le informazioni account da più sorgenti. Questa guida fornisce dettagli sull’interazione con i profili account nell’interfaccia utente di Adobe Experience Platform.
source-git-commit: 5301cf870052f537a34913beb0b814212bdaadaa
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 0%

---


# Guida all’interfaccia utente del profilo account

>[!IMPORTANT]
>
>Real-time Customer Data Platform B2B Edition è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

>[!NOTE]
>
>I profili account sono disponibili solo per i clienti Real-time Customer Data Platform B2B Edition. Per ulteriori informazioni su Real-time CDP, incluse le funzioni e le funzionalità disponibili per ogni tipo di licenza, si prega di iniziare leggendo la [Panoramica di Real-time CDP](../overview.md).

I profili account ti consentono di unificare le informazioni dell’account da più sorgenti. Questa visualizzazione unificata di un account riunisce dati provenienti da diversi canali di marketing e dai diversi sistemi che la tua organizzazione sta attualmente utilizzando per memorizzare le informazioni sull’account del cliente. Questo documento fornisce una guida all’interazione con i profili account tramite le funzionalità Real-time CDP e B2B Edition disponibili nell’interfaccia utente di Adobe Experience Platform (UI).

## Sfoglia profili account

Per sfogliare i profili di account, inizia selezionando **[!UICONTROL Profili]** in Account nella navigazione a sinistra.

![](images/b2b-account-browse.png)

Nella scheda **[!UICONTROL Sfoglia]** è possibile esplorare i profili dell&#39;account utilizzando un ID account di un&#39;origine aziendale connessa o immettendo direttamente i dettagli dell&#39;origine.

![](images/b2b-account-browse-by.png)

### Sfoglia per [!UICONTROL Origine enterprise connessa]

Per sfogliare i profili account in base a un&#39;origine enterprise connessa, è innanzitutto necessario selezionare un&#39;origine connessa utilizzando il pulsante di selezione accanto al campo **[!UICONTROL Origine]**.

![](images/b2b-account-browse.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Seleziona origine]**, in cui è possibile selezionare un&#39;origine in base alle connessioni stabilite dall&#39;organizzazione.

>[!NOTE]
>
>L&#39;organizzazione può disporre di più origini configurate per lo stesso provider di servizi (ad esempio, Marketo), pertanto è importante rivedere il nome della connessione, il sistema di origine e l&#39;istanza del sistema di origine per assicurarsi che la ricerca venga eseguita dall&#39;istanza di origine corretta.

Per ulteriori informazioni sulla connessione delle origini aziendali, consulta la [panoramica delle origini](../sources/sources-overview.md).

![](images/b2b-account-select-source.png)

È possibile scegliere un&#39;origine selezionando il pulsante di scelta accanto al nome della connessione, quindi utilizzare **[!UICONTROL Seleziona]** per tornare alla scheda [!UICONTROL Sfoglia].

Con una sorgente selezionata, è ora necessario inserire un **[!UICONTROL ID account]** relativo all&#39;origine. Ad esempio, la selezione di un’origine Salesforce richiede l’inserimento di un ID account dall’istanza Salesforce per visualizzare il profilo account associato a tale ID.

>[!NOTE]
>
>Per gli ID account Marketo, è possibile fare riferimento a due possibili tabelle account, pertanto devi utilizzare una sintassi specifica per assicurarti di visualizzare l’account corretto.
>
>La sintassi standard più comune è l&#39;ID account Marketo aggiunto da `.mkto_org` (ad esempio, `1234567.mkto_org`). I clienti Marketo di Marketing basati su account possono avere valori aggiuntivi che si trovano utilizzando l&#39;ID account Marketo aggiunto da `.mkto_account`. Se non sai con certezza quale sintassi utilizzare, rivolgiti al tuo amministratore Marketo.

![](images/b2b-account-browse-id.png)

### Sfoglia per [!UICONTROL Altro]

Real-time CDP, B2B Edition supporta la possibilità di eseguire una ricerca diretta consentendo di inserire un **[!UICONTROL Nome origine]**, **[!UICONTROL Istanza sorgente]** e **[!UICONTROL ID account]** per un account che si desidera visualizzare. Inserendo direttamente il nome e l’istanza di origine, fornisci il contesto necessario per consentire ad Experience Platform la ricerca e la visualizzazione dei dati di profilo account corretti.

La capacità di eseguire una ricerca diretta è utile in circostanze in cui non è possibile una connessione sorgente diretta ai dati. Ad esempio, se la tua organizzazione dispone di criteri di governance dei dati che impediscono la connessione diretta a un sistema di gestione delle relazioni con i clienti, puoi esportare tali dati in un sistema di archiviazione cloud e quindi trasferirli in Experience Platform.

Un altro esempio potrebbe essere la trasformazione dei dati che si sta effettuando tra il momento in cui lascia un sistema ed entra in Platform. Puoi utilizzare la funzionalità di ricerca diretta per fornire contesto per i dati (ad esempio per specificare che si tratta di dati Marketo, nonostante provengano, ad esempio, da un bucket Amazon S3) in modo che il sistema sappia dove cercare e come eseguire correttamente il rendering dei dati.

![](images/b2b-account-browse-adhoc.png)

## Visualizza dettagli profilo account

Dopo aver utilizzato la scheda **[!UICONTROL Sfoglia]** per individuare un profilo account, selezionando l&#39; **[!UICONTROL ID profilo]** viene aperta la scheda **[!UICONTROL Dettagli]** per il profilo account. Le informazioni di profilo visualizzate nella scheda **[!UICONTROL Dettaglio]** sono state unite da più frammenti di profilo per formare una singola visualizzazione del singolo account. Ciò include dettagli dell&#39;account come attributi di base e dati sui social media.

I campi predefiniti visualizzati possono essere modificati anche a livello organizzativo per visualizzare gli attributi di profilo dell’account preferiti.

>[!NOTE]
>
>Funzionalità simili sono disponibili per i profili dei clienti e è stata creata una guida dettagliata con istruzioni per aggiungere e rimuovere attributi, ridimensionare pannelli e così via. Per ulteriori informazioni, leggi la [guida alla personalizzazione dei dettagli del profilo](../../profile/ui/profile-customization.md) .

![](images/b2b-account-details.png)

Puoi visualizzare ulteriori dettagli relativi all’account selezionando un’altra delle schede disponibili. Queste schede includono attributi, persone e la scheda opportunità che mostra opportunità aperte e chiuse correlate all’account nei sistemi aziendali. Per ulteriori informazioni su ciascuna scheda, consulta le sezioni seguenti.

## Scheda Attributi

La scheda **[!UICONTROL Attributi]** elenca tutte le informazioni sui record relative all&#39;account. Ciò include i dati attributo provenienti da più origini che sono stati uniti per formare una singola vista dell’account.

Oltre a poter visualizzare i dati in un elenco, puoi utilizzare la barra di ricerca per cercare attributi specifici o visualizzare i dati del record come JSON.

![](images/b2b-account-attributes.png)

## Scheda Persone

La scheda **[!UICONTROL Persone]** fornisce un elenco di singole persone associate all’account. Queste persone possono essere contatti e lead da diversi sistemi aziendali gestiti da diversi team all&#39;interno della tua organizzazione, ma in Real-time CDP, B2B Edition sono presentati insieme come un unico elenco che ti permette di vedere una visione più olistica dei tuoi contatti del tuo account.

>[!NOTE]
>
>La scheda [!UICONTROL Persone] visualizza un elenco di fino a 25 persone associate all’account. Per account con più di 25 persone associate, il sistema mostra un campionamento casuale di 25 record.

Oltre a mostrarti un&#39;istantanea delle informazioni per il contatto, ogni persona elencata include anche un **[!UICONTROL ID profilo]**, che è un collegamento cliccabile che ti consente di esplorare il Profilo cliente in tempo reale per quella persona. Per ulteriori informazioni sulla visualizzazione dei profili dei singoli clienti relativi ai tuoi account, visita la guida per [profili di navigazione in Real-time CDP, B2B Edition](../profile/profile-browse.md).

![](images/b2b-account-people.png)

## Scheda Opportunità

La scheda **[!UICONTROL Opportunità]** fornisce informazioni sulle opportunità aperte e chiuse relative all’account. Queste opportunità possono essere acquisite in Experience Platform da più sorgenti, tuttavia Real-time CDP, B2B Edition rende facile per gli esperti di marketing vedere tutte queste opportunità insieme in un&#39;unica posizione.

>[!NOTE]
>
>La scheda [!UICONTROL Opportunità] visualizza un elenco di fino a 25 opportunità associate all’account. Per account con più di 25 opportunità associate, il sistema mostra un campionamento casuale di 25 record.

Ogni opportunità include informazioni quali il nome dell’opportunità, la sua quantità, lo stadio e se l’opportunità è aperta, chiusa, vinta o persa.

![](images/b2b-account-opportunities.png)
