---
keywords: Experience Platform ;file sorgente del pacchetto;Data Science Workspace;argomenti più comuni;Docker;immagine docker
solution: Experience Platform
title: Creare pacchetti di file sorgente in una composizione
topic: tutorial
type: Tutorial
description: Questa esercitazione fornisce istruzioni su come creare pacchetti di file sorgente di esempio per le vendite al dettaglio in un file di archivio, che può essere utilizzato per creare una ricetta in Adobe Experience Platform Data Science Workspace seguendo il flusso di lavoro di importazione delle ricette nell'interfaccia utente o utilizzando l'API.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 0%

---


# Creare pacchetti di file sorgente in una ricetta

Questa esercitazione fornisce istruzioni su come creare pacchetti di file sorgente di esempio per le vendite al dettaglio in un file di archivio, che può essere utilizzato per creare una ricetta in Adobe Experience Platform [!DNL Data Science Workspace] seguendo il flusso di lavoro di importazione delle ricette nell&#39;interfaccia utente o utilizzando l&#39;API.

Concetti da comprendere:

- **Ricette**: Una ricetta è  termine  Adobe per una specifica del modello ed è un contenitore di primo livello che rappresenta uno specifico machine learning, un algoritmo di intelligenza artificiale o un insieme di algoritmi, una logica di elaborazione e una configurazione necessarie per creare ed eseguire un modello preparato e quindi aiutare a risolvere problemi aziendali specifici.
- **File** sorgente: Singoli file nel progetto che contengono la logica per una ricetta.

## Prerequisiti

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## Creazione di ricette

La creazione di ricette inizia con la creazione di pacchetti di file sorgente per creare un file di archivio. I file di origine definiscono la logica di machine learning e gli algoritmi utilizzati per risolvere un problema specifico a portata di mano e sono scritti in [!DNL Python], R, PySpark o Scala. I file di archivio generati hanno la forma di un&#39;immagine Docker. Una volta creato, il file di archivio del pacchetto viene importato in [!DNL Data Science Workspace] per creare una ricetta [nell&#39;interfaccia utente](./import-packaged-recipe-ui.md) o [utilizzando l&#39;API](./import-packaged-recipe-api.md).

### Authoring di modelli basati su docker {#docker-based-model-authoring}

Un&#39;immagine Docker consente a uno sviluppatore di creare un pacchetto con tutte le parti necessarie, come librerie e altre dipendenze, e inviarlo come un unico pacchetto.

L&#39;immagine Docker predefinita viene inviata al Registro di sistema del contenitore di Azure utilizzando le credenziali fornite durante il flusso di lavoro di creazione della ricetta.

Per ottenere le credenziali del Registro di sistema del contenitore di Azure, accedere a [Adobe Experience Platform](https://platform.adobe.com). Nella colonna di navigazione a sinistra, andate a **[!UICONTROL Workflows]**. Selezionare **[!UICONTROL Import Recipe]**, quindi **[!UICONTROL Launch]**. Per riferimento, vedere la schermata sottostante.

![](../images/models-recipes/package-source-files/import.png)

Viene aperta la pagina **[!UICONTROL Configure]**. Fornite una **[!UICONTROL Recipe Name]** appropriata, ad esempio &quot;Ricetta vendite al dettaglio&quot; e, facoltativamente, fornite una descrizione o un URL della documentazione. Al termine, fare clic su **[!UICONTROL Next]**.

![](../images/models-recipes/package-source-files/configure.png)

Selezionare il *Runtime* appropriato, quindi scegliere un **[!UICONTROL Classification]** per *Type*. Le credenziali del Registro di sistema del contenitore di Azure vengono generate una volta completate.

>[!NOTE]
>
>** Typeis è la classe di problema di apprendimento automatico per cui la ricetta è progettata ed è utilizzata dopo la formazione per aiutare a personalizzare la valutazione del corso di formazione.

>[!TIP]
>
>- Per le ricette [!DNL Python] selezionare il runtime **[!UICONTROL Python]**.
>- Per le ricette R, selezionate il runtime **[!UICONTROL R]**.
>- Per le ricette PySpark, selezionate il runtime **[!UICONTROL PySpark]**. Un tipo di artefatto compila automaticamente.
>- Per le ricette Scala, selezionate il runtime **[!UICONTROL Spark]**. Un tipo di artefatto compila automaticamente.


![](../images/models-recipes/package-source-files/docker-creds.png)

Notate i valori per l&#39;host Docker, il nome utente e la password. Vengono utilizzati per creare e inviare l&#39;immagine [!DNL Docker] nei flussi di lavoro indicati di seguito.

>[!NOTE]
>
>L’URL di origine viene fornito dopo aver completato i passaggi descritti di seguito. Il file di configurazione è spiegato nelle esercitazioni successive riportate in [passaggi successivi](#next-steps).

### Creare pacchetti di file sorgente

Per iniziare, ottenere il codice di esempio trovato nella directory archivio <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank"> Data Science Workspace Reference</a>.

- [Creare un&#39;immagine Python Docker](#python-docker)
- [Genera immagine Docker R](#r-docker)
- [Genera immagine PySpark Docker](#pyspark-docker)
- [Immagine Docker Scala (Spark)](#scala-docker)

### Genera [!DNL Python] immagine Docker {#python-docker}

In caso contrario, clonate il repository [!DNL GitHub] nel sistema locale con il comando seguente:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Andate alla directory `experience-platform-dsw-reference/recipes/python/retail`. Qui si trovano gli script `login.sh` e `build.sh` utilizzati per accedere al Docker e per creare l&#39;immagine [!DNL Python Docker]. Se le credenziali [Docker](#docker-based-model-authoring) sono pronte, immettere i comandi seguenti nell&#39;ordine:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Durante l&#39;esecuzione dello script di login, è necessario fornire l&#39;host Docker, il nome utente e la password. Durante la creazione, è necessario fornire l&#39;host Docker e un tag di versione per la build.

Una volta completato lo script di compilazione, nell&#39;output della console viene fornito un URL del file sorgente Docker. Per questo esempio specifico, avrà un aspetto simile a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

Copiate questo URL e passate ai [passaggi successivi](#next-steps).

### Genera immagine R [!DNL Docker] {#r-docker}

In caso contrario, clonate il repository [!DNL GitHub] nel sistema locale con il comando seguente:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Andate alla directory `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` all&#39;interno del repository clonato. Qui troverete i file `login.sh` e `build.sh` che verranno utilizzati per accedere al Docker e per creare l&#39;immagine del Docker R. Se le credenziali [Docker](#docker-based-model-authoring) sono pronte, immettere i comandi seguenti nell&#39;ordine:

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

Durante l&#39;esecuzione dello script di login, è necessario fornire l&#39;host Docker, il nome utente e la password. Durante la creazione, è necessario fornire l&#39;host Docker e un tag di versione per la build.

Una volta completato lo script di compilazione, nell&#39;output della console viene fornito un URL del file sorgente Docker. Per questo esempio specifico, avrà un aspetto simile a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

Copiate questo URL e passate ai [passaggi successivi](#next-steps).

### Genera immagine PySpark Docker {#pyspark-docker}

Per iniziare, clonate il repository [!DNL GitHub] nel sistema locale con il seguente comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Andate alla directory `experience-platform-dsw-reference/recipes/pyspark/retail`. Gli script `login.sh` e `build.sh` si trovano qui e vengono utilizzati per accedere al Docker e per creare l&#39;immagine Docker. Se le credenziali [Docker](#docker-based-model-authoring) sono pronte, immettere i comandi seguenti nell&#39;ordine:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Durante l&#39;esecuzione dello script di login, è necessario fornire l&#39;host Docker, il nome utente e la password. Durante la creazione, è necessario fornire l&#39;host Docker e un tag di versione per la build.

Una volta completato lo script di compilazione, nell&#39;output della console viene fornito un URL del file sorgente Docker. Per questo esempio specifico, avrà un aspetto simile a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

Copiate questo URL e passate ai [passaggi successivi](#next-steps).

### Genera immagine Docker Scala {#scala-docker}

Per iniziare, clonate il repository [!DNL GitHub] nel sistema locale con il seguente comando nel terminale:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Passare quindi alla directory `experience-platform-dsw-reference/recipes/scala` in cui è possibile trovare gli script `login.sh` e `build.sh`. Questi script vengono utilizzati per accedere al Docker e generare l&#39;immagine Docker. Se le credenziali [Docker](#docker-based-model-authoring) sono pronte, immettere i seguenti comandi per il terminale in ordine:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>Se ricevi un errore di autorizzazione durante il tentativo di accedere a Docker utilizzando lo script `login.sh`, prova a utilizzare il comando `bash login.sh`.

Durante l&#39;esecuzione dello script di login, è necessario fornire l&#39;host Docker, il nome utente e la password. Durante la creazione, è necessario fornire l&#39;host Docker e un tag di versione per la build.

Una volta completato lo script di compilazione, nell&#39;output della console viene fornito un URL del file sorgente Docker. Per questo esempio specifico, avrà un aspetto simile a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Copiate questo URL e passate ai [passaggi successivi](#next-steps).

## Passaggi successivi {#next-steps}

Questa esercitazione ha sostituito i file sorgente del pacchetto in una Ricetta, il passaggio preliminare per l&#39;importazione di una Ricetta in [!DNL Data Science Workspace]. È ora necessario disporre di un&#39;immagine Docker nel Registro di sistema del contenitore di Azure insieme all&#39;URL immagine corrispondente. È ora possibile iniziare l&#39;esercitazione sull&#39;importazione di una ricetta in un pacchetto in [!DNL Data Science Workspace]. Per iniziare, seleziona uno dei collegamenti di esercitazione seguenti:

- [Importare una ricetta in un pacchetto nell’interfaccia utente](./import-packaged-recipe-ui.md)
- [Importare una composizione in pacchetti utilizzando l&#39;API](./import-packaged-recipe-api.md)