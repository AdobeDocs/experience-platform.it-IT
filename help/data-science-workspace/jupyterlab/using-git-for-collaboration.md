---
keywords: Experience Platform;JupyterLab;notebook;Data Science Workspace;argomenti comuni;Git;Github
solution: Experience Platform
title: Collaborare in JupyterLab utilizzando Git
type: Tutorial
description: Git è un sistema distribuito di controllo della versione per tenere traccia delle modifiche nel codice sorgente durante lo sviluppo del software. Git è preinstallato nell’ambiente JupyterLab di Data Science Workspace.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# Collabora in [!DNL JupyterLab] utilizzo [!DNL Git]

[!DNL Git] è un sistema distribuito di controllo della versione per tenere traccia delle modifiche nel codice sorgente durante lo sviluppo del software. Git è preinstallato all’interno di [!DNL Data Science Workspace JupyterLab] ambiente.

## Prerequisiti

>[!NOTE]
>
> Il server Git che intendi utilizzare deve essere accessibile via Internet.

La [!DNL Data Science Workspace JupyterLab] l’ambiente è un ambiente in hosting e non è implementato all’interno del firewall aziendale, pertanto il server Git a cui ti connetti deve essere accessibile dall’Internet pubblico. Questo potrebbe essere un archivio pubblico o privato su [GitHub](https://github.com/) o un&#39;altra istanza di un [!DNL Git] server che hai deciso di ospitare.

## Connetti [!DNL Git] al [!DNL Data Science Workspace JupyterLab Notebooks] ambiente

Inizia con l&#39;avvio [!DNL Adobe Experience Platform] e la navigazione al [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab) ambiente.

Within [!DNL JupyterLab], seleziona **[!UICONTROL File]** quindi passa il mouse **[!UICONTROL Nuovo]**. Dal menu a discesa visualizzato, seleziona **[!UICONTROL Terminale]**.

![Navigazione JupyterLab](../images/jupyterlab/tutorials/open-terminal.png)

Avanti, entro *Terminale* accedere all’area di lavoro utilizzando il seguente comando: `cd my-workspace`.

![spazio dei cd](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Per visualizzare un elenco dei comandi Git disponibili, esegui il comando: `git -help` all&#39;interno del Terminal.

Quindi, duplica l’archivio che desideri utilizzare con il `git clone` comando. Clona il progetto utilizzando un’ `https://` URL anziché `ssh://`.

**Esempio**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clone](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Per eseguire eventuali operazioni di scrittura (`git push` ad esempio) è necessario eseguire i seguenti comandi di configurazione per ogni nuova sessione. Inoltre, qualsiasi comando push richiede un nome utente e una password.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Passaggi successivi

Dopo aver completato la clonazione dell’archivio, puoi utilizzare Git come faresti normalmente sul computer locale per collaborare con altri su notebook. Per ulteriori informazioni su cosa è possibile fare in [!DNL JupyterLab], vedi [[!DNL JupyterLab user guide]](./overview.md).
