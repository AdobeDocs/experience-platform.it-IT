---
title: Destinazione identità organizzazione Merkury
description: Scopri come creare una connessione di destinazione Merkury Enterprise Identity utilizzando l’interfaccia utente di Adobe Experience Platform.
last-substantial-update: 2024-07-20T00:00:00Z
exl-id: a5452183-289c-49c3-9574-e09b0153dc00
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 3%

---

# Destinazione identità organizzazione Merkury

>[!NOTE]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team [!DNL Merkury]. Per richieste di informazioni o richieste di aggiornamento, contattare il rappresentante dell&#39;account [!DNL Merkury].

## Panoramica

Utilizza la [!DNL Merkury Enterprise Identity] destinazione per generare profili di consumatori più accurati, completi e approfonditi. Grazie ai dati di profilo migliorati, gli esperti di marketing possono migliorare informazioni, segmenti e modelli, con conseguente targeting più preciso e modellazione predittiva.

![Diagramma che mostra l&#39;interconnessione tra Merkury e Experience Platform, incluse l&#39;acquisizione e l&#39;attivazione](../../assets/catalog/data-partners/merkury-identity/media/image1.png)

Segui i passaggi descritti in questa pagina della documentazione per creare una connessione di destinazione [!DNL Merkury Identity] e attivare i tipi di pubblico per l&#39;identificazione e l&#39;arricchimento tramite l&#39;interfaccia utente di Adobe Experience Platform.

>[!NOTE]
>
>Se desideri attivare i tipi di pubblico nelle destinazioni dei contenuti multimediali con il tuo account [!DNL Merkury Connect], utilizza invece la destinazione [!DNL Merkury Connections].

![La scheda di destinazione di Merkury Enterprise Identity è evidenziata nel catalogo delle destinazioni di Experience Platform.](../../assets/catalog/data-partners/merkury-identity/media/image2.png)

## Casi d’uso

La destinazione [!DNL Merkury Enterprise Identity] consente di trasferire in modo sicuro i dati PII del consumer per le seguenti funzionalità [!DNL Merkury]:

* **Qualità dei dati**: migliora la qualità dei dati del profilo del consumatore con l&#39;igiene dei dati e la standardizzazione. [!DNL Merkury] include l&#39;igiene postale negli Stati Uniti e l&#39;identificazione degli spostamenti per supportare i casi d&#39;uso di marketing di direct mailing più avanzati.
* **Risoluzione identità**: crea una singola vista accurata e completa del cliente, informata da [!DNL Merkury] ID individuali e domestici. Gli ID Merkury forniscono un livello profondo di collegamento del profilo basato sul grafico completo dell&#39;identità del consumatore adulto di [!DNL Merkury], costituito da oltre 268 milioni di persone.
* **Arricchimento**: migliora le informazioni e la personalizzazione con [!DNL Merkury Data]. [!DNL Merkury Data] include oltre 10.000 attributi di dati disponibili, che vanno da dati demografici, lifestyle, finanziari, eventi vita e dati di acquisto da [!DNL Merkury Data Suite].

>[!NOTE]
>
>Questi casi d’uso vengono eseguiti tramite una combinazione di connettori di destinazione e sorgente. Il cliente inizierebbe esportando i propri record esistenti dei clienti per l’arricchimento utilizzando questo connettore di destinazione. Il servizio di [!DNL Merkury] cercherà il file, lo recupererà, lo arricchirà con i dati di [!DNL Merkury] e genererà un file. Il cliente utilizzerà quindi la scheda di origine del connettore Source [!DNL Merkury] corrispondente per acquisire nuovamente i profili cliente idrati in Adobe Real-Time CDP.

## Prerequisiti

>[!IMPORTANT]
>
>* Per connettersi alla destinazione, è necessario **Visualizzare le destinazioni** e **Gestire le destinazioni**, **Attivare le destinazioni**, **Visualizzare i profili** e **Visualizzare i segmenti** [[Autorizzazioni di controllo di accesso]](https://experienceleague.adobe.com/it/docs/experience-platform/access-control/home#permissions). Leggere la [[panoramica sul controllo di accesso]](https://experienceleague.adobe.com/it/docs/experience-platform/access-control/ui/overview) o contattare l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario **Visualizza grafo identità** [[autorizzazione di controllo di accesso]](https://experienceleague.adobe.com/it/docs/experience-platform/access-control/home#permissions).\![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](../../assets/catalog/data-partners/merkury-identity/media/image3.png)

## Identità supportate {#supported-identities}

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Seleziona l’identità di destinazione GAID quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per inserzionisti | Selezionare l&#39;identità di destinazione IDFA quando l&#39;identità di origine è uno spazio dei nomi IDFA. |
| ECID | Experience Cloud ID | Uno spazio dei nomi che rappresenta ECID. A questo spazio dei nomi possono fare riferimento anche i seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Per ulteriori informazioni, consulta il seguente documento su [ECID](/help/identity-service/features/ecid.md). |
| phone_sha256 | Numeri di telefono con hash con algoritmo SHA256 | I numeri di telefono con hash SHA256 e testo normale sono supportati da Adobe Experience Platform. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per impostare [!DNL Experience Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per impostare [!DNL Experience Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. |
| extern_id | ID utente personalizzati | Seleziona questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi personalizzato. |

{style="table-layout:auto"}

## Tipi di pubblico supportati

Questa sezione descrive il tipo di pubblico che puoi esportare in questa destinazione.

| **Destinatari** | **Supportato** | **Descrizione** | **origine** |
|---|---|---|---|
| Servizio di segmentazione | ✓ | Tipi di pubblico generati tramite Experience Platform [[Servizio di segmentazione]](https://experienceleague.adobe.com/it/docs/experience-platform/segmentation/home). |
| Caricamenti personalizzati | x | Tipi di pubblico [[importato]](https://experienceleague.adobe.com/it/docs/experience-platform/segmentation/ui/overview#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| **Destinatari** | **Supportato** | **Origine descrizione** |
|---|---|---|      
| Servizio di segmentazione | ✓ | Tipi di pubblico generati tramite Experience Platform [[Servizio di segmentazione]](https://experienceleague.adobe.com/it/docs/experience-platform/segmentation/home). |
| Caricamenti personalizzati | X | Tipi di pubblico [[importato]](https://experienceleague.adobe.com/it/docs/experience-platform/segmentation/ui/overview#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Connettersi alla destinazione

>[!IMPORTANT]
>
>Per connettersi alla destinazione, è necessario **Visualizza destinazioni** e **Gestisci e attiva destinazioni set di dati** [[autorizzazioni controllo di accesso]](https://experienceleague.adobe.com/it/docs/experience-platform/access-control/home#permissions). Leggere la [[panoramica sul controllo di accesso]](https://experienceleague.adobe.com/it/docs/experience-platform/access-control/ui/overview) o contattare l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nel [[tutorial sulla configurazione della destinazione]](https://experienceleague.adobe.com/it/docs/experience-platform/destinations/ui/connect-destination). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione

Per eseguire l&#39;autenticazione nella destinazione, compilare i campi obbligatori e selezionare **Connetti alla destinazione**.

Per accedere al bucket su Experience Platform, devi fornire valori validi per le seguenti credenziali:

| **Credenziali** | **Descrizione** |
|---|---|
| Chiave di accesso | ID della chiave di accesso per il bucket. Puoi recuperare questo valore dal team Merkury. |
| Chiave segreta | ID della chiave segreta del bucket. Puoi recuperare questo valore dal team Merkury. |
| Nome del bucket | Questo è il bucket in cui verranno condivisi i file. Puoi recuperare questo valore dal team Merkury. |

{style="table-layout:auto"}

![nuova schermata di creazione della destinazione](../../assets/catalog/data-partners/merkury-identity/media/image4.png)

### Inserire i dettagli della destinazione

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Schermata dei dettagli della destinazione](../../assets/catalog/data-partners/merkury-identity/media/image6.png)


* **Nome (obbligatorio)** - Nome in cui verrà salvata la destinazione
* **Descrizione** - Breve spiegazione dello scopo della destinazione
* **Nome bucket (obbligatorio)** - Nome del bucket Amazon S3 configurato in S3
* **Percorso cartella (obbligatorio)** - Se vengono utilizzate sottodirectory in un bucket, è necessario definire un percorso oppure &#39;/&#39; per fare riferimento al percorso principale.
* **Tipo file** - Selezionare il formato che Experience Platform deve utilizzare per i file esportati. Consulta il team di Merkury per il tipo di file previsto per il tuo account.

>[!NOTE]
>
>Quando selezioni l’opzione CSV, vengono visualizzate le opzioni Delimitatore, Carattere preventivo, Carattere escape, Valore vuoto, Valore nullo, Formato compressione e Includi file manifesto, consulta il team Merkury per le impostazioni appropriate per il tuo account.

![immagine dell&#39;opzione csv](../../assets/catalog/data-partners/merkury-identity/media/image8.png)

### Account esistente

Gli account già definiti utilizzando la destinazione Merkury Enterprise Identity vengono visualizzati in un pop-up di elenco. Se questa opzione è selezionata, i dettagli dell’account sono visualizzati nella barra a destra. Visualizza l&#39;esempio dall&#39;interfaccia utente quando passi a **Destinazioni** > **Account**;

![Schermata dell&#39;account di destinazione nella pagina degli account di destinazione](../../assets/catalog/data-partners/merkury-identity/media/image5.png)


### Abilita avvisi

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](https://experienceleague.adobe.com/it/docs/experience-platform/destinations/ui/alerts).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **Avanti**.

## Attivare tipi di pubblico in questa destinazione

>[!IMPORTANT]
>
>* Per attivare i dati, sono necessarie le autorizzazioni di controllo di accesso **Visualizza destinazioni**, **Attiva destinazioni**, **Visualizza profili** e **Visualizza segmenti**. Leggi la panoramica sul controllo degli accessi o contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare le identità, è necessario disporre dell&#39;autorizzazione di controllo dell&#39;accesso **Visualizza grafo identità**.

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, leggi [Attiva dati pubblico per esportare i profili in batch](https://experienceleague.adobe.com/it/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations).

## Suggerimenti di mappatura

La corretta elaborazione dei file sul lato [!DNL Merkury] richiede elementi di nome e indirizzo. Anche se non tutti gli elementi sono necessari, fornire il più possibile contribuirà ad una corrispondenza di successo.

I suggerimenti di mappatura sono forniti nella tabella seguente che elenca gli attributi sul lato destinazione utilizzati dall&#39;elaborazione [!DNL Merkury] a cui i clienti possono mappare gli attributi del profilo. Considera questi elementi come suggerimenti, in quanto non tutti gli elementi sono necessari e i valori sorgente dipenderanno dalle esigenze dell’account.

| Campo di destinazione | Descrizione Source |
|---|---|
| id | Campo di identità da utilizzare per mappare i dati [!DNL Merkury] su Experience Platform tramite il connettore Source [!DNL Merkury Enterprise Identity] |
| Input_First_Name | Il valore `person.name.firstName` in Experience Platform. |
| Input_Last_Name | Il valore `person.name.lastName` in Experience Platform. |
| Input_Address_Line_1 | Il valore `mailingAddress.street` in Experience Platform. |
| Input_City | Il valore `mailingAddress.city` in Experience Platform. |
| Input_State_Province_Code | Il valore `mailingAddress.state` in Experience Platform. Da utilizzare se lo stato è nel formato di codice a due caratteri. |
| Nome_Provincia_Stato_Input | Il valore `mailingAddress.state` in Experience Platform. Usa se lo stato è il nome completo dello stato |
| Codice_postale_di_input | Il valore `mailingAddress.postalCode` in Experience Platform. |
| Input_Email_Address | Il valore che desideri mappare come indirizzo e-mail dei profili. |
| Input_Phone | Il valore da mappare come numero di telefono dei profili. |

{style="table-layout:auto"}

## Convalidare l’esportazione dei dati

Per verificare se i dati sono stati esportati correttamente, controlla il bucket di archiviazione Amazon S3 e assicurati che i file esportati contengano le popolazioni di profilo previste.

## Utilizzo dei dati e governance

Tutte le destinazioni Adobe Experience Platform sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come Adobe Experience Platform applica la governance dei dati, consulta la [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/it/docs/experience-platform/data-governance/home).

## Passaggi successivi

Seguendo questa esercitazione, è stato creato un flusso di dati per esportare i dati del profilo da Experience Platform nel percorso S3 gestito di [!DNL Merkury]. Quindi, devi contattare il tuo rappresentante [!DNL Merkury] con il nome dell&#39;account, i nomi dei file e il percorso del bucket in modo da poter configurare l&#39;elaborazione.
