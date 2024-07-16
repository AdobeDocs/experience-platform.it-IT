---
title: Panoramica origine RainFocus
description: Scopri come portare i dati di analisi e gestione degli eventi dall’account RainFocus all’Experience Platform
last-substantial-update: 2023-06-21T00:00:00Z
badge: Beta
exl-id: 88e333e3-2b93-4d66-8412-efadea58ac46
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 4%

---

# [!DNL RainFocus]

>[!NOTE]
>
>L&#39;origine [!DNL RainFocus] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, leggere la [panoramica delle origini](../../home.md#terms-and-conditions).

[!DNL RainFocus] è una piattaforma che puoi utilizzare per promuovere i tuoi eventi e creare il tuo pubblico. È possibile utilizzare [!DNL RainFocus] per creare belle pagine promozionali, tenere traccia delle prestazioni delle campagne e ottimizzare le conversioni delle registrazioni.

Utilizza l&#39;origine [!DNL RainFocus] in Adobe Experience Platform e Real-time Customer Data Platform per arricchire automaticamente i profili di dati dei clienti con eventi di esperienza dei partecipanti in tempo reale. Una volta abilitati, gli eventi di esperienza vengono automaticamente inviati in streaming a Real-Time CDP, consentendo una potente segmentazione del pubblico, l’analisi dei dati e l’attivazione del percorso di partecipanti con destinazioni e applicazioni a valle come Customer Journey Analytics e Adobe Journey Optimizer.

>[!IMPORTANT]
>
>Il connettore di origine e la pagina della documentazione vengono creati e gestiti dal team [!DNL RainFocus]. Per eventuali richieste di informazioni o richieste di aggiornamento, contattali direttamente all&#39;indirizzo clientcare<span>@rainfocus.com o visita il [[!DNL RainFocus] Centro assistenza](https://help.rainfocus.com/hc/en-us)

## Prerequisiti

Prima di attivare l&#39;integrazione di [!DNL RainFocus] su Experience Platform, è necessario completare i seguenti prerequisiti:

[Creare un account di servizio Adobe (JWT) nel portale Adobe Developer](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)

>[!IMPORTANT]
>
>Adobe ha recentemente annunciato la rimozione dei token JWT a favore di OAuth. Per adattarsi a questa modifica, l&#39;origine [!DNL RainFocus] eseguirà la migrazione a OAuth nel prossimo futuro.

### Raccogli le credenziali richieste

Per connettere [!DNL RainFocus] a Experience Platform, è necessario fornire i valori per le seguenti proprietà di connessione in [!DNL RainFocus]:

| Credenziali | Descrizione | Esempio |
| --- | --- | --- |
| ID client | L’ID client può essere ottenuto dall’account del servizio Adobe nel portale Adobe Developer. | `b9c32a63e7d41a0f87d3e8b52a16e7a2` |
| Segreto client | Il segreto client può essere ottenuto dall’account del servizio Adobe nel portale Adobe Developer. | `k1b-p-umplcjtg_arnw-R-Bx44bybu` |
| ID account tecnico | L’ID dell’account tecnico può essere ottenuto dall’account del servizio Adobe nel portale Adobe Developer. | `B3F9D2E8A64C573D21ABFE97@techacct.adobe.com` |
| ID organizzazione | L’ID organizzazione può essere ottenuto dall’account del servizio Adobe nel portale Adobe Developer | `D9A6F3BCE82FD147C50E3A19@techacct.adobe.com` |

### Creare uno schema XDM e definire il campo di identità {#create-an-xdm-schema-and-define-the-identity-field}

Per memorizzare gli eventi esperienza da [!DNL RainFocus] in Experience Platform, è necessario creare uno schema Experience Data Model (XDM) per descrivere un set di dati in cui sono memorizzati i possibili campi e tipi di dati che verranno inviati da [!DNL RainFocus].

[!DNL RainFocus] consiglia i campi seguenti, che coprono tutti i possibili dati inviati per impostazione predefinita.

Sono inoltre consigliati i seguenti gruppi di campi (indicati da un prefisso):

* Partecipante
* Espositore
* Lead
* Session
* SessionTime

**Lo schema deve contenere i campi seguenti:**

| Campo | Tipo | Esempio | Descrizione |
| --- | --- | --- | --- |
| `attendee.registered` | Stringa | Sì | Flag che determina se il partecipante è considerato registrato. |
| `attendee.attendeeId` | Stringa | 1619119968857001fvLB | ID partecipante in [!DNL RainFocus]. |
| `attendee.externalId` | Stringa | 1666809456617001viaPj | L’ID esterno specificato da un’organizzazione. |
| `attendee.clientId` | Stringa | 8EFC1F57631CAFE70A495ECB@8f3f1f5c631caf3e495fd8.e | ID client SSO partecipante. |
| `attendee.email` | Stringa | utente<span>@company.com | L’indirizzo e-mail del partecipante. |
| `transmissionId` | Stringa | 1680309557133001YHZ | Identificatore univoco utilizzato per il push dei dati. |
| `eventType` | Stringa | SessionScheduled | Nome dell&#39;evento esperienza partecipante. |
| `timestamp` | Data e ora | 01.00:41:57.000Z | La marca temporale del push dati. |
| `event.name` | Stringa | Adobe Summit 2023 | Il nome dell’evento in cui si è verificata una trasmissione. |
| `exhibitor.exhibitorId` | Stringa | 1680309557133001YHZ | L&#39;identificatore [!DNL RainFocus] dell&#39;espositore. |
| `exhibitor.externalId` | Stringa | 1666809514105001lSJN | L’identificatore dell’espositore nel sistema client. |
| `exhibitor.name` | Stringa | IBM | Il nome dell’espositore. |
| `lead.leadId` | Stringa | 1666809456617001viaPj | Identificatore [!DNL RainFocus] per il lead. |
| `lead.note` | Stringa | | |
| `session.sessionId` | Stringa | 1666809373585001t4aV | Identificatore [!DNL RainFocus] per la sessione. |
| `session.externalId` | Stringa | 1666809456617001viaPj | Identificatore della sessione nel sistema client. |
| `session.code` | Stringa | GS3 | Il codice per la sessione. |
| `session.title` | Stringa | Keynote su ispirazione | Titolo della sessione. |
| `session.length` | Intero | 90 | La durata della sessione. |
| `sessiontime.sessiontimeId` | Stringa | 1673033149739001OJLZ | L&#39;identificatore [!DNL RainFocus] per l&#39;ora della sessione. |
| `sessiontime.startTime` | Stringa | 2023-03-22 10:00:00 | Ora di inizio della sessione. |
| `sessiontime.endTime` | Stringa | 2023-03-22 10:00:00 | Ora di fine della sessione. |
| `sessiontime.room` | Stringa | B32 | Stanza utilizzata per la sessione. |

{style="table-layout:auto"}

Per creare lo schema per i dati [!DNL RainFocus], leggere la documentazione seguente per i passaggi su come creare uno schema utilizzando le API o l&#39;interfaccia utente.

* [Creare lo schema tramite l’interfaccia utente](../../../xdm/tutorials/create-schema-ui.md)
* [Creare lo schema utilizzando l’API](../../../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>* Lo schema deve estendere la classe ExperienceEvent **XDM.**
>* Assicurati che lo schema includa una **identità primaria** ed sia **abilitato per il profilo**. Per ulteriori informazioni, consulta la guida su [definizione dei campi di identità nell&#39;interfaccia utente](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)
>* Puoi sostituire l’identità di esempio (e-mail) con un altro identificatore appropriato, ad esempio un messaggio e-mail sha256 o un ECID.

### Creare un profilo di integrazione in RainFocus {#create-an-integration-profile-in-rainfocus}

Quando l&#39;account del servizio e lo schema XDM sono pronti, è ora possibile attivare [!DNL Integration Profile] tramite la piattaforma [!DNL RainFocus]. [!DNL Integration Profile] è responsabile dello streaming dei dati su Experience Platform.

Accedi alla [[!DNL RainFocus] piattaforma](https://app.rainfocus.com). Nella navigazione principale, selezionare **[!DNL Libraries]**, quindi selezionare **[!DNL Integration Profiles]**

![Interfaccia utente RainFocus con librerie e profili di integrazione selezionati.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile.png)

Per creare un nuovo profilo, selezionare l&#39;icona **(`+`)**. Selezionare **Adobe Real-time Customer Data Platform**, quindi **OK**.

![Finestra Crea profilo di integrazione nell&#39;interfaccia utente di RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-select.png)

Quindi, fornisci le credenziali recuperate nel progetto Adobe Developer Portal:

* **ID client**
* **Segreto client**
* **ID account tecnico**
* **ID organizzazione**

Dopo aver fornito le credenziali, selezionare **[!DNL Save]**. Il nuovo [!DNL Integration Profile] dovrebbe essere elencato nel dashboard [!DNL RainFocus].

Seleziona [!DNL Integration Profile] appena creato per visualizzare un elenco di **tipi push** predefiniti già configurati. Questi sono i [Eventi esperienza](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html) che verranno inviati all&#39;Experience Platform quando si verificano.

![Elenco dei tipi di push predefiniti nel dashboard RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-setup.png)

Per recuperare una copia del payload JSON di esempio, selezionare **[!DNL Sample JSON Payload]**. Quindi, evidenzia e copia il payload JSON di esempio e **salvalo in un nuovo file con estensione .json**. Verrà utilizzato in seguito in Experience Platform per [configurazioni di mappatura](../../tutorials/ui/create/analytics/rainfocus.md#mapping).

![Un payload JSON di esempio nel dashboard RainFocus.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-json.png)

>[!TIP]
>
>**Installazione non ancora completata**: una volta creato il flusso di dati, sarà necessario tornare alla dashboard [!DNL RainFocus] per completare [!DNL Integration Profile] fornendo il **URL endpoint di streaming** e il **ID flusso di dati**.

## Passaggi successivi

Dopo aver letto questo documento, hai completato la configurazione dei prerequisiti necessaria per inviare dati dall&#39;account [!DNL RainFocus] all&#39;Experience Platform. Ora puoi passare alla guida in [connessione [!DNL RainFocus] all&#39;Experience Platform utilizzando l&#39;interfaccia utente](../../tutorials/ui/create/analytics/rainfocus.md).
