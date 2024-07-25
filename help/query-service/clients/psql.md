---
keywords: Experience Platform;home;argomenti popolari;PSQL;psqlconnect to query service;Query service;query service;
solution: Experience Platform
title: Connetti PSQL a Query Service
description: PSQL è un'interfaccia della riga di comando disponibile quando si installa PostgreSQL nel computer. È possibile installarlo seguendo queste istruzioni.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# Connetti PSQL a Query Service

PSQL è un&#39;interfaccia della riga di comando installata quando si installa [!DNL PostgreSQL] nel computer. Questo documento descrive i passaggi per la connessione di PSQL con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL PSQL] e che tu abbia familiarità con le modalità di utilizzo. Ulteriori informazioni su [!DNL PSQL] sono disponibili nella [documentazione [!DNL PSQL] ufficiale](https://www.postgresql.org/docs/current/app-psql.html).

Dopo aver installato PSQL nel computer, è possibile connettersi a PSQL con Query Service. Torna all&#39;interfaccia utente [!DNL Platform], quindi seleziona **[!UICONTROL Query]**, seguito da **[!UICONTROL Credenziali]**.

Nella sezione **[!UICONTROL Comando PSQL]**, seleziona l&#39;icona **[!UICONTROL Copia negli Appunti]** (![Copia icona](/help/images/icons/copy.png)) per copiare la stringa di comando.

![Scheda Credenziali del dashboard delle query con l&#39;icona Copia evidenziata.](../images/clients/psql/connect-bi.png)

Incollare la stringa di comando in un terminale o in una finestra della riga di comando e premere **Invio** sulla tastiera.

>[!IMPORTANT]
>
>Se utilizzi un PC, utilizza un editor di testo per rimuovere le interruzioni di riga nella stringa di comando, quindi copia la stringa. Se si utilizza la versione 12.0 o successiva, sarà necessario aggiungere `PGGSSENCMODE=disable` alla stringa di connessione. Inoltre, se si utilizzano credenziali senza scadenza, assicurarsi di sostituire il campo password con la password delle credenziali senza scadenza. Per ulteriori informazioni sulle credenziali senza scadenza, leggere la [guida delle credenziali](../ui/credentials.md).

Dovresti vedere un risultato come questo:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Se non vedi almeno la versione 10.5, devi scaricare tale versione o successiva.

## Passaggi successivi

Dopo aver stabilito la connessione con [!DNL Query Service], è possibile utilizzare PSQL per scrivere query. Per ulteriori informazioni su come scrivere ed eseguire query, leggere la guida in [esecuzione di query](../best-practices/writing-queries.md).
