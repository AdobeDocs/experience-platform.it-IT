---
title: Connessione a Data Distiller da un notebook Jupyter
description: Scopri come connettersi a Data Distiller da un Jupyter Notebook.
exl-id: e6238b00-aaeb-40c0-a90f-9aebb1a1c421
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---

# Connessione a Data Distiller da un notebook Jupyter

Per arricchire le pipeline di apprendimento automatico con dati di alta qualità sull&#39;esperienza del cliente, devi prima connetterti a Data Distiller da [!DNL Jupyter Notebooks]. Questo documento descrive i passaggi necessari per connettersi a Data Distiller da un blocco appunti [!DNL Python] nell&#39;ambiente di machine learning.

## Introduzione

Questa guida presuppone che tu abbia familiarità con i notebook interattivi [!DNL Python] e che tu abbia accesso a un ambiente notebook. Il blocco appunti può essere ospitato in un ambiente di apprendimento automatico basato su cloud oppure localmente con [[!DNL Jupyter Notebook]](https://jupyter.org/).

### Ottenere le credenziali di connessione {#obtain-credentials}

Per connettersi a Data Distiller e ad altri servizi Adobe Experience Platform, è necessario disporre di una credenziale API Experience Platform. Le credenziali API possono essere create in [Adobe Developer Console](https://developer.adobe.com/console/projects) da un utente con accesso per sviluppatori all&#39;Experience Platform. Ti consigliamo di creare una credenziale API OAuth2 specifica per i flussi di lavoro di data science e di chiedere a un amministratore di Adobe della tua organizzazione di assegnare la credenziale a un ruolo con le autorizzazioni appropriate.

Per istruzioni dettagliate sulla creazione di credenziali API e sull&#39;ottenimento delle autorizzazioni necessarie, vedere [Autenticazione e accesso alle API Experience Platform](../../../landing/api-authentication.md).

Le autorizzazioni consigliate per la data science includono:

- Sandbox che verranno utilizzate per data science (in genere `prod`)
- Modellazione dati: [!UICONTROL Gestisci schemi]
- Gestione dati: [!UICONTROL Gestisci set di dati]
- Acquisizione dati: [!UICONTROL Visualizza origini]
- Destinazioni: [!UICONTROL Gestire e attivare le destinazioni del set di dati]
- Servizio query: [!UICONTROL Gestisci query]

Per impostazione predefinita, a un ruolo (e alle credenziali API assegnate a tale ruolo) viene impedito l’accesso ai dati con etichetta. In base ai criteri di governance dei dati dell’organizzazione, un amministratore di sistema può concedere al ruolo l’accesso a determinati dati etichettati ritenuti appropriati per l’utilizzo della scienza dei dati. I clienti di Platform hanno la responsabilità di gestire in modo appropriato l’accesso alle etichette e le policy al fine di rispettare le normative e le politiche organizzative pertinenti.

### Memorizza le credenziali in un file di configurazione separato {#store-credentials}

Per proteggere le credenziali, è consigliabile evitare di scrivere le informazioni direttamente nel codice. Le informazioni sulle credenziali vengono invece conservate in un file di configurazione separato e lette nei valori necessari per la connessione a Experience Platform e Data Distiller.

Ad esempio, è possibile creare un file denominato `config.ini` e includere le seguenti informazioni (insieme a qualsiasi altra informazione, ad esempio gli ID dei set di dati, che risulterebbero utili per il salvataggio tra le sessioni):

```ini
[Credential]
ims_org_id=<YOUR_IMS_ORG_ID>
sandbox_name=<YOUR_SANDBOX_NAME>
client_id=<YOUR_CLIENT_ID>
client_secret=<YOUR_CLIENT_SECRET>
scopes=openid, AdobeID, read_organizations, additional_info.projectedProductContext, session
tech_acct_id=<YOUR_TECHNICAL_ACCOUNT_ID>
```

Nel blocco appunti è quindi possibile leggere le informazioni sulle credenziali in memoria utilizzando il pacchetto `configParser` dalla libreria [!DNL Python] standard:

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)
```

È quindi possibile fare riferimento ai valori delle credenziali all&#39;interno del codice nel modo seguente:

```python
org_id = config.get('Credential', 'ims_org_id')
```

## Installare la libreria app Python {#install-python-library}

[aepp](https://github.com/adobe/aepp/tree/main) è una libreria [!DNL Python] open source gestita da Adobe che fornisce funzioni per la connessione a Data Distiller e l&#39;invio di query, come l&#39;esecuzione di richieste ad altri servizi Experience Platform. La libreria `aepp` a sua volta si basa sul pacchetto dell&#39;adattatore di database PostgreSQL `psycopg2` per le query interattive di Data Distiller. È possibile connettersi a Data Distiller ed eseguire query sui set di dati di Experience Platform solo con `psycopg2`, ma `aepp` offre maggiore comodità e funzionalità aggiuntive per effettuare richieste a tutti i servizi API di Experience Platform.

Per installare o aggiornare `aepp` e `psycopg2` nel tuo ambiente, puoi utilizzare il comando magico `%pip` nel tuo blocco appunti:

```python
%pip install --upgrade aepp
%pip install --upgrade psycopg2-binary
```

È quindi possibile configurare la libreria `aepp` con le credenziali utilizzando il codice seguente:

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)

# Configure aepp with your credentials
import aepp

aepp.configure(
  org_id=config.get('Credential', 'ims_org_id'),
  sandbox=config.get('Credential', 'sandbox_name'),
  client_id=config.get('Credential', 'client_id'), 
  secret=config.get('Credential', 'client_secret'),
  scopes=config.get('Credential', 'scopes'),
  tech_id=config.get('Credential', 'tech_acct_id')
)
```

## Creare una connessione a Data Distiller {#create-connection}

Dopo aver configurato `aepp` con le credenziali, è possibile utilizzare il codice seguente per creare una connessione a Data Distiller e avviare una sessione interattiva nel modo seguente:

```python
from aepp import queryservice

dd_conn = queryservice.QueryService().connection()
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

Puoi quindi eseguire una query sui set di dati nella sandbox di Experience Platform. Dato l’ID di un set di dati su cui desideri eseguire una query, puoi recuperare il nome della tabella corrispondente dal servizio Catalogo ed eseguire query sulla tabella:

```python
table_name = 'ecommerce_events'
simple_query = f'''SELECT * FROM {table_name} LIMIT 5'''
dd_cursor.query(simple_query)
```

### Connessione a un singolo set di dati per prestazioni di query più veloci {#connect-to-single-dataset}

Per impostazione predefinita, la connessione a Data Distiller si connette a tutti i set di dati nella sandbox. Per query più veloci e un utilizzo ridotto delle risorse, puoi invece connetterti a un set di dati specifico di tuo interesse. Per eseguire questa operazione, modificare `dbname` nell&#39;oggetto connessione Data Distiller in `{sandbox}:{table_name}`:

```python
from aepp import queryservice

sandbox = config.get('Credential', 'sandbox_name')
table_name = 'ecommerce_events'

dd_conn = queryservice.QueryService().connection()
dd_conn['dbname'] = f'{sandbox}:{table_name}'
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

## Passaggi successivi

Dopo aver letto questo documento, hai imparato a connetterti a Data Distiller da un blocco appunti [!DNL Python] nell&#39;ambiente di machine learning. Il passaggio successivo nella creazione di pipeline di funzioni da Experience Platform per alimentare modelli personalizzati nell&#39;ambiente di apprendimento automatico consiste nell&#39;esplorare e analizzare [i set di dati](./exploratory-analysis.md).
