---
title: Acquisire dati crittografati nel Workspace dell’interfaccia utente Sources
description: Scopri come acquisire i dati crittografati nell’area di lavoro dell’interfaccia utente delle origini.
badge: Beta
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1457'
ht-degree: 6%

---

# Acquisire dati crittografati nell’interfaccia utente delle origini

>[!AVAILABILITY]
>
>Il supporto per l’acquisizione di dati crittografati nell’interfaccia utente delle sorgenti è in versione beta. La funzione e la documentazione sono soggette a modifiche.

È possibile inserire file e cartelle di dati crittografati in Adobe Experience Platform utilizzando cloud origini batch di archiviazione. Con l&#39;assimilazione di dati crittografati, è possibile sfruttare meccanismi di crittografia asimmetrica per trasferire in modo sicuro dati batch in Experience Platform. I meccanismi di crittografia asimmetrica supportati sono PGP e GPG.

Leggi questa guida per scoprire come inserire dati crittografati con origini batch di archiviazione cloud utilizzando interfaccia.

## Introduzione

Prima di continuare con questo esercitazione, leggere i seguenti documenti per comprendere meglio le seguenti Experience Platform caratteristiche e concetti.

* [Origini](../../home.md): utilizza le origini in Experience Platform per acquisire dati da un&#39;applicazione Adobe o da un&#39;origine dati di terze parti.
* [Flussi dati](../../../dataflows/home.md): i flussi dati sono rappresentazioni dei processi di dati che spostano i dati in Experience Platform. Puoi usare l&#39;area di lavoro Origini per creare flussi di dati che inseriscono dati da una determinata origine a Experience Platform.
* [Sandbox](../../../sandboxes/home.md): utilizza le sandbox in Experience Platform per creare partizioni virtuali tra le tue istanze Experience Platform e creare ambienti dedicati allo sviluppo o alla produzione.

### Schema di alto livello

* Crea una coppia di chiavi di crittografia utilizzando l&#39;area di lavoro Origini nel interfaccia Experience Platform.
   * Facoltativamente, puoi anche creare una coppia di chiavi di verifica dei segni personalizzata per fornire un ulteriore livello di sicurezza ai dati crittografati.
* Utilizza la chiave pubblica della coppia di chiavi di crittografia per crittografare i dati.
* Inserisci i dati crittografati nell’archiviazione cloud. Durante questo passaggio, devi anche assicurarti di disporre di un file di esempio dei tuoi dati nell’archiviazione cloud che possa essere utilizzato come riferimento per mappare i dati di origine su uno schema Experience Data Model (XDM).
* Utilizza l’origine del batch di archiviazione cloud e inizia il processo di acquisizione dei dati nell’area di lavoro origini nell’interfaccia utente di Experience Platform.
* Durante il processo di creazione della connessione di origine, fornisci l’ID della chiave che corrisponde alla chiave pubblica utilizzata per crittografare i dati.
   * Se è stato utilizzato anche il meccanismo della coppia di chiavi di verifica del segno, è necessario fornire anche l&#39;ID della chiave di verifica del segno corrispondente ai dati crittografati.
* Procedi ai passaggi di creazione del flusso di dati.

## Creare una coppia di chiavi di crittografia {#create-an-encryption-key-pair}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="ID chiave di crittografia"
>abstract="Fornisci l’ID chiave di crittografia corrispondente alla chiave di crittografia utilizzata per crittografare i dati di origine."

>[!BEGINSHADEBOX]

**Che cos&#39;è una coppia di chiavi di crittografia?**

Una coppia di chiavi di crittografia è un meccanismo di crittografia asimmetrica costituito da una chiave pubblica e una chiave privata. La chiave pubblica viene utilizzata per crittografare i dati e la chiave privata viene quindi utilizzata per decrittografare tali dati.

È possibile creare la coppia di chiavi di crittografia tramite il interfaccia Experience Platform. Una volta generato, riceverai una chiave pubblica e un ID chiave corrispondente. Utilizzare la chiave pubblica per crittografare i dati e quindi utilizzare l&#39;ID chiave per confermare l&#39;identità, quando si è in procinto di inserire i dati crittografati. La chiave privata va automaticamente a Experience Platform, dove viene archiviata in un vault sicuro, e verrà utilizzata solo quando i dati sono pronti per la decrittografia.

>[!ENDSHADEBOX]

Nella interfaccia Experience Platform, passare all&#39;area di lavoro origini e quindi selezionare [!UICONTROL Coppie di] chiavi dall&#39;intestazione superiore.

![Catalogo delle origini con l&#39;intestazione &quot;Coppie di chiavi&quot; selezionata.](../../images/tutorials/edi/catalog.png)

Viene visualizzata una pagina in cui sono elencate le coppie di chiavi di crittografia esistenti nell&#39;organizzazione. Questa pagina fornisce informazioni su titolo, ID, tipo, algoritmo di crittografia, scadenza e stato di una determinata chiave. Per creare una nuova coppia di chiavi, selezionate **[!UICONTROL Crea chiave]**.

![La pagina Coppie di chiavi, con &quot;chiave di crittografia&quot; selezionata come tipo di chiave e &quot;Crea chiave&quot; pulsante selezionata.](../../images/tutorials/edi/encryption_key_page.png)

Successivo, scegli il tipo di chiave che vuoi impostare. Per creare una chiave di crittografia, selezionare **[!UICONTROL Chiave di crittografia, quindi Continua**&#x200B;**.]**

![Finestra di creazione della chiave, con la chiave di crittografia selezionata.](../../images/tutorials/edi/choose_encryption_key_type.png)

Fornisci un titolo e una passphrase per la chiave di crittografia. La passphrase rappresenta un ulteriore livello di protezione per le chiavi di crittografia. Al momento della creazione, Experience Platform memorizza la passphrase in un archivio protetto diverso dalla chiave pubblica. Specificare una stringa non vuota come passphrase. Al termine, selezionare **[!UICONTROL Crea]**.

![Finestra di creazione della chiave di crittografia, in cui sono specificati un titolo e una passphrase.](../../images/tutorials/edi/create_encryption_key.png)

In caso di esito positivo, viene visualizzata una nuova finestra in cui viene visualizzata la nuova chiave di crittografia, con titolo, chiave pubblica e ID della chiave. Usa il valore della chiave pubblica per crittografare i tuoi dati. In un passaggio successivo, utilizzerai l’ID chiave per dimostrare la tua identità al momento dell’acquisizione dei dati crittografati durante il processo di creazione del flusso di dati.

![Finestra in cui vengono visualizzate le informazioni sulla coppia di chiavi di crittografia appena creata.](../../images/tutorials/edi/encryption_key_details.png)

Per visualizzare le informazioni su una chiave di crittografia esistente, selezionare i puntini di sospensione (`...`) accanto al titolo della chiave. Seleziona **[!UICONTROL Dettagli chiave]** per visualizzare la chiave pubblica e l&#39;ID chiave. In alternativa, per eliminare la chiave di crittografia, selezionare **[!UICONTROL Elimina]**.

![Pagina delle coppie di chiavi, in cui viene visualizzato un elenco di chiavi di crittografia. I puntini di sospensione accanto a &quot;acme-encryption-key&quot; sono selezionati e il menu a discesa mostra le opzioni per visualizzare i dettagli della chiave o eliminare le chiavi.](../../images/tutorials/edi/configuration_options.png)

### Creare una chiave di verifica della firma {#create-a-sign-verification-key}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="ID chiave di verifica firma"
>abstract="Fornisci l’ID della chiave di verifica della firma che corrisponde ai dati di origine crittografati e firmati."

>[!BEGINSHADEBOX]

**Cos&#39;è una chiave di verifica del segno?**

Una chiave di verifica del segno è un altro meccanismo di crittografia che coinvolge una chiave privata e una chiave pubblica. In questo caso, puoi creare la coppia di chiavi di verifica della firma e utilizzare la chiave privata per firmare e fornire un ulteriore livello di crittografia ai dati. Quindi condividerai la chiave pubblica corrispondente con Experience Platform. Durante l’acquisizione, Experience Platform utilizzerà la chiave pubblica per verificare la firma associata alla chiave privata.

>[!ENDSHADEBOX]

Per creare una chiave di verifica della firma, selezionare **[!UICONTROL Firma chiave di verifica]** nella finestra di selezione del tipo di chiave, quindi selezionare **[!UICONTROL Continua]**.

![Finestra di selezione del tipo di chiave in cui è selezionata la chiave di verifica della firma.](../../images/tutorials/edi/choose_sign_verification_key_type.png)

Quindi, fornisci un titolo e una chiave PGP con codifica [!DNL Base64] come chiave pubblica, quindi seleziona **[!UICONTROL Crea]**.

![Finestra Crea chiave di verifica della firma.](../../images/tutorials/edi/create_sign_verification_key.png)

In caso di esito positivo, viene visualizzata una nuova finestra in cui è visualizzata la nuova chiave di verifica del segno, inclusi il titolo e l&#39;ID della chiave.

![Dettagli della chiave di verifica della firma appena creata.](../../images/tutorials/edi/sign_verification_key_details.png)

## Acquisire dati crittografati {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="Il file è crittografato?"
>abstract="Seleziona questo pulsante di attivazione/disattivazione se acquisisci un file già crittografato."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="Selezionare file di esempio"
>abstract="Per creare una mappatura, è necessario acquisire un file di esempio durante l’acquisizione di dati crittografati."

È possibile inserire dati crittografati utilizzando le seguenti origini batch di archiviazione cloud:

* [[!DNL Amazon S3]](../ui/create/cloud-storage/s3.md)
* [[!DNL Azure Blob]](../ui/create/cloud-storage/blob.md)
* [[!DNL Azure Data Lake Storage Gen2]](../ui/create/cloud-storage/adls-gen2.md)
* [[!DNL Azure File Storage]](../ui/create/cloud-storage/azure-file-storage.md)
* [[!DNL Data Landing Zone]](../ui/create/cloud-storage/data-landing-zone.md)
* [[!DNL FTP]](../ui/create/cloud-storage/ftp.md)
* [[!DNL Google Cloud Storage]](../ui/create/cloud-storage/google-cloud-storage.md)
* [[!DNL HDFS]](../ui/create/cloud-storage/hdfs.md)
* [[!DNL Oracle Object Storage]](../ui/create/cloud-storage/oracle-object-storage.md)
* [[!DNL SFTP]](../ui/create/cloud-storage/sftp.md)

Esegui l&#39;autenticazione con l&#39;cloud l&#39;origine di archiviazione scelta. Durante il passaggio di selezione dei dati del workflow, selezionare il file crittografato o la cartella che si desidera ingerire e quindi attivare l&#39;interruttore **[!UICONTROL È il file crittografato]** .

![Il passaggio &quot;seleziona i dati&quot; delle origini workflow, in cui viene selezionato un file di dati crittografati per l&#39;acquisizione.](../../images/tutorials/edi/select_data.png)

Quindi, seleziona un file di esempio dai dati di origine. Poiché i dati sono crittografati, Experience Platform richiederà un file di esempio per creare uno schema XDM da mappare ai dati di origine.

![L&#39;opzione &quot;Questo file è criptato?&quot; attivato e pulsante selezionato &quot;Seleziona file di esempio&quot;. ](../../images/tutorials/edi/select_sample_file.png)

Dopo aver selezionato il file di esempio, configurare le impostazioni dei dati, ad esempio il formato di dati corrispondente, il delimitatore e il tipo di compressione. Attendere un certo tempo per il rendering completo dell&#39;interfaccia di anteprima, quindi selezionare **[!UICONTROL Salva]**.

![Viene selezionato un campione per l&#39;inserimento e l&#39;anteprima del file viene caricata completamente.](../../images/tutorials/edi/file_preview.png)

Da qui, utilizza il menu a discesa per selezionare il titolo della chiave pubblica dell’ID della chiave pubblica che corrisponde alla chiave pubblica utilizzata per crittografare i dati.

![Titolo della chiave pubblica dell&#39;ID della chiave pubblica che corrisponde alla chiave pubblica utilizzata per crittografare i dati.](../../images/tutorials/edi/public_key_id.png)

Se hai utilizzato anche la coppia di chiavi di verifica della firma per fornire un ulteriore livello di crittografia, quindi abilita l’interruttore della chiave di verifica della firma e in modo simile, utilizza il menu a discesa per selezionare l’ID della chiave di verifica della firma che corrisponde alla chiave utilizzata per crittografare i dati.

![Titolo della chiave di verifica della firma dell&#39;ID della chiave che corrisponde alla crittografia di verifica della firma.](../../images/tutorials/edi/custom_key_id.png)

Al termine, seleziona **[!UICONTROL Avanti]**.

Completa i passaggi rimanenti nel flusso di lavoro sorgenti per completare la creazione del flusso di dati.

* [Fornisci i dettagli del flusso di dati e del set di dati](../ui/dataflow/batch/cloud-storage.md#provide-dataflow-details)
* [Mappare i dati di origine su uno schema XDM](../ui/dataflow/batch/cloud-storage.md#map-data-fields-to-an-xdm-schema)
* [Configurare una pianificazione di acquisizione per il flusso di dati](../ui/dataflow/batch/cloud-storage.md#schedule-ingestion-runs)
* [Verifica il flusso di dati](../ui/dataflow/batch/cloud-storage.md#review-your-dataflow)

Puoi continuare a [apportare aggiornamenti al flusso di dati](../ui/update-dataflows.md) una volta creato correttamente.

## Passaggi successivi

Leggendo questo documento, è ora possibile inserire dati crittografati dall&#39;origine batch di archiviazione cloud a Experience Platform. Per informazioni su come inserire dati crittografati utilizzando le API, leggi la guida sull&#39;inserimento [di dati crittografati tramite l&#39;API](../api/encrypt-data.md) [!DNL Flow Service] . Per informazioni generali sulle fonti su Experience Platform, leggi la panoramica[&#128279;](../../home.md) delle fonti.
