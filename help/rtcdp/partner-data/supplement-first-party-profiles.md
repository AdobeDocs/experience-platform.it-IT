---
title: (Beta) Integrazione dei profili di prime parti con gli attributi forniti dai partner
description: Scopri come integrare i profili di prime parti con attributi di partner di dati affidabili, per migliorare le basi dati, acquisire nuove informazioni sulla base dei clienti e ottimizzare meglio il pubblico.
hide: true
hidefromtoc: true
badgeBeta: label="Beta" type="informative" before-title="true"
source-git-commit: 2a072ce9351a84263a50597967b994162de18d81
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 0%

---

# Integrare i profili di prime parti con gli attributi forniti dai partner

>[!AVAILABILITY]
>
>* Questa funzionalità beta è disponibile per i clienti che dispongono di una licenza per Real-Time CDP (App Service), Adobe Experience Platform Activation, Real-time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Ulteriori informazioni su questi pacchetti sono disponibili in [descrizioni dei prodotti](https://helpx.adobe.com/legal/product-descriptions.html) e contatta il rappresentante del tuo Adobe per ulteriori informazioni.

Puoi integrare i profili di prime parti con attributi di partner dati affidabili, per migliorare la base di dati, acquisire nuove informazioni sulla base dei clienti e ottimizzare meglio il pubblico.

![Arricchisci i profili con gli attributi forniti dai partner; caso d’uso: panoramica visiva di alto livello.](/help/rtcdp/assets/partner-data/enrichment-use-case-overview.png)

## Prerequisiti e pianificazione {#prerequisites-and-planning}

Se prendi in considerazione l’integrazione dei profili di prime parti con gli attributi dei partner dati, dovresti discutere e indirizzare i seguenti dettagli sul ciclo di arricchimento dei dati con il partner dati:

* Pensa alla posizione in cui l’elenco dei tipi di pubblico verrà esportato da Real-Time CDP per essere condiviso con il fornitore dei dati. Questa posizione deve supportare l&#39;esportazione di file.
* Quali sono gli identificatori previsti dal fornitore dei dati in modo che possano sovrapporre attributi aggiuntivi?
* Come verrà acquisito in Real-time CDP il file contenente gli attributi forniti dal partner? Ad esempio, i file possono essere acquisiti tramite i connettori di origine dell’archiviazione cloud, come [Amazon S3](/help/sources/connectors/cloud-storage/s3.md) o [SFTP](/help/sources/connectors/cloud-storage/sftp.md).
* Qual è la cadenza con cui si prevede che gli attributi forniti dai partner vengano riportati in Real-Time CDP e aggiornati?

>[!WARNING]
>
>Gli attributi aggiuntivi forniti dal partner acquisiti in Real-Time CDP influiscono sui *ricchezza media del profilo*. Leggi le [Descrizione del prodotto Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) per ulteriori informazioni sulla ricchezza dei profili.

## Come ottenere il caso d’uso: panoramica di alto livello {#achieve-the-use-case-high-level}

![Arricchisci i profili con gli attributi forniti dai partner; caso d’uso: panoramica visiva di alto livello.](/help/rtcdp/assets/partner-data/enrichment-use-case-steps.png)

1. As a **cliente**, gli attributi della licenza vengono forniti da **partner dati**.
2. As a **cliente**, puoi estendere i dati del profilo e il modello di governance per supportare **partner** attributi forniti da.
3. As a **cliente**, puoi integrare i tipi di pubblico che desideri arricchire con il partner dati. In genere, questi tipi di pubblico sono ricavati da identificatori di input come elementi PII (Personally Identifiable Information) come e-mail, nome, indirizzo o altri.
4. Il **partner** aggiunge gli attributi concessi in licenza per i profili con cui sono in grado di eseguire il confronto. Facoltativamente, un [ID partner](/help/identity-service/namespaces.md) può essere incluso e acquisito nello spazio dei nomi ID con ambito partner.
5. As a **cliente**, in Real-Time CDP puoi caricare gli attributi del partner dati nei profili cliente.

## Come ottenere il caso d’uso: istruzioni dettagliate {#step-by-step-instructions}

Leggi le sezioni seguenti, che includono collegamenti a ulteriore documentazione, per completare ciascuno dei passaggi descritti nella panoramica di alto livello precedente.

### Attributi di licenza dal partner {#license-attributes-from-partner}

Questa fase è descritta nella sezione [prerequisiti](#prerequisites-and-planning) e Adobe presuppone che tu abbia stipulato i giusti accordi contrattuali con fornitori di dati affidabili per migliorare i profili di prime parti.

### Estendi i dati del profilo e il modello di governance per adattarli agli attributi forniti dai partner. {#extend-governance-model}

A questo punto, stai estendendo il framework di gestione dati in Real-Time CDP per adattarlo agli attributi forniti dai partner.

È possibile creare un nuovo schema del **[!UICONTROL Profilo individuale XDM]** o estendere uno schema esistente dello stesso tipo per includere gli attributi forniti dal partner. L’Adobe consiglia vivamente di creare un nuovo schema con un nuovo set di gruppi di campi che rappresentino al meglio gli attributi aggiuntivi del fornitore dei dati. In questo modo gli schemi di dati sono puliti e possono evolvere indipendentemente l’uno dall’altro.

Per includere in uno schema gli attributi forniti dal partner, è possibile creare un nuovo gruppo di campi con gli attributi previsti oppure utilizzare uno dei gruppi di campi preconfigurati forniti da Adobe.

Per ulteriori informazioni, consulta le pagine della documentazione seguenti:

* [Nozioni di base sulla composizione dello schema](/help/xdm/schema/composition.md)
* [Panoramica di [!UICONTROL Profilo individuale XDM] classe](/help/xdm/classes/individual-profile.md)
* [Creare e modificare gli schemi nell’interfaccia utente](/help/xdm/ui/resources/schemas.md)
* [Creare e modificare gruppi di campi schema nell’interfaccia utente](/help/xdm/ui/resources/field-groups.md)

<!--

Commenting out links for now
* [Create and edit schemas using the API](/help/xdm/api/schemas.md#create)
* [Update an existing schema to add field groups using the API](/help/xdm/api/schemas.md#patch)
* Link to new field group documentation page when it exists

-->

Anche in questo passaggio, pensa a come cambia il modello di governance dei dati quando espandi la tua strategia di gestione dati per includere i dati di terze parti forniti dal partner. Consulta le considerazioni riportate nei collegamenti alla documentazione riportati di seguito:

* (**Disponibile a breve**) Mantieni i dati di terze parti in un set di dati separato in modo che sia facile eliminarli e annullare le integrazioni.
* (**Disponibile a breve**) Utilizzare [Time-to-live (TTL)](/help/hygiene/ui/dataset-expiration.md) sul set di dati per i clienti che hanno acquistato il componente aggiuntivo di igiene dei dati.
* (**Disponibile a breve**) Presta attenzione quando crei set di dati derivati che estraggono dati di terze parti, perché una volta combinati, l’unica soluzione per rimuovere i dati di terze parti è quella di eliminare l’intero set di dati derivati.

>[!TIP]
>
>Se scegli di integrare i profili dei clienti con un identificatore basato su persona del fornitore di dati, puoi creare un nuovo tipo di identità **[[!UICONTROL ID partner]](/help/identity-service/namespaces.md)**.
>
>Per ulteriori informazioni sull&#39;ID partner, consulta [sezione tipi di identità](/help/identity-service/namespaces.md).
>Ulteriori informazioni [come definire i campi di identità](/help/xdm/ui/fields/identity.md) nell’interfaccia utente di Experience Platform.

### Esporta i tipi di pubblico che desideri arricchire quando vengono ricavati dai dati PII (Personal Identifiable Information) o PII con hash {#export-audiences}

Esporta i tipi di pubblico che desideri arricchire con il partner. Utilizza le destinazioni dell’archiviazione cloud fornite da Real-time CDP, ad esempio Amazon S3 o SFTP. Per completare questo passaggio, leggi le seguenti pagine della documentazione:

* [Destinazione Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md) pagina della documentazione
* [Destinazione SFTP](/help/destinations/catalog/cloud-storage/sftp.md) pagina della documentazione
* Procedura [connettersi a una destinazione](/help/destinations/ui/connect-destination.md)
* Procedura [esportare i dati in una destinazione di archiviazione cloud](/help/destinations/ui/activate-batch-profile-destinations.md)

### Il partner dati aggiunge attributi con licenza per i profili che è in grado di confrontare {#partner-appends-attributes}

In questo passaggio, il partner dati aggiunge gli attributi con licenza per il pubblico esportato. L’output è generalmente disponibile come file flat che può essere acquisito nuovamente in Real-Time CDP. Ulteriori informazioni su [acquisizione di file in Real-Time CDP](/help/ingestion/tutorials/ingest-batch-data.md#upload-file).

### Real-Time CDP aggiunge attributi arricchiti al profilo cliente {#ingest-data}

Ora devi acquisire i dati dal partner tramite un connettore di origine per inserire nuovamente i dati arricchiti in Real-Time CDP e integrare i profili con i dati forniti dal partner.

Alcuni connettori di origine consigliati a questo scopo possono essere:

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

## Limitazioni e risoluzione dei problemi {#limitations-and-troubleshooting}

Durante l’esplorazione del caso d’uso descritto in questa pagina, tieni presente le seguenti limitazioni:

* Se scegli di utilizzare gli ID partner, tieni presente che non vengono utilizzati durante la creazione [grafo delle identità](/help/identity-service/ui/identity-graph-viewer.md).

## Altri casi d’uso ottenuti tramite il supporto dei dati dei partner {#other-use-cases}

Esplora altri casi d’uso abilitati tramite il supporto dei dati dei partner in Real-Time CDP:

* (**Disponibile a breve**) [!BADGE Beta]{type=Informative}**Utilizzo del riconoscimento assistito dai partner** per personalizzare le esperienze nel sito durante la visita e per il retargeting fuori sito dopo la visita, senza che l’utente si autentichi o abbia antecedenti con il tuo marchio.
* (**Disponibile a breve**) [!BADGE Beta]{type=Informative}**Attivazione espansa** utilizzo degli ID partner per pubblicare ecosistemi che non accettano PII o PII con hash.