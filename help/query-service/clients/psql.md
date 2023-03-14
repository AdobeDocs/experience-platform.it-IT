---
keywords: Experience Platform;home;argomenti popolari;PSQL;psqlconnect to query service;Query service;query service;
solution: Experience Platform
title: Connetti PSQL a Query Service
description: PSQL è un'interfaccia della riga di comando disponibile quando si installa PostgreSQL nel computer. È possibile installarlo seguendo queste istruzioni.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Connetti PSQL a Query Service

PSQL è un&#39;interfaccia della riga di comando installata durante l&#39;installazione [!DNL PostgreSQL] sul tuo computer. Questo documento descrive i passaggi per la connessione di PSQL con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL PSQL] e hanno familiarità con le modalità di utilizzo. Ulteriori informazioni su [!DNL PSQL] si trova nella sezione [ufficiale [!DNL PSQL] documentazione](https://www.postgresql.org/docs/current/app-psql.html).

Dopo aver installato PSQL nel computer, è possibile connettersi a PSQL con Query Service. Torna a [!DNL Platform] UI, quindi seleziona **[!UICONTROL Query]**, seguito da **[!UICONTROL Credenziali]**.

Sotto **[!UICONTROL Comando PSQL]** , seleziona la sezione **[!UICONTROL Copia negli Appunti]** icona (![Copia icona](../images/clients/psql/copy-icon.png)) per copiare la stringa di comando.

![La scheda Credenziali del dashboard delle query con l’icona Copia evidenziata.](../images/clients/psql/connect-bi.png)

Incollare la stringa di comando in un terminale o in una finestra della riga di comando e premere **Invio** sulla tastiera.

>[!IMPORTANT]
>
>Se utilizzi un PC, utilizza un editor di testo per rimuovere le interruzioni di riga nella stringa di comando, quindi copia la stringa. Se utilizzi la versione 12.0 o successiva, dovrai aggiungere `PGGSSENCMODE=disable` alla stringa di connessione. Inoltre, se si utilizzano credenziali senza scadenza, assicurarsi di sostituire il campo password con la password delle credenziali senza scadenza. Per ulteriori informazioni sulle credenziali senza scadenza, leggere [guida alle credenziali](../ui/credentials.md).

Dovresti vedere un risultato come questo:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Se non vedi almeno la versione 10.5, devi scaricare tale versione o successiva.

## Passaggi successivi

Ora che hai stabilito una connessione con [!DNL Query Service], è possibile utilizzare PSQL per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire query, consulta la guida su [esecuzione di query](../best-practices/writing-queries.md).
