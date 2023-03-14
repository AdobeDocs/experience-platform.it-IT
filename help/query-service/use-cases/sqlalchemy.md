---
title: Gestire i dati della piattaforma utilizzando Python e SQLAlchemy
description: Scopri come utilizzare SQLAlchemy per gestire i dati di Platform utilizzando Python anziché SQL.
exl-id: 9fba942e-9b3d-4efe-ae94-aed685025dea
source-git-commit: 8644b78c947fd015f6a169c9440b8d1df71e5e17
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Gestire i dati di Platform tramite [!DNL Python] e [!DNL SQLAlchemy]

Scopri come utilizzare SQLAlchemy per una maggiore flessibilità nella gestione dei dati Adobe Experience Platform. Per coloro che non hanno familiarità con SQL, SQLAlchemy può migliorare notevolmente i tempi di sviluppo quando si lavora con i database relazionali. Questo documento fornisce istruzioni ed esempi per la connessione [!DNL SQLAlchemy] a Query Service e iniziare a utilizzare Python per interagire con i database.

[!DNL SQLAlchemy] è un Object Relational Mapper (ORM) e [!DNL Python] libreria di codici in grado di trasferire i dati memorizzati in un database SQL in [!DNL Python] oggetti. Puoi quindi eseguire operazioni CRUD sui dati conservati nel data lake di Platform utilizzando [!DNL Python] codice. Questo elimina la necessità di gestire i dati utilizzando solo PSQL.

## Introduzione

Per acquisire le credenziali necessarie per la connessione [!DNL SQLAlchemy] ad Experience Platform, devi avere accesso all’area di lavoro Query nell’interfaccia utente di Platform. Se al momento non disponi dell’accesso all’area di lavoro Query, contatta l’amministratore dell’organizzazione.

## [!DNL Query Service] credenziali {#credentials}

Per trovare le credenziali, accedi all’interfaccia utente di Platform e seleziona **[!UICONTROL Query]** dal menu di navigazione a sinistra, seguito da **[!UICONTROL Credenziali]**. Per le istruzioni complete su come trovare le credenziali di accesso, leggere [guida alle credenziali](../ui/credentials.md).

![Viene evidenziata la scheda Credenziali con le credenziali in scadenza per Query Service.](../images/use-cases/credentials.png)

Sebbene la porta 80 sia la porta consigliata per una connessione a Query Service, è possibile utilizzare anche la porta 5432.

>[!IMPORTANT]
>
>Se utilizzi le credenziali in scadenza (come mostrato nell’immagine precedente) per connetterti a Query Service, la durata della sessione per la connessione scadrà dopo il periodo di tempo impostato definito nelle impostazioni della tua organizzazione. Per impostazione predefinita, questo periodo è di 24 ore. Consulta la documentazione per scoprire come [connettere un client con credenziali senza scadenza](../ui/credentials.md#non-expiring-credentials), o come [modifica la durata della sessione per le credenziali in scadenza](../ui/credentials.md#expiring-credentials).

Una volta che hai accesso alle tue credenziali QS, apri il tuo [!DNL Python] editor di scelta.

### Memorizza credenziali in [!DNL Python] {#store-credentials}

Nel tuo [!DNL Python] editor, importa `urllib.parse.quote` e salva ciascuna variabile di credenziali come parametro. Il `urllib.parse` Il modulo fornisce un’interfaccia standard per suddividere le stringhe URL in componenti. La funzione delle virgolette sostituisce i caratteri speciali nella stringa URL per rendere i dati sicuri da utilizzare come componenti URL. Di seguito è riportato un esempio del codice richiesto:

>[!TIP]
>
>Utilizzare [!DNL Python]tre virgolette per immettere la stringa di password su più righe.

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
>Password fornita per la connessione [!DNL SQLAlchemy] L&#39;Experience Platform di a scadrà se si utilizzano le credenziali di scadenza. Consulta la [sezione delle credenziali](#credentials) per ulteriori informazioni.

### Creare un’istanza del motore [#create-engine]

Dopo la creazione delle variabili, importa `create_engine` e creare una stringa per compilare e formattare le credenziali di Query Service in SQLAlchemy. Il `create_engine` viene quindi utilizzata per creare un’istanza del motore.

>[!NOTE]
>
>`create_engine`restituisce un&#39;istanza di un motore. Tuttavia, non apre la connessione a Query Service finché non viene chiamata una query che richiede una connessione.

SSL deve essere abilitato quando si accede a Platform utilizzando client di terze parti. Come parte del motore, utilizza `connect_args` per immettere argomenti aggiuntivi per la parola chiave. Si consiglia di impostare la modalità SSL su `require`. Consulta la [Documentazione sulle modalità SSL](../clients/ssl-modes.md) per ulteriori informazioni sui valori accettati.

L’esempio seguente mostra il [!DNL Python] codice necessario per inizializzare un motore e una stringa di connessione.

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
>Password fornita per la connessione [!DNL SQLAlchemy] L&#39;Experience Platform di a scadrà se si utilizzano le credenziali di scadenza. Consulta la [sezione delle credenziali](#credentials) per ulteriori informazioni.

Ora puoi eseguire query sui dati di Platform tramite [!DNL Python]. L’esempio riportato di seguito restituisce una matrice di nomi di tabella di Query Service.

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
