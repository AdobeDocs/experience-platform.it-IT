---
title: Casi di utilizzo della segmentazione per Real-time CDP B2B Edition
description: Panoramica dei vari casi d’uso disponibili in tempo reale CDP B2B Edition.
exl-id: 2a99b85e-71b3-4781-baf7-a4d5436339d3
source-git-commit: 1fed0cf37e7297c21330ebf51ae15054aa21c781
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 0%

---

# Casi d’uso della segmentazione per Real-time Customer Data Platform B2B Edition

Questo documento fornisce esempi di definizioni di segmenti in Real-time CDP B2B Edition e di come diversi tipi di attributi possono essere combinati per i casi d’uso comuni B2B. Per capire come le destinazioni si adattano al tuo flusso di lavoro B2B, consulta [esercitazione end-to-end](../b2b-tutorial.md#create-a-segment-to-evaluate-your-data).

>[!NOTE]
>
>Gli attributi richiesti per questi casi d’uso di segmentazione sono disponibili solo per i clienti Real-time Customer Data Platform B2B Edition. Se non utilizzi Real-time Customer Data Platform B2B Edition, consulta la sezione [panoramica sulla segmentazione](./segmentation-overview.md) invece.

## Prerequisiti {#prerequisites}

Prima di poter utilizzare gli attributi di segmentazione per le classi B2B, è necessario completare i seguenti passaggi:

1. Creare schemi che utilizzano le classi B2B. Le classi B2B Edition includono Account, Campaign, Opportunity, Marketing List e altro ancora. Per informazioni su [come impostare schemi da utilizzare con le classi B2B](../schemas/b2b.md) consulta la documentazione sullo schema.
1. Crea relazioni tra gli schemi B2B Experience Data Model (XDM). I segmenti basati sugli attributi B2B Edition richiedono relazioni tra le classi per utilizzare appieno la funzionalità estesa di segmentazione B2B. Consulta la documentazione su [come definire una relazione tra due schemi B2B](../../xdm/tutorials/relationship-b2b.md) per ulteriori informazioni.
1. Acquisisci dati utilizzando set di dati basati sugli schemi B2B. Consulta la documentazione sulle sorgenti per [informazioni su come acquisire i dati](../../sources/connectors/adobe-applications/marketo/marketo.md).
1. Leggi la sezione [Guida utente di Segment Builder](../../segmentation/ui/segment-builder.md) per istruzioni più dettagliate su come creare i segmenti.

Una volta soddisfatti questi requisiti, puoi combinare questi attributi per i casi d’uso comuni B2B.

## Introduzione {#getting-started}

Una volta che gli schemi di unione per le classi B2B hanno relazioni stabilite e sono stati utilizzati per acquisire dati, i loro attributi sono resi disponibili nella barra a sinistra del Generatore di segmenti.

Le classi B2B e i relativi attributi sono aggiunti con un `B2B` all’interno dell’area di lavoro Segmentazione per distinguerli da quelli disponibili come standard in Real-time Customer Data Platform.

Per creare in modo efficace segmenti per i casi di utilizzo B2B, è importante avere una conoscenza approfondita dello schema e capire come si presenta il modello di dati. È inoltre utile conoscere il percorso che i dati prendono da un oggetto dati all’altro.

L&#39;immagine seguente illustra le relazioni tra le classi B2B disponibili in Real-time CDP B2B Edition.

![Classe B2B ERD](../assets/segmentation/b2b-classes.png)

Poiché il modello dati può essere complicato, puoi utilizzare l’interfaccia utente di Platform per visualizzare una rappresentazione visiva più dettagliata del modello dati, al fine di trovare gli attributi rilevanti per il tuo caso d’uso. Per iniziare, passa all’interfaccia utente di Platform e seleziona Schemi nella navigazione a sinistra.

Seleziona lo schema appropriato dall’elenco disponibile e seleziona la relazione appropriata dal [!UICONTROL Composizione] barra laterale. Nell&#39;esempio seguente, selezionando la relazione &quot;Persona&quot; viene mostrato quale attributo nello schema corrente fa riferimento allo schema &quot;Persona&quot; correlato (se si tratta dello schema di origine nella relazione), o viene fatto riferimento dallo schema &quot;Persona&quot; (se si tratta dello schema di destinazione nella relazione).

![esempio di chiave di origine che utilizza la relazione persone nell&#39;area di lavoro schema](../assets/segmentation/source-key-schema-relationship-example.png)

Questa relazione si riflette nel Generatore di segmenti attraverso l’utilizzo di `Key` come illustrato di seguito.

![esempio chiave sorgente utilizzando il generatore di segmenti nell’area di lavoro segmentazione](../assets/segmentation/source-key-segmentation-example.png)

Fai riferimento alla [Schemi nella documentazione di Real-time Customer Data Platform B2B Edition](../schemas/b2b.md) per ulteriori informazioni sulle classi B2B disponibili.

I casi di utilizzo riportati di seguito forniscono informazioni sulle classi utilizzate per stabilire relazioni tra i diversi schemi per ottenere questi risultati. Questi esempi possono essere utilizzati per creare segmenti personalizzati.

## Esempi di diversi casi di utilizzo della segmentazione {#use-cases}

I seguenti casi d’uso sono disponibili per la segmentazione con l’edizione B2B. Ogni esempio fornisce una descrizione delle attività del segmento e una descrizione delle classi utilizzate per crearle. Le immagini fornite evidenziano il percorso del file nel [!UICONTROL Attributi] barra laterale che riflette la struttura dello schema. La [!UICONTROL Proprietà del segmento] la sezione a destra della visualizzazione contiene una suddivisione scritta degli attributi del segmento.

### Esempio 1: Trova i &quot;responsabili decisionali&quot; per le opportunità B2B {#find-decision-maker}

Trova tutte le persone che sono il &quot;Decisore&quot; di qualsiasi opportunità. Questo segmento richiede un collegamento tra [!UICONTROL Profilo individuale XDM] la classe e [!UICONTROL Relazione personale opportunità di business XDM] classe.

![Interfaccia utente che visualizza le impostazioni di esempio 1](../assets/segmentation/example-1.png)

### Esempio 2: Trova profili B2B assegnati a opportunità con un determinato importo in dollari {#find-opportunities-amount}

Trova tutte le persone che sono direttamente assegnate a qualsiasi opportunità di cui l&#39;importo dell&#39;opportunità è superiore all&#39;importo dato ($1 milione). Questo segmento richiede un collegamento tra [!UICONTROL Profilo individuale XDM] classe, [!UICONTROL Relazione personale opportunità di business XDM] e [!UICONTROL Opportunità aziendali XDM] classe.

![Interfaccia utente che visualizza le impostazioni di esempio 2](../assets/segmentation/example-2.png)

### Esempio 3: Trova profili B2B assegnati alle opportunità per posizione {#find-opportunities-location}

Trova tutte le persone che sono direttamente assegnate a qualsiasi opportunità in cui l&#39;account si trova in una determinata posizione (Canada). Questo segmento richiede un collegamento tra [!UICONTROL Profilo individuale XDM] classe, [!UICONTROL Relazione personale opportunità di business XDM] classe, [!UICONTROL Opportunità aziendali XDM] e [!UICONTROL Account aziendale XDM] classe.

![Interfaccia utente che visualizza le impostazioni di esempio 3](../assets/segmentation/example-3.png)

### Esempio 4: Trova i &quot;responsabili delle decisioni&quot; per opportunità per settore e comportamento di navigazione {#find-industry-browsing-behavior}

Trova tutte le persone che sono un &quot;Decisore&quot; di qualsiasi opportunità in cui il conto è nel settore &quot;Finanza&quot;, e ha visitato la pagina dei prezzi negli ultimi tre giorni. Questo segmento richiede un collegamento tra [!UICONTROL Profilo individuale XDM] classe, [!UICONTROL Relazione personale opportunità di business XDM] classe, [!UICONTROL Opportunità aziendali XDM] e [!UICONTROL Account aziendale XDM] e [!UICONTROL ExperienceEvent XDM] classe.

![Interfaccia utente che visualizza le impostazioni di esempio 4](../assets/segmentation/example-4.png)

### Esempio 5: Trova profili B2B per opportunità per nome del reparto e importo opportunità {#find-department-opportunity-amount}

Trova tutte le persone che lavorano in un reparto Risorse Umane (HR) e sono legate a qualsiasi account che ha almeno una opportunità aperta per il valore dato (1 milione di dollari) o più. Questo segmento richiede un collegamento tra [!UICONTROL Profilo individuale XDM] classe, [!UICONTROL Account aziendale XDM] e [!UICONTROL Opportunità aziendali XDM] classe.

![Interfaccia utente che visualizza impostazioni di esempio 5](../assets/segmentation/example-5.png)

### Esempio 6: Trovare profili B2B per titolo di lavoro e ricavi annuali del conto {#find-by-job-title-and-revenue}

Trova tutte le persone il cui titolo professionale è Vice Presidente e sono correlate a qualsiasi conto con entrate annuali pari o superiori al dato importo (100 milioni di dollari) e ha visitato la pagina prezzi almeno 3 volte nell&#39;ultimo mese. Questo segmento richiede un collegamento tra [!UICONTROL Profilo individuale XDM] classe, [!UICONTROL Account aziendale XDM] e [!UICONTROL ExperienceEvent XDM] classe.

![Interfaccia utente che mostra le impostazioni di esempio 6](../assets/segmentation/example-6.png)

### Esempio 7: Trovare i &quot;decisori&quot; in base allo stato delle opportunità e al comportamento di navigazione {#find-by-opportunity-status-and-browsing-behavior}

Trova tutte le persone che sono un &quot;Decisore&quot; di qualsiasi opportunità persa e ha visitato la pagina dei prezzi nell&#39;ultima settimana. Questo segmento richiede un collegamento tra [!UICONTROL Profilo individuale XDM] classe, [!UICONTROL Relazione personale opportunità di business XDM] classe, [!UICONTROL Opportunità aziendali XDM] e [!UICONTROL ExperienceEvent XDM] classe.

![Interfaccia utente con impostazioni di esempio 7](../assets/segmentation/example-7.png)

### Esempio 8: Utilizzare account correlati per espandere la portata di segmentazione {#related-accounts}

Trova tutte le persone che lavorano in un reparto Risorse Umane (HR) e sono relative a qualsiasi account *o uno dei conti correlati del conto* che ha almeno un&#39;opportunità aperta per un determinato importo (1 milione di dollari) o più. Questo segmento richiede un collegamento tra [!UICONTROL Profilo individuale XDM] classe, [!UICONTROL Account aziendale XDM] e [!UICONTROL Opportunità aziendali XDM] classe.

![Visualizzazione della segmentazione dell&#39;interfaccia utente per gli account correlati](../assets/segmentation/segmentation-related-accounts.png)

### Esempio 9: Utilizza i punteggi lead e/o i punteggi del conto per qualificare il profilo {#account-scoring}

Trova tutti i profili con il punteggio di lead superiore a 80.

![Visualizzazione della segmentazione dell’interfaccia utente per il punteggio predittivo del lead e dell’account](../assets/segmentation/segmentation-predictive-lead-and-account-scoring.png)

## Passaggi successivi {#next-steps}

Dopo aver letto questa panoramica, ora hai una comprensione delle possibilità di segmentazione disponibili utilizzando Real-time CDP, B2B Edition. Per ulteriori informazioni sul servizio di segmentazione, consulta il [Documentazione sulla segmentazione](../../segmentation/home.md).
