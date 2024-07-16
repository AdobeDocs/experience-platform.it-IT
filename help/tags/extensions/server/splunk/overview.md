---
title: Panoramica dell’estensione Splunk
description: Scopri l’estensione Splunk per l’inoltro di eventi in Adobe Experience Platform.
exl-id: 653b5897-493b-44f2-aeea-be492da2b108
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 1%

---

# Panoramica dell’estensione Splunk

[Splunk](https://www.splunk.com) è una piattaforma di osservabilità che fornisce ricerche, analisi e visualizzazioni per approfondimenti fruibili sui tuoi dati. L&#39;estensione Splunk [inoltro eventi](../../../ui/event-forwarding/overview.md) sfrutta l&#39;API REST [Agente di raccolta eventi HTTP Splunk](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/HECRESTendpoints) per inviare eventi dall&#39;Edge Network Adobe Experience Platform all&#39;Agente di raccolta eventi HTTP [Splunk](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector).

Splunk utilizza token bearer come meccanismo di autenticazione per comunicare con l’API Splunk Event Collector.

## Casi d’uso {#use-cases}

I team di marketing possono utilizzare l’estensione per i seguenti casi d’uso:

| Caso d’uso | Descrizione |
| --- | --- |
| Analisi del comportamento dei clienti | Le organizzazioni possono acquisire i dati degli eventi di interazione con il cliente dal proprio sito web e inoltrare gli eventi rilevanti a Splunk. I team di marketing e analisi possono quindi eseguire analisi successive all’interno della piattaforma Splunk per comprendere le interazioni e il comportamento chiave degli utenti. La piattaforma Splunk può essere utilizzata per generare grafici, dashboard o altre visualizzazioni per informare le parti interessate. |
| Ricerca scalabile su set di dati di grandi dimensioni | Le organizzazioni possono acquisire input transazionali o conversazionali come dati evento dal sito web e inoltrare gli eventi a Splunk. I team di Analytics possono quindi sfruttare le funzionalità di indicizzazione scalabile di Splunk per filtrare ed elaborare set di dati di grandi dimensioni per ricavare informazioni aziendali e prendere decisioni informate. |

{style="table-layout:auto"}

## Prerequisiti {#prerequisites}

Per utilizzare questa estensione è necessario disporre di un account Splunk. È possibile registrarsi per un account Splunk nella [home page Splunk](https://www.splunk.com/page/sign_up).

>[!NOTE]
>
> L’estensione Splunk supporta sia le istanze Enterprise di Splunk Cloud che di Splunk. Questa guida documenta un&#39;implementazione utilizzando [Splunk Cloud](https://www.splunk.com/en_us/products/splunk-cloud-platform.html) come riferimento. Il processo di configurazione per [Splunk Enterprise](https://www.splunk.com/en_us/products/splunk-enterprise.html) è simile, ma richiede istruzioni specifiche da parte dell&#39;amministratore di Splunk Enterprise.

Per configurare l&#39;estensione è necessario disporre anche dei seguenti valori tecnici:

* Token [Raccolta eventi](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector#Create_an_Event_Collector_token_on_Splunk_Cloud_Platform). I token sono in genere in formato UUIDv4 come segue: `12345678-1234-1234-1234-1234567890AB`.
* L’indirizzo e la porta dell’istanza della piattaforma Splunk per la tua organizzazione. L&#39;indirizzo e la porta di un&#39;istanza della piattaforma avranno in genere il seguente formato: `mysplunkserver.example.com:443`.
  >[!IMPORTANT]
  >
  > Gli endpoint Splunk a cui si fa riferimento nell&#39;inoltro degli eventi devono utilizzare solo la porta `443`. Le porte non standard non sono attualmente supportate nelle implementazioni di inoltro degli eventi.

## Installare l’estensione Splunk {#install}

Per installare l&#39;estensione Splunk Event Collector nell&#39;interfaccia utente, passare a **Inoltro eventi** e selezionare una proprietà a cui aggiungere l&#39;estensione oppure creare una nuova proprietà.

Dopo aver selezionato o creato la proprietà desiderata, passa a **Estensioni** > **Catalogo**. Cercare &quot;[!DNL Splunk]&quot;, quindi selezionare **[!DNL Install]** nell&#39;estensione Splunk.

![Pulsante Installa per l&#39;estensione Splunk selezionata nell&#39;interfaccia utente](../../../images/extensions/server/splunk/install.png)

## Configurare l’estensione Splunk {#configure_extension}

>[!IMPORTANT]
>
>A seconda delle esigenze di implementazione, potrebbe essere necessario creare uno schema, elementi di dati e un set di dati prima di configurare l’estensione. Prima di iniziare, controlla tutti i passaggi di configurazione per determinare quali entità devi impostare per il tuo caso d’uso.

Seleziona **Estensioni** nel menu di navigazione a sinistra. In **Installed**, selezionare **Configure** nell&#39;estensione Splunk.

![Pulsante Configura per l&#39;estensione Splunk selezionata nell&#39;interfaccia utente](../../../images/extensions/server/splunk/configure.png)

Per **[!UICONTROL URL agente di raccolta eventi HTTP]**, immettere l&#39;indirizzo e la porta dell&#39;istanza della piattaforma Splunk. In **[!UICONTROL Token di accesso]**, immetti il valore [!DNL Event Collector Token]. Al termine, selezionare **[!UICONTROL Salva]**.

![Opzioni di configurazione compilate nell&#39;interfaccia utente](../../../images/extensions/server/splunk/input.png)

## Configurare una regola di inoltro degli eventi {#config_rule}

Inizia a creare una nuova regola di inoltro eventi [regola](../../../ui/managing-resources/rules.md) e configurane le condizioni come desiderato. Quando selezioni le azioni per la regola, seleziona l&#39;estensione [!UICONTROL Splunk], quindi seleziona il tipo di azione [!UICONTROL Crea evento]. Vengono visualizzati controlli aggiuntivi per configurare ulteriormente l&#39;evento Splunk.

![Definisci configurazione azione](../../../images/extensions/server/splunk/action-configurations.png)

Il passaggio successivo consiste nel mappare le proprietà dell’evento Splunk agli elementi dati creati in precedenza. Di seguito sono riportate le mappature opzionali supportate basate sui dati dell’evento di input che è possibile impostare. Per ulteriori dettagli, consulta la [documentazione Splunk](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/FormateventsforHTTPEventCollector#Event_metadata).

| Nome campo | Descrizione |
| --- | --- |
| [!UICONTROL Evento ]<br><br>**(OBBLIGATORIO)** | Indica come desideri fornire i dati dell’evento. I dati dell&#39;evento possono essere assegnati alla chiave `event` all&#39;interno dell&#39;oggetto JSON nella richiesta HTTP oppure possono essere testo non elaborato. La chiave `event` si trova allo stesso livello delle chiavi di metadati all&#39;interno del pacchetto eventi JSON. All&#39;interno delle parentesi graffe chiave-valore `event`, i dati possono trovarsi in qualsiasi formato richiesto, ad esempio una stringa, un numero, un altro oggetto JSON e così via. |
| [!UICONTROL Host] | Il nome host del client da cui stai inviando i dati. |
| [!UICONTROL Tipo Source] | Tipo di origine da assegnare ai dati dell&#39;evento. |
| [!UICONTROL Source] | Valore di origine da assegnare ai dati dell’evento. Ad esempio, se invii dati da un’app che stai sviluppando, imposta questa chiave sul nome dell’app. |
| [!UICONTROL Indice] | Nome dell&#39;indice dei dati dell&#39;evento. Se per il token è impostato il parametro indexes, l’indice specificato deve trovarsi all’interno dell’elenco degli indici consentiti. |
| [!UICONTROL Tempo] | Ora dell’evento. Il formato di ora predefinito è l&#39;ora UNIX (nel formato `<sec>.<ms>`) e dipende dal fuso orario locale. Ad esempio, `1433188255.500` indica 1433188255 secondi e 500 millisecondi dopo l&#39;epoca oppure lunedì 1 giugno 2015 alle 19:15 GMT.:50: |
| [!UICONTROL Campi] | Specifica un oggetto JSON non elaborato o un set di coppie chiave-valore contenenti campi personalizzati espliciti da definire al momento dell’indice.  La chiave `fields` non è applicabile ai dati non elaborati.<br><br>Le richieste contenenti la proprietà `fields` devono essere inviate all&#39;endpoint `/collector/event`, altrimenti non verranno indicizzate. Per ulteriori informazioni, consulta la documentazione di Splunk su [estrazioni di campi indicizzati](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/IFXandHEC). |

### Convalidare i dati in Splunk {#validate}

Dopo aver creato ed eseguito la regola di inoltro degli eventi, verifica se l’evento inviato all’API Splunk viene visualizzato come previsto nell’interfaccia utente di Splunk. Se la raccolta di eventi e l’integrazione di Experienci Platform hanno avuto esito positivo, nella console Splunk verranno visualizzati gli eventi seguenti:

![Dati evento visualizzati nell&#39;interfaccia utente Splunk durante la convalida](../../../images/extensions/server/splunk/splunk-data.png)

## Passaggi successivi

Questo documento illustra come installare e configurare l’estensione di inoltro degli eventi Splunk nell’interfaccia utente. Per ulteriori informazioni sulla raccolta dei dati evento in Splunk, consulta la documentazione ufficiale:

* [Configurare e utilizzare il servizio Raccolta eventi HTTP nel Web Splunk](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector)
* [Configura autenticazione con token](https://docs.splunk.com/Documentation/Splunk/8.2.5/Security/Setupauthenticationwithtokens#Prerequisites_for_activating_tokens)
* [Risoluzione dei problemi dell&#39;agente di raccolta eventi HTTP](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector) (elenca anche un compendio di [possibili codici di errore](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector#Possible_error_codes))
