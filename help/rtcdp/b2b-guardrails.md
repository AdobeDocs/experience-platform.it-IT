---
keywords: profilo;real-time customer profile;risoluzione dei problemi;guardrail;linee guida;limit;entity;primary entity;dimension entity;RTCDP;CDP;B2B edition;Real-Time Customer Data Platform;real time customer data platform;real time cdp;b2b;cdp;
title: Guardrail predefiniti per Real-Time Customer Data Platform B2B edition
type: Documentation
description: Adobe Experience Platform utilizza un modello di dati ibridi altamente denormalizzati che differisce dal modello tradizionale di dati relazionali. Questo documento fornisce i limiti predefiniti di utilizzo e tasso per aiutarti a modellare i tuoi dati per ottenere prestazioni di sistema ottimali utilizzando Adobe Real-Time Customer Data Platform B2B edition.
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/it/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
feature: Guardrails, B2B
exl-id: 8eff8c3f-a250-4aec-92a1-719ce4281272
source-git-commit: bc399f3af0524232671af780ea1380f1a71a5b7e
workflow-type: tm+mt
source-wordcount: '1817'
ht-degree: 2%

---

# Guardrail predefiniti per Real-Time Customer Data Platform B2B edition

>[!NOTE]
>
>I limiti descritti in questo documento rappresentano le modifiche abilitate da Real-Time Customer Data Platform B2B edition. Per un elenco completo dei limiti predefiniti per Real-Time CDP B2B edition, combina questi limiti con i limiti generali di Adobe Experience Platform descritti nella [documentazione sui guardrail per i dati del profilo cliente in tempo reale](../profile/guardrails.md).

Real-Time Customer Data Platform B2B edition consente di fornire esperienze cross-channel personalizzate basate su informazioni comportamentali e attributi del cliente sotto forma di profili cliente in tempo reale e profili account. Per supportare questo nuovo approccio ai profili, Experience Platform utilizza un modello di dati ibridi altamente denormalizzati che differisce dal modello tradizionale di dati relazionali.

>[!IMPORTANT]
>
>Controlla i diritti di licenza nell&#39;ordine di vendita e la corrispondente [descrizione del prodotto](https://helpx.adobe.com/it/legal/product-descriptions.html) sui limiti di utilizzo effettivi, oltre a questa pagina di guardrail.

Questo documento fornisce i limiti predefiniti di utilizzo e tasso per aiutarti a modellare i tuoi dati per ottenere prestazioni di sistema ottimali. Durante l’esame dei seguenti guardrail, si presume che i dati siano stati modellati correttamente. In caso di domande su come modellare i dati, contatta il rappresentante del servizio clienti.

>[!INFO]
>
>La maggior parte dei clienti non supera questi limiti predefiniti. Per informazioni sui limiti personalizzati, contatta il rappresentante dell’assistenza clienti.

## Tipi di limite

In questo documento sono disponibili due tipi di limiti predefiniti:

| Tipo di guardrail | Descrizione |
| -------------- | ----------- |
| **Guardrail delle prestazioni (limite software)** | I guardrail di prestazioni sono limiti di utilizzo relativi all’ambito dei tuoi casi d’uso. Quando si superano i guardrail delle prestazioni, è possibile che si verifichi un peggioramento delle prestazioni e della latenza. Adobe non è responsabile di tale degrado delle prestazioni. I clienti che superano costantemente il limite di prestazioni possono scegliere di concedere licenze aggiuntive per evitare il degrado delle prestazioni. |
| **Guardrail applicati dal sistema (limite rigido)** | I guardrail applicati dal sistema vengono applicati dall’interfaccia utente o dall’API di Real-Time CDP. Questi sono i limiti che non puoi superare, poiché l’interfaccia utente e l’API ti impediranno di farlo o restituiranno un errore. |

>[!INFO]
>
>I limiti delineati nel presente documento vengono costantemente migliorati. Controlla regolarmente se ci sono aggiornamenti. Se ti interessa conoscere i limiti personalizzati, contatta il rappresentante dell’assistenza clienti.

## Limiti del modello dati

Le seguenti protezioni forniscono i limiti consigliati per la modellazione dei dati Profilo cliente in tempo reale. Per ulteriori informazioni sulle entità primarie e sulle entità dimensione, vedere la sezione relativa ai [tipi di entità](#entity-types) nell&#39;appendice.

### Guardrail dell’entità primaria

>[!NOTE]
>
>I limiti del modello dati descritti in questa sezione rappresentano le modifiche abilitate da Real-Time Customer Data Platform B2B edition. Per un elenco completo dei limiti predefiniti per Real-Time CDP B2B edition, combina questi limiti con i limiti generali di Adobe Experience Platform descritti nella [documentazione sui guardrail per i dati del profilo cliente in tempo reale](../profile/guardrails.md).

| Guardrail | Limite | Tipo limite | Descrizione |
| --------- | ----- | ---------- | ----------- |
| Set di dati della classe XDM standard di Real-Time CDP B2B edition | 60 | Guardrail delle prestazioni | Si consiglia un massimo di 60 set di dati che sfruttano le classi standard Experience Data Model (XDM) fornite da Real-Time CDP B2B edition. Per un elenco completo delle classi XDM standard per i casi di utilizzo B2B, consulta [gli schemi nella documentazione di Real-Time CDP B2B edition](schemas/b2b.md). <br/><br/>*Nota: a causa della natura del modello di dati ibridi denormalizzati di Experience Platform, la maggior parte dei clienti non supera questo limite. Per domande su come modellare i dati o per ulteriori informazioni sui limiti personalizzati, contatta il rappresentante dell&#39;Assistenza clienti.* |
| Conteggio delle identità per un singolo account in un grafico delle identità | 50 | Guardrail delle prestazioni | Il numero massimo di identità in un grafico delle identità per un singolo account è 50. Tutti i profili con più di 50 identità sono esclusi da segmentazione, esportazioni e ricerche. |
| Relazioni legacy tra più entità | 20 | Guardrail delle prestazioni | Si consiglia di definire un massimo di 20 relazioni tra più entità tra entità principali ed entità dimensione. Non è consigliabile eseguire mapping di relazioni aggiuntivi finché non viene rimossa o disabilitata una relazione esistente. |
| Relazioni molti-a-uno per classe XDM | 2 | Guardrail delle prestazioni | Si consiglia un massimo di 2 relazioni molti-a-uno definite per classe XDM. Non è consigliabile creare una relazione aggiuntiva finché non viene rimossa o disabilitata una relazione esistente. Per i passaggi su come creare una relazione tra due schemi, consulta l&#39;esercitazione su [definizione delle relazioni tra schemi B2B](../xdm/tutorials/relationship-b2b.md). |

### guardrail di entità Dimension

>[!NOTE]
>
>I limiti del modello dati descritti in questa sezione rappresentano le modifiche abilitate da Real-Time Customer Data Platform B2B edition. Per un elenco completo dei limiti predefiniti per Real-Time CDP B2B edition, combina questi limiti con i limiti generali di Adobe Experience Platform descritti nella [documentazione sui guardrail per i dati del profilo cliente in tempo reale](../profile/guardrails.md).

| Guardrail | Limite | Tipo limite | Descrizione |
| --------- | ----- | ---------- | ----------- |
| Nessuna relazione legacy nidificata | 0 | Guardrail delle prestazioni | Non creare una relazione tra due schemi diversi da [!DNL XDM Individual Profile]. La creazione di relazioni è **non** consigliata per gli schemi che non fanno parte dello schema di unione [!DNL Profile]. |
| Solo gli oggetti B2B possono partecipare a relazioni molti-a-uno | 0 | Guarddrail imposto dal sistema | Il sistema supporta solo relazioni molti-a-uno tra oggetti B2B. Per ulteriori informazioni sulle relazioni molti-a-uno, consulta l&#39;esercitazione su [definizione delle relazioni tra schemi B2B](../xdm/tutorials/relationship-b2b.md). |
| Profondità massima delle relazioni nidificate tra oggetti B2B | 3 | Guarddrail imposto dal sistema | La profondità massima delle relazioni nidificate tra oggetti B2B è 3. Ciò significa che in uno schema con annidamento elevato non dovrebbe esistere una relazione tra oggetti B2B nidificati a più di 3 livelli di profondità. |
| Schema singolo per ogni entità dimensione | 1 | Guarddrail imposto dal sistema | Ogni entità dimensione deve avere un singolo schema. Il tentativo di utilizzare le entità dimensione create da più schemi può influire sui risultati della segmentazione. È previsto che entità di dimensione diverse abbiano schemi separati. |

## Limiti di dimensione dei dati

I seguenti guardrail si riferiscono alle dimensioni dei dati e forniscono i limiti consigliati per i dati che possono essere acquisiti, memorizzati e interrogati come previsto. Per ulteriori informazioni sulle entità primarie e sulle entità dimensione, vedere la sezione relativa ai [tipi di entità](#entity-types) nell&#39;appendice.

>[!INFO]
>
>La dimensione dei dati viene misurata come dati non compressi in JSON al momento dell’acquisizione.

### Guardrail dell’entità primaria

>[!NOTE]
>
>I limiti di dimensione dei dati descritti in questa sezione rappresentano le modifiche abilitate da Real-Time Customer Data Platform B2B edition. Per un elenco completo dei limiti predefiniti per Real-Time CDP B2B edition, combina questi limiti con i limiti generali di Adobe Experience Platform descritti nella [documentazione sui guardrail per i dati del profilo cliente in tempo reale](../profile/guardrails.md).

| Guardrail | Limite | Tipo limite | Descrizione |
| --------- | ----- | ---------- | ----------- |
| Batch acquisiti per classe XDM al giorno | 45 | Guardrail delle prestazioni | Il numero totale di batch acquisiti ogni giorno per classe XDM non deve superare 45. L&#39;acquisizione di batch aggiuntivi può impedire prestazioni ottimali. |

### guardrail di entità Dimension

>[!NOTE]
>
>I limiti di dimensione dei dati descritti in questa sezione rappresentano le modifiche abilitate da Real-Time Customer Data Platform B2B edition. Per un elenco completo dei limiti predefiniti per Real-Time CDP B2B edition, combina questi limiti con i limiti generali di Adobe Experience Platform descritti nella [documentazione sui guardrail per i dati del profilo cliente in tempo reale](../profile/guardrails.md).

| Guardrail | Limite | Tipo limite | Descrizione |
| --------- | ----- | ---------- | ----------- |
| Dimensione totale per tutte le entità dimensionali | 5GB | Guardrail delle prestazioni | La dimensione totale consigliata per tutte le entità dimensionali è 5 GB. L&#39;inserimento di entità di dimensioni grandi può influire sulle prestazioni del sistema. Ad esempio, non è consigliabile tentare di caricare un catalogo di prodotti da 10 GB come entità dimensione. |
| Set di dati per schema di entità dimensionale | 5 | Guardrail delle prestazioni | Si consiglia un massimo di 5 set di dati associati a ogni schema di entità dimensionale. Ad esempio, se crei uno schema per &quot;prodotti&quot; e aggiungi cinque set di dati contributivi, non devi creare un sesto set di dati associato allo schema prodotti. |
| Batch di entità Dimension acquisiti al giorno | 4 per entità | Guardrail delle prestazioni | Il numero massimo consigliato di batch di entità dimensione acquisiti al giorno è 4 per entità. Ad esempio, puoi acquisire gli aggiornamenti di un catalogo di prodotti fino a 4 volte al giorno. L&#39;acquisizione di batch di entità di dimensione aggiuntivi per la stessa entità può influire sulle prestazioni del sistema. |

## Guardrail di segmentazione

I guardrail descritti in questa sezione si riferiscono al numero e alla natura dei tipi di pubblico che un’organizzazione può creare in Experience Platform, nonché alla mappatura e all’attivazione dei tipi di pubblico nelle destinazioni.

>[!NOTE]
>
>I limiti di segmentazione descritti in questa sezione rappresentano le modifiche abilitate da Real-Time Customer Data Platform B2B edition. Per un elenco completo dei limiti predefiniti per Real-Time CDP B2B edition, combina questi limiti con i limiti generali di Adobe Experience Platform descritti nella [documentazione sui guardrail per i dati del profilo cliente in tempo reale](../profile/guardrails.md).

| Guardrail | Limite | Tipo limite | Descrizione |
| --------- | ----- | ---------- | ----------- |
| Definizioni dei segmenti per sandbox B2B | 400 | Guardrail delle prestazioni | Un’organizzazione può avere più di 400 definizioni di segmenti in totale, purché ci siano meno di 400 definizioni di segmenti in ogni singola sandbox B2B. Il tentativo di creare ulteriori definizioni di segmenti può influire sulle prestazioni del sistema. |

## Passaggi successivi

I limiti descritti in questo documento rappresentano le modifiche abilitate da Real-Time Customer Data Platform B2B edition. Per un elenco completo dei limiti predefiniti per Real-Time CDP B2B edition, combina questi limiti con i limiti generali di Adobe Experience Platform descritti nella [documentazione sui guardrail per i dati del profilo cliente in tempo reale](../profile/guardrails.md).

## Appendice

Questa sezione fornisce ulteriori dettagli sui limiti riportati in questo documento.

### Tipi di entità

Il modello dati dell&#39;archivio [!DNL Profile] è costituito da due tipi di entità di base: [entità primarie](#primary-entity) e [entità dimensionali](#dimension-entity).

#### Entità primaria

Un’entità primaria, o entità di profilo, unisce i dati per formare una &quot;singola sorgente di verità&quot; per un individuo. Questi dati unificati vengono rappresentati utilizzando la cosiddetta &quot;visualizzazione unione&quot;. Una vista unione aggrega i campi di tutti gli schemi che implementano la stessa classe in un unico schema di unione. Lo schema di unione per [!DNL Real-Time Customer Profile] è un modello di dati ibridi denormalizzati che funge da contenitore per tutti gli attributi di profilo e gli eventi comportamentali.

Gli attributi indipendenti dal tempo, noti anche come &quot;dati record&quot;, vengono modellati utilizzando [!DNL XDM Individual Profile], mentre i dati della serie temporale, noti anche come &quot;dati evento&quot;, vengono modellati utilizzando [!DNL XDM ExperienceEvent]. Quando i dati dei record e delle serie temporali vengono acquisiti in Adobe Experience Platform, attiva [!DNL Real-Time Customer Profile] per iniziare ad acquisire i dati abilitati per il relativo utilizzo. Più interazioni e dettagli vengono acquisiti, più solidi saranno i singoli profili.

![Un&#39;infografica che illustra le differenze tra i dati dei record e i dati della serie temporale.](../profile/images/guardrails/profile-entity.png)

#### Entità Dimension

Anche se l’archivio dati profilo che gestisce i dati profilo non è un archivio relazionale, Profilo consente l’integrazione con entità dimensionali di piccole dimensioni per creare tipi di pubblico in modo semplificato e intuitivo. Questa integrazione è nota come [segmentazione con più entità](../segmentation/tutorials/multi-entity-segmentation.md).

La tua organizzazione può anche definire classi XDM per descrivere elementi diversi dai singoli utenti, ad esempio store, prodotti o proprietà. Questi schemi non [!DNL XDM Individual Profile] sono denominati &quot;entità dimensione&quot; (note anche come &quot;entità di ricerca&quot;) e non contengono dati di serie temporali. Gli schemi che rappresentano entità dimensione sono collegati alle entità profilo tramite l&#39;utilizzo di [relazioni schema](../xdm/tutorials/relationship-ui.md).

Le entità Dimension forniscono dati di ricerca che facilitano e semplificano le definizioni dei segmenti con più entità e devono essere sufficientemente piccole da consentire al motore di segmentazione di caricare l’intero set di dati in memoria per un’elaborazione ottimale (ricerca rapida dei punti).

![Infografica che mostra che un&#39;entità profilo è composta da entità dimensione.](../profile/images/guardrails/profile-and-dimension-entities.png)
