---
title: Panoramica dell’origine PubSub di Google
description: Scopri come collegare Google PubSub a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7c78173d-2639-47cb-8935-77fb7841a121
source-git-commit: c8fc447631f5382d49022b525a10edeadbd5ab46
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 0%

---

# [!DNL Google PubSub] sorgente

>[!IMPORTANT]
>
>Il [!DNL Google PubSub] è disponibile nel catalogo delle origini per gli utenti che hanno acquistato Real-time Customer Data Platform Ultimate.

Adobe Experience Platform fornisce connettività nativa per provider cloud come [!DNL AWS], [!DNL Google Cloud Platform], e [!DNL Azure], che consente di inserire in Platform i dati provenienti da questi sistemi per utilizzarli nei servizi e nelle destinazioni a valle.

Le origini di archiviazione cloud possono inserire i dati in Platform senza dover scaricare, formattare o caricare. I dati acquisiti possono essere formattati come XDM JSON, XDM Parquet o delimitati. Ogni fase del processo viene integrata nel flusso di lavoro delle origini. Platform consente di inserire dati da [!DNL Google PubSub] in tempo reale.

## Prerequisiti {#prerequisites}

Questa sezione descrive le impostazioni dei prerequisiti che è necessario completare prima di collegare il [!DNL Google PubSub] da Experience Platform.

### Crea account del servizio {#create-service-account}

A **account del servizio** è un tipo di account spesso utilizzato da un’applicazione o da un carico di lavoro di calcolo, anziché da una persona. Un account di servizio è identificato dal relativo indirizzo e-mail, che è univoco per l’account.

* Da un lato, gli account di servizio sono **entità** - è possibile concedere l&#39;accesso agli account del servizio a [!DNL Google Cloud] risorse. Ad esempio, puoi assegnare a un account di servizio il ruolo Amministratore di calcolo `(roles/compute.admin)` su un determinato progetto. Questo consente all’account del servizio di gestire le risorse del motore di calcolo in quel particolare progetto.
* D&#39;altra parte, gli account del servizio sono anche risorse: è possibile concedere ad altri utenti/gruppi/ruoli l&#39;autorizzazione per accedere all&#39;account del servizio. Ad esempio, puoi assegnare a un utente il ruolo Utente dell’account di servizio `(roles/iam.serviceAccountUser)` su un account di servizio per consentire all’utente di collegare tale account di servizio alle risorse. In alternativa, puoi assegnare a un utente il ruolo di amministratore dell’account di servizio `(roles/iam.serviceAccountAdmin)` per consentire all’utente di completare attività quali visualizzare, modificare, disabilitare ed eliminare l’account del servizio.

Per ulteriori informazioni su come determinare il tipo di autenticazione corretto per il caso d’uso, consulta [[!DNL Google] guida ai metodi di autenticazione](https://cloud.google.com/docs/authentication).

Per creare un account di servizio, attenersi alla procedura descritta di seguito.

Innanzitutto, passa a [!DNL IAM] pagina di [!DNL Google Developer Console] e quindi seleziona **[!DNL Create Service Account]**.

![Finestra Crea account del servizio in Google Developer Console](../../images/tutorials/create/google-pubsub/create-service-account.png)

Quindi, inserisci un nome visualizzato e un ID per l’account di servizio, quindi seleziona **[!DNL Create and Continue]**.

![Dettagli dell’account del servizio in Google Developer Console](../../images/tutorials/create/google-pubsub/service-account-details.png)

### Genera chiavi account del servizio {#generate-service-account-keys}

Per generare le chiavi per l&#39;account di servizio, selezionare l&#39;intestazione delle chiavi nella pagina Account di servizio. Da qui, seleziona **[!DNL Add key]** e quindi seleziona **[!DNL Create new key]** dal menu a discesa. Puoi anche utilizzare questo pannello per caricare una chiave esistente.

![Finestra Aggiungi chiave in Google Developer Console](../../images/tutorials/create/google-pubsub/add-key.png)

Se l&#39;operazione ha esito positivo, verrà visualizzato un messaggio che indica che la chiave privata è stata salvata nel computer e che verrà scaricato un file. È quindi possibile utilizzare il contenuto di questo file come credenziali durante la creazione di [!DNL Google PubSub] account su Experience Platform.

### Concedere le autorizzazioni a livello di argomento e di abbonamento {#grant-permissions}

Per concedere le autorizzazioni a livello di argomento e di sottoscrizione, passare alla pagina della console argomenti e quindi selezionare **[!DNL Show info panel]**. Avanti, sotto [!DNL Permissions] , seleziona [!DNL Add Principal] quindi aggiungere l&#39;entità account del servizio insieme alle autorizzazioni.

![Finestra popup in Google Developer Console in cui è possibile concedere autorizzazioni a livello di argomento e di abbonamento](../../images/tutorials/create/google-pubsub/add-principal.png)

## Configurazioni ottimali [!DNL Google PubSub usage] {#optimal-configurations}

Questa sezione descrive le configurazioni che si consiglia di effettuare per ottimizzare l’utilizzo del [!DNL Google PubSub] sorgente su Experience Platform.

### Proprietà abbonamento {#subscription-properties}

Utilizza il [!DNL Google Developer Console] a **aumentare la scadenza del riconoscimento**. Ciò consente [!DNL Google Publisher] per attendere in base al tempo configurato prima di inviare nuovamente il messaggio. Questo ritardo consente di ridurre il carico superfluo a livello di abbonato.

![Interfaccia della scadenza della conferma in Google Developer Console.](../../images/tutorials/create/google-pubsub/acknowledgement-deadline.png)

Abilita **[!DNL exactly one delivery]**. Questa configurazione informa [!DNL Google Publisher] per garantire che i messaggi inviati all’abbonamento non vengano inviati nuovamente prima della scadenza della conferma. È possibile utilizzare questa impostazione per assicurarsi che i messaggi di conferma non vengano inviati nuovamente all&#39;abbonamento.

![La pagina contenente esattamente una configurazione di consegna in Google Developer Console.](../../images/tutorials/create/google-pubsub/exactly-one-delivery.png)

È possibile abilitare **[!DNL Retry after exponential backoff delay]** per ridurre il rischio di sovraccaricare ulteriormente il server. Puoi abilitare questa configurazione in [!DNL Google Developer Console] per attenuare meglio gli errori temporanei (errori temporanei che in genere si risolvono da soli), concedendo al sistema più tempo per il ripristino prima di tentare un&#39;altra connessione.

![Finestra Criterio Riprova in Google Developer Console.](../../images/tutorials/create/google-pubsub/retry-policy.png)

Devi **imposta la durata di conservazione dei messaggi di abbonamento su 24 ore o più** per evitare che dati non riconosciuti vadano persi durante i picchi di carico. Inoltre, **abilita un argomento lettera non recapitata** per garantire che la perdita di dati non si verifichi anche durante rari casi edge.

>[!IMPORTANT]
>
>Puoi creare un solo flusso di dati di origine per [!DNL Google PubSub] abbonamento. Il riutilizzo di un abbonamento, anche tra sandbox diverse, comporta la perdita di dati.

## Connetti [!DNL Google PubSub] all&#39;Experience Platform

La documentazione seguente fornisce informazioni sulle modalità di connessione [!DNL Google PubSub] in Platform tramite API o l’interfaccia utente:

### Utilizzo delle API

* [Creare una connessione sorgente PubSub di Google utilizzando l’API del servizio Flusso](../../tutorials/api/create/cloud-storage/google-pubsub.md)
* [Raccogliere dati in streaming utilizzando l’API del servizio Flusso](../../tutorials/api/collect/streaming.md)

### Utilizzo dell’interfaccia utente

* [Creare una connessione sorgente PubSub di Google nell’interfaccia utente](../../tutorials/ui/create/cloud-storage/google-pubsub.md)
* [Configurare un flusso di dati per una connessione all’archiviazione cloud nell’interfaccia utente](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
