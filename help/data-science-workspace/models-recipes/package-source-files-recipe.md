---
keywords: Experience Platform;file di origine del pacchetto;Data Science Workspace;argomenti popolari;Docker;docker image
solution: Experience Platform
title: Creare pacchetti di file di origine in una ricetta
type: Tutorial
description: Questa esercitazione fornisce istruzioni su come creare un pacchetto dei file di origine di esempio per le vendite al dettaglio in un file di archivio, che può essere utilizzato per creare una ricetta in Adobe Experience Platform Data Science Workspace seguendo il flusso di lavoro di importazione delle ricette nell’interfaccia utente o utilizzando l’API.
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 0%

---

# Creare pacchetti di file di origine in una ricetta

Questa esercitazione fornisce istruzioni su come creare un pacchetto dei file di origine di esempio di vendita al dettaglio forniti in un file di archivio, che può essere utilizzato per creare una ricetta in Adobe Experience Platform [!DNL Data Science Workspace] seguendo il flusso di lavoro di importazione delle ricette nell’interfaccia utente o utilizzando l’API.

Concetti da comprendere:

- **Ricette**: una ricetta è il termine di Adobe per una specifica di modello ed è un contenitore di livello superiore che rappresenta un apprendimento automatico specifico, un algoritmo di intelligenza artificiale o un insieme di algoritmi, una logica di elaborazione e una configurazione necessarie per creare ed eseguire un modello addestrato e quindi contribuire a risolvere problemi di business specifici.
- **File di origine**: singoli file nel progetto che contengono la logica per una ricetta.

## Prerequisiti

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## Creazione ricetta

La creazione della ricetta inizia con la creazione di pacchetti di file di origine per la creazione di un file di archivio. I file di origine definiscono la logica di apprendimento automatico e gli algoritmi utilizzati per risolvere un problema specifico presente e sono scritti in [!DNL Python], R, PySpark o Scala. I file di archivio creati si presentano come un’immagine Docker. Una volta generato, il file di archivio viene importato in [!DNL Data Science Workspace] per creare una ricetta [nell’interfaccia utente](./import-packaged-recipe-ui.md) o [utilizzo dell’API](./import-packaged-recipe-api.md).

### Authoring di modelli basato su Docker {#docker-based-model-authoring}

Un’immagine Docker consente a uno sviluppatore di creare un pacchetto di un’applicazione con tutte le parti necessarie, come librerie e altre dipendenze, e di distribuirlo come un unico pacchetto.

L’immagine Docker generata viene inviata al registro dei contenitori di Azure utilizzando le credenziali fornite durante il flusso di lavoro per la creazione della ricetta.

Per ottenere le credenziali del Registro di sistema del contenitore di Azure, accedi a [Adobe Experience Platform](https://platform.adobe.com). Nella colonna di navigazione a sinistra, passa a **[!UICONTROL Flussi di lavoro]**. Seleziona **[!UICONTROL Importa ricetta]** seguito dalla selezione **[!UICONTROL Launch]**. Per maggiori informazioni, vedere la schermata seguente.

![](../images/models-recipes/package-source-files/import.png)

Il **[!UICONTROL Configura]** viene visualizzata la pagina. Fornisci un **[!UICONTROL Nome ricetta]**, ad esempio &quot;ricetta di vendita al dettaglio&quot; e, facoltativamente, fornire una descrizione o un URL della documentazione. Al termine, fai clic su **[!UICONTROL Successivo]**.

![](../images/models-recipes/package-source-files/configure.png)

Seleziona la scheda appropriata *Runtime*, quindi scegli un **[!UICONTROL Classificazione]** per *Tipo*. Le credenziali del Registro di sistema del contenitore di Azure vengono generate una volta completate.

>[!NOTE]
>
>*Tipo* è la classe di problema di apprendimento automatico per cui la ricetta è progettata e viene utilizzata dopo l’addestramento per aiutare a personalizzare la valutazione della fase di addestramento.

>[!TIP]
>
>- Per [!DNL Python] ricette seleziona la **[!UICONTROL Python]** runtime.
>- Per le ricette R seleziona la **[!UICONTROL R]** runtime.
>- Per le ricette PySpark, seleziona la **[!UICONTROL PySpark]** runtime. Un tipo di artefatto viene popolato automaticamente.
>- Per le ricette Scala seleziona la **[!UICONTROL Scintilla]** runtime. Un tipo di artefatto viene popolato automaticamente.


![](../images/models-recipes/package-source-files/docker-creds.png)

Osserva i valori per Docker host, nome utente e password. Questi vengono utilizzati per generare e inviare [!DNL Docker] immagine nei flussi di lavoro descritti di seguito.

>[!NOTE]
>
>L’URL di origine viene fornito dopo aver completato i passaggi descritti di seguito. Il file di configurazione viene descritto nelle esercitazioni successive disponibili in [passaggi successivi](#next-steps).

### Creare un pacchetto dei file di origine

Inizia ottenendo il codebase di esempio trovato nella <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform di riferimento di Data Science Workspace</a> archivio.

- [Creare un’immagine Python Docker](#python-docker)
- [Genera immagine Docker R](#r-docker)
- [Crea immagine Docker PySpark](#pyspark-docker)
- [Crea immagine Docker Scala (Spark)](#scala-docker)

### Genera [!DNL Python] Immagine Docker {#python-docker}

Se non lo hai fatto, clona il file [!DNL GitHub] sul sistema locale con il seguente comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Passa alla directory `experience-platform-dsw-reference/recipes/python/retail`. Qui troverai gli script `login.sh` e `build.sh` utilizzato per accedere a Docker e per generare [!DNL Python Docker] immagine. Se ha il suo [Credenziali Docker](#docker-based-model-authoring) a questo punto, immetti i seguenti comandi nell’ordine indicato:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Durante l’esecuzione dello script di accesso, devi fornire l’host Docker, il nome utente e la password. Durante la generazione, devi fornire l’host Docker e un tag di versione per la build.

Una volta completato lo script di build, nell’output della console viene fornito l’URL del file di origine Docker. Per questo esempio specifico, avrà un aspetto simile a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

Copia questo URL e passa a [passaggi successivi](#next-steps).

### Build R [!DNL Docker] immagine {#r-docker}

Se non lo hai fatto, clona il file [!DNL GitHub] sul sistema locale con il seguente comando:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Passa alla directory `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` nell’archivio clonato. Qui troverai i file `login.sh` e `build.sh` che utilizzerai per accedere a Docker e per generare l’immagine R Docker. Se ha il suo [Credenziali Docker](#docker-based-model-authoring) a questo punto, immetti i seguenti comandi nell’ordine indicato:

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

Durante l’esecuzione dello script di accesso, devi fornire l’host Docker, il nome utente e la password. Durante la generazione, devi fornire l’host Docker e un tag di versione per la build.

Una volta completato lo script di build, nell’output della console viene fornito l’URL del file di origine Docker. Per questo esempio specifico, avrà un aspetto simile a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

Copia questo URL e passa a [passaggi successivi](#next-steps).

### Crea immagine Docker PySpark {#pyspark-docker}

Iniziare clonando il file [!DNL GitHub] sul sistema locale con il seguente comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Passa alla directory `experience-platform-dsw-reference/recipes/pyspark/retail`. Gli script `login.sh` e `build.sh` si trovano qui e vengono utilizzati per accedere a Docker e per generare l’immagine Docker. Se ha il suo [Credenziali Docker](#docker-based-model-authoring) a questo punto, immetti i seguenti comandi nell’ordine indicato:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Durante l’esecuzione dello script di accesso, devi fornire l’host Docker, il nome utente e la password. Durante la generazione, devi fornire l’host Docker e un tag di versione per la build.

Una volta completato lo script di build, nell’output della console viene fornito l’URL del file di origine Docker. Per questo esempio specifico, avrà un aspetto simile a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

Copia questo URL e passa a [passaggi successivi](#next-steps).

### Crea immagine Docker Scala {#scala-docker}

Iniziare clonando il file [!DNL GitHub] sul sistema locale con il seguente comando nel terminale:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Quindi, passa alla directory `experience-platform-dsw-reference/recipes/scala` dove trovare gli script `login.sh` e `build.sh`. Questi script vengono utilizzati per accedere a Docker e generare l’immagine Docker. Se ha il suo [Credenziali Docker](#docker-based-model-authoring) a questo punto, immettere i seguenti comandi nel terminale:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>Se ricevi un errore di autorizzazione quando tenti di accedere a Docker utilizzando `login.sh` script, prova a utilizzare il comando `bash login.sh`.

Durante l’esecuzione dello script di accesso, devi fornire l’host Docker, il nome utente e la password. Durante la generazione, devi fornire l’host Docker e un tag di versione per la build.

Una volta completato lo script di build, nell’output della console viene fornito l’URL del file di origine Docker. Per questo esempio specifico, avrà un aspetto simile a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Copia questo URL e passa a [passaggi successivi](#next-steps).

## Passaggi successivi {#next-steps}

Questo tutorial illustra come creare pacchetti di file di origine in una ricetta, il passaggio preliminare per importare una ricetta in [!DNL Data Science Workspace]. Ora dovresti disporre di un’immagine Docker nel registro dei contenitori di Azure insieme all’URL dell’immagine corrispondente. Ora puoi iniziare il tutorial sull’importazione di una ricetta in pacchetti in [!DNL Data Science Workspace]. Per iniziare, seleziona uno dei collegamenti alle esercitazioni seguenti:

- [Importare una composizione in pacchetti nell’interfaccia utente](./import-packaged-recipe-ui.md)
- [Importare una composizione in pacchetti utilizzando l’API](./import-packaged-recipe-api.md)
