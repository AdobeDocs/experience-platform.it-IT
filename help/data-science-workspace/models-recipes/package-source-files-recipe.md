---
keywords: Experience Platform;package source files;Data Science Workspace;popular topics
solution: Experience Platform
title: Creare pacchetti di file sorgente in una ricetta
topic: Tutorial
translation-type: tm+mt
source-git-commit: f2a7300d4ad75e3910abbdf2ecc2946a2dfe553c
workflow-type: tm+mt
source-wordcount: '1096'
ht-degree: 0%

---


# Creare pacchetti di file sorgente in una ricetta

Questa esercitazione fornisce istruzioni su come creare pacchetti di file sorgente di esempio per le vendite al dettaglio in un file di archivio, che può essere utilizzato per creare una ricetta in Adobe Experience Platform Data Science Workspace seguendo il flusso di lavoro di importazione delle ricette nell&#39;interfaccia utente o utilizzando l&#39;API.

Concetti da comprendere:

- **Ricette**: Una ricetta è il termine utilizzato da Adobe per specificare un modello ed è un contenitore di primo livello che rappresenta uno specifico sistema di machine learning, un algoritmo di intelligenza artificiale o un insieme di algoritmi, una logica di elaborazione e una configurazione necessarie per creare ed eseguire un modello qualificato e quindi per risolvere problemi aziendali specifici.
- **File** sorgente: Singoli file nel progetto che contengono la logica per una ricetta.

## Prerequisiti

- [Docker](https://docs.docker.com/install/#supported-platforms)
- [Python 3 e pip](https://docs.conda.io/en/latest/miniconda.html)
- [Scala](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [Paradiso](https://maven.apache.org/install.html)

## Creazione di ricette

La creazione di ricette inizia con la creazione di pacchetti di file sorgente per creare un file di archivio. I file di origine definiscono la logica di machine learning e gli algoritmi utilizzati per risolvere un problema specifico a portata di mano e sono scritti in Python, R, PySpark o Scala. I file di archivio generati hanno la forma di un&#39;immagine Docker. Una volta creato, il file di archivio del pacchetto viene importato in Data Science Workspace per creare una ricetta [nell&#39;interfaccia utente](./import-packaged-recipe-ui.md) o [utilizzando l&#39;API](./import-packaged-recipe-api.md).

### Authoring di modelli basato su docker {#docker-based-model-authoring}

Un&#39;immagine Docker consente a uno sviluppatore di creare un pacchetto con tutte le parti necessarie, come librerie e altre dipendenze, e inviarlo come un unico pacchetto.

L&#39;immagine Docker predefinita viene inviata al Registro di sistema del contenitore di Azure utilizzando le credenziali fornite durante il flusso di lavoro di creazione della ricetta.

Per ottenere le credenziali del Registro di sistema del contenitore di Azure, accedi ad <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a>. Nella colonna di navigazione a sinistra, andate a **[!UICONTROL Workflows]**. Selezionate **[!UICONTROL Import Recipe]** seguito da **[!UICONTROL Launch]**. Per riferimento, vedere la schermata sottostante.

![](../images/models-recipes/package-source-files/import.png)

Viene visualizzata la pagina *Configura* . Fornite un Nome ** ricetta appropriato, ad esempio &quot;Ricetta vendite al dettaglio&quot;, e facoltativamente fornite una descrizione o un URL della documentazione. Al termine, fate clic **[!UICONTROL Next]**.

![](../images/models-recipes/package-source-files/configure.png)

Selezionate il *runtime* appropriato, quindi scegliete un **[!UICONTROL Classification]** per *Tipo*. Le credenziali del Registro di sistema del contenitore di Azure vengono generate una volta completate.

>[!NOTE]
>*Tipo *è la classe di problema di apprendimento automatico per cui la ricetta è progettata ed è utilizzata dopo la formazione per aiutare a personalizzare la valutazione dell&#39;esecuzione della formazione.

>[!TIP]
>- Per le ricette Python selezionate il **[!UICONTROL Python]** runtime.
>- Per le ricette R, selezionate il **[!UICONTROL R]** runtime.
>- Per le ricette PySpark, selezionate il **[!UICONTROL PySpark]** runtime. Un tipo di artefatto compila automaticamente.
>- Per le ricette Scala, selezionate il **[!UICONTROL Spark]** runtime. Un tipo di artefatto compila automaticamente.


![](../images/models-recipes/package-source-files/docker-creds.png)

Prendete nota dei valori per *Docker Host*, *Nome utente* e *Password*. Vengono utilizzati per creare e inviare l&#39;immagine Docker nei flussi di lavoro descritti di seguito.

>[!NOTE]
>L’URL di origine viene fornito dopo aver completato i passaggi descritti di seguito. Il file di configurazione è spiegato nelle esercitazioni successive riportate nei passaggi [successivi](#next-steps).

### Creare pacchetti di file sorgente

Per iniziare, ottieni il codice di esempio trovato nell’archivio di riferimento <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">di</a> Experience Platform Data Science Workspace.

- [Creare un&#39;immagine Python Docker](#python-docker)
- [Genera immagine Docker R](#r-docker)
- [Genera immagine PySpark Docker](#pyspark-docker)
- [Immagine Docker Scala (Spark)](#scala-docker)

### Creare un&#39;immagine Python Docker {#python-docker}

Se non lo avete fatto, clonate il repository github nel sistema locale con il seguente comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigate to the directory `experience-platform-dsw-reference/recipes/python/retail`. Qui troverete gli script `login.sh` e `build.sh` utilizzati per accedere a Docker e per creare l&#39;immagine di python Docker. Se disponete delle credenziali [](#docker-based-model-authoring) Docker, immettete i seguenti comandi nell&#39;ordine:

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

Copiate questo URL e passate ai passaggi [successivi](#next-steps).

### Genera immagine Docker R {#r-docker}

Se non lo avete fatto, clonate il repository github nel sistema locale con il seguente comando:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Andate alla directory `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` all&#39;interno del repository clonato. Qui troverete i file `login.sh` e `build.sh` che si utilizzerà per accedere al Docker e per creare l&#39;immagine del Docker R. Se disponete delle credenziali [](#docker-based-model-authoring) Docker, immettete i seguenti comandi nell&#39;ordine:

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

Copiate questo URL e passate ai passaggi [successivi](#next-steps).

### Genera immagine PySpark Docker {#pyspark-docker}

Per iniziare, clonate il repository github sul sistema locale con il seguente comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigate to the directory `experience-platform-dsw-reference/recipes/pyspark/retail`. Gli script `login.sh` e `build.sh` sono situati qui e utilizzati per accedere a Docker e per creare l&#39;immagine Docker. Se disponete delle credenziali [](#docker-based-model-authoring) Docker, immettete i seguenti comandi nell&#39;ordine:

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

Copiate questo URL e passate ai passaggi [successivi](#next-steps).

### Genera immagine Docker scala {#scala-docker}

Per iniziare, clonate il repository github sul sistema locale con il seguente comando nel terminale:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Quindi, passare alla directory `experience-platform-dsw-reference/recipes/scala/retail` in cui è possibile trovare gli script `login.sh` e `build.sh`. Questi script vengono utilizzati per accedere al Docker e generare l&#39;immagine Docker. Se disponete delle credenziali [](#docker-based-model-authoring) Docker, immettete i seguenti comandi per il terminale in ordine:

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
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Copiate questo URL e passate ai passaggi [successivi](#next-steps).

## Passaggi successivi {#next-steps}

Questa esercitazione ha passato i file di origine del pacchetto in una Ricetta, il passaggio preliminare per l&#39;importazione di una Ricetta in Data Science Workspace. È ora necessario disporre di un&#39;immagine Docker nel Registro di sistema del contenitore di Azure insieme all&#39;URL immagine corrispondente. È ora possibile iniziare l&#39;esercitazione sull&#39;importazione di una ricetta in un pacchetto in Data Science Workspace. Per iniziare, seleziona uno dei collegamenti di esercitazione seguenti:

- [Importare una ricetta in un pacchetto nell’interfaccia utente](./import-packaged-recipe-ui.md)
- [Importare una composizione in pacchetti utilizzando l&#39;API](./import-packaged-recipe-api.md)