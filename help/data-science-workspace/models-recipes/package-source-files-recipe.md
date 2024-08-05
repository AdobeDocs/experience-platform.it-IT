---
keywords: Experience Platform;file di origine del pacchetto;Data Science Workspace;argomenti popolari;Docker;docker image
solution: Experience Platform
title: Creare pacchetti di file Source in una ricetta
type: Tutorial
description: Questa esercitazione fornisce istruzioni su come creare un pacchetto dei file di origine di esempio per le vendite al dettaglio in un file di archivio, che può essere utilizzato per creare una ricetta in Adobe Experience Platform Data Science Workspace seguendo il flusso di lavoro di importazione delle ricette nell’interfaccia utente o utilizzando l’API.
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 0%

---

# Creare un pacchetto di file di origine per una ricetta

>[!NOTE]
>
>Data Science Workspace non è più disponibile per l’acquisto.
>
>Questa documentazione è destinata ai clienti esistenti che dispongono di diritti precedenti su Data Science Workspace.

Questo tutorial fornisce istruzioni su come creare un pacchetto dei file di origine di esempio per le vendite al dettaglio in un file di archivio, che può essere utilizzato per creare una ricetta in Adobe Experience Platform [!DNL Data Science Workspace] seguendo il flusso di lavoro di importazione delle ricette nell&#39;interfaccia utente o utilizzando l&#39;API.

Concetti da comprendere:

- **Ricette**: una ricetta è il termine di Adobe Systems per una specifica del modello ed è un contenitore di primo livello che rappresenta uno specifico algoritmo di apprendimento automatico, intelligence artificiale o un insieme di algoritmi, logica di elaborazione e configurazione necessari per versione ed eseguire un modello addestrato e quindi aiutare a risolvere problemi aziendali specifici.
- **** File Origine: singoli file nel progetto che contengono la logica per una ricetta.

## Prerequisiti

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## Creazione ricetta

La creazione della ricetta inizia con la creazione di pacchetti di file di origine per la creazione di un file di archivio. I file Source definiscono la logica di apprendimento automatico e gli algoritmi utilizzati per risolvere un problema specifico e sono scritti in [!DNL Python], R, PySpark o Scala. I file di archivio creati si presentano come un’immagine Docker. Una volta generato, il file di archivio collocato viene importato in [!DNL Data Science Workspace] per creare una ricetta [nell&#39;interfaccia utente](./import-packaged-recipe-ui.md) o [utilizzando l&#39;API](./import-packaged-recipe-api.md).

### Authoring di modelli basato su Docker {#docker-based-model-authoring}

Un’immagine Docker consente a uno sviluppatore di creare un pacchetto di un’applicazione con tutte le parti necessarie, come librerie e altre dipendenze, e di distribuirlo come un unico pacchetto.

L’immagine Docker generata viene inviata al registro dei contenitori di Azure utilizzando le credenziali fornite durante il flusso di lavoro per la creazione della ricetta.

Per ottenere le credenziali del Registro di sistema del contenitore di Azure, accedi a [Adobe Experience Platform](https://platform.adobe.com). Nella colonna di navigazione sinistra, passa a **[!UICONTROL Flussi di lavoro]**. Seleziona **[!UICONTROL Importa ricetta]**, quindi seleziona **[!UICONTROL Avvia]**. Per maggiori informazioni, vedere la schermata seguente.

![](../images/models-recipes/package-source-files/import.png)

Viene visualizzata la pagina **[!UICONTROL Configura]**. Fornisci un **[!UICONTROL nome ricetta]** appropriato, ad esempio &quot;ricetta di vendita al dettaglio&quot;, e facoltativamente fornisci una descrizione o un URL della documentazione. Al termine, fai clic su **[!UICONTROL Avanti]**.

![](../images/models-recipes/package-source-files/configure.png)

Seleziona il *Runtime* appropriato, quindi scegli una **[!UICONTROL Classificazione]** per *Tipo*. Le credenziali del Registro di sistema del contenitore di Azure vengono generate una volta completate.

>[!NOTE]
>
>*Tipo* è la classe di problema di apprendimento automatico per cui la ricetta è progettata e viene utilizzata dopo l&#39;addestramento per aiutare a personalizzare la valutazione dell&#39;esecuzione dell&#39;addestramento.

>[!TIP]
>
>- Per [!DNL Python] ricette selezionare il runtime **[!UICONTROL Python]**.
>- Per le ricette R selezionare il runtime **[!UICONTROL R]**.
>- Per le ricette PySpark, seleziona il runtime **[!UICONTROL PySpark]**. Un tipo di artefatto viene popolato automaticamente.
>- Per le ricette Scala, seleziona il runtime **[!UICONTROL Spark]**. Un tipo di artefatto viene popolato automaticamente.

![](../images/models-recipes/package-source-files/docker-creds.png)

Prendi nota dei valori per host, nome utente e password Docker. Questi vengono utilizzati per versione e spingere la tua [!DNL Docker] immagine nei flussi di lavoro descritti di seguito.

>[!NOTE]
>
>Il Origine URL viene fornito dopo aver completato i passaggi descritti di seguito. Il file di configurazione viene spiegato nelle esercitazioni successive che si trovano nei [passaggi](#next-steps) successivi.

### Creare un pacchetto dei file di origine

Per prima cosa, ottenere il codebase di esempio trovato nell&#39;archivio <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform Data Science Workspace Reference</a>.

- [Creare un’immagine Python Docker](#python-docker)
- [Genera immagine Docker R](#r-docker)
- [Crea immagine Docker PySpark](#pyspark-docker)
- [Crea immagine Docker Scala (Spark)](#scala-docker)

### Genera immagine Docker [!DNL Python] {#python-docker}

In caso contrario, clonare l&#39;archivio [!DNL GitHub] nel sistema locale con il comando seguente:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Passare alla directory `experience-platform-dsw-reference/recipes/python/retail`. Qui troverai gli script `login.sh` e `build.sh` utilizzati per accedere a Docker e per generare l&#39;immagine [!DNL Python Docker]. Se le tue [credenziali Docker](#docker-based-model-authoring) sono pronte, immetti i seguenti comandi nell&#39;ordine:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Durante l’esecuzione dello script di accesso, devi fornire l’host Docker, il nome utente e la password. Durante la generazione, devi fornire l’host Docker e un tag di versione per la build.

Una volta completato lo script di build, nell’output della console viene fornito l’URL del file di origine Docker. Per questo esempio specifico, avrà un aspetto simile like:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

Copia questo URL e passa ai [passaggi](#next-steps) successivi.

### Genera immagine R [!DNL Docker] {#r-docker}

Se non è stato fatto, clonare il [!DNL GitHub] archivio nel sistema locale con il seguente comando:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Passare alla directory `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` all&#39;interno dell&#39;archivio clonato. Qui troverai i file `login.sh` e `build.sh` che utilizzerai per accedere a Docker e per generare l&#39;immagine R Docker. Se le tue [credenziali Docker](#docker-based-model-authoring) sono pronte, immetti i seguenti comandi nell&#39;ordine:

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

Copia questo URL e passa ai [passaggi successivi](#next-steps).

### Crea immagine Docker PySpark {#pyspark-docker}

Per iniziare, clonare l&#39;archivio [!DNL GitHub] nel sistema locale con il comando seguente:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Passare alla directory `experience-platform-dsw-reference/recipes/pyspark/retail`. Gli script `login.sh` e `build.sh` si trovano qui e vengono utilizzati per accedere a Docker e per generare l&#39;immagine Docker. Se le tue [credenziali Docker](#docker-based-model-authoring) sono pronte, immetti i seguenti comandi nell&#39;ordine:

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

Copia questo URL e passa ai [passaggi successivi](#next-steps).

### Crea immagine Docker Scala {#scala-docker}

Iniziare clonando l&#39;archivio [!DNL GitHub] nel sistema locale con il seguente comando nel terminale:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Passare quindi alla directory `experience-platform-dsw-reference/recipes/scala` in cui è possibile trovare gli script `login.sh` e `build.sh`. Questi script vengono utilizzati per accedere a Docker e generare l’immagine Docker. Se le tue [credenziali Docker](#docker-based-model-authoring) sono pronte, immetti i seguenti comandi da terminare in ordine:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>Se viene visualizzato un errore autorizzazione quando si tenta di login a Docker utilizzando lo `login.sh` script, provare a utilizzare il comando `bash login.sh`.

Quando si esegue lo script login, è necessario fornire l&#39;host Docker, il nome utente e il password. Durante la compilazione, è necessario fornire l&#39;host Docker e un tag di versione per il versione.

Una volta completato lo script versione, viene fornito un file di origine Docker URL nell&#39;output della console. Per questo esempio specifico, avrà un aspetto simile like:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Copia questo URL e passa ai [passaggi successivi](#next-steps).

## Passaggi successivi {#next-steps}

Questo tutorial ha esaminato il packaging dei file di origine in una ricetta, il passaggio preliminare per l&#39;importazione di una ricetta in [!DNL Data Science Workspace]. Ora dovresti disporre di un’immagine Docker nel registro dei contenitori di Azure insieme all’URL dell’immagine corrispondente. È ora possibile iniziare l&#39;esercitazione sull&#39;importazione di una composizione in pacchetti in [!DNL Data Science Workspace]. Per iniziare, seleziona uno dei collegamenti alle esercitazioni seguenti:

- [Importare una composizione in pacchetti nell’interfaccia utente](./import-packaged-recipe-ui.md)
- [Importare una composizione in pacchetti utilizzando l’API](./import-packaged-recipe-api.md)
