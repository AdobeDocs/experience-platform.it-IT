---
keywords: Experience Platform;home;intelligent services;popular topics
solution: Experience Platform
title: Preparare i dati per l'utilizzo in Intelligent Services
topic: Intelligent Services
translation-type: tm+mt
source-git-commit: 03135f564bd72fb60e41b02557cb9ca9ec11e6e8

---


# Preparare i dati per l&#39;utilizzo in Intelligent Services

Per consentire ai servizi intelligenti di scoprire informazioni ricavate dai dati degli eventi di marketing, i dati devono essere arricchiti e mantenuti in modo semantico in una struttura standard. I servizi intelligenti sfruttano gli schemi XDM (Experience Data Model) per ottenere questo risultato. Nello specifico, tutti i set di dati utilizzati in Intelligent Services devono essere conformi allo schema XDM **Consumer ExperienceEvent (CEE)** .

Questo documento fornisce linee guida generali sulla mappatura dei dati degli eventi di marketing da più canali a questo schema, delineando le informazioni sui campi importanti all&#39;interno dello schema per consentire di determinare in modo efficace come mappare i dati alla relativa struttura.

## Informazioni sullo schema CEE

Lo schema Consumer ExperienceEvent descrive il comportamento di un individuo in quanto si riferisce a eventi di marketing digitale (Web o mobile) nonché alle attività commerciali online o offline. L&#39;utilizzo di questo schema è richiesto per i servizi intelligenti a causa dei relativi campi (colonne) semanticamente ben definiti, evitando nomi sconosciuti che altrimenti renderebbero i dati meno chiari.

Come tutti gli schemi XDM, il mixin CEE è estensibile. In altre parole, è possibile aggiungere altri campi al mixin CEE, e se necessario è possibile includere diverse varianti in più schemi.

Un esempio completo del mixin può essere trovato nel repository [XDM](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)pubblico e dovrebbe essere utilizzato come riferimento per i campi chiave descritti nella sezione seguente.

### Campi chiave

La tabella seguente evidenzia i campi chiave all&#39;interno del mixin CEE che dovrebbero essere utilizzati per consentire ai servizi intelligenti di generare informazioni utili, tra cui descrizioni e collegamenti alla documentazione di riferimento per ulteriori esempi.

| Campo XDM | Descrizione | Riferimenti |
| --- | --- | --- |
| `xdm:channel` | Canale di marketing correlato a ExperienceEvent. Il campo include informazioni sul tipo di canale, il tipo di supporto e il tipo di posizione. **Questo campo _deve_essere fornito per consentire l&#39;utilizzo dei dati** da parte di AI di attribuzione. Per alcuni esempi di mappature, vedere la [tabella seguente](#example-channels) . | [Schema canale esperienza](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) |
| `xdm:productListItems` | Un array di elementi che rappresentano i prodotti selezionati da un cliente, inclusi SKU di prodotto, nome, prezzo e quantità. | [Schema dettagli Commerce](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) |
| `xdm:commerce` | Contiene informazioni commerciali sull’ExperienceEvent, compreso il numero dell’ordine di acquisto e le informazioni di pagamento. | [Schema dettagli Commerce](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) |
| `xdm:web` | Rappresenta i dettagli Web relativi all’evento ExperienceEvent, ad esempio l’interazione, i dettagli della pagina e il referente. | [Schema dei dettagli Web ExperienceEvent](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) |

### Canali di esempio {#example-channels}

Il `xdm:channel` campo rappresenta il canale di marketing relativo a ExperienceEvent. Nella tabella seguente sono riportati alcuni esempi di canali di marketing mappati su XDM:

| Canale | `channel.mediaType` | `channel._type` | `channel.mediaAction` |
| --- | --- | --- | --- |
| Ricerca a pagamento | PAGATO | CERCA | FATE CLIC |
| Social - Marketing | EARNED | SOCIAL | FATE CLIC |
| Visualizzazione | PAGATO | DISPLAY | FATE CLIC |
| E-mail | PAGATO | E-MAIL | FATE CLIC |
| Referente interno | PROPRIETARIO | DIRECT | FATE CLIC |
| VisualizzazioneTramite | PAGATO | DISPLAY | IMPRESSIONE |
| Reindirizzamento del codice QR | PROPRIETARIO | DIRECT | FATE CLIC |
| SMS Text Message | PROPRIETARIO | SMS | FATE CLIC |
| Dispositivi mobili | PROPRIETARIO | MOBILE | FATE CLIC |

## Mapping e acquisizione dei dati

Una volta determinato se i dati degli eventi di marketing possono essere mappati allo schema CEE, è possibile avviare il processo di inserimento dei dati in Servizi intelligenti. Contattate i servizi di consulenza Adobe per facilitare la mappatura dei dati sullo schema e l&#39;inserimento nel servizio.

Se disponete di un’iscrizione Adobe Experience Platform e desiderate mappare e assimilare i dati voi stessi, seguite i passaggi descritti nella sezione seguente.

### Utilizzo di Adobe Experience Platform

>[!NOTE] I passaggi seguenti richiedono un’iscrizione a Experience Platform. Se non disponete dell&#39;accesso alla piattaforma, passate alla sezione dei passaggi [](#next-steps) successivi.

In questa sezione viene illustrato il flusso di lavoro per la mappatura e l’assimilazione dei dati in Experience Platform per l’utilizzo in Intelligent Services, compresi i collegamenti alle esercitazioni per passaggi dettagliati.

#### Creare uno schema e un dataset CEE

Quando si è pronti per iniziare a preparare i dati per l&#39;assimilazione, il primo passo consiste nel creare un nuovo schema XDM che utilizzi il mixin CEE. Le seguenti esercitazioni forniscono informazioni dettagliate sul processo di creazione di un nuovo schema nell&#39;interfaccia utente o nell&#39;API:

* [Creare uno schema nell&#39;interfaccia utente](../xdm/tutorials/create-schema-ui.md)
* [Creare uno schema nell&#39;API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT] Le esercitazioni riportate sopra seguono un flusso di lavoro generico per la creazione di uno schema. Quando si sceglie una classe per lo schema, è necessario utilizzare la classe **ExperienceEvent** XDM. Una volta scelta questa classe, è possibile aggiungere il mixin CEE allo schema.

Dopo aver aggiunto il mixin CEE allo schema, è possibile aggiungere altri mixin come richiesto per campi aggiuntivi all&#39;interno dei dati.

Dopo aver creato e salvato lo schema, è possibile creare un nuovo dataset basato su tale schema. Le seguenti esercitazioni forniscono informazioni dettagliate sul processo di creazione di un nuovo set di dati nell&#39;interfaccia utente o nell&#39;API:

* [Creare un set di dati nell’interfaccia](../catalog/datasets/user-guide.md#create) (seguire il flusso di lavoro per utilizzare uno schema esistente)
* [Creare un set di dati nell&#39;API](../catalog/datasets/create.md)

#### Mappa e acquisizione dei dati

Dopo aver creato uno schema CEE e un set di dati, è possibile iniziare a mappare le tabelle di dati sullo schema e a assimilare i dati in Platform. Per informazioni su come eseguire questa operazione nell’interfaccia utente, consultate l’esercitazione sulla [mappatura di un file CSV su uno schema](../ingestion/tutorials/map-a-csv-file.md) XDM. Una volta compilato il set di dati, lo stesso set di dati può essere utilizzato per acquisire file di dati aggiuntivi.

## Passaggi successivi {#next-steps}

Questo documento fornisce indicazioni generali sulla preparazione dei dati per l&#39;utilizzo in Intelligent Services. Se avete bisogno di consulenza aggiuntiva in base al caso d&#39;uso, contattate l&#39;Assistenza Consultiva Adobe.

Dopo aver compilato con successo un dataset con i dati sull&#39;esperienza cliente, puoi utilizzare i servizi intelligenti per generare informazioni approfondite. Per iniziare, consulta i seguenti documenti:

* [Panoramica di AI per attribuzione](./attribution-ai/overview.md)
* [Panoramica dell&#39;AI del cliente](./customer-ai/overview.md)
