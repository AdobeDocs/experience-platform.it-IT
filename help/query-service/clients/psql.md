---
keywords: ' Experience Platform;home;argomenti popolari;PSQL;psqlconnect to query service;Query service;query service;'
solution: Experience Platform
title: Connetti con PSQL
topic: connect
description: 'PSQL è un''interfaccia della riga di comando che viene visualizzata quando si installa PostgreSQL nel computer. Potete installarlo seguendo queste istruzioni. '
translation-type: tm+mt
source-git-commit: bc1bbdddd75b11ac180b5e6faa391fd74e5f7e02
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 1%

---


# PSQL

PSQL è un&#39;interfaccia della riga di comando che viene installata quando si installa [!DNL PostgreSQL] nel computer. Questo documento descrive i passaggi per la connessione di PSQL con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che abbiate già accesso a [!DNL PSQL] e che abbiate familiarità con come usarlo. Ulteriori informazioni su [!DNL PSQL] sono disponibili nella [documentazione ufficiale [!DNL PSQL]](https://www.postgresql.org/docs/current/app-psql.html.

## Connect PSQL e [!DNL Query Service]

Dopo aver installato PSQL sul computer, è possibile collegare PSQL con Query Service. Tornate all&#39;interfaccia [!DNL Platform], quindi selezionate **[!UICONTROL Queries]**, seguito da **[!UICONTROL Credentials]**.

![Immagine](../images/clients/psql/connect-bi.png)

Selezionare l&#39;icona per copiare la sezione etichettata **[!UICONTROL PSQL Command]**, quindi incollare la stringa del comando in un terminale o in una finestra della riga di comando prima di premere Invio.

>[!IMPORTANT]
>
>Se ti trovi su un PC, utilizza un editor di testo per rimuovere le interruzioni di riga nella stringa del comando, quindi copia la stringa. Inoltre, se si utilizza la versione 12.0 o successiva, sarà necessario aggiungere `PGGSSENCMODE=disable` alla stringa di connessione.

Dovreste visualizzare un risultato simile al seguente:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Se non visualizzi almeno la versione 10.5, devi scaricare la versione o la versione successiva.

## Passaggi successivi

Ora che si è connessi con [!DNL Query Service], è possibile utilizzare PSQL per scrivere le query. Per ulteriori informazioni su come scrivere ed eseguire query, consultare la guida in [esecuzione query](../best-practices/writing-queries.md).