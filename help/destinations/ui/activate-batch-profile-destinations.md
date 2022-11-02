---
keywords: attivare destinazioni profilo;attivare destinazioni;attivare dati; attivare le destinazioni di e-mail marketing; attivare le destinazioni di archiviazione cloud
title: Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch
type: Tutorial
description: Scopri come attivare i dati del pubblico in Adobe Experience Platform inviando segmenti a destinazioni basate su profili in batch.
exl-id: 82ca9971-2685-453a-9e45-2001f0337cda
source-git-commit: 79fc200f4e56699013b1ba3f91f5e383cea77e2a
workflow-type: tm+mt
source-wordcount: '3411'
ht-degree: 0%

---

# Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.
>
>Alcuni clienti che partecipano al programma beta migliorato per la funzionalità di esportazione dei file visualizzano il nuovo **[!UICONTROL Mappatura]** come parte del loro flusso di lavoro di attivazione per [nuove destinazioni di archiviazione cloud beta](/help/release-notes/2022/october-2022.md#destinations). Si prega inoltre di notare [limitazioni note](#known-limitations) come parte del rilascio.

## Panoramica {#overview}

Questo articolo spiega il flusso di lavoro necessario per attivare i dati del pubblico nelle destinazioni basate su profili batch di Adobe Experience Platform, come l’archiviazione cloud e le destinazioni di marketing via e-mail.

## Prerequisiti {#prerequisites}

Per attivare i dati nelle destinazioni, è necessario aver completato l&#39;operazione [connesso a una destinazione](./connect-destination.md). Se non lo hai già fatto, vai alla [catalogo delle destinazioni](../catalog/overview.md), sfoglia le destinazioni supportate e configura la destinazione che desideri utilizzare.

## Seleziona la destinazione {#select-destination}

1. Vai a **[!UICONTROL Connessioni > Destinazioni]**, quindi seleziona la **[!UICONTROL Catalogo]** scheda .

   ![Immagine che evidenzia come accedere alla scheda del catalogo delle destinazioni](../assets/ui/activate-batch-profile-destinations/catalog-tab.png)

1. Seleziona **[!UICONTROL Attivare i segmenti]** sulla scheda corrispondente alla destinazione in cui desideri attivare i segmenti, come illustrato di seguito.

   ![Immagine che evidenzia il pulsante Attiva segmenti](../assets/ui/activate-batch-profile-destinations/activate-segments-button.png)

1. Seleziona la connessione di destinazione che desideri utilizzare per attivare i segmenti, quindi seleziona **[!UICONTROL Successivo]**.

   ![Immagine che evidenzia come selezionare una o più destinazioni per attivare i segmenti in](../assets/ui/activate-batch-profile-destinations/select-destination.png)

1. Passa alla sezione successiva in [seleziona i segmenti](#select-segments).

## Selezionare i segmenti {#select-segments}

Utilizza le caselle di controllo a sinistra dei nomi dei segmenti per selezionare i segmenti che desideri attivare nella destinazione, quindi seleziona **[!UICONTROL Successivo]**.

![Immagine che evidenzia come selezionare uno o più segmenti da attivare](../assets/ui/activate-batch-profile-destinations/select-segments.png)


## Esportazione di segmenti programmata {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_schedule"
>title="Pianificazione"
>abstract="Utilizza l’icona a forma di matita per impostare il tipo di esportazione del file (file completi o incrementali) e la frequenza di esportazione."

[!DNL Adobe Experience Platform] esporta i dati per le destinazioni di marketing e archiviazione cloud sotto forma di [!DNL CSV] file. In **[!UICONTROL Pianificazione]** È possibile configurare la pianificazione e i nomi dei file per ciascun segmento che si sta esportando. La configurazione della pianificazione è obbligatoria, ma il nome del file è facoltativo.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] divide automaticamente i file di esportazione a 5 milioni di record (righe) per file. Ogni riga rappresenta un profilo.
>
>I nomi dei file divisi vengono aggiunti con un numero che indica che il file fa parte di un’esportazione più grande, in quanto tale: `filename.csv`, `filename_2.csv`, `filename_3.csv`.

Seleziona la **[!UICONTROL Crea pianificazione]** corrispondente al segmento da inviare alla destinazione.

![Immagine che evidenzia il pulsante Crea pianificazione](../assets/ui/activate-batch-profile-destinations/create-schedule-button.png)

### Esportare file completi {#export-full-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_exportoptions"
>title="Opzioni di esportazione file"
>abstract="Seleziona **Esportare file completi** per esportare uno snapshot completo di tutti i profili idonei per il segmento. Seleziona **Esportare file incrementali** per esportare solo i profili qualificati per il segmento dall’ultima esportazione. <br> La prima esportazione di file incrementali include tutti i profili idonei per il segmento, che agiscono come backfill. I file incrementali futuri includono solo i profili qualificati per il segmento a partire dalla prima esportazione di file incrementali."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#export-incremental-files" text="Esportare file incrementali"

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_aftersegmentevaluation"
>title="Attiva dopo la valutazione dei segmenti"
>abstract="L’attivazione viene eseguita immediatamente dopo il completamento del processo di segmentazione giornaliera. In questo modo i profili più aggiornati vengono esportati."

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_scheduled"
>title="Attivazione pianificata"
>abstract="L&#39;attivazione viene eseguita a un&#39;ora fissa del giorno."

Seleziona **[!UICONTROL Esportare file completi]** per attivare l’esportazione di un file contenente uno snapshot completo di tutte le qualifiche di profilo per il segmento selezionato.

![Immagine dell’interfaccia utente con l’opzione Esporta file completi selezionata.](../assets/ui/activate-batch-profile-destinations/export-full-files.png)

1. Utilizza la **[!UICONTROL Frequenza]** selettore per selezionare la frequenza di esportazione:

   * **[!UICONTROL Una volta]**: pianificare un&#39;esportazione di file completi on-demand una sola volta.
   * **[!UICONTROL Giornaliero]**: pianifica esportazioni di file completi una volta al giorno, ogni giorno, al momento specificato.

1. Utilizza la **[!UICONTROL Time]** per selezionare se l’esportazione deve essere eseguita immediatamente dopo la valutazione del segmento o su base pianificata, a un’ora specificata. Quando selezioni **[!UICONTROL Pianificato]** puoi utilizzare il selettore per scegliere l’ora del giorno, in [!DNL UTC] formato, quando deve aver luogo l&#39;esportazione.

   >[!NOTE]
   >
   >La **[!UICONTROL Dopo la valutazione dei segmenti]** l’opzione descritta di seguito è attualmente disponibile solo per alcuni clienti Beta.

   Utilizza la **[!UICONTROL Dopo la valutazione dei segmenti]** opzione per eseguire il processo di attivazione immediatamente dopo il completamento del processo di segmentazione batch giornaliero di Platform. In questo modo, quando il processo di attivazione viene eseguito, i profili più aggiornati vengono esportati nella destinazione.

   <!-- Batch segmentation currently runs at {{insert time of day}} and lasts for an average {{x hours}}. Adobe reserves the right to modify this schedule. -->

   ![Immagine che evidenzia l’opzione di valutazione Dopo segmento nel flusso di attivazione per le destinazioni batch.](../assets/ui/activate-batch-profile-destinations/after-segment-evaluation-option.png)
Utilizza la **[!UICONTROL Pianificato]** per fare in modo che il processo di attivazione venga eseguito a un orario fisso. In questo modo i dati del profilo di Experience Platform vengono esportati allo stesso tempo ogni giorno, ma i profili esportati potrebbero non essere i più aggiornati, a seconda che il processo di segmentazione del batch sia stato completato prima che il processo di attivazione inizi.

   ![Immagine che evidenzia l’opzione Pianificata nel flusso di attivazione per le destinazioni batch e mostra il selettore dell’ora.](../assets/ui/activate-batch-profile-destinations/scheduled-option.png)

   >[!IMPORTANT]
   >
   >A causa del modo in cui vengono configurati i processi di Experience Platform interni, la prima esportazione di file incrementali o completi potrebbe non contenere tutti i dati di backfill. <br> <br> Per garantire un’esportazione completa e più aggiornata dei dati di backfill sia per i file completi che per quelli incrementali, l’Adobe consiglia di impostare l’orario di esportazione del primo file dopo le 12:00 GMT del giorno successivo. Questa limitazione sarà affrontata nelle prossime versioni.

1. Utilizza la **[!UICONTROL Data]** selettore per scegliere il giorno o l’intervallo in cui deve aver luogo l’esportazione. Per le esportazioni giornaliere, la best practice prevede di impostare la data di inizio e di fine in modo che corrisponda alla durata delle campagne nelle piattaforme downstream.

   >[!IMPORTANT]
   >
   > Quando si seleziona un intervallo di esportazione, l’ultimo giorno dell’intervallo non viene incluso nelle esportazioni. Ad esempio, se selezioni un intervallo tra il 4 e l’11 gennaio, l’ultima esportazione di file avrà luogo il 10 gennaio.

1. Seleziona **[!UICONTROL Crea]** per salvare la pianificazione.

### Esportare file incrementali {#export-incremental-files}

Seleziona **[!UICONTROL Esportare file incrementali]** per attivare un’esportazione in cui il primo file è uno snapshot completo di tutte le qualifiche di profilo per il segmento selezionato e i file successivi sono qualifiche di profilo incrementali a partire dall’esportazione precedente.

>[!IMPORTANT]
>
>Il primo file incrementale esportato include tutti i profili idonei per un segmento, che funzionano come backfill.

![Immagine dell’interfaccia utente con l’opzione Esporta file incrementali selezionata.](../assets/ui/activate-batch-profile-destinations/export-incremental-files.png)

1. Utilizza la **[!UICONTROL Frequenza]** selettore per selezionare la frequenza di esportazione:

   * **[!UICONTROL Giornaliero]**: pianifica esportazioni incrementali di file una volta al giorno, ogni giorno, al momento specificato.
   * **[!UICONTROL Orario]**: pianificare esportazioni di file incrementali ogni 3, 6, 8 o 12 ore.

1. Utilizza la **[!UICONTROL Time]** selettore per scegliere l’ora del giorno, in [!DNL UTC] formato, quando deve aver luogo l&#39;esportazione.

   >[!IMPORTANT]
   >
   >A causa del modo in cui vengono configurati i processi di Experience Platform interni, la prima esportazione di file incrementali o completi potrebbe non contenere tutti i dati di backfill. <br> <br> Per garantire un’esportazione completa e più aggiornata dei dati di backfill sia per i file completi che per quelli incrementali, l’Adobe consiglia di impostare l’orario di esportazione del primo file dopo le 12:00 GMT del giorno successivo. Questa limitazione sarà affrontata nelle prossime versioni.

1. Utilizza la **[!UICONTROL Data]** selettore per scegliere l’intervallo in cui deve avvenire l’esportazione. È consigliabile impostare la data di inizio e di fine in modo che corrisponda alla durata delle campagne nelle piattaforme downstream.

   >[!IMPORTANT]
   >
   >L’ultimo giorno dell’intervallo non è incluso nelle esportazioni. Ad esempio, se selezioni un intervallo tra il 4 e l’11 gennaio, l’ultima esportazione di file avrà luogo il 10 gennaio.

1. Seleziona **[!UICONTROL Crea]** per salvare la pianificazione.

### Configurare i nomi dei file {#file-names}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_filename"
>title="Configura nome file"
>abstract="Per le destinazioni basate su file, viene generato un nome file univoco per segmento. Utilizza l’editor dei nomi file per creare e modificare un nome file univoco o per mantenere il nome predefinito."

Per la maggior parte delle destinazioni, i nomi file predefiniti sono costituiti dal nome di destinazione, dall’ID del segmento e da un indicatore di data e ora. Ad esempio, puoi modificare i nomi dei file esportati per distinguere tra campagne diverse o per far sì che il tempo di esportazione dei dati sia aggiunto ai file. Tieni presente che alcuni sviluppatori di destinazione potrebbero scegliere di visualizzare opzioni di aggiunta di nomi file predefiniti diverse per le rispettive destinazioni.

Seleziona l’icona a forma di matita per aprire una finestra modale e modificare i nomi dei file. I nomi dei file sono limitati a 255 caratteri.

>[!NOTE]
>
>L&#39;immagine seguente mostra come modificare i nomi dei file [!DNL Amazon S3] destinazioni ma il processo è identico per tutte le destinazioni batch (ad esempio SFTP, [!DNL Azure Blob Storage]oppure [!DNL Google Cloud Storage]).

![Immagine che evidenzia l’icona della matita, utilizzata per configurare i nomi dei file.](../assets/ui/activate-batch-profile-destinations/configure-name.png)

Nell’editor dei nomi dei file, puoi selezionare diversi componenti da aggiungere al nome del file.

![Immagine che visualizza tutte le opzioni disponibili per il nome del file.](../assets/ui/activate-batch-profile-destinations/activate-workflow-configure-step-2.png)

Impossibile rimuovere il nome di destinazione e l’ID del segmento dai nomi dei file. Oltre a questi, puoi aggiungere quanto segue:

| Opzione nome file | Descrizione |
|---------|----------|
| **[!UICONTROL Nome del segmento]** | Nome del segmento esportato. |
| **[!UICONTROL Data e ora]** | Seleziona tra l’aggiunta di un `MMDDYYYY_HHMMSS` o un timestamp Unix a 10 cifre dell’ora in cui i file vengono generati. Scegliere una di queste opzioni se si desidera che i file abbiano un nome file dinamico generato con ogni esportazione incrementale. |
| **[!UICONTROL Testo personalizzato]** | Testo personalizzato da aggiungere ai nomi dei file. |
| **[!UICONTROL ID destinazione]** | ID del flusso di dati di destinazione utilizzato per esportare il segmento. <br> **Nota**: Questa opzione di aggiunta del nome file è disponibile solo per i clienti beta che partecipano al programma beta della funzionalità di esportazione file migliorata. Contatta il tuo rappresentante di Adobe o l’Assistenza clienti se desideri accedere al programma beta. |
| **[!UICONTROL Nome destinazione]** | Nome del flusso di dati di destinazione utilizzato per esportare il segmento. <br> **Nota**: Questa opzione di aggiunta del nome file è disponibile solo per i clienti beta che partecipano al programma beta della funzionalità di esportazione file migliorata. Contatta il tuo rappresentante di Adobe o l’Assistenza clienti se desideri accedere al programma beta. |
| **[!UICONTROL Nome dell&#39;organizzazione]** | Nome dell’organizzazione in Experience Platform. <br> **Nota**: Questa opzione di aggiunta del nome file è disponibile solo per i clienti beta che partecipano al programma beta della funzionalità di esportazione file migliorata. Contatta il tuo rappresentante di Adobe o l’Assistenza clienti se desideri accedere al programma beta. |
| **[!UICONTROL Nome della sandbox]** | ID della sandbox utilizzata per esportare il segmento. <br> **Nota**: Questa opzione di aggiunta del nome file è disponibile solo per i clienti beta che partecipano al programma beta della funzionalità di esportazione file migliorata. Contatta il tuo rappresentante di Adobe o l’Assistenza clienti se desideri accedere al programma beta. |

{style=&quot;table-layout:auto&quot;}

Seleziona **[!UICONTROL Applica modifiche]** per confermare la selezione.

>[!IMPORTANT]
> 
>Se non si seleziona il **[!UICONTROL Data e ora]** i nomi dei file saranno statici e il nuovo file esportato sovrascriverà il file precedente nel percorso di archiviazione con ogni esportazione. Quando esegui un processo di importazione ricorrente da un percorso di archiviazione in una piattaforma di marketing e-mail, questa è l’opzione consigliata.

Al termine della configurazione di tutti i segmenti, seleziona **[!UICONTROL Successivo]** per continuare.

## Selezionare gli attributi del profilo {#select-attributes}

Per le destinazioni basate su profili, devi selezionare gli attributi di profilo da inviare alla destinazione.

1. In **[!UICONTROL Seleziona attributi]** pagina, seleziona **[!UICONTROL Aggiungi nuovo campo]**.

   ![Immagine che evidenzia il pulsante Aggiungi nuovo campo .](../assets/ui/activate-batch-profile-destinations/add-new-field.png)

1. Seleziona la freccia a destra del **[!UICONTROL Campo schema]** voce.

   ![Immagine che evidenzia come selezionare un campo sorgente.](../assets/ui/activate-batch-profile-destinations/select-target-field.png)

1. In **[!UICONTROL Seleziona campo]** seleziona gli attributi XDM da inviare alla destinazione, quindi scegli **[!UICONTROL Seleziona]**.

   ![Immagine che mostra i vari campi disponibili come campi di origine.](../assets/ui/activate-batch-profile-destinations/target-field-page.png)

1. Per aggiungere altre mappature, ripeti i passaggi da uno a tre.

>[!NOTE]
>
> Adobe Experience Platform precompila la selezione con quattro attributi consigliati e di uso comune dallo schema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

>[!IMPORTANT]
>
>A causa di una limitazione nota, al momento non è possibile utilizzare il **[!UICONTROL Seleziona campo]** finestra da aggiungere `segmentMembership.status` alle esportazioni di file. È invece necessario incollare manualmente il valore `xdm: segmentMembership.status` nel campo schema, come illustrato di seguito.
>
>![Registrazione su schermo che mostra la soluzione per l’appartenenza al segmento nella fase di mappatura del flusso di lavoro di attivazione.](/help/destinations/assets/ui/activate-batch-profile-destinations/segment-membership.gif)

Le esportazioni di file variano nei seguenti modi, a seconda che `segmentMembership.status` è selezionato:
* Se la `segmentMembership.status` campo selezionato, i file esportati includono **[!UICONTROL Attivo]** membri nello snapshot completo iniziale e **[!UICONTROL Attivo]** e **[!UICONTROL Scaduto]** membri nelle esportazioni incrementali successive.
* Se la `segmentMembership.status` campo non selezionato, i file esportati includono solo **[!UICONTROL Attivo]** membri nello snapshot completo iniziale e nelle esportazioni incrementali successive.

![Immagine che mostra gli attributi consigliati precompilati nella fase di mappatura del flusso di lavoro di attivazione dei segmenti.](../assets/ui/activate-batch-profile-destinations/mandatory-deduplication.png)

### Attributi obbligatori {#mandatory-attributes}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_mandatorykey"
>title="Informazioni sugli attributi obbligatori"
>abstract="Seleziona gli attributi dello schema XDM che tutti i profili esportati devono includere. I profili senza la chiave obbligatoria non vengono esportati nella destinazione . Se non selezioni una chiave obbligatoria, vengono esportati tutti i profili qualificati, indipendentemente dai relativi attributi."

Un attributo obbligatorio è una casella di controllo abilitata dall’utente che assicura che tutti i record del profilo contengano l’attributo selezionato. Ad esempio: tutti i profili esportati contengono un indirizzo e-mail. &#x200B;

Puoi contrassegnare gli attributi come obbligatori per garantire che [!DNL Platform] esporta solo i profili che includono l’attributo specifico. Di conseguenza, può essere utilizzato come ulteriore forma di filtro. Contrassegnare un attributo come obbligatorio è **not** obbligatorio.

Se non selezioni un attributo obbligatorio, vengono esportati tutti i profili qualificati, indipendentemente dai relativi attributi.

È consigliabile che uno degli attributi sia un [identificatore univoco](../../destinations/catalog/email-marketing/overview.md#identity) dallo schema. Per ulteriori informazioni sugli attributi obbligatori, consulta la sezione relativa all’identità in [Destinazioni di marketing e-mail](../../destinations/catalog/email-marketing/overview.md#identity) documentazione.

### Chiavi di deduplicazione {#deduplication-keys}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_deduplicationkey"
>title="Informazioni sulle chiavi di deduplicazione"
>abstract="Elimina più record dello stesso profilo nei file di esportazione selezionando una chiave di deduplicazione. Seleziona un singolo spazio dei nomi o fino a due attributi di schema XDM come chiave di deduplicazione. La mancata selezione di una chiave di deduplicazione può causare la presenza di voci di profilo duplicate nei file di esportazione."

Una chiave di deduplicazione è una chiave primaria definita dall’utente che determina l’identità in base alla quale gli utenti desiderano che i loro profili vengano deduplicati. &#x200B;

Le chiavi di deduplicazione eliminano la possibilità di avere più record dello stesso profilo in un unico file di esportazione.

Esistono tre modi per utilizzare le chiavi di deduplicazione in [!DNL Platform]:

* Utilizzo di un singolo spazio dei nomi di identità come [!UICONTROL chiave di deduplicazione]
* Utilizzo di un singolo attributo di profilo da un [!DNL XDM] profilo come [!UICONTROL chiave di deduplicazione]
* Utilizzo di una combinazione di due attributi di profilo da un [!DNL XDM] profilo come chiave composita

>[!IMPORTANT]
>
> È possibile esportare un singolo namespace di identità in una destinazione e lo spazio dei nomi viene impostato automaticamente come chiave di deduplicazione. L’invio di più namespace a una destinazione non è supportato.
> 
> Non è possibile utilizzare una combinazione di namespace identità e attributi di profilo come chiavi di deduplicazione.

### Esempio di deduplicazione {#deduplication-example}

Questo esempio illustra il funzionamento della deduplicazione, a seconda delle chiavi di deduplicazione selezionate.

Consideriamo i due profili seguenti.

**Profilo A**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_1@example.com"
      },
      {
        "id": "johndoe_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "existing",
        "lastQualificationTime": "2021-03-10 10:03:08"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "Doe",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

**Profilo B**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_1@example.com"
      },
      {
        "id": "johndoe_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "existing",
        "lastQualificationTime": "2021-04-10 11:33:28"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "D",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

### Caso di utilizzo della deduplicazione 1: nessuna deduplicazione {#deduplication-use-case-1}

Senza la deduplicazione, il file di esportazione conterrebbe le seguenti voci.

| personalEmail | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | Doe |
| johndoe@example.com | John | D |


### Caso di utilizzo della deduplicazione 2: deduplicazione basata sullo spazio dei nomi identità {#deduplication-use-case-2}

Presupponendo una deduplicazione da parte della [!DNL Email] spazio dei nomi, il file di esportazione conterrà le seguenti voci. Il profilo B è l’ultimo ad essere qualificato per il segmento, quindi è l’unico ad essere esportato.

| E-mail* | personalEmail | firstName | lastName |
|---|---|---|---|
| johndoe_1@example.com | johndoe@example.com | John | D |
| johndoe_2@example.com | johndoe@example.com | John | D |

### Caso di utilizzo della deduplicazione 3: deduplicazione basata su un singolo attributo di profilo {#deduplication-use-case-3}

Presupponendo una deduplicazione da parte della `personal Email` attributo , il file di esportazione conterrà la seguente voce. Il profilo B è l’ultimo ad essere qualificato per il segmento, quindi è l’unico ad essere esportato.

| personalEmail* | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | D |


### Caso di utilizzo della deduplicazione 4: deduplicazione basata su due attributi di profilo {#deduplication-use-case-4}

Supponendo la deduplicazione da parte della chiave composita `personalEmail + lastName`, il file di esportazione conterrebbe le seguenti voci.

| personalEmail* | lastName* | firstName |
|---|---|---|
| johndoe@example.com | D | John |
| johndoe@example.com | Doe | John |


Adobe consiglia di selezionare uno spazio dei nomi di identità, ad esempio un [!DNL CRM ID] o indirizzo e-mail come chiave di deduplicazione, per garantire che tutti i record di profilo siano identificati in modo univoco.

>[!NOTE]
> 
>Se sono state applicate etichette di utilizzo dei dati a determinati campi all’interno di un set di dati (anziché all’intero set di dati), l’applicazione di tali etichette a livello di campo all’attivazione si verifica nelle seguenti condizioni:
>
>* I campi vengono utilizzati nella definizione del segmento.
>* I campi sono configurati come attributi proiettati per la destinazione di destinazione.
>
> Ad esempio, se il campo `person.name.firstName` dispone di alcune etichette di utilizzo dei dati in conflitto con l&#39;azione di marketing della destinazione; nel passaggio di revisione viene visualizzata una violazione dei criteri di utilizzo dei dati. Per ulteriori informazioni, consulta [Governance dei dati in Adobe Experience Platform](../../rtcdp/privacy/data-governance-overview.md#destinations).

## Mappatura (Beta) {#mapping}

>[!IMPORTANT]
> 
>Seleziona i clienti beta possono visualizzare un miglioramento **[!UICONTROL Mappatura]** passo che sostituisce [Selezionare gli attributi del profilo](#select-attributes) passo descritto in precedenza. Questo nuovo **[!UICONTROL Mappatura]** consente di modificare le intestazioni dei file esportati in tutti i nomi personalizzati desiderati.
> 
> La funzionalità e la documentazione sono soggette a modifiche. Contatta il tuo rappresentante di Adobe o l’Assistenza clienti se desideri accedere a questo programma beta.

In questo passaggio, devi selezionare gli attributi di profilo da aggiungere ai file esportati nella destinazione di destinazione. Per selezionare gli attributi di profilo e le identità da esportare:

1. In **[!UICONTROL Mappatura]** pagina, seleziona **[!UICONTROL Aggiungi nuovo campo]**.

   ![Aggiungi un nuovo controllo campo evidenziato nel flusso di lavoro di mappatura.](../assets/ui/activate-batch-profile-destinations/add-new-field-mapping.png)

1. Seleziona la freccia a destra del **[!UICONTROL Campo di origine]** voce.

   ![Seleziona il controllo del campo sorgente evidenziato nel flusso di lavoro di mappatura.](../assets/ui/activate-batch-profile-destinations/select-source-field.png)

1. In **[!UICONTROL Selezionare il campo di origine]** , seleziona gli attributi di profilo e le identità da includere nei file esportati nella destinazione, quindi scegli **[!UICONTROL Seleziona]**.

   >[!TIP]
   > 
   >Puoi usare il campo di ricerca per limitare la selezione, come illustrato di seguito.

   ![Finestra modale che mostra gli attributi di profilo che possono essere esportati nella destinazione.](../assets/ui/activate-batch-profile-destinations/select-source-field-modal.png)


1. Il campo selezionato per l’esportazione viene ora visualizzato nella vista di mappatura. Se lo desideri, puoi modificare il nome dell’intestazione nel file esportato. A questo scopo, seleziona l’icona nel campo di destinazione.

   ![Finestra modale che mostra gli attributi di profilo che possono essere esportati nella destinazione.](../assets/ui/activate-batch-profile-destinations/mapping-step-select-target-field.png)

1. In **[!UICONTROL Selezionare il campo di destinazione]** , digita il nome desiderato nell’intestazione del file esportato, quindi scegli **[!UICONTROL Seleziona]**.

   ![Finestra modale che mostra un nome descrittivo digitato per un&#39;intestazione.](../assets/ui/activate-batch-profile-destinations/select-target-field-mapping.png)

1. Il campo selezionato per l’esportazione viene ora visualizzato nella vista di mappatura e mostra l’intestazione modificata nel file esportato.

   ![Finestra modale che mostra gli attributi di profilo che possono essere esportati nella destinazione.](../assets/ui/activate-batch-profile-destinations/select-target-field-updated.png)

1. (Facoltativo) Puoi selezionare il campo esportato come un [chiave obbligatoria](#mandatory-keys) o [chiave di deduplicazione](#deduplication-keys).

   ![Finestra modale che mostra gli attributi di profilo che possono essere esportati nella destinazione.](../assets/ui/activate-batch-profile-destinations/select-mandatory-deduplication-key.png)

1. Per aggiungere altri campi per l’esportazione, ripeti i passaggi precedenti.

### Limitazioni note {#known-limitations}

Il nuovo **[!UICONTROL Mappatura]** la pagina presenta le seguenti limitazioni note:

#### L’attributo di appartenenza al segmento non può essere selezionato tramite il flusso di lavoro di mappatura

A causa di una limitazione nota, al momento non è possibile utilizzare il **[!UICONTROL Seleziona campo]** finestra da aggiungere `segmentMembership.status` alle esportazioni di file. È invece necessario incollare manualmente il valore `xdm: segmentMembership.status` nel campo schema, come illustrato di seguito.

![Registrazione su schermo che mostra la soluzione per l’appartenenza al segmento nella fase di mappatura del flusso di lavoro di attivazione.](/help/destinations/assets/ui/activate-batch-profile-destinations/segment-membership-mapping-step.gif)

Le esportazioni di file variano nei seguenti modi, a seconda che `segmentMembership.status` è selezionato:
* Se la `segmentMembership.status` campo selezionato, i file esportati includono **[!UICONTROL Attivo]** membri nello snapshot completo iniziale e **[!UICONTROL Attivo]** e **[!UICONTROL Scaduto]** membri nelle esportazioni incrementali successive.
* Se la `segmentMembership.status` campo non selezionato, i file esportati includono solo **[!UICONTROL Attivo]** membri nello snapshot completo iniziale e nelle esportazioni incrementali successive.

#### Impossibile selezionare i namespace identità per le esportazioni

La selezione degli spazi dei nomi delle identità da esportare, come illustrato nell’immagine seguente, non è attualmente supportata. Quando si selezionano i namespace di identità per l’esportazione, viene generato un errore **[!UICONTROL Revisione]** passo.

![Mappatura non supportata che mostra esportazioni di identità](/help/destinations/assets/ui/activate-batch-profile-destinations/unsupported-identity-mapping.png)

Come soluzione temporanea se devi aggiungere spazi dei nomi di identità ai file esportati durante la versione beta, puoi:
* Utilizza le destinazioni di archiviazione cloud legacy per i flussi di dati in cui desideri includere i namespace di identità nelle esportazioni
* Carica le identità come attributi in Experience Platform, quindi esportale nelle destinazioni di archiviazione cloud.

## Revisione {#review}

Sulla **[!UICONTROL Revisione]** per visualizzare un riepilogo della selezione. Seleziona **[!UICONTROL Annulla]** per interrompere il flusso, **[!UICONTROL Indietro]** per modificare le impostazioni, oppure **[!UICONTROL Fine]** per confermare la selezione e iniziare a inviare dati alla destinazione.

>[!IMPORTANT]
>
>In questo passaggio, Adobe Experience Platform verifica la presenza di violazioni dei criteri di utilizzo dei dati. Di seguito è riportato un esempio di violazione di un criterio. Non puoi completare il flusso di lavoro di attivazione dei segmenti finché non avrai risolto la violazione. Per informazioni su come risolvere le violazioni dei criteri, vedi [Applicazione delle politiche](../../rtcdp/privacy/data-governance-overview.md#enforcement) nella sezione documentazione sulla governance dei dati .

![Immagine che mostra un esempio di violazione dei criteri sui dati.](../assets/common/data-policy-violation.png)

Se non sono state rilevate violazioni dei criteri, seleziona **[!UICONTROL Fine]** per confermare la selezione e iniziare a inviare dati alla destinazione.

![Immagine che mostra la schermata di revisione del flusso di lavoro di attivazione dei segmenti.](../assets/ui/activate-batch-profile-destinations/review.png)

## Verificare l’attivazione dei segmenti {#verify}

Per le destinazioni di e-mail marketing e di cloud storage, Adobe Experience Platform crea un `.csv` nel percorso di archiviazione fornito. Attendi la creazione di un nuovo file nel percorso di archiviazione in base alla pianificazione impostata nel flusso di lavoro. Il formato predefinito del file è:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

Ad esempio, se hai selezionato una frequenza di esportazione giornaliera, i file che riceveresti per tre giorni consecutivi potrebbero avere questo aspetto:

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

La presenza di questi file nel percorso di archiviazione è la conferma di un&#39;attivazione riuscita. Per comprendere la struttura dei file esportati, puoi [scaricare un file .csv di esempio](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). Questo file di esempio include gli attributi del profilo `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`e `personalEmail.address`.
