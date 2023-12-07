---
title: Estensione di inoltro eventi Zendesk
description: Estensione di inoltro eventi Zendesk per Adobe Experience Platform.
exl-id: 22e94699-5b84-4a73-b007-557221d3e223
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 4%

---

# [!DNL Zendesk] Panoramica dell’estensione API Events

[Zendesk](https://www.zendesk.com) è una soluzione di assistenza clienti e uno strumento di vendita. Lo Zendesk [inoltro eventi](../../../ui/event-forwarding/overview.md) l&#39;estensione sfrutta [[!DNL Zendesk Events API]](https://developer.zendesk.com/documentation/ticketing/events/about-the-events-api/) per inviare eventi da Adobe Experience Platform Edge Network a Zendesk per ulteriore elaborazione. Puoi utilizzare l’estensione per raccogliere le interazioni del profilo cliente da utilizzare nell’analisi e nell’azione a valle.

Questo documento illustra come installare e configurare l’estensione nell’interfaccia utente di.

## Prerequisiti

Per utilizzare questa estensione è necessario disporre di un account Zendesk. Puoi registrarti per un account Zendesk sul sito [Sito Web Zendesk](https://www.zendesk.com/register/).

È inoltre necessario raccogliere i seguenti dettagli per la configurazione Zendesk:

| Tipo di chiave | Descrizione | Esempio |
| --- | --- | --- |
| Subdomain | Durante il processo di registrazione, viene **sottodominio** viene creato in modo specifico per l’account. Consulta la sezione [Documentazione di Zendesk](https://developer.zendesk.com/documentation/ticketing/working-with-oauth/creating-and-using-oauth-tokens-with-the-api/) per ulteriori informazioni. | `xxxxx.zendesk.com` (dove `xxxxx` è il valore fornito durante la creazione dell’account) |
| Token API | Zendesk utilizza token bearer come meccanismo di autenticazione per comunicare con l’API di Zendesk. Dopo aver effettuato l’accesso al portale Zendesk, genera un token API. Consulta la sezione [Documentazione di Zendesk](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token) per ulteriori informazioni. | `cwWyOtHAv12w4dhpiulfe9BdZFTz3OKaTSzn2QvV` |

{style="table-layout:auto"}

Infine, devi creare un segreto per l’inoltro degli eventi per il token API. Imposta il tipo di segreto su **[!UICONTROL Token]**, e imposta il valore sul token API raccolto dalla configurazione Zendesk. Consulta la documentazione su [segreti nell’inoltro degli eventi](../../../ui/event-forwarding/secrets.md) per ulteriori dettagli sulla configurazione dei segreti.

## Installare l’estensione {#install}

Per installare l’estensione Zendesk nell’interfaccia utente, passa a **Inoltro eventi** e seleziona una proprietà a cui aggiungere l’estensione oppure crea una nuova proprietà.

Dopo aver selezionato o creato la proprietà desiderata, passa a **Estensioni** > **Catalogo**. Cerca &quot;[!DNL Zendesk]&quot;, quindi seleziona **[!DNL Install]** sull&#39;estensione Zendesk.

![Pulsante di installazione per l’estensione Zendesk selezionata nell’interfaccia utente](../../../images/extensions/server/zendesk/install.png)

## Configurare l&#39;estensione {#configure}

>[!IMPORTANT]
>
>A seconda delle esigenze di implementazione, potrebbe essere necessario creare uno schema, elementi di dati e un set di dati prima di configurare l’estensione. Prima di iniziare, controlla tutti i passaggi di configurazione per determinare quali entità devi impostare per il tuo caso d’uso.

Seleziona **Estensioni** nel menu di navigazione a sinistra. Sotto **Installato**, seleziona **Configura** sull&#39;estensione Zendesk.

![Pulsante Configura per l’estensione Zendesk selezionata nell’interfaccia utente](../../../images/extensions/server/zendesk/configure.png)

Sotto **[!UICONTROL Dominio Zendesk]**, immetti il valore per il sottodominio Zendesk. Sotto **[!UICONTROL Token Zendesk]**, seleziona il segreto creato in precedenza che contiene il token API.

![Opzioni di configurazione compilate nell’interfaccia utente](../../../images/extensions/server/zendesk/input.png)

## Configurare una regola di inoltro degli eventi

Inizia a creare una nuova regola di inoltro degli eventi [regola](../../../ui/managing-resources/rules.md) e configurarne le condizioni come desiderato. Quando selezioni le azioni per la regola, seleziona la [!UICONTROL Zendesk] , quindi seleziona la [!UICONTROL Crea evento] tipo di azione.

![Definisci regola](../../../images/extensions/server/zendesk/rule.png)

Quando si imposta la configurazione dell’azione, viene richiesto di assegnare elementi dati alle varie proprietà che verranno inviate a Zendesk.

![Definisci configurazione azione](../../../images/extensions/server/zendesk/action-configurations.png)

Questi elementi dati devono essere mappati come indicato di seguito.

### `event` tasti

`event` è un oggetto JSON che rappresenta l’evento attivato dall’utente. Consulta il documento Zendesk sulla [anatomia di un evento](https://developer.zendesk.com/documentation/ticketing/events/anatomy-of-an-event/) per informazioni dettagliate sulle proprietà acquisite da `event` oggetto.

È possibile fare riferimento alle seguenti chiavi all&#39;interno di `event` oggetto durante il mapping agli elementi dati:

| `event` chiave | Tipo | Percorso piattaforma | Descrizione | Obbligatorio | Limiti |
| --- | --- | --- | --- | --- | --- |
| `source` | Stringa | `arc.event.xdm._extconndev.event_source` | Applicazione che ha inviato l&#39;evento. | Sì | Non usi `Zendesk` come valore, in quanto è un nome di origine protetto per gli eventi standard di Zendesk. I tentativi di utilizzarlo genereranno un errore.<br>La lunghezza del valore non deve superare i 40 caratteri. |
| `type` | Stringa | `arc.event.xdm._extconndev.event_type` | Nome per il tipo di evento. È possibile utilizzare questo campo per indicare diversi tipi di eventi per una determinata origine. Ad esempio, puoi creare un set di eventi per gli accessi degli utenti e un altro per i carrelli acquisti. | Sì | La lunghezza del valore non deve superare i 40 caratteri. |
| `description` | Stringa | `arc.event.xdm._extconndev.description` | Descrizione dell&#39;evento. | No | (N/D) |
| `created_at` | Stringa | `arc.event.xdm.timestamp` | Una marca temporale ISO-8601 che riflette l’ora di creazione dell’evento. | No | (N/D) |
| `properties` | Oggetto | `arc.event.xdm._extconndev.EventProperties` | Oggetto JSON personalizzato con dettagli sull’evento. | Sì | (N/D) |

{style="table-layout:auto"}

>[!NOTE]
>
>Consulta la sezione [[!DNL Zendesk Events API] documentazione](https://developer.zendesk.com/documentation/ticketing/events/about-the-events-api/) per ulteriori informazioni sulle proprietà dell’evento.

### `profile` tasti

`profile` è un oggetto JSON che rappresenta l’utente che ha attivato l’evento. Consulta il documento Zendesk sulla [anatomia di un profilo](https://developer.zendesk.com/documentation/ticketing/profiles/anatomy-of-a-profile/) per informazioni dettagliate sulle proprietà acquisite da `profile` oggetto.

È possibile fare riferimento alle seguenti chiavi all&#39;interno di `profile` oggetto durante il mapping agli elementi dati:

| `profile` chiave | Tipo | Percorso piattaforma | Descrizione | Obbligatorio | Limiti |
| --- | --- | --- | --- | --- | --- |
| `source` | Stringa | `arc.event.xdm._extconndev.profile_source` | Il prodotto o servizio associato al profilo, ad esempio `Support`, `CompanyName`, o `Chat`. | Sì | (N/D) |
| `type` | Stringa | `arc.event.xdm._extconndev.profile_type` | Nome per il tipo di profilo. Puoi utilizzare questo campo per creare diversi tipi di profili per una determinata origine. Ad esempio, puoi creare un set di profili aziendali per i clienti e un altro per i dipendenti. | Sì | La lunghezza del tipo di profilo non deve superare i 40 caratteri. |
| `name` | Stringa | `arc.event.xdm._extconndev.name` | Nome della persona dal profilo | No | (N/D) |
| `user_id` | Stringa | `arc.event.xdm._extconndev.user_id` | ID utente della persona in Zendesk. | No | (N/D) |
| `identifiers` | Array | `arc.event.xdm._extconndev.identifiers` | Matrice contenente almeno un identificatore. Ogni identificatore è costituito da un tipo e da un valore. | Sì | Consulta la sezione [Documentazione di Zendesk](https://developer.zendesk.com/api-reference/ticketing/users/profiles_api/profiles_api/#identifiers-array) per ulteriori informazioni su `identifiers` array. Tutti i campi e i valori devono essere univoci. |
| `attributes` | Oggetto | `arc.event.xdm._extconndev.attrbutes` | Oggetto contenente le proprietà definite dall’utente sulla persona. | No | Consulta la sezione [Documentazione di Zendesk](https://developer.zendesk.com/documentation/ticketing/profiles/anatomy-of-a-profile/#attributes) per ulteriori informazioni sugli attributi del profilo. |

{style="table-layout:auto"}

## Convalidare i dati in Zendesk {#validate}

Se la raccolta di eventi e l’integrazione di Adobe Experience Platform hanno esito positivo, gli eventi all’interno della console Zendesk dovrebbero apparire come mostrato di seguito. Ciò indica un’integrazione riuscita.

Profili:

![Pagina Profili Zendesk](../../../images/extensions/server/zendesk/zendesk-profiles.png)

Eventi:

![Pagina Eventi Zendesk](../../../images/extensions/server/zendesk/zendesk-events.png)

## Limiti di richieste {#limits}

In base al tipo di account, Zendesk [!DNL Events API] è in grado di gestire il seguente numero di richieste al minuto:

| [!DNL Account Type] | Richieste al minuto |
| --- | --- |
| [!DNL Team] | 250 |
| [!DNL Growth] | 250 |
| [!DNL Professional] | 500 |
| [!DNL Enterprise] | 750 |
| [!DNL Enterprise Plus] | 1000 |

{style="table-layout:auto"}

Consulta la sezione [Documentazione di Zendesk](https://developer.zendesk.com/api-reference/ticketing/account-configuration/usage_limits/#:~:text=API%20requests%20made%20by%20Zendesk%20apps%20are%20subject,sources%20for%20the%20account%2C%20including%20internal%20product%20requests.) per ulteriori informazioni su questi limiti.

## Errori e risoluzione problemi {#errors-and-troubleshooting}

Durante l’utilizzo o la configurazione dell’estensione, l’API degli eventi Zendesk potrebbe restituire gli errori seguenti:

| Codice di errore | Descrizione | Risoluzione | Esempio |
|---|---|---|---|
| 400 | **Lunghezza profilo non valida:** Questo errore si verifica quando la lunghezza di un attributo di profilo supera i 40 caratteri. | Limita la lunghezza dei dati dell’attributo del profilo a un massimo di 40 caratteri. | `{"error": [{"code":"InvalidProfileTypeLength","title": "Profile type length > 40 chars"}]}` |
| 401 | **Route non trovata:** Questo errore si verifica quando viene fornito un dominio non valido. | Verifica che sia fornito un dominio valido nel seguente formato: `{subdomain}.zendesk.com` | `{"error": [{"description": "No route found for host {subdomain}.zendesk.com","title": "RouteNotFound"}]}` |
| 401 | **Autenticazione non valida o mancante:** Questo errore si verifica quando l’accesso al token non è valido, è mancante o è scaduto. | Verifica che il token di accesso sia valido e non sia scaduto. | `{"error": [{"code":"MissingOrInvalidAuthentication","title": "Invalid or Missing Authentication"}]}` |
| 403 | **Autorizzazioni insufficienti:** Questo errore si verifica quando non vengono fornite autorizzazioni sufficienti per accedere alla risorsa. | Verifica che siano state fornite le autorizzazioni necessarie. | `{"error": [{"code":"PermissionDenied","title": "Insufficient permisssions to perform operation"}]}` |
| 429 | **Troppe richieste:** Questo errore si verifica quando viene superato il limite di record dell’oggetto endpoint. | Consulta la sezione precedente su [limiti di richiesta](#limits) per informazioni dettagliate sulle soglie per limite. | `{"error": [{"code":"TooManyRequests","title": "Too Many Requests"}]}` |

{style="table-layout:auto"}

## Passaggi successivi

Questo documento illustra come installare e configurare l’estensione di inoltro degli eventi Zendesk nell’interfaccia utente. Per ulteriori informazioni sulla raccolta dei dati sull’evento in Zendesk, consulta la documentazione ufficiale:

* [Guida introduttiva agli eventi](https://developer.zendesk.com/documentation/ticketing/events/getting-started-with-events/)
* [API per eventi Zendesk](https://developer.zendesk.com/api-reference/ticketing/users/events-api/events-api/)
* [Informazioni sull’API degli eventi](https://developer.zendesk.com/documentation/ticketing/events/about-the-events-api/)
* [Anatomia di un evento](https://developer.zendesk.com/documentation/ticketing/events/anatomy-of-an-event/)
* [API dei profili Zendesk](https://developer.zendesk.com/api-reference/ticketing/users/events-api/events-api/#profile-object)
* [Informazioni sull’API Profiles](https://developer.zendesk.com/documentation/ticketing/profiles/about-the-profiles-api/)
* [Anatomia di un profilo](https://developer.zendesk.com/documentation/ticketing/profiles/anatomy-of-a-profile/)
