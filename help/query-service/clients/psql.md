---
keywords: Experience Platform;home;popular topics;PSQL;psql
solution: Experience Platform
title: Connetti con PSQL
topic: connect
description: 'PSQL è un''interfaccia della riga di comando che viene visualizzata quando installate Postgres sul computer. Potete installarlo seguendo queste istruzioni. '
translation-type: tm+mt
source-git-commit: 1bb896f7629d7b71b94dd107eeda87701df99208
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 1%

---


# Connetti con PSQL

PSQL è un&#39;interfaccia della riga di comando che viene visualizzata quando si esegue l&#39;installazione [!DNL Postgres] sul computer. Potete installarlo seguendo queste istruzioni.

## Installare i post su Mac

Aprite una finestra terminale ed eseguite i seguenti tre comandi:

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

```shell
brew install postgres
```

```shell
which psql
```

Dopo aver emesso questi comandi, dovrebbero essere visualizzati i seguenti elementi:

```shell
/usr/local/bin/psql
```

## Installazione [!DNL Postgres] su un PC

Scarica e installa [!DNL Postgres] da questa [posizione](https://www.postgresql.org/download/windows/).

Modificate la variabile del percorso:

![Immagine](../images/clients/psql/path.png)

Aggiungete le due righe visualizzate che includono &quot;[!DNL Postgres]&quot;.

Salva gli aggiornamenti, quindi apri un prompt dei comandi e digita:

```shell
psql -V
```

Dovresti vedere qualcosa di simile a questo:

```shell
psql (PostgreSQL) 9.5.14
```

## Connect PSQL e [!DNL Query Service]

Tornate all’ [!DNL Platform] interfaccia sulla **[!UICONTROL Connect BI Tools]** pagina.

Fate clic **[!UICONTROL copy]** per **[!UICONTROL PSQL Command]**.

![Immagine](../images/clients/psql/connect-bi.png)

>[!IMPORTANT]
>
>Se ti trovi su un PC, utilizza un editor di testo per rimuovere le interruzioni di riga nella stringa del comando, quindi copia la stringa.

Incollare la stringa del comando in una finestra di terminale o di comando e premere Invio.

Dovreste visualizzare un risultato simile al seguente:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Se non visualizzi almeno la versione 10.5, devi scaricare la versione o la versione successiva.