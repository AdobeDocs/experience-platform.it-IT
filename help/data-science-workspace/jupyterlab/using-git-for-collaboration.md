---
keywords: Experience Platform;JupyterLab;notebook;Data Science Workspace;argomenti comuni;Git;Github
solution: Experience Platform
title: Collaborare in JupyterLab utilizzando Git
topic-legacy: tutorial
type: Tutorial
description: Git è un sistema distribuito di controllo della versione per tenere traccia delle modifiche nel codice sorgente durante lo sviluppo del software. Git è preinstallato nell’ambiente JupyterLab di Data Science Workspace.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# Collabora in [!DNL JupyterLab] utilizzando [!DNL Git]

[!DNL Git] è un sistema distribuito di controllo della versione per tenere traccia delle modifiche nel codice sorgente durante lo sviluppo del software. Git è preinstallato nell’ambiente [!DNL Data Science Workspace JupyterLab].

## Prerequisiti

>[!NOTE]
>
> Il server Git che intendi utilizzare deve essere accessibile via Internet.

L’ambiente [!DNL Data Science Workspace JupyterLab] è un ambiente in hosting e non è implementato all’interno del firewall aziendale, pertanto il server Git a cui ti connetti deve essere accessibile dall’Internet pubblico. Potrebbe trattarsi di un archivio pubblico o privato su [GitHub](https://github.com/) o di un&#39;altra istanza di un server [!DNL Git] che hai deciso di ospitare.

## Connetti [!DNL Git] all&#39;ambiente [!DNL Data Science Workspace JupyterLab Notebooks]

Per iniziare, avvia [!DNL Adobe Experience Platform] e passa all&#39;ambiente [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab).

In [!DNL JupyterLab], seleziona **[!UICONTROL File]** e passa il puntatore del mouse su **[!UICONTROL New]**. Dal menu a discesa visualizzato, seleziona **[!UICONTROL Terminal]**.

![Navigazione JupyterLab](../images/jupyterlab/tutorials/open-terminal.png)

Quindi, all&#39;interno di *Terminal* accedi all&#39;area di lavoro utilizzando il seguente comando: `cd my-workspace`.

![spazio dei cd](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Per visualizzare un elenco dei comandi Git disponibili, esegui il comando: `git -help` all&#39;interno del terminale.

Quindi, clonare l&#39;archivio che si desidera utilizzare utilizzando il comando `git clone`. Clona il progetto utilizzando un URL `https://` anziché `ssh://`.

**Esempio**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clone](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Per eseguire eventuali operazioni di scrittura (`git push` ad esempio), è necessario eseguire i seguenti comandi di configurazione per ogni nuova sessione. Inoltre, qualsiasi comando push richiede un nome utente e una password.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Passaggi successivi

Dopo aver completato la clonazione dell’archivio, puoi utilizzare Git come faresti normalmente sul computer locale per collaborare con altri su notebook. Per ulteriori informazioni sulle operazioni che è possibile eseguire all&#39;interno di [!DNL JupyterLab], consulta la sezione [[!DNL JupyterLab user guide]](./overview.md).
