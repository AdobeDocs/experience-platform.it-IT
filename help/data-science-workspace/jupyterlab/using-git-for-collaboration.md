---
keywords: Experience Platform;JupyterLab;notebook;Data Science Workspace;argomenti popolari;Git;Github
solution: Experience Platform
title: Collaborare in JupyterLab utilizzando Git
type: Tutorial
description: Git è un sistema distribuito di controllo della versione per il tracciamento delle modifiche nel codice sorgente durante lo sviluppo del software. Git è preinstallato nell’ambiente JupyterLab di Data Science Workspace.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 1%

---

# Collabora in [!DNL JupyterLab] utilizzando [!DNL Git]

[!DNL Git] è un sistema distribuito di controllo della versione per il rilevamento delle modifiche nel codice sorgente durante lo sviluppo del software. Git è preinstallato nell&#39;ambiente [!DNL Data Science Workspace JupyterLab].

## Prerequisiti

>[!NOTE]
>
> Il server Git che intendi utilizzare deve essere accessibile tramite Internet.

L&#39;ambiente [!DNL Data Science Workspace JupyterLab] è un ambiente ospitato e non distribuito all&#39;interno del firewall aziendale. Il server Git a cui ci si connette deve pertanto essere accessibile da Internet. Potrebbe trattarsi di un archivio pubblico o privato su [GitHub](https://github.com/) o di un&#39;altra istanza di un server [!DNL Git] che si è deciso di ospitare.

## Connetti [!DNL Git] all&#39;ambiente [!DNL Data Science Workspace JupyterLab Notebooks]

Avviare [!DNL Adobe Experience Platform] e passare all&#39;ambiente [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab).

In [!DNL JupyterLab], seleziona **[!UICONTROL File]**, quindi passa il puntatore del mouse su **[!UICONTROL Nuovo]**. Dal menu a discesa visualizzato, selezionare **[!UICONTROL Terminal]**.

![Navigazione JupyterLab](../images/jupyterlab/tutorials/open-terminal.png)

Successivamente, all&#39;interno di *Terminal*, passare all&#39;area di lavoro utilizzando il comando seguente: `cd my-workspace`.

![area di lavoro cd](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Per visualizzare un elenco dei comandi Git disponibili, esegui il comando: `git -help` nel terminale.

Clonare quindi l&#39;archivio che si desidera utilizzare utilizzando il comando `git clone`. Clonare il progetto utilizzando un URL `https://` anziché `ssh://`.

**Esempio**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clone](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Per eseguire le operazioni di scrittura (`git push`, ad esempio), è necessario eseguire i seguenti comandi di configurazione per ogni nuova sessione. Inoltre, qualsiasi comando push richiede un nome utente e una password.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Passaggi successivi

Dopo aver completato la clonazione dell’archivio, puoi utilizzare Git come di consueto sul computer locale per collaborare con altri utenti sui notebook. Per ulteriori informazioni sulle operazioni possibili in [!DNL JupyterLab], vedere [[!DNL JupyterLab user guide]](./overview.md).
