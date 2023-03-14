---
keywords: Experience Platform;JupyterLab;notebook;Data Science Workspace;argomenti popolari;Git;Github
solution: Experience Platform
title: Collaborare in JupyterLab utilizzando Git
type: Tutorial
description: Git è un sistema distribuito di controllo della versione per il tracciamento delle modifiche nel codice sorgente durante lo sviluppo del software. Git è preinstallato nell’ambiente JupyterLab di Data Science Workspace.
exl-id: d7b766f7-b97d-4007-bc53-b83742425047
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 1%

---

# Collaborare in [!DNL JupyterLab] utilizzo [!DNL Git]

[!DNL Git] è un sistema di controllo della versione distribuito per il monitoraggio delle modifiche al codice sorgente durante lo sviluppo del software. Git è preinstallato all&#39;interno di [!DNL Data Science Workspace JupyterLab] ambiente.

## Prerequisiti

>[!NOTE]
>
> Il server Git che intendi utilizzare deve essere accessibile tramite Internet.

Il [!DNL Data Science Workspace JupyterLab] L’ambiente è un ambiente in hosting e non viene distribuito all’interno del firewall aziendale; pertanto, il server Git a cui ti connetti deve essere accessibile da Internet pubblica. Questo potrebbe essere un archivio pubblico o privato su [GitHub](https://github.com/) o un&#39;altra istanza di un [!DNL Git] server che hai deciso di ospitare autonomamente.

## Connetti [!DNL Git] al [!DNL Data Science Workspace JupyterLab Notebooks] ambiente

Inizia avviando [!DNL Adobe Experience Platform] e navigando su [[!DNL JupyterLabs Notebooks]](https://platform.adobe.com/notebooks/jupyterLab) ambiente.

Entro [!DNL JupyterLab], seleziona **[!UICONTROL File]** quindi passa il cursore sopra **[!UICONTROL Nuovo]**. Dal menu a discesa visualizzato, seleziona **[!UICONTROL Terminale]**.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

Avanti, entro *Terminale* passa all&#39;area di lavoro utilizzando il comando seguente: `cd my-workspace`.

![area di lavoro cd](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
>
> Per visualizzare un elenco dei comandi Git disponibili, esegui il comando: `git -help` nel tuo terminale.

Quindi, clona l’archivio che desideri utilizzare utilizzando `git clone` comando. Clona il progetto utilizzando un `https://` URL anziché `ssh://`.

**Esempio**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clone](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
>
> Per eseguire operazioni di scrittura (`git push` ad esempio) per ogni nuova sessione è necessario eseguire i seguenti comandi di configurazione. Inoltre, qualsiasi comando push richiede un nome utente e una password.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Passaggi successivi

Dopo aver completato la clonazione dell’archivio, puoi utilizzare Git come di consueto sul computer locale per collaborare con altri utenti sui notebook. Per ulteriori informazioni su cosa è possibile fare in [!DNL JupyterLab], vedere [[!DNL JupyterLab user guide]](./overview.md).
