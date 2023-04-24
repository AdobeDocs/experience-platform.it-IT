---
keywords: Experience Platform;home;argomenti popolari;identità;identità;grafici XDM;servizio identità;servizio Identity
solution: Experience Platform
title: Panoramica del servizio Identity
description: Il servizio Adobe Experience Platform Identity consente di acquisire una visione migliore del cliente e del suo comportamento attraverso il collegamento di identità tra dispositivi e sistemi, consentendo di fornire in tempo reale esperienze digitali personali e di forte impatto.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: ad9fb0bcc7bca55da432c72adc94d49e3c63ad6e
workflow-type: tm+mt
source-wordcount: '1839'
ht-degree: 7%

---

# Panoramica di [!DNL Identity Service]

Fornire esperienze digitali rilevanti richiede una comprensione completa del cliente. Ciò è reso più difficile quando i dati dei clienti sono frammentati in diversi sistemi, il che fa sì che ogni singolo cliente sembri avere più &quot;identità&quot;.

Il servizio Adobe Experience Platform Identity offre una panoramica completa dei clienti e del loro comportamento attraverso la creazione di identità tra dispositivi e sistemi, consentendo di fornire in tempo reale esperienze digitali personali di forte impatto.

Con [!DNL Identity Service], puoi:

- Assicurati che i tuoi clienti ricevano un’esperienza coerente, personalizzata e pertinente attraverso ogni interazione.
- Unisci diverse identità da diverse fonti e crea una visione completa dei tuoi clienti.
- Utilizza un grafico di identità per mappare diversi namespace di identità, fornendo una rappresentazione visiva di come i clienti interagiscono con il tuo marchio su diversi canali.

## Introduzione

Prima di immergersi nei dettagli di [!DNL Identity Service], ecco una breve sintesi dei termini chiave:

| Termine | Definizione |
| --- | --- |
| Identità | Un’identità è un dato univoco per un’entità, in genere una singola persona. Un&#39;identità, ad esempio un ID di accesso, un ECID o un ID fedeltà, viene anche definita &quot;identità nota&quot;. |
| ECID | Experience Cloud ID (ECID) è uno spazio dei nomi di identità condivisa utilizzato nelle applicazioni Experience Platform e Adobe Experience Cloud. ECID fornisce una base per l’identità del cliente e viene utilizzato come ID principale per i dispositivi e come nodo di base per i grafici di identità. Consulta la sezione [Panoramica ECID](./ecid.md) per ulteriori informazioni. |
| Spazio dei nomi identità | Uno spazio dei nomi delle identità consente di distinguere il contesto o il tipo di un’identità. Ad esempio, un’identità distingue “nome<span>@e-mail.com” come indirizzo e-mail o “443522” come ID CRM numerico. I namespace Identity vengono utilizzati per cercare le singole identità e fornire il contesto per i valori di identità. Questo consente di determinare che due [!DNL Profile] frammenti che contengono ID primari diversi, ma condividono lo stesso valore per `email` lo spazio dei nomi delle identità, infatti, è lo stesso individuo. Consulta la sezione [panoramica dello spazio dei nomi identità](./namespaces.md) per ulteriori informazioni. |
| Grafico di identità | Un grafico delle identità è una mappa delle relazioni tra identità diverse, che ti consente di visualizzare e comprendere meglio quali identità dei clienti sono unite e come. Guarda l’esercitazione su [utilizzo del visualizzatore grafico delle identità](./ui/identity-graph-viewer.md) per ulteriori informazioni. |
| Informazioni personali (PII) | Le informazioni PII sono informazioni che possono identificare direttamente un cliente, ad esempio un indirizzo e-mail o un numero di telefono. I valori PII vengono spesso utilizzati per la corrispondenza. identità multiple di un cliente tra diversi sistemi. |
| Identità sconosciute o anonime | Le identità sconosciute o anonime sono indicatori che isolano i dispositivi senza identificare la persona effettiva che utilizza il dispositivo. Le identità sconosciute e anonime includono informazioni quali l&#39;indirizzo IP di un visitatore e l&#39;ID cookie. Sebbene le identità sconosciute e anonime possano fornire dati comportamentali, sono limitate fino a quando un cliente non fornisce i propri dati PII. |

## Che cosa è [!DNL Identity Service]?

Ogni giorno i clienti interagiscono con il tuo business e instaurano una relazione in continuo aumento con il tuo marchio. Un cliente tipico può essere attivo in un numero qualsiasi di sistemi all&#39;interno dell&#39;infrastruttura dati della tua organizzazione, come i sistemi di e-commerce, fidelizzazione e help-desk. Lo stesso cliente può anche impegnarsi in modo anonimo su qualsiasi numero di dispositivi. [!DNL Identity Service] consente di creare un quadro completo del cliente, aggregando dati correlati che altrimenti potrebbero essere memorizzati in più sistemi diversi.

Considera un esempio quotidiano del rapporto di un consumatore con il tuo marchio:

- Mary ha un account sul tuo sito di e-commerce dove ha completato alcuni ordini in passato. Di solito usa il suo portatile personale per fare acquisti, dove accede ogni volta. Tuttavia, durante una delle sue visite utilizza il suo tablet per comprare sandali, ma non effettua un ordine e non effettua l&#39;accesso.
- A questo punto, l’attività di Mary viene visualizzata come due profili separati:
   - Accesso a e-commerce
   - Dispositivo tablet, forse identificato dall&#39;ID dispositivo
- Mary riprende in seguito la sessione del tablet e fornisce il suo indirizzo e-mail durante l&#39;iscrizione alla newsletter. In questo modo, l’acquisizione in streaming aggiunge una nuova identità come dati di record all’interno del suo profilo. Di conseguenza, [!DNL Identity Service] ora fa riferimento all’attività di Mary relativa ai dispositivi tablet con la cronologia del suo account di e-commerce.
- Al prossimo clic sul suo tablet, il tuo contenuto di destinazione potrebbe riflettere l&#39;intero profilo e la storia di Mary, piuttosto che un semplice tablet utilizzato da un acquirente sconosciuto.

![Unione delle identità su Platform](./images/identity-service-stitching.png)

Essenzialmente, [!DNL Identity Service] consente di creare un quadro completo del cliente, aggregando dati correlati che potrebbero altrimenti essere dispersi tra sistemi diversi. Le relazioni di identità che [!DNL Identity Service] Le definizioni e gli strumenti di manutenzione sono sfruttati dal Profilo cliente in tempo reale per creare un quadro completo di un cliente e delle sue interazioni con il tuo marchio. Per ulteriori informazioni, consulta la sezione [Panoramica del profilo cliente in tempo reale](../profile/home.md).

### Casi d’uso

Esempi di [!DNL Identity Service] le implementazioni includono:

- Un&#39;azienda di telecomunicazioni può basarsi sul valore &quot;numero di telefono&quot;, dove un numero di telefono fa riferimento allo stesso individuo di interesse sia per i set di dati offline che online.
- Una società di vendita al dettaglio può utilizzare &quot;indirizzo e-mail&quot; nei set di dati offline e ECID nei set di dati online a causa dell&#39;alta percentuale di visitatori anonimi.
- Una banca può preferire il &quot;numero di conto&quot; nei set di dati offline, ad esempio le transazioni di ramo. Possono dipendere dall’&quot;ID di accesso&quot; nei set di dati online, perché la maggior parte dei visitatori verrebbe autenticata durante la visita.
- I clienti possono inoltre disporre di ID proprietari univoci, ad esempio GUID o altri identificatori univoci universalmente.

## Spazio dei nomi identità {#identity-namespace}

>[!CONTEXTUALHELP]
>id="platform_identity_namespace"
>title="Spazi dei nomi delle identità"
>abstract="Uno spazio dei nomi delle identità consente di distinguere il contesto o il tipo di un’identità. Ad esempio, un’identità distingue “nome<span>@e-mail.com” come indirizzo e-mail o “443522” come ID CRM numerico."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_identity_value"
>title="Valori identità"
>abstract="Un valore di identità è un identificatore che rappresenta una persona, organizzazione o risorsa univoca. Il contesto o il tipo di identità che il valore rappresenta è definito da uno spazio dei nomi delle identità corrispondente. Quando si abbinano i dati dei record a frammenti di profilo, lo spazio dei nomi e il valore di identità devono corrispondere."
>text="Learn more in documentation"

Se hai chiesto a una persona &quot;Qual è il tuo ID?&quot; senza ulteriore contesto, sarebbe difficile per loro fornire una risposta utile. Per la stessa logica, un valore stringa che rappresenta un valore di identità, sia che si tratti di un ID generato dal sistema o di un indirizzo e-mail, è completo solo se viene fornito con un qualificatore che fornisce il contesto del valore stringa: lo spazio dei nomi identity.

I clienti possono interagire con il tuo marchio tramite una combinazione di canali online e offline, il che può comportare la sfida di riconciliare queste interazioni frammentate in un’unica identità del cliente.

Per comprendere il cliente su più dispositivi e canali, è innanzitutto necessario riconoscerlo in ciascun canale. A tal fine, Platform utilizza i namespace di identità. Uno spazio dei nomi di identità è un identificatore come E-mail o telefono, utilizzato per fornire contesto aggiuntivo alle identità dei clienti. I namespace di identità vengono utilizzati per cercare o collegare singole identità e fornire contesto per i valori di identità. Consulta la sezione [panoramica dello spazio dei nomi identità](./namespaces.md) per ulteriori informazioni.

## Grafici di identità

Un grafico di identità è una mappa delle relazioni tra i diversi namespace di identità, che consente di visualizzare e comprendere meglio quali sono le identità dei clienti unite e come. Guarda l’esercitazione su [utilizzo del visualizzatore grafico delle identità](./ui/identity-graph-viewer.md) per ulteriori informazioni.

Il seguente video è pensato per supportare la tua comprensione di identità e grafici di identità.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## Fornitura di dati di identità a [!DNL Identity Service]

Questa sezione descrive come vengono elaborati i dati forniti a Adobe Experience Platform prima di essere utilizzati da [!DNL Identity Service] per creare un grafico delle identità per ogni cliente.

### Decidere sui campi di identità

A seconda della strategia di raccolta dati aziendale, i campi dati etichettati come identità determinano quali dati vengono inclusi nella mappa di identità. Per ottenere il massimo vantaggio da Adobe Experience Platform e le identità cliente più complete possibili, è necessario caricare sia i dati online che offline.

- I dati online sono dati che descrivono la presenza e il comportamento online, ad esempio nomi utente e indirizzi e-mail.

- I dati offline si riferiscono a dati che non sono direttamente correlati alla presenza online, come gli ID dai sistemi CRM. Questo tipo di dati rende le identità più solide e supporta la coesione dei dati tra i diversi sistemi.

### Creare spazi dei nomi di identità aggiuntivi

Sebbene Experience Platform offra una varietà di namespace standard, potrebbe essere necessario creare altri namespace per classificare in modo appropriato le identità. Per ulteriori informazioni, consulta la sezione su [visualizzazione e creazione di spazi dei nomi per la tua organizzazione](./namespaces.md) nella panoramica dello spazio dei nomi identità.

>[!NOTE]
>
>Gli spazi dei nomi di identità sono un qualificatore per le identità. Di conseguenza, una volta creato uno spazio dei nomi, non può essere eliminato.

### Includi dati di identità in [!DNL Experience Data Model] (XDM)

Come quadro standardizzato [!DNL Platform] organizza i dati dei clienti, [!DNL Experience Data Model] (XDM) consente la condivisione e comprensione dei dati tra Experience Platform e altri servizi che interagiscono con [!DNL Platform]. Per ulteriori informazioni, consulta la sezione [Panoramica del sistema XDM](../xdm/home.md).

Gli schemi di record e serie temporali forniscono i mezzi per includere i dati di identità. Durante l’acquisizione dei dati, il grafico dell’identità crea nuove relazioni tra frammenti di dati provenienti da namespace diversi se questi condividono i dati di identità comuni.

### Contrassegno dei campi XDM come identità

Qualsiasi campo di tipo `string` negli schemi che implementano le classi XDM di record o serie temporali possono essere etichettate come campo di identità. Di conseguenza, tutti i dati acquisiti in quel campo saranno considerati dati di identità.

>[!NOTE]
>
>I campi tipo matrice e tipo mappa non sono supportati e non possono essere contrassegnati ed etichettati come campi di identità.

I campi di identità consentono anche il collegamento di identità se condividono dati PII comuni.
Ad esempio, etichettando i campi del numero di telefono come campi di identità, [!DNL Identity Service] traccia automaticamente le relazioni con gli altri individui che utilizzano lo stesso numero di telefono.

>[!NOTE]
>
>Lo spazio dei nomi delle identità risultanti viene fornito al momento dell’etichettatura del campo.

### Configurare un set di dati per [!DNL Identity Service]

Durante il processo di acquisizione in streaming, [!DNL Identity Service ]estrae automaticamente i dati di identità dai dati di record e dalle serie temporali. Tuttavia, prima di poter acquisire i dati, è necessario attivarli per [!DNL Identity Service]. Guarda l’esercitazione su  [configurazione di un set di dati per il profilo cliente in tempo reale e il servizio Identity tramite API](../profile/tutorials/dataset-configuration.md) per ulteriori informazioni.

### Inserire dati in [!DNL Identity Service]

[!DNL Identity Service] consuma i dati conformi a XDM inviati ad Experience Platform da [ingestione in batch](../ingestion/batch-ingestion/overview.md) o [acquisizione in streaming](../ingestion/streaming-ingestion/overview.md).

Il video seguente è pensato per comprendere meglio il servizio Identity. Questo video illustra come etichettare i campi dati come identità, acquisire i dati di identità e verificare che siano stati inseriti nei grafici privati del servizio Adobe Experience Platform Identity.

>[!WARNING]
>
>La [!DNL Platform] L’interfaccia utente mostrata nel video seguente è obsoleta. Consulta la documentazione per le ultime schermate e funzionalità dell’interfaccia utente .

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## Governance dei dati

Adobe Experience Platform è stato creato tenendo presente la privacy e include un framework di governance dei dati per proteggere i dati PII dei clienti. I dati di identità nello spazio dei nomi &quot;e-mail&quot; o &quot;telefono&quot; sono crittografati per impostazione predefinita, ma per garantire che i dati sensibili vengano crittografati prima che vengano mantenuti, le etichette di utilizzo dei dati possono essere applicate ai dati così come vengono acquisiti o una volta che arrivano in [!DNL Platform]. Per ulteriori informazioni, leggere il [Panoramica sulla governance dei dati](../data-governance/home.md).

## Passaggi successivi

Ora che hai capito i concetti chiave di [!DNL Identity Service] e il suo ruolo all&#39;interno dell&#39;Experience Platform, puoi iniziare a imparare a lavorare con il tuo grafico di identità utilizzando [[!DNL Identity Service API]](./api/getting-started.md).
