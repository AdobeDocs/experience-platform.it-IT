---
keywords: Experience Platform;file di origine del pacchetto;Data Science Workspace;argomenti comuni;Docker;docker immagine
solution: Experience Platform
title: File di origine del pacchetto in una composizione
type: Tutorial
description: Questa esercitazione fornisce istruzioni su come creare un pacchetto dei file di origine di esempio Vendite al dettaglio forniti in un file di archivio, che può essere utilizzato per creare una ricetta in Adobe Experience Platform Data Science Workspace seguendo il flusso di lavoro di importazione delle ricette nell'interfaccia utente o utilizzando l'API.
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 0%

---

# Creare pacchetti di file sorgente in una ricetta

Questa esercitazione fornisce istruzioni su come creare un pacchetto dei file di origine di esempio Vendite al dettaglio forniti in un file di archivio che può essere utilizzato per creare una ricetta in Adobe Experience Platform [!DNL Data Science Workspace] seguendo il flusso di lavoro di importazione della ricetta nell’interfaccia utente o utilizzando l’API .

Concetti da comprendere:

- **Ricette**: Una ricetta è un termine Adobe per una specifica di modello ed è un contenitore di livello superiore che rappresenta uno specifico apprendimento automatico, un algoritmo di intelligenza artificiale o un insieme di algoritmi, logica di elaborazione e configurazione necessari per creare ed eseguire un modello addestrato e quindi aiutare a risolvere problemi di business specifici.
- **File di origine**: Singoli file nel progetto che contengono la logica per una ricetta.

## Prerequisiti

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## Creazione di ricette

La creazione di ricette inizia con la creazione di pacchetti di file sorgente per creare un file di archivio. I file di origine definiscono la logica di apprendimento automatico e gli algoritmi utilizzati per risolvere un problema specifico a portata di mano e sono scritti in [!DNL Python], R, PySpark o Scala. I file di archivio generati si presentano sotto forma di immagine Docker. Una volta generato, il file di archivio in pacchetto viene importato in [!DNL Data Science Workspace] per creare una ricetta [nell’interfaccia utente](./import-packaged-recipe-ui.md) o [utilizzo dell’API](./import-packaged-recipe-api.md).

### Authoring di modelli basato su docker {#docker-based-model-authoring}

Un&#39;immagine Docker consente allo sviluppatore di creare un pacchetto di un&#39;applicazione con tutte le parti necessarie, come librerie e altre dipendenze, e di distribuirlo come un unico pacchetto.

L’immagine Docker creata viene inviata al Registro di sistema del contenitore di Azure utilizzando le credenziali fornite durante il flusso di lavoro di creazione della ricetta.

Per ottenere le credenziali del Registro di sistema del contenitore di Azure, accedi a [Adobe Experience Platform](https://platform.adobe.com). Nella colonna di navigazione a sinistra, passa a **[!UICONTROL Flussi di lavoro]**. Seleziona **[!UICONTROL Ricetta importazione]** seguito dalla selezione **[!UICONTROL Launch]**. Vedi la schermata sottostante per riferimento.

![](../images/models-recipes/package-source-files/import.png)

La **[!UICONTROL Configura]** viene visualizzata la pagina . Fornire un **[!UICONTROL Nome ricetta]**, ad esempio &quot;Ricetta vendite al dettaglio&quot; e, facoltativamente, fornisci una descrizione o un URL della documentazione. Al termine, fai clic su **[!UICONTROL Successivo]**.

![](../images/models-recipes/package-source-files/configure.png)

Selezionare il *Runtime*, quindi scegli un **[!UICONTROL Classificazione]** per *Tipo*. Le credenziali del Registro di sistema del contenitore di Azure vengono generate una volta completate.

>[!NOTE]
>
>*Tipo* è la classe del problema di apprendimento automatico per cui la ricetta è progettata e viene utilizzata dopo l&#39;allenamento per aiutare a personalizzare la valutazione del percorso di formazione.

>[!TIP]
>
>- Per [!DNL Python] le ricette selezionano **[!UICONTROL Pitone]** runtime.
>- Per le ricette R, seleziona la **[!UICONTROL R]** runtime.
>- Per le ricette PySpark, seleziona la **[!UICONTROL PySpark]** runtime. Un tipo di artefatto viene compilato automaticamente.
>- Per le ricette Scala selezionare la **[!UICONTROL Parco]** runtime. Un tipo di artefatto viene compilato automaticamente.


![](../images/models-recipes/package-source-files/docker-creds.png)

Osserva i valori per l’host Docker, il nome utente e la password. Vengono utilizzati per generare e inviare [!DNL Docker] nei flussi di lavoro descritti di seguito.

>[!NOTE]
>
>L’URL sorgente viene fornito dopo aver completato i passaggi descritti di seguito. Il file di configurazione è spiegato nelle esercitazioni successive disponibili in [passaggi successivi](#next-steps).

### Creare un pacchetto con i file di origine

Inizia ottenendo la base di codice campione trovata nella <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Riferimento ad Experience Platform Data Science Workspace</a> archivio.

- [Crea immagine Piton Docker](#python-docker)
- [Crea immagine Docker R](#r-docker)
- [Crea immagine Docker PySpark](#pyspark-docker)
- [Immagine Docker Scala (Spark)](#scala-docker)

### Crea [!DNL Python] Immagine Docker {#python-docker}

Se non lo hai fatto, duplica il [!DNL GitHub] nel sistema locale con il seguente comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Passa alla directory `experience-platform-dsw-reference/recipes/python/retail`. Qui trovi gli script `login.sh` e `build.sh` utilizzato per accedere a Docker e per generare il [!DNL Python Docker] immagine. Se hai [Credenziali Docker](#docker-based-model-authoring) pronti, immetti i seguenti comandi nell&#39;ordine:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Quando esegui lo script di accesso, devi fornire l’host Docker, il nome utente e la password. Durante la creazione, devi fornire l’host Docker e un tag di versione per la build.

Una volta completato lo script di compilazione, nell’output della console viene assegnato un URL del file di origine Docker. Per questo esempio specifico, avrà un aspetto simile a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

Copia questo URL e passa a [passaggi successivi](#next-steps).

### Crea R [!DNL Docker] immagine {#r-docker}

Se non lo hai fatto, duplica il [!DNL GitHub] nel sistema locale con il seguente comando:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Passa alla directory `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` all’interno dell’archivio clonato. Qui trovi i file `login.sh` e `build.sh` che utilizzerai per accedere a Docker e per generare l&#39;immagine R Docker. Se hai [Credenziali Docker](#docker-based-model-authoring) pronti, immetti i seguenti comandi nell&#39;ordine:

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

Quando esegui lo script di accesso, devi fornire l’host Docker, il nome utente e la password. Durante la creazione, devi fornire l’host Docker e un tag di versione per la build.

Una volta completato lo script di compilazione, nell’output della console viene assegnato un URL del file di origine Docker. Per questo esempio specifico, avrà un aspetto simile a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

Copia questo URL e passa a [passaggi successivi](#next-steps).

### Crea immagine Docker PySpark {#pyspark-docker}

Inizia clonando il [!DNL GitHub] nel sistema locale con il seguente comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Passa alla directory `experience-platform-dsw-reference/recipes/pyspark/retail`. Gli script `login.sh` e `build.sh` si trovano qui e vengono utilizzati per accedere a Docker e per creare l&#39;immagine Docker. Se hai [Credenziali Docker](#docker-based-model-authoring) pronti, immetti i seguenti comandi nell&#39;ordine:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Quando esegui lo script di accesso, devi fornire l’host Docker, il nome utente e la password. Durante la creazione, devi fornire l’host Docker e un tag di versione per la build.

Una volta completato lo script di compilazione, nell’output della console viene assegnato un URL del file di origine Docker. Per questo esempio specifico, avrà un aspetto simile a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

Copia questo URL e passa a [passaggi successivi](#next-steps).

### Immagine Docker Scala {#scala-docker}

Inizia clonando il [!DNL GitHub] repository sul sistema locale con il seguente comando nel terminale:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Quindi, accedi alla directory `experience-platform-dsw-reference/recipes/scala` dove è possibile trovare gli script `login.sh` e `build.sh`. Questi script vengono utilizzati per accedere a Docker e generare l&#39;immagine Docker. Se hai [Credenziali Docker](#docker-based-model-authoring) pronto, immetti i seguenti comandi al terminale in ordine:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>Se ricevi un errore di autorizzazione quando tenti di accedere a Docker utilizzando il `login.sh` script, provare a utilizzare il comando `bash login.sh`.

Quando esegui lo script di accesso, devi fornire l’host Docker, il nome utente e la password. Durante la creazione, devi fornire l’host Docker e un tag di versione per la build.

Una volta completato lo script di compilazione, nell’output della console viene assegnato un URL del file di origine Docker. Per questo esempio specifico, avrà un aspetto simile a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Copia questo URL e passa a [passaggi successivi](#next-steps).

## Passaggi successivi {#next-steps}

Questa esercitazione ha superato il package dei file di origine in una composizione, il passaggio preliminare per l&#39;importazione di una composizione in [!DNL Data Science Workspace]. Ora devi disporre di un’immagine Docker nel Registro di sistema dei contenitori di Azure insieme all’URL dell’immagine corrispondente. È ora possibile iniziare l’esercitazione sull’importazione di una ricetta in pacchetto [!DNL Data Science Workspace]. Seleziona uno dei collegamenti tutorial seguenti per iniziare:

- [Importare una composizione in pacchetto nell’interfaccia utente](./import-packaged-recipe-ui.md)
- [Importare una composizione in pacchetto utilizzando l’API](./import-packaged-recipe-api.md)
