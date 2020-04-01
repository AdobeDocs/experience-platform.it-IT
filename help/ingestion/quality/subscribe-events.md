---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Iscrizione agli eventi di assimilazione dei dati
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# Notifiche di assimilazione dei dati

Il processo di assimilazione dei dati in Adobe Experience Platform consiste di più passaggi. Una volta identificati i file di dati che devono essere trasferiti in Piattaforma, il processo di assimilazione inizia e ogni passaggio avviene consecutivamente fino a quando i dati non vengono correttamente assimilati o non hanno esito negativo. Il processo di assimilazione può essere avviato tramite l’API [di inserimento dati di](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) Adobe Experience Platform o tramite l’interfaccia utente di Experience Platform.

I dati caricati nella piattaforma devono passare attraverso più passaggi per raggiungere la destinazione, il Data Lake o l&#39;archivio dati del profilo cliente in tempo reale. Ogni passaggio prevede l&#39;elaborazione dei dati, la convalida dei dati e la memorizzazione dei dati prima di passare al passaggio successivo. A seconda della quantità di dati che vengono acquisiti, questo può diventare un processo che richiede molto tempo ed è sempre possibile che il processo non riesca a causa di errori di convalida, semantica o elaborazione. In caso di errore, i problemi relativi ai dati devono essere risolti e l&#39;intero processo di assimilazione deve essere riavviato utilizzando i file di dati corretti.

Per facilitare il monitoraggio del processo di assimilazione, Experience Platform consente di iscriversi a una serie di eventi pubblicati in ogni fase del processo, notificandovi lo stato dei dati acquisiti e ogni possibile errore.

## Eventi di notifica dello stato disponibili

Di seguito è riportato un elenco delle notifiche di stato relative all’inserimento dei dati disponibili a cui puoi iscriverti.

>[!NOTE] È disponibile un solo argomento evento per tutte le notifiche di assimilazione dei dati. Per distinguere tra stati diversi, è possibile utilizzare il codice evento.

| Servizio piattaforma | Stato | Descrizione evento | Codice evento |
| ---------------- | ------ | ----------------- | ---------- |
| Destinazione dati | success | Ingestione - Batch completato | ing_load_success |
| Destinazione dati | fallimento | Ingestione - Batch non riuscito | ing_load_failure |
| Profilo cliente in tempo reale | success | Servizio profilo - Batch di caricamento dati completato | ps_load_success |
| Profilo cliente in tempo reale | fallimento | Servizio profilo: batch di caricamento dati non riuscito | ps_load_failure |
| Grafico identità | success | Grafico identità: batch di caricamento dati completato | ig_load_success |
| Grafico identità | fallimento | Grafico identità: batch di caricamento dati non riuscito | ig_load_failure |

## Schema payload di notifica

Lo schema dell&#39;evento di notifica dell&#39;assimilazione dei dati è uno schema del modello dati esperienza (XDM) che contiene campi e valori che forniscono dettagli sullo stato dei dati che si stanno ingerendo. Visitate il repo pubblico XDM GitHub per visualizzare lo schema [di payload di](https://github.com/adobe/xdm/blob/master/schemas/common/notifications/ingestion.schema.json)notifica più recente.

## Iscriviti alle notifiche di stato di inserimento dati

Attraverso gli eventi di I/O [Adobe](https://www.adobe.io/apis/experienceplatform/events.html), potete abbonarvi a più tipi di notifiche mediante i webhooks. Per ulteriori informazioni sui webhooks e su come iscriversi agli eventi di I/O Adobe mediante i webhooks, consultare l&#39; [introduzione alla guida agli](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) eventi di I/O di Adobe.

### Creazione di una nuova integrazione tramite la console di I/O di Adobe

Effettuate l&#39;accesso ad [Adobe I/O Console](https://console.adobe.io/home) e fate clic sulla scheda *Integrazioni* oppure fate clic su **Crea integrazione** in Avvio rapido. Quando viene visualizzata la schermata *Integrazione* , fate clic su **Nuova integrazione** per creare una nuova integrazione.

![Crea nuova integrazione](../images/quality/subscribe-events/create_integration_start.png)

Viene visualizzata la schermata *Crea nuova integrazione* . Selezionate **Ricevi eventi** in tempo quasi reale, quindi fate clic su **Continua**.

![Ricevere eventi in tempo reale](../images/quality/subscribe-events/create_integration_receive_events.png)

Nella schermata successiva sono disponibili opzioni per creare integrazioni con eventi, prodotti e servizi diversi disponibili per l&#39;organizzazione in base a iscrizioni, adesioni e autorizzazioni. Per questa integrazione, seleziona Notifiche **sulla** piattaforma in Experience Platform (Piattaforma esperienza), quindi fai clic su **Continue (Continua)**.

![Selezione del provider di eventi](../images/quality/subscribe-events/create_integration_select_provider.png)

Viene visualizzato il modulo Dettagli ** integrazione, che richiede di fornire un nome e una descrizione per l&#39;integrazione, nonché un certificato di chiave pubblica.

Se non disponete di un certificato pubblico, potete generarne uno nel terminale utilizzando il seguente comando:

```shell
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub
```

Dopo aver generato un certificato, trascinate e rilasciate il file nella casella Certificati **di chiavi** pubbliche oppure fate clic su **Seleziona un file** per esplorare la directory del file e selezionare il certificato direttamente.

Dopo aver aggiunto il certificato, viene visualizzata l&#39;opzione Registrazione ** evento. Fate clic su **Aggiungi registrazione** evento.

![dettagli di integrazione](../images/quality/subscribe-events/create_integration_details.png)

La finestra di dialogo dei dettagli *di registrazione all’* evento si espande per visualizzare ulteriori controlli. Qui potete selezionare i tipi di evento desiderati e registrare il webhook. Immettete un nome per la registrazione dell’evento, l’URL del webhook *(facoltativo)* e una breve descrizione. Infine, selezionate i tipi di evento a cui desiderate iscrivervi (notifica di inserimento dati), quindi fate clic su **Salva**.

![Selezione degli eventi](../images/quality/subscribe-events/create_integration_select_event.png)

## Passaggi successivi

Una volta creata l&#39;integrazione I/O, puoi visualizzare tutte le notifiche ricevute per tale integrazione. Per istruzioni dettagliate su come tenere traccia degli eventi, consultate la guida [Tracing Adobe I/O Events](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) .
