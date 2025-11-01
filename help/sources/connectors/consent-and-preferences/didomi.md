---
title: Panoramica di Didomi Source
description: Scopri come collegare Didomi a Adobe Experience Platform utilizzando l’interfaccia utente.
last-substantial-update: 2025-07-29T00:00:00Z
badge: Beta
exl-id: c59bcfb8-e831-4a13-8b0e-4c6d538f1059
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 1%

---

# [!DNL Didomi]

>[!AVAILABILITY]
>
>L&#39;origine [!DNL Didomi] è in versione beta. Leggi i [termini e condizioni](../../home.md#terms-and-conditions) nella panoramica delle origini per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta.

[!DNL Didomi] è una piattaforma di gestione del consenso e delle preferenze che consente alle organizzazioni di raccogliere, gestire e applicare le scelte degli utenti in merito ai dati personali su siti Web, app e strumenti interni.

Adobe Experience Platform supporta l&#39;acquisizione di dati da un&#39;ampia gamma di sistemi esterni, inclusi l&#39;archiviazione cloud, i database e le applicazioni come [!DNL Didomi] tramite un sistema di connettori di origine. Utilizza le origini per autenticare i sistemi esterni, gestire il flusso di dati in Experience Platform e garantire l’acquisizione coerente e strutturata dei dati dei clienti.

Utilizza l&#39;origine [!DNL Didomi] per inviare in streaming i dati di consenso utente e preferenze in tempo reale dalla piattaforma di gestione delle preferenze e dei consensi di [!DNL Didomi] ad Experience Platform. Tramite l&#39;origine [!DNL Didomi], puoi centralizzare e agire sui dati del consenso in Experience Platform, mantenendo in tal modo i profili dei clienti e i flussi di lavoro a valle conformi e aggiornati.

![Architettura di elaborazione dati &quot;Didomi&quot;.](../../images/tutorials/create/didomi/flux.jpeg)

## Prerequisiti

Completa i passaggi preliminari descritti di seguito per connettere correttamente l&#39;account [!DNL Didomi] ad Experience Platform.

### Indirizzo IP inserisco nell&#39;elenco Consentiti

Prima di collegare le origini a Experience Platform, è necessario aggiungere al elenco Consentiti di indirizzi IP specifici per l’area geografica. Per ulteriori informazioni, leggere la guida in [inserire nell&#39;elenco Consentiti degli indirizzi IP per la connessione ad Experience Platform](../../ip-address-allow-list.md).

### Configurare le autorizzazioni su Experience Platform

Per connettere l&#39;account **[!UICONTROL View Sources]** ad Experience Platform, è necessario che per l&#39;account siano abilitate sia le autorizzazioni **[!UICONTROL Manage Sources]** che quelle [!DNL Didomi]. Contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie. Per ulteriori informazioni, leggere la [guida all&#39;interfaccia utente per il controllo degli accessi](../../../access-control/ui/overview.md).

### Raccogliere le credenziali API di Adobe

Per connettere in modo sicuro [!DNL Didomi] ad Experience Platform, è necessario eseguire l&#39;autenticazione utilizzando le credenziali API di Adobe. Queste credenziali sono essenziali per la configurazione del webhook e per l’acquisizione dei dati.

Per informazioni su come effettuare correttamente chiamate alle API di Experience Platform, leggi la guida [guida introduttiva alle API di Experience Platform](../../../landing/api-authentication.md).

### Creare uno schema Experience Platform

>[!TIP]
>
>Puoi saltare questo passaggio se disponi già di uno schema XDM.

Uno schema **Experience Data Model (XDM)** definisce la struttura dei dati che invierai da [!DNL Didomi] (ad esempio, ID utente, scopo del consenso) ad Experience Platform.

Per creare uno schema, seleziona [!UICONTROL Schemas] nell&#39;area di navigazione a sinistra dell&#39;interfaccia utente di Experience Platform, quindi seleziona **[!UICONTROL Create schema]**. Selezionare **[!UICONTROL Standard]** come tipo di schema, quindi **[!UICONTROL Manual]** per creare manualmente i campi. Seleziona una classe base per lo schema e fornisci un nome per lo schema.

Dopo la creazione, aggiorna lo schema aggiungendo uno dei campi obbligatori. Assicurati che almeno un campo sia un campo [!UICONTROL Identity] per informare Experience Platform dei valori di identità primari. Infine, assicurati di abilitare l&#39;interruttore [!UICONTROL Profile] per memorizzare correttamente i dati.

![create-schema](../../images/tutorials/create/didomi/create-schema.png)

Per ulteriori informazioni, consulta la guida su [creazione di schemi nell&#39;interfaccia utente](../../../xdm/tutorials/create-schema-ui.md).

### Creare un set di dati

>[!TIP]
>
>Puoi saltare questo passaggio se disponi già di un set di dati.

Un **set di dati** in Experience Platform viene utilizzato per memorizzare i dati in arrivo in base allo schema definito.

Per creare un set di dati, seleziona [!UICONTROL Datasets] nella navigazione a sinistra dell&#39;interfaccia utente di Experience Platform, quindi seleziona **[!UICONTROL Create dataset]**. Quindi, seleziona **[!UICONTROL Create dataset from schema]** e quindi lo schema da associare al nuovo set di dati.

![create-dataset](../../images/tutorials/create/didomi/create-dataset.png)

## Configurare il webhook HTTP nella console [!DNL Didomi]

[!DNL Webhooks] ti consente di abbonarti agli eventi attivati sulla piattaforma [!DNL Didomi] quando gli utenti interagiscono con le loro preferenze di consenso. Quando si verifica un evento rilevante, ad esempio quando un utente concede o revoca il consenso, [!DNL Didomi] invia una richiesta HTTP POST in tempo reale contenente un payload JSON all&#39;endpoint [!DNL webhook] configurato.

![console-didomi](../../images/tutorials/create/didomi/didomi-console.png)

Per garantire la compatibilità con Experience Platform, il webhook deve soddisfare i seguenti requisiti.

| Campo | Descrizione | Esempio |
| --- | --- | --- | 
| Segreto client | La chiave segreta associata alle credenziali API di Adobe. | `d8f3b2e1-4c9a-4a7f-9b2e-8f1c3d2a1b6e` |
| Chiave API | Chiave API pubblica utilizzata per autenticare le richieste ai servizi Adobe. |  |
| Tipo di concessione | Metodo tramite il quale un&#39;applicazione ottiene un token di accesso dal server autorizzazioni. Imposta questo valore su `client_credentials`. | `client_credentials` |
| Portata | Gli ambiti di autorizzazione definiscono le autorizzazioni o i livelli di accesso specifici richiesti da un’applicazione al provider API. | `openid,AdobeID,read_organizations,additional_info.projectedProductContext,session` |
| Intestazione di autenticazione | Le intestazioni aggiuntive necessarie per la richiesta del token Adobe. | `{"Content-type": "application/x-www-form-urlencoded"}` |
| URL token | Endpoint token Adobe. | `https://ims-na1.adobelogin.com/ims/token/v3` |
| URL dell’endpoint | URL finale del connettore Adobe (fornito alla fine della configurazione). | `https://dcs.adobedc.net/collection/your-adobe-endpoint-id` |

{style="table-layout:auto"}

Quindi, configurare le seguenti opzioni per [!DNL webhook].

| Campo | Descrizione | Valore |
| ---| --- | --- | 
| Intestazioni richiesta | Intestazioni personalizzate per [!DNL webhook]. Assicurarsi di includere `x-adobe-flow-id`. Puoi recuperare questo valore dopo la creazione del [flusso di dati](../../tutorials/ui/create/consent-and-preferences/didomi.md#retrieve-the-streaming-endpoint-url). | `{"Content-Type": "application/json", "Cache-Control": "no-cache", "x-adobe-flow-id": "{DATAFLOW_ID}"}` |
| Appiattisci | Questa proprietà deve essere selezionata in quanto garantisce che i dati [!DNL webhook] vengano inviati come oggetto flat. | Abilitata |
| Tipi di evento | Selezionare il gruppo specifico di [!DNL Didomi] eventi (`event.*` o `user.*`) che deve attivare [!DNL webhook]. Utilizza `event.*` per tenere traccia delle modifiche di consenso o preferenze e `user.*` per tenere traccia degli aggiornamenti del profilo utente. Questa selezione è necessaria per garantire che solo gli eventi compatibili vengano inviati ad Adobe. Adobe supporta un solo schema per flusso di dati, pertanto la selezione di entrambi i tipi di evento può causare errori di acquisizione. | L’elenco dei tipi di evento supportati è: <ul><li>`Event.created`</li><li>`Event.updated`</li><li>`Event.deleted`</li><li>`User.created`</li><li>`User.updated`</li><li>`User.deleted`</li></ul> |

### Scarica il file di payload di esempio {#download-the-sample-payload-file}

In base al gruppo di eventi selezionato, scarica il **file di payload di esempio** appropriato direttamente dalla console [!DNL Didomi]. Questo file rappresenta la struttura dei dati e verrà utilizzato durante i passaggi di schema e mappatura in Adobe.

| **Gruppo di eventi** | **File di esempio da scaricare** | **Opzione filtro** |
| --- | ---| --- |
| `event.*` | Scarica un esempio per `event.created` | Filtra solo per `event.*` eventi |
| `user.*` | Scarica un esempio per `user.created` | Filtra solo per `user.*` eventi |

## Connetti il tuo account [!DNL Didomi] ad Experience Platform

Leggi la guida su [connessione [!DNL Didomi] ad Experience Platform](../../tutorials/ui/create/consent-and-preferences/didomi.md) per scoprire come creare una connessione di origine e acquisire i dati di consenso e preferenze da [!DNL Didomi] in Experience Platform.
