---
keywords: Experience Platform;home;argomenti popolari;PSQL;psqlconnect a query service;Query service;query service;
solution: Experience Platform
title: Collegare PSQL al servizio query
description: PSQL è un'interfaccia a riga di comando che viene quando si installa PostgreSQL sul computer. È possibile installarlo seguendo queste istruzioni.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Collegare PSQL al servizio query

PSQL è un&#39;interfaccia della riga di comando che viene installata quando si installa [!DNL PostgreSQL] sulla tua macchina. Questo documento descrive i passaggi per la connessione di PSQL con Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Questa guida presuppone che tu abbia già accesso a [!DNL PSQL] e sono a conoscenza di come usarlo. Ulteriori informazioni [!DNL PSQL] si trova nella [ufficiale [!DNL PSQL] documentazione](https://www.postgresql.org/docs/current/app-psql.html).

Dopo aver installato PSQL sul computer, è possibile collegare PSQL con Query Service. Torna a [!DNL Platform] Interfaccia utente, quindi seleziona **[!UICONTROL Query]**, seguita da **[!UICONTROL Credenziali]**.

Sotto la **[!UICONTROL Comando PSQL]** seleziona la sezione **[!UICONTROL Copia negli Appunti]** icona (![Icona Copia](../images/clients/psql/copy-icon.png)) per copiare la stringa di comando.

![La scheda Credenziali dashboard Query con l&#39;icona di copia evidenziata.](../images/clients/psql/connect-bi.png)

Incolla la stringa di comando in una finestra del terminale o della riga di comando e premi **Invio** sulla tastiera.

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
