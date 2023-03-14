---
keywords: Experience Platform;home;argomenti popolari;identità;identità;grafi XDM;servizio identità;servizio identità
solution: Experience Platform
title: Panoramica del servizio Identity
description: Il servizio Adobe Experience Platform Identity consente di ottenere una visione migliore del cliente e del suo comportamento, collegando le identità tra dispositivi e sistemi diversi e consentendo di fornire esperienze digitali personali e di impatto in tempo reale.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: ad9fb0bcc7bca55da432c72adc94d49e3c63ad6e
workflow-type: tm+mt
source-wordcount: '1839'
ht-degree: 0%

---

# Panoramica di [!DNL Identity Service]

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Questo è reso più difficile quando i dati del cliente sono frammentati tra sistemi diversi, facendo apparire ogni singolo cliente con più &quot;identità&quot;.

Il servizio Adobe Experience Platform Identity offre una panoramica completa dei clienti e del loro comportamento, collegando le identità attraverso diversi dispositivi e sistemi e consentendo di offrire esperienze digitali personali e di forte impatto in tempo reale.

Con [!DNL Identity Service], è possibile:

- Assicurati che i tuoi clienti ricevano un’esperienza coerente, personalizzata e rilevante tramite ogni interazione.
- Unisci diverse identità da sorgenti diverse e crea una visualizzazione completa dei tuoi clienti.
- Utilizza un grafo di identità per mappare diversi spazi dei nomi di identità, fornendo una rappresentazione visiva di come i clienti interagiscono con il tuo marchio su canali diversi.

## Introduzione

Prima di immergerti nei dettagli di [!DNL Identity Service], ecco una breve sintesi dei termini chiave:

| Termine | Definizione |
| --- | --- |
| Identità | Un’identità è un dato univoco per un’entità, in genere una singola persona. Un’identità, ad esempio un ID di accesso, ECID o ID fedeltà, viene indicata anche come &quot;identità nota&quot;. |
| ECID | L’ID Experience Cloud (ECID) è uno spazio dei nomi di identità condiviso e utilizzato nelle applicazioni Experience Platform e Adobe Experience Cloud. ECID fornisce una base per l’identità del cliente e viene utilizzato come ID principale per i dispositivi e come nodo di base per i grafici di identità. Consulta la [Panoramica di ECID](./ecid.md) per ulteriori informazioni. |
| Spazio dei nomi dell’identità | Uno spazio dei nomi delle identità serve a distinguere il contesto o il tipo di un’identità. Ad esempio, un’identità distingue &quot;name&quot;<span>@email.com&quot; come indirizzo e-mail o &quot;443522&quot; come ID CRM numerico. Gli spazi dei nomi delle identità vengono utilizzati per cercare le singole identità e fornire il contesto per i valori di identità. Questo consente di determinare che due [!DNL Profile] frammenti che contengono ID primari diversi, ma condividono lo stesso valore per `email` lo spazio dei nomi dell’identità, sono in realtà lo stesso individuo. Consulta la [panoramica dello spazio dei nomi delle identità](./namespaces.md) per ulteriori informazioni. |
| Grafo identità | Un grafo di identità è una mappa di relazioni tra identità diverse, che ti consente di visualizzare e comprendere meglio quali identità dei clienti sono unite tra loro e come. Guarda il tutorial su [utilizzo del visualizzatore del grafico delle identità](./ui/identity-graph-viewer.md) per ulteriori informazioni. |
| Informazioni personali (PII) | I dati PII sono informazioni che possono identificare direttamente un cliente, ad esempio un indirizzo e-mail o un numero di telefono. I valori PII vengono spesso utilizzati per la corrispondenza. le identità multiple di un cliente su diversi sistemi. |
| Identità sconosciute o anonime | Identità sconosciute o anonime sono indicatori che isolano i dispositivi senza identificare la persona effettiva che utilizza il dispositivo. Le identità sconosciute e anonime includono informazioni quali l’indirizzo IP e l’ID cookie di un visitatore. Anche se le identità sconosciute e anonime possono fornire dati comportamentali, sono limitate fino a quando un cliente non fornisce i suoi dati PII. |

## Che cosa è [!DNL Identity Service]?

Ogni giorno, i clienti interagiscono con la tua azienda e stabiliscono una relazione in continua crescita con il tuo marchio. Un cliente tipico può essere attivo in qualsiasi numero di sistemi all’interno dell’infrastruttura dati della tua organizzazione, ad esempio i sistemi di e-commerce, fidelizzazione e help desk. Lo stesso cliente può anche impegnarsi in modo anonimo su qualsiasi numero di dispositivi. [!DNL Identity Service] consente di creare un quadro completo del cliente, aggregando dati correlati che potrebbero altrimenti essere inseriti in silos in sistemi diversi.

Prendi in considerazione un esempio quotidiano della relazione di un consumatore con il tuo marchio:

- Mary ha un account sul tuo sito di e-commerce in cui ha completato alcuni ordini in passato. Di solito usa il suo laptop personale per fare acquisti, dove accede ogni volta. Tuttavia, durante una delle sue visite utilizza il suo tablet per fare acquisti di sandali, ma non effettua un ordine e non accede.
- A questo punto, l’attività di Mary viene visualizzata come due profili separati:
   - Il suo accesso e-commerce
   - Il suo dispositivo tablet, forse identificato dall&#39;ID dispositivo
- Mary successivamente riprende la sessione del tablet e fornisce il suo indirizzo e-mail durante l’abbonamento alla newsletter. In questo modo, l’acquisizione in streaming aggiunge una nuova identità come dati di record all’interno del suo profilo. Di conseguenza, [!DNL Identity Service] ora mette in relazione l’attività sul tablet di Mary con la cronologia del suo account di e-commerce.
- Al prossimo clic sul tablet, il contenuto mirato potrebbe riflettere il profilo completo e la storia di Mary, piuttosto che solo un tablet utilizzato da un acquirente sconosciuto.

![Unione delle identità su Platform](./images/identity-service-stitching.png)

Essenzialmente, [!DNL Identity Service] consente di creare un quadro completo del cliente, aggregando dati correlati che potrebbero altrimenti essere dispersi in sistemi diversi. Le relazioni di identità che [!DNL Identity Service] Le definizioni e i processi di manutenzione vengono utilizzati da Real-Time Customer Profile per creare un quadro completo di un cliente e delle sue interazioni con il brand. Per ulteriori informazioni, vedere [Panoramica del profilo cliente in tempo reale](../profile/home.md).

### Casi d’uso

Esempi di [!DNL Identity Service] Le implementazioni includono:

- Una società di telecomunicazioni può basarsi sul valore &quot;numero di telefono&quot;, in cui un numero di telefono si riferisce allo stesso individuo di interesse in set di dati offline e online.
- Una società di vendita al dettaglio può utilizzare &quot;indirizzo e-mail&quot; nei set di dati offline e ECID nei set di dati online a causa dell’alta percentuale di visitatori anonimi.
- Una banca può preferire il &quot;numero di conto&quot; nei set di dati offline, ad esempio nelle transazioni di filiale. Possono dipendere da &quot;login ID&quot; nei set di dati online, perché la maggior parte dei visitatori verrebbe autenticata durante la visita.
- I clienti possono inoltre disporre di ID proprietari univoci, ad esempio GUID o altri identificatori univoci universali.

## Spazio dei nomi dell’identità {#identity-namespace}

>[!CONTEXTUALHELP]
>id="platform_identity_namespace"
>title="Spazi dei nomi delle identità"
>abstract="Uno spazio dei nomi delle identità serve a distinguere il contesto o il tipo di un’identità. Ad esempio, un’identità distingue &quot;name&quot;<span>@email.com&quot; come indirizzo e-mail o &quot;443522&quot; come ID CRM numerico."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_identity_value"
>title="Valori identità"
>abstract="Un valore di identità è un identificatore che rappresenta un individuo, un’organizzazione o una risorsa univoca. Il contesto o il tipo di identità rappresentato dal valore è definito da uno spazio dei nomi di identità corrispondente. Quando si abbinano dati record tra frammenti di profilo, lo spazio dei nomi e il valore di identità devono corrispondereQuando si abbinano dati record tra frammenti di profilo, lo spazio dei nomi e il valore di identità devono corrispondere."
>text="Learn more in documentation"

Se hai chiesto a una persona &quot;Qual è il tuo ID?&quot; senza ulteriore contesto, sarebbe difficile per loro fornire una risposta utile. Secondo la stessa logica, un valore stringa che rappresenta un valore di identità, sia esso un ID generato dal sistema o un indirizzo e-mail, è completo solo se fornito con un qualificatore che fornisce il contesto del valore stringa: lo spazio dei nomi dell’identità.

I clienti possono interagire con il brand attraverso una combinazione di canali online e offline, con conseguente sfida di come riconciliare tali interazioni frammentate in un’unica identità cliente.

La comprensione del cliente su più dispositivi e canali inizia con il riconoscimento in ciascun canale. Platform ottiene questo risultato utilizzando spazi dei nomi di identità. Uno spazio dei nomi delle identità è un identificatore come e-mail o telefono, utilizzato per fornire contesto aggiuntivo alle identità dei clienti. Gli spazi dei nomi delle identità vengono utilizzati per cercare o collegare singole identità e fornire contesto per i valori di identità. Consulta la [panoramica dello spazio dei nomi delle identità](./namespaces.md) per ulteriori informazioni.

## Grafici delle identità

Un grafo di identità è una mappa di relazioni tra diversi spazi dei nomi di identità, che ti consente di visualizzare e comprendere meglio quali identità dei clienti sono unite tra loro e come. Guarda il tutorial su [utilizzo del visualizzatore del grafico delle identità](./ui/identity-graph-viewer.md) per ulteriori informazioni.

Il video seguente ha lo scopo di aiutarti a comprendere le identità e i grafici di identità.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## Fornitura di dati di identità a [!DNL Identity Service]

Questa sezione descrive come vengono elaborati i dati forniti a Adobe Experience Platform prima di essere utilizzati da [!DNL Identity Service] per creare un grafico delle identità per ciascun cliente.

### Decidere sui campi di identità

A seconda della strategia di raccolta dati aziendale, i campi dati etichettati come identità determinano quali dati includere nella mappa delle identità. Per ottenere il massimo vantaggio da Adobe Experience Platform e dalle identità cliente più complete possibili, devi caricare dati sia online che offline.

- I dati online sono dati che descrivono la presenza e il comportamento online, ad esempio nomi utente e indirizzi e-mail.

- I dati offline si riferiscono a dati che non sono direttamente correlati alla presenza online, come gli ID provenienti dai sistemi CRM. Questo tipo di dati rende le identità più solide e supporta la coesione dei dati tra sistemi diversi.

### Creare spazi dei nomi di identità aggiuntivi

Sebbene Experience Platform offra diversi spazi dei nomi standard, potrebbe essere necessario creare spazi dei nomi aggiuntivi per categorizzare correttamente le identità. Per ulteriori informazioni, consulta la sezione su [visualizzazione e creazione di spazi dei nomi per l’organizzazione](./namespaces.md) nella panoramica dello spazio dei nomi delle identità.

>[!NOTE]
>
>Gli spazi dei nomi di identità sono un qualificatore per le identità. Di conseguenza, una volta creato, uno spazio dei nomi non può essere eliminato.

### Includi dati di identità in [!DNL Experience Data Model] (XDM)

Come quadro standardizzato mediante il quale [!DNL Platform] organizza i dati dei clienti, [!DNL Experience Data Model] (XDM) consente la condivisione e la comprensione dei dati tra Experience Platform e altri servizi che interagiscono con [!DNL Platform]. Per ulteriori informazioni, consulta [Panoramica del sistema XDM](../xdm/home.md).

Sia gli schemi di record che quelli di serie temporali forniscono i mezzi per includere i dati di identità. Quando i dati vengono acquisiti, il grafico delle identità crea nuove relazioni tra frammenti di dati da spazi dei nomi diversi se tali frammenti condividono dati di identità comuni.

### Marcatura dei campi XDM come identità

Qualsiasi campo di tipo `string` negli schemi che implementano classi XDM di record o serie temporali, può essere etichettato come un campo di identità. Di conseguenza, tutti i dati acquisiti in quel campo verrebbero considerati dati di identità.

>[!NOTE]
>
>I campi di tipo matrice e mappa non sono supportati e non possono essere contrassegnati ed etichettati come campi di identità.

I campi di identità consentono anche il collegamento di identità se condividono dati PII comuni.
Ad esempio, etichettando i campi del numero di telefono come campi di identità, [!DNL Identity Service] crea automaticamente un grafico delle relazioni con gli altri individui che utilizzano lo stesso numero di telefono.

>[!NOTE]
>
>Lo spazio dei nomi delle identità risultanti viene fornito quando il campo viene etichettato.

### Configurare un set di dati per [!DNL Identity Service]

Durante il processo di acquisizione in streaming, [!DNL Identity Service ]estrae automaticamente i dati di identità dai dati di record e serie temporali. Tuttavia, prima che i dati possano essere acquisiti, devono essere abilitati per [!DNL Identity Service]. Guarda il tutorial su  [configurazione di un set di dati per Real-Time Customer Profile e Identity Service tramite API](../profile/tutorials/dataset-configuration.md) per ulteriori informazioni.

### Acquisire dati in [!DNL Identity Service]

[!DNL Identity Service] utilizza dati conformi a XDM inviati all’Experience Platform da [acquisizione batch](../ingestion/batch-ingestion/overview.md) o [acquisizione in streaming](../ingestion/streaming-ingestion/overview.md).

Il video seguente ha lo scopo di illustrare il servizio Identity. Questo video illustra come etichettare i campi dati come identità, acquisire i dati di identità e verificare che siano stati inseriti nel grafico privato del servizio Adobe Experience Platform Identity.

>[!WARNING]
>
>Il [!DNL Platform] L’interfaccia utente mostrata nel video seguente non è aggiornata. Consulta la documentazione per le schermate e le funzionalità più recenti dell’interfaccia utente.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## Governance dei dati

Adobe Experience Platform è stato creato pensando alla privacy e include un framework di governance dei dati per proteggere i dati PII dei clienti. I dati di identità nello spazio dei nomi &quot;e-mail&quot; o &quot;telefono&quot; sono crittografati per impostazione predefinita, ma per garantire che i dati sensibili siano crittografati prima che vengano mantenuti, le etichette di utilizzo dei dati possono essere applicate ai dati al momento dell’acquisizione o al momento dell’arrivo [!DNL Platform]. Per ulteriori informazioni, leggere [Panoramica sulla governance dei dati](../data-governance/home.md).

## Passaggi successivi

Ora che conosci i concetti chiave di [!DNL Identity Service] e il suo ruolo all’interno di Experience Platform, puoi imparare a lavorare con il grafico delle identità utilizzando [[!DNL Identity Service API]](./api/getting-started.md).
