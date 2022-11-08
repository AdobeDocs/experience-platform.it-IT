---
title: Estensione di inoltro eventi Zendesk
description: Estensione di inoltro eventi Zendesk per Adobe Experience Platform.
exl-id: 22e94699-5b84-4a73-b007-557221d3e223
source-git-commit: a9887535b12b8c4aeb39bb5a6646da88db4f0308
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 6%

---

# [!DNL Zendesk] Panoramica dell’estensione API degli eventi

[Zendesk](https://www.zendesk.com) è una soluzione di assistenza clienti e uno strumento di vendita. Lo Zendesk [inoltro eventi](../../../ui/event-forwarding/overview.md) sfrutta [[!DNL Zendesk Events API]](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/) per inviare eventi da Adobe Experience Platform Edge Network a Zendesk per un’ulteriore elaborazione. Puoi utilizzare l’estensione per raccogliere le interazioni del profilo del cliente da utilizzare nell’analisi e nell’azione a valle.

Questo documento illustra come installare e configurare l&#39;estensione nell&#39;interfaccia utente di .

## Prerequisiti

Per utilizzare questa estensione è necessario disporre di un account Zendesk. È possibile registrarsi per un account Zendesk sul [Sito web Zendesk](https://www.zendesk.com/register/).

È inoltre necessario raccogliere i seguenti dettagli per la configurazione di Zendesk:

| Tipo di chiave | Descrizione | Esempio |
| --- | --- | --- |
| Subdomain | Durante il processo di registrazione, un **sottodominio** viene creato in modo specifico per l’account . Fai riferimento a [Documentazione di Zendesk](https://developer.zendesk.com/documentation/ticketing/working-with-oauth/creating-and-using-oauth-tokens-with-the-api/) per ulteriori informazioni. | `xxxxx.zendesk.com` (4) `xxxxx` è il valore fornito durante la creazione dell&#39;account) |
| Token API | Zendesk utilizza i token portatori come meccanismo di autenticazione per comunicare con l&#39;API Zendesk. Dopo aver effettuato l’accesso al portale Zendesk, genera un token API. Fai riferimento a [Documentazione di Zendesk](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token) per ulteriori informazioni. | `cwWyOtHAv12w4dhpiulfe9BdZFTz3OKaTSzn2QvV` |

{style=&quot;table-layout:auto&quot;}

Infine, devi creare un segreto di inoltro evento per il token API. Imposta il tipo di segreto su **[!UICONTROL Token]**, e imposta il valore sul token API che hai raccolto dalla configurazione di Zendesk. Consulta la documentazione su [segreti nell&#39;inoltro di eventi](../../../ui/event-forwarding/secrets.md) per ulteriori informazioni sulla configurazione dei segreti.

## Installare l’estensione {#install}

Per installare l’estensione Zendesk nell’interfaccia utente, passa a **Inoltro eventi** e seleziona una proprietà a cui aggiungere l&#39;estensione oppure crea una nuova proprietà.

Dopo aver selezionato o creato la proprietà desiderata, passa a **Estensioni** > **Catalogo**. Cerca &quot;[!DNL Zendesk]&quot;, quindi seleziona **[!DNL Install]** sull&#39;estensione Zendesk.

![Pulsante di installazione per l’estensione Zendesk selezionata nell’interfaccia utente](../../../images/extensions/zendesk/install.png)

## Configura l&#39;estensione {#configure}

>[!IMPORTANT]
>
>A seconda delle esigenze di implementazione, potrebbe essere necessario creare uno schema, elementi dati e un set di dati prima di configurare l’estensione. Controlla tutti i passaggi di configurazione prima di iniziare per determinare quali entità devi impostare per il tuo caso d’uso.

Seleziona **Estensioni** nella navigazione a sinistra. Sotto **Installato**, seleziona **Configura** sull&#39;estensione Zendesk.

![Pulsante Configura per l’estensione Zendesk selezionata nell’interfaccia utente](../../../images/extensions/zendesk/configure.png)

Sotto **[!UICONTROL Dominio Zendesk]**, immetti il valore del sottodominio Zendesk . Sotto **[!UICONTROL Token Zendesk]**, seleziona il segreto creato in precedenza che contiene il token API.

![Opzioni di configurazione inserite nell’interfaccia utente](../../../images/extensions/zendesk/input.png)

## Configurare una regola di inoltro eventi

Avvia la creazione di una nuova regola di inoltro eventi [regola](../../../ui/managing-resources/rules.md) e configurane le condizioni desiderate. Quando selezioni le azioni per la regola, seleziona la [!UICONTROL Zendesk] , quindi seleziona la [!UICONTROL Crea evento] tipo di azione.

![Definisci regola](../../../images/extensions/zendesk/rule.png)

Quando si imposta la configurazione dell&#39;azione, viene richiesto di assegnare elementi dati alle varie proprietà che verranno inviate a Zendesk.

![Definire la configurazione dell’azione](../../../images/extensions/zendesk/action-configurations.png)

Questi elementi dati devono essere mappati come riferimento di seguito.

### `event` chiavi

`event` è un oggetto JSON che rappresenta l’evento attivato dall’utente. Fai riferimento al documento Zendesk sul [anatomia di un evento](https://developer.zendesk.com/documentation/custom-data/events/anatomy-of-an-event/) per informazioni dettagliate sulle proprietà acquisite dalla `event` oggetto.

È possibile fare riferimento alle seguenti chiavi all&#39;interno del `event` oggetto durante la mappatura a elementi dati:

| `event` key | Tipo | Percorso piattaforma | Descrizione | Obbligatorio | Limiti |
| --- | --- | --- | --- | --- | --- |
| `source` | Stringa | `arc.event.xdm._extconndev.event_source` | L&#39;applicazione che ha inviato l&#39;evento. | Sì | Non utilizzare `Zendesk` come valore in quanto è un nome sorgente protetto per eventi standard Zendesk. I tentativi di utilizzarlo genereranno un errore.<br>La lunghezza del valore non deve superare i 40 caratteri. |
| `type` | Stringa | `arc.event.xdm._extconndev.event_type` | Un nome per il tipo di evento. È possibile utilizzare questo campo per indicare diversi tipi di eventi per una determinata origine. Ad esempio, puoi creare un set di eventi per gli accessi utente e un altro per i carrelli. | Sì | La lunghezza del valore non deve superare i 40 caratteri. |
| `description` | Stringa | `arc.event.xdm._extconndev.description` | Una descrizione dell’evento. | No | (N/D) |
| `created_at` | Stringa | `arc.event.xdm.timestamp` | Una marca temporale ISO-8601 che riflette l’ora in cui è stato creato l’evento. | No | (N/D) |
| `properties` | Oggetto | `arc.event.xdm._extconndev.EventProperties` | Un oggetto JSON personalizzato con dettagli sull’evento. | Sì | (N/D) |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Fai riferimento a [[!DNL Zendesk Events API] documentazione](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/) per ulteriori informazioni sulle proprietà dell’evento.

### `profile` chiavi

`profile` è un oggetto JSON che rappresenta l&#39;utente che ha attivato l&#39;evento. Fai riferimento al documento Zendesk sul [anatomia di un profilo](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/) per informazioni dettagliate sulle proprietà acquisite dalla `profile` oggetto.

È possibile fare riferimento alle seguenti chiavi all&#39;interno del `profile` oggetto durante la mappatura a elementi dati:

| `profile` key | Tipo | Percorso piattaforma | Descrizione | Obbligatorio | Limiti |
| --- | --- | --- | --- | --- | --- |
| `source` | Stringa | `arc.event.xdm._extconndev.profile_source` | Il prodotto o il servizio associato al profilo, ad esempio `Support`, `CompanyName`oppure `Chat`. | Sì | (N/D) |
| `type` | Stringa | `arc.event.xdm._extconndev.profile_type` | Un nome per il tipo di profilo. Puoi utilizzare questo campo per creare diversi tipi di profili per una determinata origine. Ad esempio, puoi creare un set di profili aziendali per i clienti e un altro per i dipendenti. | Sì | La lunghezza del tipo di profilo non deve superare i 40 caratteri. |
| `name` | Stringa | `arc.event.xdm._extconndev.name` | Nome della persona dal profilo | No | (N/D) |
| `user_id` | Stringa | `arc.event.xdm._extconndev.user_id` | L&#39;ID utente della persona a Zendesk. | No | (N/D) |
| `identifiers` | Array | `arc.event.xdm._extconndev.identifiers` | Matrice contenente almeno un identificatore. Ogni identificatore è costituito da un tipo e un valore. | Sì | Fai riferimento a [Documentazione di Zendesk](https://developer.zendesk.com/api-reference/custom-data/profiles_api/profiles_api/#identifiers-array) per ulteriori informazioni sul `identifiers` array. Tutti i campi e i valori devono essere univoci. |
| `attributes` | Oggetto | `arc.event.xdm._extconndev.attrbutes` | Un oggetto contenente proprietà definite dall&#39;utente sulla persona. | No | Fai riferimento a [Documentazione di Zendesk](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/#attributes) per ulteriori informazioni sugli attributi del profilo. |

{style=&quot;table-layout:auto&quot;}

## Convalidare i dati in Zendesk {#validate}

Se la raccolta di eventi e l’integrazione di Adobe Experience Platform hanno esito positivo, gli eventi all’interno della console Zendesk dovrebbero essere visualizzati come mostrato di seguito. Indica un&#39;integrazione riuscita.

Profili:

![Pagina Profili Zendesk](../../../images/extensions/zendesk/zendesk-profiles.png)

Eventi:

![Pagina Eventi Zendesk](../../../images/extensions/zendesk/zendesk-events.png)

## Limiti di richiesta {#limits}

In base al tipo di account, la Zendesk [!DNL Events API] può gestire il seguente numero di richieste al minuto:

| [!DNL Account Type] | Richieste al minuto |
| --- | --- |
| [!DNL Team] | 250 |
| [!DNL Growth] | 250 |
| [!DNL Professional] | 500 |
| [!DNL Enterprise] | 750 |
| [!DNL Enterprise Plus] | 1000 |

{style=&quot;table-layout:auto&quot;}

Fai riferimento a [Documentazione di Zendesk](https://developer.zendesk.com/api-reference/ticketing/account-configuration/usage_limits/#:~:text=API%20requests%20made%20by%20Zendesk%20apps%20are%20subject,sources%20for%20the%20account%2C%20including%20internal%20product%20requests.) per ulteriori informazioni su questi limiti.

## Errori e risoluzione dei problemi {#errors-and-troubleshooting}

Durante l&#39;utilizzo o la configurazione dell&#39;estensione, gli errori seguenti potrebbero essere restituiti dall&#39;API Zendesk Events:

| Codice di errore | Descrizione | Risoluzione | Esempio |
|---|---|---|---|
| 400 | **Lunghezza profilo non valida:** Questo errore si verifica quando la lunghezza di un attributo di profilo contiene più di 40 caratteri. | Limita la lunghezza dei dati dell’attributo del profilo a un massimo di 40 caratteri. | `{"error": [{"code":"InvalidProfileTypeLength","title": "Profile type length > 40 chars"}]}` |
| 401 | **Percorso non trovato:** Questo errore si verifica quando viene fornito un dominio non valido. | Verifica che sia fornito un dominio valido nel seguente formato: `{subdomain}.zendesk.com` | `{"error": [{"description": "No route found for host {subdomain}.zendesk.com","title": "RouteNotFound"}]}` |
| 401 | **Autenticazione non valida o mancante:** Questo errore si verifica quando l’accesso al token non è valido, mancante o scaduto. | Verifica che il token di accesso sia valido e non sia scaduto. | `{"error": [{"code":"MissingOrInvalidAuthentication","title": "Invalid or Missing Authentication"}]}` |
| 403 | **Autorizzazioni insufficienti:** Questo errore si verifica quando non vengono fornite autorizzazioni sufficienti per accedere alla risorsa. | Verifica che siano state fornite le autorizzazioni richieste. | `{"error": [{"code":"PermissionDenied","title": "Insufficient permisssions to perform operation"}]}` |
| 429 | **Troppe richieste:** Questo errore si verifica quando il limite di record dell&#39;oggetto endpoint è stato superato. | Fai riferimento alla sezione precedente su [limiti della richiesta](#limits) per informazioni dettagliate sulle soglie per limite. | `{"error": [{"code":"TooManyRequests","title": "Too Many Requests"}]}` |

{style=&quot;table-layout:auto&quot;}

## Passaggi successivi

Questo documento illustra come installare e configurare l&#39;estensione di inoltro eventi Zendesk nell&#39;interfaccia utente. Per ulteriori informazioni sulla raccolta dei dati dell&#39;evento a Zendesk, consulta la documentazione ufficiale:

* [Guida introduttiva agli eventi](https://developer.zendesk.com/documentation/custom-data/events/getting-started-with-events/)
* [API eventi Zendesk](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/)
* [Informazioni sull’API degli eventi](https://developer.zendesk.com/documentation/custom-data/events/about-the-events-api/)
* [Anatomia di un evento](https://developer.zendesk.com/documentation/custom-data/events/anatomy-of-an-event/)
* [API dei profili Zendesk](https://developer.zendesk.com/api-reference/custom-data/events-api/events-api/#profile-object)
* [Informazioni sull’API Profiles](https://developer.zendesk.com/documentation/custom-data/profiles/about-the-profiles-api/)
* [Anatomia di un profilo](https://developer.zendesk.com/documentation/custom-data/profiles/anatomy-of-a-profile/)
