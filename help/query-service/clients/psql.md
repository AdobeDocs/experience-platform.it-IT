---
keywords: Experience Platform;home;argomenti popolari;PSQL;psqlconnect a query service;Query service;query service;
solution: Experience Platform
title: Collegare PSQL al servizio query
topic-legacy: connect
description: PSQL è un'interfaccia a riga di comando che viene quando si installa PostgreSQL sul computer. È possibile installarlo seguendo queste istruzioni.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 06d3a8aa6f2f73c2d5392a76fb5b36b18691cf0d
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 1%

---

# Collegare PSQL al servizio query

PSQL è un&#39;interfaccia della riga di comando che viene installata quando si installa [!DNL PostgreSQL] sulla tua macchina. Questo documento descrive i passaggi per la connessione di PSQL con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL PSQL] e sono a conoscenza di come usarlo. Ulteriori informazioni [!DNL PSQL] si trova nella [ufficiale [!DNL PSQL] documentazione](https://www.postgresql.org/docs/current/app-psql.html).

Dopo aver installato PSQL sul computer, è possibile collegare PSQL con Query Service. Torna a [!DNL Platform] Interfaccia utente, quindi seleziona **[!UICONTROL Query]**, seguita da **[!UICONTROL Credenziali]**.

![Immagine](../images/clients/psql/connect-bi.png)

Seleziona l’icona per copiare la sezione etichettata **[!UICONTROL Comando PSQL]**, quindi incollare la stringa di comando in un terminale o in una finestra della riga di comando prima di premere Invio.

>[!IMPORTANT]
>
>Se ti trovi su un PC, utilizza un editor di testo per rimuovere le interruzioni di riga nella stringa di comando, quindi copia la stringa. Se utilizzi la versione 12.0 o successiva, dovrai aggiungere `PGGSSENCMODE=disable` alla stringa di connessione. Inoltre, se utilizzi credenziali non in scadenza, assicurati di sostituire il campo password con la password delle credenziali non in scadenza. Per ulteriori informazioni sulle credenziali non in scadenza, leggere il [guida alle credenziali](../ui/credentials.md).

Dovresti vedere un risultato come questo:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Se non trovi almeno la versione 10.5, devi scaricare quella versione o quella successiva.

## Passaggi successivi

Ora che ti sei connesso [!DNL Query Service], è possibile utilizzare PSQL per scrivere le query. Per ulteriori informazioni su come scrivere ed eseguire le query, leggere la guida in [query in esecuzione](../best-practices/writing-queries.md).
