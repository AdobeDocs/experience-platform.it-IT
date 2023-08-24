---
title: Integrare i profili di prime parti con gli attributi forniti dai partner
description: Scopri come integrare i profili di prime parti con attributi di partner di dati affidabili, per migliorare le basi dati, acquisire nuove informazioni sulla clientela e una migliore ottimizzazione del pubblico.
source-git-commit: 9dd305be4dcb45c290a2b8ee0476191949369adc
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 94%

---

# Integrare i profili di prime parti con gli attributi forniti dai partner

>[!AVAILABILITY]
>
>* Questa funzionalità in versione è disponibile per i clienti che dispongono di una licenza per Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Ulteriori informazioni su questi pacchetti sono disponibili nelle [descrizioni dei prodotti](https://helpx.adobe.com/it/legal/product-descriptions.html). Contatta il tuo rappresentante Adobe per ulteriori informazioni.

Puoi integrare i profili di prime parti con attributi di partner di dati affidabili, per migliorare la base di dati, acquisire nuove informazioni sulla base dei clienti e una migliore ottimizzazione del pubblico.

![Panoramica visiva di alto livello su come arricchire i profili con i casi d’uso degli attributi forniti dai partner.](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-overview.png)

## Prerequisiti e pianificazione {#prerequisites-and-planning}

Se prendi in considerazione l’integrazione dei profili di prime parti con gli attributi dei partner di dati, dovresti discutere e indirizzare i seguenti dettagli sul ciclo di arricchimento dei dati con il partner dati:

* Prendi in considerazione la posizione in cui l’elenco dei tipi di pubblico verrà esportato da Real-Time CDP per essere condiviso con il fornitore dei dati. Questa posizione deve supportare l’esportazione di file.
* Quali sono gli identificatori previsti dal fornitore dei dati in modo che possano essere sovrapposti agli attributi aggiuntivi?
* In che modo verrà acquisito il file contenente gli attributi forniti dal partner in Real-time CDP? Ad esempio, i file possono essere acquisiti tramite i connettori di origine dell’archiviazione cloud, come [Amazon S3](/help/sources/connectors/cloud-storage/s3.md) o [SFTP](/help/sources/connectors/cloud-storage/sftp.md).
* Qual è la cadenza con cui si prevede che gli attributi forniti dai partner vengano riportati in Real-Time CDP e aggiornati?

>[!WARNING]
>
>Gli attributi aggiuntivi forniti dal partner e acquisiti in Real-Time CDP influiscono sulla *ricchezza media del profilo*. Per ulteriori informazioni sulla ricchezza dei profili, consulta la [descrizione del prodotto Real-time Customer Data Platform](https://helpx.adobe.com/it/legal/product-descriptions/real-time-customer-data-platform.html).

## Come utilizzare il caso d’uso: panoramica di alto livello {#achieve-the-use-case-high-level}

![Panoramica visiva di alto livello su come arricchire i profili con i casi d’uso degli attributi forniti dai partner.](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-steps.png)

1. Come **cliente**, gli attributi della licenza vengono forniti dal **partner di dati**.
2. Come **cliente**, puoi estendere i dati del profilo e il modello di governance per adattare gli attributi forniti dal **partner**.
3. Come **cliente**, puoi integrare i tipi di pubblico che desideri arricchire con il partner di dati. In genere, questi tipi di pubblico sono ricavati da identificatori di input come elementi PII (Informazioni d’identificazione personale) come e-mail, nome, indirizzo o altri.
4. Il **partner** aggiunge gli attributi concessi in licenza per i profili con cui è in grado di eseguire il confronto. Facoltativamente, un [ID partner](/help/identity-service/namespaces.md) può essere incluso e acquisito nello spazio dei nomi ID con ambito partner.
5. Come **cliente**, in Real-Time CDP puoi caricare gli attributi del partner di dati nei profili cliente.

## Come utilizzare il caso d’uso: istruzioni dettagliate {#step-by-step-instructions}

Leggi le sezioni seguenti, che includono collegamenti a un ulteriore documentazione, per completare ciascuno dei passaggi descritti nella panoramica di alto livello qui sopra.

### Attributi di licenza dal partner {#license-attributes-from-partner}

Questa fase è descritta nella sezione [prerequisiti](#prerequisites-and-planning) e Adobe presuppone che tu abbia stipulato i giusti accordi contrattuali con fornitori di dati affidabili per migliorare i profili di prime parti.

### Estendi i dati del profilo e il modello di governance per adattarli agli attributi forniti dai partner. {#extend-governance-model}

A questo punto, estendi il framework di gestione dati in Real-Time CDP per adattarlo agli attributi forniti dai partner.

È possibile creare un nuovo schema della classe **[!UICONTROL Profilo individuale XDM]** o estendere uno schema esistente dello stesso tipo per includere gli attributi forniti dal partner. Adobe consiglia vivamente di creare un nuovo schema con un nuovo set di gruppi di campi che rappresentino al meglio gli attributi aggiuntivi del fornitore dei dati. In questo modo gli schemi di dati sono puliti e possono evolvere indipendentemente l’uno dall’altro.

Per includere in uno schema gli attributi forniti dal partner, è possibile creare un nuovo gruppo di campi con gli attributi previsti oppure utilizzare uno dei gruppi di campi preconfigurati forniti da Adobe.

Per ulteriori informazioni, consulta le pagine della documentazione seguenti:

* [Nozioni di base sulla composizione dello schema](/help/xdm/schema/composition.md)
* [Panoramica sulla classe [!UICONTROL Profilo individuale XDM]](/help/xdm/classes/individual-profile.md)
* [Creare e modificare gli schemi nell’interfaccia utente](/help/xdm/ui/resources/schemas.md)
* [Creare e modificare gruppi di campi schema nell’interfaccia utente](/help/xdm/ui/resources/field-groups.md)

<!--

Commenting out links for now
* [Create and edit schemas using the API](/help/xdm/api/schemas.md#create)
* [Update an existing schema to add field groups using the API](/help/xdm/api/schemas.md#patch)
* Link to new field group documentation page when it exists

-->

Anche in questo passaggio, tieni presente come cambia il modello di governance dei dati quando espandi la tua strategia di gestione dati per includere i dati di terze parti forniti dal partner. Consulta le considerazioni riportate nei collegamenti alla documentazione qui di seguito:

* (**Disponibile a breve**) Conservazione dei dati di terze parti in un set di dati separato in modo che sia facile eliminarli e annullare le integrazioni.
* (**Disponibile a breve**) Utilizzo della funzionalità [scadenza set di dati](/help/hygiene/ui/dataset-expiration.md) per il set di dati di clienti che hanno acquistato il componente aggiuntivo di igiene dei dati.
* (**Disponibile a breve**) Presta attenzione durante la creazione di set di dati derivati che estraggono dati di terze parti, perché una volta combinati, l’unica soluzione per rimuovere i dati di terze parti è quella di eliminare l’intero set di dati derivati.

>[!TIP]
>
>Se scegli di integrare i profili dei clienti con un identificatore basato sulla persona del fornitore di dati, puoi creare un nuovo tipo di identità del tipo **[[!UICONTROL ID partner]](/help/identity-service/namespaces.md)**.
>
>Per ulteriori informazioni sull’ID partner, consulta la [sezione sui tipi di identità](/help/identity-service/namespaces.md).
>Ulteriori informazioni su [come definire i campi di identità](/help/xdm/ui/fields/identity.md) nell’interfaccia utente di Experience Platform.

### Esportare i tipi di pubblico che si desidera arricchire quando vengono ricavati dalle PII (Informazioni d’identificazione personale) o PII con hash {#export-audiences}

Esporta i tipi di pubblico che desideri essere arricchiti dal partner. Utilizza le destinazioni dell’archiviazione cloud fornite da Real-time CDP, ad esempio Amazon S3 o SFTP. Per completare questo passaggio, leggi le seguenti pagine della documentazione:

* Pagina della documentazione sulla [destinazione Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md)
* Pagina della documentazione sulla [destinazione SFTP](/help/destinations/catalog/cloud-storage/sftp.md)
* Procedura su come [connettersi a una destinazione](/help/destinations/ui/connect-destination.md)
* Procedura su come [esportare i dati in una destinazione di archiviazione cloud](/help/destinations/ui/activate-batch-profile-destinations.md)

### Il partner di dati aggiunge attributi con licenza per i profili che è in grado di confrontare {#partner-appends-attributes}

In questo passaggio, il partner di dati aggiunge gli attributi con licenza per il pubblico esportato. L’output è generalmente disponibile come file flat che può essere acquisito nuovamente in Real-Time CDP. Ulteriori informazioni sull’[acquisizione di file in Real-Time CDP](/help/ingestion/tutorials/ingest-batch-data.md#upload-file).

### Real-Time CDP aggiunge attributi arricchiti al profilo cliente {#ingest-data}

Ora è necessario acquisire i dati dal partner tramite un connettore di origine per inserire nuovamente i dati arricchiti in Real-Time CDP e integrare i profili con i dati forniti dal partner.

Alcuni connettori di origine consigliati a questo scopo possono essere:

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

## Limitazioni e risoluzione dei problemi {#limitations-and-troubleshooting}

Durante l’esplorazione del caso d’uso descritto in questa pagina, tieni presente le seguenti limitazioni:

* Se scegli di utilizzare gli ID partner, tieni presente che non vengono utilizzati durante la creazione del [grafico identità](/help/identity-service/ui/identity-graph-viewer.md).

## Altri casi d’uso ottenuti tramite il supporto dei dati dei partner {#other-use-cases}

Esplora altri casi d’uso abilitati tramite il supporto dei dati dei partner in Real-Time CDP:

* Utilizzare il supporto dati di terze parti in Real-Time CDP per [espandi la base di profili con i profili prospect dei partner dati e interagisci con loro per acquisire o raggiungere nuovi clienti](/help/rtcdp/partner-data/prospecting.md).
* [Utilizzo del riconoscimento supportato dai partner per la personalizzazione delle esperienze sul sito](/help/rtcdp/partner-data/onsite-personalization.md) durante la visita senza che l’utente si autentichi o abbia una storia precedente con il tuo marchio.
* [Attivazione estesa di profili di potenziali clienti e tipi di pubblico di potenziali clienti](/help/destinations/ui/activate-prospect-audiences.md) per selezionare le destinazioni.