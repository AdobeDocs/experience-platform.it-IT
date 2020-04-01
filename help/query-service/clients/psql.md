---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connetti con PSQL
topic: connect
translation-type: tm+mt
source-git-commit: 8310204071375a55329f661c9ac678f96979a594

---


# Connetti con PSQL

PSQL è un&#39;interfaccia della riga di comando che viene visualizzata quando installate Postgres sul computer. Potete installarlo seguendo queste istruzioni.

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

## Installare i post su un PC

Scarica e installa i post da questa [posizione](https://www.postgresql.org/download/windows/).

Modificate la variabile del percorso:

![Immagine](../images/clients/psql/path.png)

Aggiungete le due righe visualizzate che includono &quot;Postgres&quot;.

Salva gli aggiornamenti, quindi apri un prompt dei comandi e digita:

```shell
psql -V
```

Dovresti vedere qualcosa di simile a questo:

```shell
psql (PostgreSQL) 9.5.14
```

## Connect PSQL e servizio query

Tornate all&#39;interfaccia utente della piattaforma nella pagina &quot;Connect BI Tools&quot;.

Fate clic su **Copia** per &quot;Comando PSQL&quot;.

![Immagine](../images/clients/psql/connect-bi.png)

> [!IMPORTANT]: Se ti trovi su un PC, utilizza un editor di testo per rimuovere le interruzioni di riga nella stringa del comando, quindi copia la stringa.

Incollare la stringa del comando in una finestra di terminale o di comando e premere Invio.

Dovresti vedere un risultato come questo:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Se non viene visualizzata almeno la versione 10.5, è necessario scaricare tale versione o la versione successiva.