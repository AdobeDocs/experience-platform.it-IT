---
title: Destinazione Marketo Measure Ultimate
description: Scopri come collegare e attivare i dati alla destinazione Marketo Measure Ultimate.
last-substantial-update: 2023-03-07T00:00:00Z
exl-id: b4220841-8908-41ff-b977-dbeebfa787c8
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 2%

---

# Destinazione Marketo Measure Ultimate {#mmu-destination}

## Panoramica {#overview}

Marketo Measure (precedentemente Bizible) offre agli esperti di marketing informazioni approfondite sulle attività di marketing più efficaci per incrementare le entrate e massimizzare il ritorno sull&#39;investimento per l&#39;azienda. Marketo Measure è una soluzione di attribuzione marketing che tiene traccia automaticamente delle prestazioni dei canali e genera rapporti su di esse, fornendo visibilità sui canali che generano il maggior coinvolgimento dei clienti e consentendoti di ottimizzare le spese di marketing di conseguenza.

La destinazione abilita i flussi di dati business-to-business (B2B) da Adobe Experience Platform a Marketo Measure. La scheda è disponibile solo per i clienti di Marketo Measure Ultimate.

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la destinazione Marketo Measure, ecco alcuni esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione. Questa integrazione:

* Soddisfa i complessi requisiti di reporting relativi ai dati e alle prestazioni delle grandi aziende.
* Abilita la generazione di rapporti di attribuzione B2B con più sistemi di gestione delle relazioni con i clienti e automazione del marketing.
* Semplifica l’inserimento di dati punto di contatto offline di terze parti.

## Prerequisiti {#prerequisites}

Prendi nota dei seguenti prerequisiti per la destinazione Marketo Measure:

* Experience Platform La mappatura delle sandbox deve essere completata dall’amministratore nella pagina delle impostazioni di Marketo Measure. Senza la mappatura sandbox, non puoi completare il flusso di lavoro per connetterti alla destinazione e salvare e attivare i dati.
* È possibile esportare solo i set di dati delle classi XDM B2B (vedi, ad esempio, le classi XDM Business Account e XDM Business Opportunity ). Non è possibile inserire più set di dati della stessa classe XDM B2B per una determinata origine dati.
* Ogni set di dati può essere incluso in un solo flusso di dati per la destinazione Marketo Measure.

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione set di dati]** | Stai esportando set di dati non elaborati, che non sono raggruppati o strutturati in base agli interessi o alle qualifiche del pubblico. Ulteriori informazioni sulle [esportazioni di set di dati](/help/destinations/destination-types.md#dataset-export-destinations). |
| Frequenza di esportazione | **[!UICONTROL Batch]** | Questa destinazione batch esporta i file sulla piattaforma Marketo Measure ogni due ore. Ulteriori informazioni sulla [pianificazione delle esportazioni dei set di dati](/help/destinations/ui/export-datasets.md#scheduling). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni per gestire e attivare le destinazioni del set di dati]** [Controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nella sezione seguente.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.

![Flusso di lavoro Connetti a destinazione per la destinazione Marketo Measure.](/help/destinations/assets/catalog/adobe/marketo-measure-ultimate/marketo-measure-connect-to-destination.png)

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Esporta set di dati in questa destinazione {#export-datasets}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]** e **[!UICONTROL Gestisci e attiva destinazioni set di dati]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per istruzioni dettagliate sull&#39;esportazione dei set di dati in questa destinazione, leggi l&#39;esercitazione [Esporta set di dati](/help/destinations/ui/export-datasets.md).

## Convalidare l’esportazione dei dati {#exported-data}

Per convalidare un&#39;esportazione di set di dati riuscita, puoi verificare che il set di dati sia stato correttamente eseguito nel tuo data warehouse di [Snowflake](https://experienceleague.adobe.com/docs/marketo-measure/using/marketo-measure-data-warehouse/data-warehouse-access-reader-account.html).

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](/help/data-governance/home.md).
