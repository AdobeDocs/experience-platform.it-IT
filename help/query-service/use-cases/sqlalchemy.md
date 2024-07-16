---
title: Gestire i dati della piattaforma utilizzando Python e SQLAlchemy
description: Scopri come utilizzare SQLAlchemy per gestire i dati di Platform utilizzando Python anziché SQL.
exl-id: 9fba942e-9b3d-4efe-ae94-aed685025dea
source-git-commit: 8644b78c947fd015f6a169c9440b8d1df71e5e17
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---

# Gestisci i dati di Platform tramite [!DNL Python] e [!DNL SQLAlchemy]

Scopri come utilizzare SQLAlchemy per una maggiore flessibilità nella gestione dei dati Adobe Experience Platform. Per coloro che non hanno familiarità con SQL, SQLAlchemy può migliorare notevolmente i tempi di sviluppo quando si lavora con i database relazionali. In questo documento vengono fornite istruzioni ed esempi per connettere [!DNL SQLAlchemy] a Query Service e iniziare a utilizzare Python per interagire con i database.

[!DNL SQLAlchemy] è un Object Relational Mapper (ORM) e una libreria di codici [!DNL Python] in grado di trasferire i dati archiviati in un database SQL in oggetti [!DNL Python]. È quindi possibile eseguire operazioni CRUD sui dati contenuti nel data lake di Platform utilizzando il codice [!DNL Python]. Questo elimina la necessità di gestire i dati utilizzando solo PSQL.

## Introduzione

Per acquisire le credenziali necessarie per la connessione di [!DNL SQLAlchemy] a Experience Platform, è necessario avere accesso all&#39;area di lavoro Query nell&#39;interfaccia utente di Platform. Se al momento non disponi dell’accesso all’area di lavoro Query, contatta l’amministratore dell’organizzazione.

## [!DNL Query Service] credenziali {#credentials}

Per trovare le credenziali, accedi all&#39;interfaccia utente di Platform e seleziona **[!UICONTROL Query]** dal menu di navigazione a sinistra, seguito da **[!UICONTROL Credenziali]**. Per le istruzioni complete su come trovare le credenziali di accesso, leggere la [guida delle credenziali](../ui/credentials.md).

![La scheda Credenziali con le credenziali in scadenza per Query Service è evidenziata.](../images/use-cases/credentials.png)

Sebbene la porta 80 sia la porta consigliata per una connessione a Query Service, è possibile utilizzare anche la porta 5432.

>[!IMPORTANT]
>
>Se utilizzi le credenziali in scadenza (come mostrato nell’immagine precedente) per connetterti a Query Service, la durata della sessione per la connessione scadrà dopo il periodo di tempo impostato definito nelle impostazioni della tua organizzazione. Per impostazione predefinita, questo periodo è di 24 ore. Consulta la documentazione per scoprire come [connettere un client con credenziali senza scadenza](../ui/credentials.md#non-expiring-credentials) o come [modificare la durata della sessione per le credenziali in scadenza](../ui/credentials.md#expiring-credentials).

Una volta ottenuto l&#39;accesso alle credenziali QS, apri l&#39;editor [!DNL Python] scelto.

### Memorizza credenziali in [!DNL Python] {#store-credentials}

Nell&#39;editor [!DNL Python], importare la libreria `urllib.parse.quote` e salvare ogni variabile di credenziali come parametro. Il modulo `urllib.parse` fornisce un&#39;interfaccia standard per suddividere le stringhe URL in componenti. La funzione delle virgolette sostituisce i caratteri speciali nella stringa URL per rendere i dati sicuri da utilizzare come componenti URL. Di seguito è riportato un esempio del codice richiesto:

>[!TIP]
>
>Utilizza le virgolette triple di [!DNL Python] per immettere la stringa della password su più righe.

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
>La password fornita per connettere [!DNL SQLAlchemy] a Experience Platform scadrà se si utilizzano credenziali in scadenza. Per ulteriori informazioni, vedere la [sezione delle credenziali](#credentials).

### Crea un&#39;istanza del motore [#create-engine]

Dopo aver creato le variabili, importare la funzione `create_engine` e creare una stringa per compilare e formattare le credenziali di Query Service in SQLAlchemy. La funzione `create_engine` viene quindi utilizzata per creare un&#39;istanza del motore.

>[!NOTE]
>
>`create_engine`restituisce un&#39;istanza di un motore. Tuttavia, non apre la connessione a Query Service finché non viene chiamata una query che richiede una connessione.

SSL deve essere abilitato quando si accede a Platform utilizzando client di terze parti. Come parte del motore, utilizzare `connect_args` per immettere argomenti aggiuntivi per parole chiave. Si consiglia di impostare la modalità SSL su `require`. Consulta la [documentazione sulle modalità SSL](../clients/ssl-modes.md) per ulteriori informazioni sui valori accettati.

Nell&#39;esempio seguente viene visualizzato il codice [!DNL Python] necessario per inizializzare un motore e una stringa di connessione.

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
>La password fornita per connettere [!DNL SQLAlchemy] a Experience Platform scadrà se si utilizzano credenziali in scadenza. Per ulteriori informazioni, vedere la [sezione delle credenziali](#credentials).

È ora possibile eseguire query sui dati di Platform utilizzando [!DNL Python]. L’esempio riportato di seguito restituisce una matrice di nomi di tabella di Query Service.

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
