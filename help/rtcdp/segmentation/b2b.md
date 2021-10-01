---
title: Panoramica dei casi di utilizzo della segmentazione per Real-time CDP B2B Edition.
description: Panoramica dei vari casi d’uso di Real-time CDP B2B Edition disponibili.
source-git-commit: e85d4b108e2d4a6a88772c071d9281603b695ada
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Panoramica dei casi di utilizzo della segmentazione per Real-time Customer Data Platform B2B Edition (Beta)

<!-- This document relates to this [ticket](https://jira.corp.adobe.com/browse/PLAT-100468) -->

>[!IMPORTANT]
>
>Real-time CDP B2B Edition è attualmente in versione beta. La documentazione e le funzionalità sono soggette a modifiche.

Questo documento fornisce esempi relativi alla segmentazione disponibile per Real-time CDP B2B Edition e a come i diversi tipi di attributi possono essere combinati per i casi d’uso comuni B2B.

>[!NOTE]
>
>Gli attributi richiesti per questi casi d’uso di segmentazione sono disponibili solo per i clienti Real-time Customer Data Platform B2B Edition. Per ulteriori informazioni su Real-time CDP, incluse le funzioni e le funzionalità disponibili per ogni tipo di licenza, si prega di iniziare leggendo la [Panoramica di Real-time CDP](../overview.md).

## Prerequisiti

Prima di poter utilizzare gli attributi di segmentazione per le classi B2B, è necessario completare i seguenti passaggi:

1. Creare schemi che utilizzano le classi B2B. Le classi B2B Edition includono Account, Campaign, Opportunity, Marketing List e altro ancora. Per informazioni su [come impostare schemi da utilizzare con le classi B2B](../schemas/b2b.md), consulta la documentazione sullo schema.
1. Crea relazioni tra gli schemi B2B Experience Data Model (XDM). I segmenti basati sugli attributi B2B Edition richiedono relazioni tra le classi per utilizzare appieno la funzionalità estesa di segmentazione B2B. Per ulteriori informazioni, consulta la documentazione su [come definire una relazione tra due schemi B2B](../../xdm/tutorials/relationship-b2b.md) .
1. Acquisisci dati utilizzando set di dati basati sugli schemi B2B. Consulta la documentazione sulle sorgenti per [informazioni su come acquisire dati](../../sources/connectors/adobe-applications/marketo/marketo.md).
1. Leggi la [guida utente del Generatore di segmenti](../../segmentation/ui/segment-builder.md) per informazioni più dettagliate su come creare i segmenti.

Una volta soddisfatti questi requisiti, puoi combinare questi attributi per i casi d’uso comuni B2B.

## Introduzione

Una volta che gli schemi di unione per le classi B2B hanno relazioni stabilite e sono stati utilizzati per acquisire dati, i loro attributi sono resi disponibili nella barra a sinistra del Generatore di segmenti.

Alle classi B2B e ai relativi attributi viene aggiunta un’etichetta `B2B` nell’area di lavoro Segmentazione per differenziarle da quelle disponibili come standard in Real-time Customer Data Platform.

Per creare in modo efficace segmenti per i casi di utilizzo B2B, è importante avere una conoscenza approfondita dello schema e capire come si presenta il modello di dati. È inoltre utile conoscere il percorso che i dati prendono da un oggetto dati all’altro.

L&#39;immagine seguente illustra le relazioni tra le classi B2B disponibili in Real-time CDP B2B Edition.

![Classe B2B ERD](../assets/segmentation/b2b-classes.png)

Poiché il modello dati può essere complicato, puoi utilizzare l’interfaccia utente di Platform per visualizzare una rappresentazione visiva più dettagliata del modello dati, al fine di trovare gli attributi rilevanti per il tuo caso d’uso. Per iniziare, passa all’interfaccia utente di Platform e seleziona Schemi nella navigazione a sinistra.

Seleziona lo schema appropriato dall&#39;elenco disponibile e seleziona la relazione appropriata dalla barra laterale [!UICONTROL Composizione]. Nell&#39;esempio seguente, selezionando la relazione &quot;Persona&quot; viene mostrato quale attributo nello schema corrente fa riferimento allo schema &quot;Persona&quot; correlato (se si tratta dello schema di origine nella relazione), o viene fatto riferimento dallo schema &quot;Persona&quot; (se si tratta dello schema di destinazione nella relazione).

![esempio di chiave di origine che utilizza la relazione persone nell&#39;area di lavoro schema](../assets/segmentation/source-key-schema-relationship-example.png)

Questa relazione si riflette all’interno del Generatore di segmenti attraverso l’uso di cartelle `Key` come mostrato nell’immagine seguente.

![esempio chiave sorgente utilizzando il generatore di segmenti nell’area di lavoro segmentazione](../assets/segmentation/source-key-segmentation-example.png)

Per ulteriori informazioni sulle classi B2B disponibili, consulta gli schemi [nella documentazione di Real-time Customer Data Platform B2B Edition](../schemas/b2b.md) .

I casi di utilizzo riportati di seguito forniscono informazioni sulle classi utilizzate per stabilire relazioni tra i diversi schemi per ottenere questi risultati. Questi esempi possono essere utilizzati per creare segmenti personalizzati.

## Esempi di diversi casi di utilizzo

I seguenti casi d’uso sono disponibili per la segmentazione con l’edizione B2B. Ogni esempio fornisce una descrizione delle attività del segmento e una descrizione delle classi utilizzate per crearle. Le immagini fornite evidenziano il percorso del file nella barra laterale [!UICONTROL Attributi] che riflette la struttura dello schema. La sezione [!UICONTROL Proprietà segmento] a destra della visualizzazione contiene una suddivisione scritta degli attributi del segmento.

### Esempio 1

Trova tutte le persone che sono il &quot;Decisore&quot; di qualsiasi opportunità. Questo segmento richiede un collegamento tra la classe [!UICONTROL Profilo individuale XDM] e la classe [!UICONTROL XDM Business Opportunity Person Relation] .

![Interfaccia utente che visualizza le impostazioni di esempio 1](../assets/segmentation/example-1.png)

### Esempio 2

Trova tutte le persone che sono direttamente assegnate a qualsiasi opportunità di cui l&#39;importo dell&#39;opportunità è superiore all&#39;importo dato ($1 milione). Questo segmento richiede un collegamento tra la classe [!UICONTROL Profilo individuale XDM], [!UICONTROL XDM Business Opportunity Person Relation] e la classe [!UICONTROL XDM Business Opportunity] .

![Interfaccia utente che visualizza le impostazioni di esempio 2](../assets/segmentation/example-2.png)

### Esempio 3

Trova tutte le persone che sono direttamente assegnate a qualsiasi opportunità in cui l&#39;account si trova in una determinata posizione (Canada). Questo segmento richiede un collegamento tra la classe [!UICONTROL Profilo individuale XDM], [!UICONTROL XDM Business Opportunity Person Relation], la classe [!UICONTROL XDM Business Opportunity] e la classe [!UICONTROL XDM Business Account].

![Interfaccia utente che visualizza le impostazioni di esempio 3](../assets/segmentation/example-3.png)

### Esempio 4

Trova tutte le persone che sono un &quot;Decisore&quot; di qualsiasi opportunità in cui il conto è nel settore &quot;Finanza&quot;, e ha visitato la pagina dei prezzi negli ultimi tre giorni. Questo segmento richiede un collegamento tra la classe [!UICONTROL Profilo individuale XDM], [!UICONTROL XDM Business Opportunity Person Relation], la classe [!UICONTROL XDM Business Opportunity] e la classe [!UICONTROL XDM Business Account] e la classe [!UICONTROL XDM ExperienceEvent].

![Interfaccia utente che visualizza le impostazioni di esempio 4](../assets/segmentation/example-4.png)

### Esempio 5

Trova tutte le persone che lavorano in un reparto Risorse Umane (HR) e sono legate a qualsiasi account che ha almeno una opportunità aperta per il valore dato (1 milione di dollari) o più. Questo segmento richiede un collegamento tra la classe [!UICONTROL Profilo individuale XDM], [!UICONTROL Account aziendale XDM] e la classe [!UICONTROL Opportunità commerciali XDM].

![Interfaccia utente che visualizza impostazioni di esempio 5](../assets/segmentation/example-5.png)

### Esempio 6

Trova tutte le persone il cui titolo professionale è Vice Presidente e sono correlate a qualsiasi conto con entrate annuali pari o superiori al dato importo (100 milioni di dollari) e ha visitato la pagina prezzi almeno 3 volte nell&#39;ultimo mese. Questo segmento richiede un collegamento tra la classe [!UICONTROL Profilo individuale XDM], [!UICONTROL Account aziendale XDM] e la classe [!UICONTROL XDM ExperienceEvent].

![Interfaccia utente che mostra le impostazioni di esempio 6](../assets/segmentation/example-6.png)

### Esempio 7

Trova tutte le persone che sono un &quot;Decisore&quot; di qualsiasi opportunità persa e ha visitato la pagina dei prezzi nell&#39;ultima settimana. Questo segmento richiede un collegamento tra la classe [!UICONTROL Profilo individuale XDM], [!UICONTROL XDM Business Opportunity Person Relation], la classe [!UICONTROL XDM Business Opportunity] e la classe [!UICONTROL XDM ExperienceEvent].

![Interfaccia utente con impostazioni di esempio 7](../assets/segmentation/example-7.png)

## Passaggi successivi

Dopo aver letto questa panoramica, ora hai una comprensione delle possibilità di segmentazione disponibili utilizzando Real-time CDP, B2B Edition. Per ulteriori informazioni sul servizio di segmentazione, consulta la [documentazione sulla segmentazione](../../segmentation/home.md).
