---
title: Connessione a Data Distiller da un notebook Jupyter
description: Scopri come connettersi a Data Distiller da un Jupyter Notebook.
source-git-commit: 60c5a624bfbe88329ab3e12962f129f03966ce77
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 1%

---

# Connessione a Data Distiller da un notebook Jupyter

Per arricchire le pipeline di apprendimento automatico con dati di alta qualità sull’esperienza del cliente, devi prima connetterti a Data Distiller da [!DNL Jupyter Notebooks]. Questo documento descrive i passaggi per connettersi a Data Distiller da un [!DNL Python] nell&#39;ambiente di machine learning.

## Introduzione

Questa guida presuppone che tu abbia familiarità con le [!DNL Python] e avere accesso a un ambiente notebook. Il notebook può essere ospitato in un ambiente di apprendimento automatico basato su cloud oppure localmente con [[!DNL Jupyter Notebook]](https://jupyter.org/).

### Ottenere le credenziali di connessione {#obtain-credentials}

Per connettersi a Data Distiller e ad altri servizi Adobe Experience Platform, è necessario disporre di una credenziale API Experienci Platform. Le credenziali API possono essere create in  [Console Adobe Developer](https://developer.adobe.com/console/projects) da un utente con accesso per sviluppatori all’Experience Platform. Ti consigliamo di creare una credenziale API OAuth2 specifica per i flussi di lavoro di data science e di chiedere a un amministratore di Adobe della tua organizzazione di assegnare la credenziale a un ruolo con le autorizzazioni appropriate.

Consulta [Autenticazione e accesso alle API di Experienci Platform](../../../landing/api-authentication.md) per istruzioni dettagliate sulla creazione di credenziali API e sull’ottenimento delle autorizzazioni necessarie.

Le autorizzazioni consigliate per la data science includono:

- Sandbox/e che verranno utilizzate per la scienza dei dati (in genere `prod`)
- Modellazione dati: [!UICONTROL Gestire gli schemi]
- Gestione dati: [!UICONTROL Gestione set di dati]
- Acquisizione dei dati: [!UICONTROL Visualizza origini]
- Destinazioni: [!UICONTROL Gestire e attivare le destinazioni dei set di dati]
- Servizio query: [!UICONTROL Gestire le query]

Per impostazione predefinita, a un ruolo (e alle credenziali API assegnate a tale ruolo) viene impedito l’accesso ai dati con etichetta. In base ai criteri di governance dei dati dell’organizzazione, un amministratore di sistema può concedere al ruolo l’accesso a determinati dati etichettati ritenuti appropriati per l’utilizzo della scienza dei dati. I clienti di Platform hanno la responsabilità di gestire in modo appropriato l’accesso alle etichette e le policy al fine di rispettare le normative e le politiche organizzative pertinenti.

### Memorizza le credenziali in un file di configurazione separato {#store-credentials}

Per proteggere le credenziali, è consigliabile evitare di scrivere le informazioni direttamente nel codice. Le informazioni sulle credenziali vengono invece conservate in un file di configurazione separato e lette nei valori necessari per la connessione a Experienci Platform e Data Distiller.

Ad esempio, puoi creare un file denominato `config.ini` e includono le seguenti informazioni (insieme a tutte le altre informazioni, come ad esempio gli ID dei set di dati, che sarebbero utili da salvare tra una sessione e l’altra):

```ini
[Credential]
ims_org_id=<YOUR_IMS_ORG_ID>
sandbox_name=<YOUR_SANDBOX_NAME>
client_id=<YOUR_CLIENT_ID>
client_secret=<YOUR_CLIENT_SECRET>
scopes=openid, AdobeID, read_organizations, additional_info.projectedProductContext, session
tech_acct_id=<YOUR_TECHNICAL_ACCOUNT_ID>
```

Nel blocco appunti è quindi possibile leggere le informazioni sulle credenziali nella memoria utilizzando `configParser` pacchetto standard [!DNL Python] libreria:

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

[aepp](https://github.com/adobe/aepp/tree/main) è un open source gestito da Adobe [!DNL Python] fornisce funzioni per la connessione a Data Distiller e l’invio di query, come l’esecuzione di richieste ad altri servizi Experienci Platform. Il `aepp` La libreria a sua volta si basa sul pacchetto dell&#39;adattatore di database PostgreSQL  `psycopg2` per query interattive di Data Distiller. È possibile connettersi a Data Distiller ed eseguire query sui set di dati di Experience Platform con `psycopg2` da solo, ma `aepp` offre maggiore comodità e funzionalità aggiuntive per effettuare richieste a tutti i servizi API Experienci Platform.

Per installare o aggiornare `aepp` e `psycopg2` nell&#39;ambiente, è possibile utilizzare `%pip` comando magico nel notebook:

```python
%pip install --upgrade aepp
%pip install --upgrade psycopg2-binary
```

È quindi possibile configurare `aepp` libreria con le credenziali utilizzando il codice seguente:

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

Una volta `aepp` è configurato con le tue credenziali, puoi utilizzare il seguente codice per creare una connessione a Data Distiller e avviare una sessione interattiva come segue:

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

Per impostazione predefinita, la connessione a Data Distiller si connette a tutti i set di dati nella sandbox. Per query più veloci e un utilizzo ridotto delle risorse, puoi invece connetterti a un set di dati specifico di tuo interesse. Per farlo, è possibile modificare `dbname` nell’oggetto connessione Data Distiller a `{sandbox}:{table_name}`:

```python
from aepp import queryservice

sandbox = config.get('Credential', 'sandbox_name')
table_name = 'ecommerce_events'

dd_conn = queryservice.QueryService().connection()
dd_conn['dbname'] = f'{sandbox}:{table_name}'
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

## Passaggi successivi

Dopo aver letto questo documento, hai imparato a connetterti a Data Distiller da un [!DNL Python] nell&#39;ambiente di machine learning. Il passaggio successivo nella creazione di pipeline di funzioni da Experienci Platform per alimentare modelli personalizzati nell’ambiente di apprendimento automatico è [esplorare e analizzare i set di dati](./exploratory-analysis.md).
