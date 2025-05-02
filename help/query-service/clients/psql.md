---
keywords: Experience Platform;home;argomenti popolari;PSQL;psqlconnect to query service;Query service;query service;
solution: Experience Platform
title: Connetti PSQL a Query Service
description: Scopri come connettere il client PSQL a Adobe Experience Platform Query Service, incluse le versioni e le istruzioni di installazione di PostgreSQL supportate.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: f75ea97e8631984dcd1d4a7f8aff3c10cba7b11f
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---

# Connetti PSQL a Query Service

PSQL è un&#39;interfaccia della riga di comando installata insieme a PostgreSQL nel computer. Questo documento descrive i passaggi per la connessione di PSQL con Adobe Experience Platform Query Service.

>[!IMPORTANT]
>
>Query Service supporta la connessione solo con PSQL versione 14.x. Le versioni precedenti a 14.x (ad esempio da 10.x a 13.x) e le versioni successive (15.x e successive) non sono ufficialmente supportate. Verificare di aver installato una versione client compatibile. Per riferimento, vedere le [Date di fine del ciclo di vita di PostgreSQL](https://endoflife.date/postgresql).

Prima di iniziare, assicurati di avere accesso a PSQL e alle nozioni di base sull’utilizzo del client. Ulteriori informazioni su PSQL sono disponibili nella [documentazione ufficiale di PSQL](https://www.postgresql.org/docs/current/app-psql.html).

>[!IMPORTANT]
>
>Quando si scarica PostgreSQL, assicurarsi di selezionare la versione 14.x. Per impostazione predefinita, il sito Web PostgreSQL offre la versione più recente, che potrebbe non essere compatibile con Query Service.

Una volta installato PSQL, è possibile collegarlo a Query Service. Torna all&#39;interfaccia utente di Experience Platform, quindi seleziona **[!UICONTROL Query]**, seguito da **[!UICONTROL Credenziali]**.

Nella sezione **[!UICONTROL Comando PSQL]**, seleziona l&#39;icona **[!UICONTROL Copia negli Appunti]** (![Copia icona](/help/images/icons/copy.png)) per copiare la stringa di comando.

![Scheda Credenziali del dashboard delle query con l&#39;icona Copia evidenziata.](../images/clients/psql/copy-credentials.png)

Incollare la stringa di comando nel terminale e premere **Invio** sulla tastiera.

>[!IMPORTANT]
>
>Se utilizzi un PC, utilizza un editor di testo per rimuovere le interruzioni di riga nella stringa di comando, quindi copia la stringa. Se si utilizza la versione 12.0 o successiva, sarà necessario aggiungere `PGGSSENCMODE=disable` alla stringa di connessione. Questa impostazione disabilita la crittografia GSSAPI, che non è necessaria per le connessioni a Query Service e può causare errori di connessione.<br>Inoltre, se si utilizzano credenziali senza scadenza, assicurarsi di sostituire il campo password con la password delle credenziali senza scadenza. Per ulteriori informazioni sulle credenziali senza scadenza, leggere la [guida delle credenziali](../ui/credentials.md).

Dovresti vedere un risultato come questo:

```shell
psql (14.4, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Se la versione 14.x non è disponibile, scaricare e installare una versione 14.x supportata di PSQL dalla [pagina di download ufficiale di PostgreSQL](https://www.postgresql.org/download/).

>[!NOTE]
>
>Seguire le istruzioni di installazione per il sistema operativo in uso, quindi verificare la versione PSQL installata eseguendo `psql --version` nel terminale.

## Passaggi successivi

Dopo aver stabilito la connessione a Query Service, è possibile utilizzare PSQL per scrivere query. Per ulteriori informazioni, consulta la guida su [query in esecuzione](../best-practices/writing-queries.md).
