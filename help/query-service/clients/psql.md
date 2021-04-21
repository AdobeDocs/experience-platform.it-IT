---
keywords: Experience Platform;home;argomenti popolari;PSQL;psqlconnect a query service;Query service;query service;
solution: Experience Platform
title: Collegare PSQL al servizio query
topic-legacy: connect
description: PSQL è un'interfaccia a riga di comando che viene quando si installa PostgreSQL sul computer. È possibile installarlo seguendo queste istruzioni.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 1%

---

# Collegare PSQL al servizio query

PSQL è un&#39;interfaccia a riga di comando che viene installata quando si installa [!DNL PostgreSQL] sul computer. Questo documento descrive i passaggi per la connessione di PSQL con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL PSQL] e che tu abbia familiarità con come usarlo. Ulteriori informazioni su [!DNL PSQL] sono disponibili nella documentazione [ufficiale [!DNL PSQL]](https://www.postgresql.org/docs/current/app-psql.html.

Dopo aver installato PSQL sul computer, è possibile collegare PSQL con Query Service. Torna all’ [!DNL Platform] interfaccia utente, quindi seleziona **[!UICONTROL Queries]**, seguito da **[!UICONTROL Credentials]**.

![Immagine](../images/clients/psql/connect-bi.png)

Selezionare l&#39;icona per copiare la sezione etichettata **[!UICONTROL PSQL Command]**, quindi incollare la stringa del comando in un terminale o in una finestra della riga di comando prima di premere Invio.

>[!IMPORTANT]
>
>Se ti trovi su un PC, utilizza un editor di testo per rimuovere le interruzioni di riga nella stringa di comando, quindi copia la stringa. Inoltre, se utilizzi una versione 12.0 o successiva, dovrai aggiungere `PGGSSENCMODE=disable` alla stringa di connessione.

Dovresti vedere un risultato come questo:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Se non trovi almeno la versione 10.5, devi scaricare quella versione o quella successiva.

## Passaggi successivi

Dopo aver effettuato la connessione con [!DNL Query Service], è possibile utilizzare PSQL per scrivere le query. Per ulteriori informazioni su come scrivere ed eseguire le query, leggere la guida sull&#39; [esecuzione delle query](../best-practices/writing-queries.md).
