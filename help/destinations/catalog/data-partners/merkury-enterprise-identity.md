---
title: Destinazione identità organizzazione Merkury
description: Scopri come creare una connessione di destinazione Merkury Enterprise Identity utilizzando l’interfaccia utente di Adobe Experience Platform.
source-git-commit: 01ce38d26cf61706de84ec143e3dd8af720d0591
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 2%

---


# Destinazione identità organizzazione Merkury

>[!NOTE]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti da [!DNL Merkury] team. Per richieste di informazioni o richieste di aggiornamento, contatta il tuo [!DNL Merkury] rappresentante dell’account.

## Panoramica

Utilizza il [!DNL Merkury Enterprise Identity] per creare profili di consumatori più precisi, completi e approfonditi. Grazie ai dati di profilo migliorati, gli esperti di marketing possono migliorare informazioni, segmenti e modelli, con conseguente targeting più preciso e modellazione predittiva.

![Schema dell’interconnessione tra Merkury e Experience Platform, compresi l’acquisizione e l’attivazione](../../assets/catalog/data-partners/merkury-identity/media/image1.png)

Segui i passaggi descritti in questa pagina della documentazione per creare un [!DNL Merkury Identity] connessione di destinazione e attivazione di tipi di pubblico per l’identificazione e l’arricchimento tramite l’interfaccia utente di Adobe Experience Platform.

>[!NOTE]
>
>Se desideri attivare dei tipi di pubblico su destinazioni multimediali con il tuo [!DNL Merkury Connect] account, utilizza [!DNL Merkury Connections] invece della destinazione.

![La scheda di destinazione Merkury Enterprise Identity evidenziata nel catalogo delle destinazioni di Experience Platform.](../../assets/catalog/data-partners/merkury-identity/media/image2.png)

## Casi d’uso

Il [!DNL Merkury Enterprise Identity] La destinazione consente di trasferire in modo sicuro i dati PII del consumatore per i seguenti elementi [!DNL Merkury] funzionalità:

* **Qualità dei dati**: migliorare la qualità dei dati del profilo dei consumatori grazie all’igiene dei dati e alla standardizzazione. [!DNL Merkury] include l’igiene postale negli Stati Uniti e l’identificazione degli spostamenti per supportare i casi d’uso più avanzati del marketing direct mailing.
* **Risoluzione identità**: crea una visione unica, accurata e completa del cliente, informata da [!DNL Merkury] ID individuali e di famiglia. Gli ID Merkury forniscono un livello profondo di collegamento del profilo basato su [!DNL Merkury]Il grafico completo dell&#39;identità del consumatore adulto degli Stati Uniti di 268+ milioni di persone.
* **Arricchimento**: informazioni e personalizzazione migliorate con [!DNL Merkury Data]. [!DNL Merkury Data] include oltre 10.000 attributi di dati disponibili, tra cui dati demografici, sullo stile di vita, finanziari, eventi vita e dati di acquisto dal [!DNL Merkury Data Suite].

>[!NOTE]
>
>Questi casi d’uso vengono eseguiti tramite una combinazione di connettori di destinazione e sorgente. Il cliente inizierebbe esportando i propri record esistenti dei clienti per l’arricchimento utilizzando questo connettore di destinazione. [!DNL Merkury]Il servizio di ricerca il file, lo recupera e lo arricchisce con [!DNL Merkury]e genera un file. Il cliente utilizzerà quindi il [!DNL Merkury] Scheda sorgente del connettore Source per acquisire i profili cliente idratati nuovamente in Adobe Real-Time CDP.

## Prerequisiti

>[!IMPORTANT]
>
>* Per connettersi alla destinazione, è necessario **Visualizza destinazioni** e **Gestire le destinazioni**, **Attivare le destinazioni**, **Visualizza profili**, e **Visualizzare segmenti** [[autorizzazioni di controllo degli accessi]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions). Leggi le [[panoramica sul controllo degli accessi]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario **Visualizza grafico delle identità** [[autorizzazione per il controllo degli accessi]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions).\![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](../../assets/catalog/data-partners/merkury-identity/media/image3.png)

## Identità supportate {#supported-identities}

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Seleziona l’identità di destinazione GAID quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per inserzionisti | Selezionare l&#39;identità di destinazione IDFA quando l&#39;identità di origine è uno spazio dei nomi IDFA. |
| ECID | Experience Cloud ID | Uno spazio dei nomi che rappresenta ECID. A questo spazio dei nomi possono fare riferimento anche i seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Vedi il seguente documento su [ECID](/help/identity-service/features/ecid.md) per ulteriori informazioni. |
| phone_sha256 | Numeri di telefono con hash con algoritmo SHA256 | I numeri di telefono con hash SHA256 e testo normale sono supportati da Adobe Experience Platform. Quando il campo sorgente contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] esegui automaticamente l’hash dei dati all’attivazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Quando il campo sorgente contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] esegui automaticamente l’hash dei dati all’attivazione. |
| extern_id | ID utente personalizzati | Seleziona questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi personalizzato. |

{style="table-layout:auto"}

## Tipi di pubblico supportati

Questa sezione descrive il tipo di pubblico che puoi esportare in questa destinazione.

| **Pubblico** | **Supportato** | **Descrizione** | **origine** |
|---|---|---|---|
| Servizio di segmentazione | ✓ | Tipi di pubblico generati dall’Experience Platform [[Servizio di segmentazione]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home). |
| Caricamenti personalizzati | x | Tipi di pubblico [[importato]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/overview#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.
|**Pubblico**|**Supportato**|**Origine descrizione**|\
|—|—|—|\
✓ |Servizio di segmentazione|Pubblico generato tramite l’Experience Platform [[Servizio di segmentazione]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/home).| Caricamenti personalizzati|X|Tipi di pubblico [[importato]](https://experienceleague.adobe.com/en/docs/experience-platform/segmentation/ui/overview#import-audience) in Experience Platform da file CSV.

{style="table-layout:auto"}

## Connettersi alla destinazione

>[!IMPORTANT]
>
>Per connettersi alla destinazione, è necessario **Visualizza destinazioni** e **Gestire e attivare le destinazioni dei set di dati** [[autorizzazioni di controllo degli accessi]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home#permissions). Leggi le [[panoramica sul controllo degli accessi]](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/ui/overview) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [[tutorial sulla configurazione della destinazione]](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/connect-destination). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione

Per autenticare nella destinazione, compila i campi obbligatori e seleziona **Connetti alla destinazione**.

Per accedere al bucket su Experience Platform, devi fornire valori validi per le seguenti credenziali:

| **Credenziali** | **Descrizione** |
|---|---|
| Chiave di accesso | ID della chiave di accesso per il bucket. Puoi recuperare questo valore dal team Merkury. |
| Chiave segreta | ID della chiave segreta del bucket. Puoi recuperare questo valore dal team Merkury. |
| Nome del bucket | Questo è il bucket in cui verranno condivisi i file. Puoi recuperare questo valore dal team Merkury. |

{style="table-layout:auto"}

![schermata di creazione nuova destinazione](../../assets/catalog/data-partners/merkury-identity/media/image4.png)

### Inserire i dettagli della destinazione

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Schermata dei dettagli della destinazione](../../assets/catalog/data-partners/merkury-identity/media/image6.png)


* **Nome (obbligatorio)** - Il nome con cui verrà salvata la destinazione
* **Descrizione** - Breve spiegazione dello scopo della destinazione
* **Nome bucket (obbligatorio)** - Nome del bucket Amazon S3 impostato su S3
* **Percorso cartella (obbligatorio)** - Se si utilizzano sottodirectory in un bucket, è necessario definire un percorso oppure &#39;/&#39; per fare riferimento al percorso principale.
* **Tipo di file** - Selezionare il formato che l&#39;Experience Platform deve utilizzare per i file esportati. Consulta il team di Merkury per il tipo di file previsto per il tuo account.

>[!NOTE]
>
>Quando selezioni l’opzione CSV, vengono visualizzate le opzioni Delimitatore, Carattere preventivo, Carattere escape, Valore vuoto, Valore nullo, Formato compressione e Includi file manifesto, consulta il team Merkury per le impostazioni appropriate per il tuo account.

![immagine dell&#39;opzione csv](../../assets/catalog/data-partners/merkury-identity/media/image8.png)

### Account esistente

Gli account già definiti utilizzando la destinazione Merkury Enterprise Identity vengono visualizzati in un pop-up di elenco. Se questa opzione è selezionata, i dettagli dell’account sono visualizzati nella barra a destra. Visualizza l’esempio dall’interfaccia utente, quando passi a **Destinazioni** > **Account**;

![Schermata dell’account di destinazione nella pagina degli account di destinazione](../../assets/catalog/data-partners/merkury-identity/media/image5.png)


### Abilita avvisi

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/alerts).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **Successivo**.

## Attivare tipi di pubblico in questa destinazione

>[!IMPORTANT]
>
>* Per attivare i dati, è necessario **Visualizza destinazioni**, **Attivare le destinazioni**, **Visualizza profili**, e **Visualizzare segmenti** autorizzazioni di controllo degli accessi. Leggi la panoramica sul controllo degli accessi o contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare le identità, è necessario **Visualizza grafico delle identità** autorizzazione per il controllo degli accessi.

Letto [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](https://experienceleague.adobe.com/en/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

## Suggerimenti di mappatura

La corretta elaborazione dei file sul [!DNL Merkury] side richiede elementi nome e indirizzo. Anche se non tutti gli elementi sono necessari, fornire il più possibile contribuirà ad una corrispondenza di successo.

I suggerimenti di mappatura sono forniti nella tabella seguente elencando gli attributi sul lato destinazione utilizzati da [!DNL Merkury] elaborazione a cui i clienti possono mappare gli attributi del profilo. Considera questi elementi come suggerimenti, in quanto non tutti gli elementi sono necessari e i valori sorgente dipenderanno dalle esigenze dell’account.

| Campo di destinazione | Descrizione Source |
|---|---|
| id | Campo di identità da utilizzare per la mappatura [!DNL Merkury] dati di cui eseguire l’Experience Platform tramite [!DNL Merkury Enterprise Identity] Connettore Source |
| Input_First_Name | Il `person.name.firstName` valore in Experience Platform. |
| Input_Last_Name | Il `person.name.lastName` valore in Experience Platform. |
| Input_Address_Line_1 | Il `mailingAddress.street` valore in Experience Platform. |
| Input_City | Il `mailingAddress.city` valore in Experience Platform. |
| Input_State_Province_Code | Il `mailingAddress.state` valore in Experience Platform. Da utilizzare se lo stato è nel formato di codice a due caratteri. |
| Nome_Provincia_Stato_Input | Il `mailingAddress.state` valore in Experience Platform. Usa se lo stato è il nome completo dello stato |
| Codice_postale_di_input | Il `mailingAddress.postalCode` valore in Experience Platform. |
| Input_Email_Address | Il valore che desideri mappare come indirizzo e-mail dei profili. |
| Input_Phone | Il valore da mappare come numero di telefono dei profili. |

{style="table-layout:auto"}

## Convalidare l’esportazione dei dati

Per verificare se i dati sono stati esportati correttamente, controlla il bucket di archiviazione Amazon S3 e assicurati che i file esportati contengano le popolazioni di profilo previste.

## Utilizzo dei dati e governance

Tutte le destinazioni Adobe Experience Platform sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come Adobe Experience Platform applica la governance dei dati, leggi [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/en/docs/experience-platform/data-governance/home).

## Passaggi successivi

Seguendo questa esercitazione, hai creato correttamente un flusso di dati per esportare i dati del profilo da Experience Platform al tuo [!DNL Merkury] posizione S3 gestita. Quindi, devi contattare il tuo [!DNL Merkury] rappresentante con il nome dell’account, i nomi dei file e il percorso del bucket, in modo da poter configurare l’elaborazione.