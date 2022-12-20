---
title: Gestire i dati della piattaforma utilizzando Python e SQLAlchemy
description: Scopri come utilizzare SQLAlchemy per gestire i dati della piattaforma utilizzando Python invece di SQL.
source-git-commit: 6b7de4236982181eaac2aa37d525604cba31198e
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Gestire i dati di Platform utilizzando [!DNL Python] e [!DNL SQLAlchemy]

Scopri come utilizzare SQLAlchemy per una maggiore flessibilità nella gestione dei dati Adobe Experience Platform. Per coloro che non hanno familiarità con SQL, SQLAlchemy può migliorare notevolmente i tempi di sviluppo quando si lavora con database relazionali. Questo documento fornisce istruzioni ed esempi per la connessione [!DNL SQLAlchemy] per eseguire query sul servizio e iniziare a utilizzare Python per interagire con i database.

[!DNL SQLAlchemy] è una mappatura relazionale a oggetti (ORM) e un [!DNL Python] libreria di codici in grado di trasferire i dati memorizzati in un database SQL in [!DNL Python] oggetti. Puoi quindi eseguire operazioni CRUD sui dati contenuti all’interno del data lake di Platform utilizzando [!DNL Python] codice. Questo elimina la necessità di gestire i dati utilizzando solo PSQL.

## Introduzione

Acquisizione delle credenziali necessarie per la connessione [!DNL SQLAlchemy] ad Experience Platform, devi disporre dell’accesso all’area di lavoro Query nell’interfaccia utente di Platform. Se al momento non disponi dell’accesso all’area di lavoro Query, contatta l’amministratore dell’organizzazione.

## [!DNL Query Service] credenziali {#credentials}

Per trovare le tue credenziali, accedi all’interfaccia utente di Platform e seleziona **[!UICONTROL Query]** dalla navigazione a sinistra, seguita da **[!UICONTROL Credenziali]**. Per istruzioni complete su come trovare le credenziali di accesso, leggere il [guida alle credenziali](../ui/credentials.md).

![È stata evidenziata la scheda Credenziali con le credenziali in scadenza per il servizio query.](../images/use-cases/credentials.png)

Anche se la porta 80 è la porta consigliata per una connessione a Query Service, è anche possibile utilizzare la porta 5432.

>[!IMPORTANT]
>
>Se utilizzi le credenziali in scadenza (come illustrato nell’immagine precedente) per connettersi al servizio query, la durata della sessione per la connessione scadrà dopo il periodo di tempo impostato nelle impostazioni dell’organizzazione. Per impostazione predefinita, questo periodo è di 24 ore. Consulta la documentazione per scoprire come [connettere un client con credenziali non in scadenza](../ui/credentials.md#non-expiring-credentials)o come [modifica della durata della sessione per le credenziali in scadenza](../ui/credentials.md#expiring-credentials).

Una volta che hai accesso alle tue credenziali QS, apri la tua [!DNL Python] editor di scelta.

### Memorizza credenziali in [!DNL Python] {#store-credentials}

Nel tuo [!DNL Python] editor, importa `urllib.parse.quote` e salva ogni variabile di credenziali come parametro. La `urllib.parse` Il modulo fornisce un’interfaccia standard per suddividere le stringhe URL in componenti. La funzione virgolette sostituisce i caratteri speciali nella stringa URL per rendere i dati sicuri per l’uso come componenti URL. Di seguito è riportato un esempio di codice richiesto:

>[!TIP]
>
>Utilizzo [!DNL Python]Le virgolette triple di per inserire la stringa di password a più righe.

```python
from urllib.parse import quote

host = "<YOUR_HOST>"

port = "<YOUR_PORT>"

dbname = "<YOUR_DATABASE>"

user = "<YOUR_USERNAME>"

password = quote('''
<YOUR_PASSWORD>
''')
```

>[!NOTE]
>
>Password fornita per la connessione [!DNL SQLAlchemy] ad Experience Platform scadrà se utilizzi credenziali in scadenza. Consulta la sezione [sezione credenziali](#credentials) per ulteriori informazioni.

### Creare un’istanza di motore [#create-engine]

Dopo la creazione delle variabili, importa il `create_engine` e creare una stringa per compilare e formattare le credenziali del servizio query in SQLAlchemy. La `create_engine` viene quindi utilizzata per creare un&#39;istanza del motore.

>[!NOTE]
>
>`create_engine`restituisce un&#39;istanza di un motore. Tuttavia, non apre la connessione a Query Service finché non viene chiamata una query che richiede una connessione.

SSL deve essere abilitato quando si accede a Platform utilizzando client di terze parti. Come parte del tuo motore, utilizza il `connect_args` per immettere argomenti di parole chiave aggiuntivi. Imposta la modalità SSL su `require`. Consulta la sezione [Documentazione sulle modalità SSL](../clients/ssl-modes.md) per ulteriori informazioni sui valori accettati.

Nell’esempio seguente viene visualizzata la variabile [!DNL Python] codice necessario per inizializzare un motore e una stringa di connessione.

```python
from sqlalchemy import create_engine

db_string = "postgresql://{user}:{password}@{host}:{port}/{dbname}".format(
    user=user,
    password=password,
    host=host,
    port = port,
    dbname = dbname
)

engine = create_engine(db_string, connect_args={'sslmode':'require'})
```

>[!NOTE]
>
>Password fornita per la connessione [!DNL SQLAlchemy] ad Experience Platform scadrà se utilizzi credenziali in scadenza. Consulta la sezione [sezione credenziali](#credentials) per ulteriori informazioni.

È ora possibile eseguire query sui dati di Platform utilizzando [!DNL Python]. L’esempio riportato di seguito restituisce un array dei nomi della tabella Query Service.

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
