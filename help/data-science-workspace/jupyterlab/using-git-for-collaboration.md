---
keywords: ' Experience Platform;JupyterLab;notebook;Data Science Workspace;argomenti più comuni;Git;Github'
solution: Experience Platform
title: Collaborazione in JupyterLab tramite Git
topic: tutorial
type: Tutorial
description: Git è un sistema distribuito di controllo delle versioni per tenere traccia delle modifiche apportate al codice sorgente durante lo sviluppo del software. Git è preinstallato nell’ambiente Data Science Workspace JupyterLab.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---


# Collaborare in [!DNL JupyterLab] utilizzando [!DNL Git]

[!DNL Git] è un sistema distribuito di controllo della versione per tenere traccia delle modifiche apportate al codice sorgente durante lo sviluppo del software. Git è preinstallato nell&#39;ambiente [!DNL Data Science Workspace JupyterLab].

## Prerequisiti

>[!NOTE]
>
> Il server Git che si intende utilizzare deve essere accessibile tramite Internet.

L&#39;ambiente [!DNL Data Science Workspace JupyterLab] è un ambiente ospitato e non è implementato all&#39;interno del firewall aziendale, pertanto il server Git a cui ci si collega deve essere accessibile da Internet pubblico. Può trattarsi di un repository pubblico o privato su [GitHub](https://github.com/) o su un&#39;altra istanza di un server [!DNL Git] che si è deciso di ospitare.

## Connetti [!DNL Git] all&#39;ambiente [!DNL Data Science Workspace JupyterLab Notebooks]

Per iniziare, avvia [!DNL Adobe Experience Platform] e passa all&#39;ambiente [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab).

In [!DNL JupyterLab], selezionare **[!UICONTROL File]**, quindi passare il mouse su **[!UICONTROL New]**. Dal menu a discesa visualizzato, selezionate **[!UICONTROL Terminal]**.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

Quindi, all&#39;interno di *Terminal* passare all&#39;area di lavoro utilizzando il seguente comando: `cd my-workspace`.

![spazio su cd](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Per visualizzare un elenco dei comandi git disponibili, esegui il comando: `git -help` all&#39;interno del terminale.

Quindi, duplicare il repository che si desidera utilizzare con il comando `git clone`. Duplica il progetto utilizzando un URL `https://` anziché `ssh://`.

**Esempio**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clone](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Per eseguire qualsiasi operazione di scrittura (`git push` ad esempio), è necessario eseguire i seguenti comandi di configurazione per ogni nuova sessione. Inoltre, qualsiasi comando push richiede un nome utente e una password.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Passaggi successivi

Dopo aver completato la duplicazione del repository, è possibile utilizzare Git come si farebbe normalmente sul computer locale per collaborare con altri utenti su notebook. Per ulteriori informazioni sulle operazioni che è possibile eseguire all&#39;interno di [!DNL JupyterLab], vedere la sezione [[!DNL JupyterLab user guide]](./overview.md).
