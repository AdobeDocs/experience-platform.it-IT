---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;Git;Github
solution: Experience Platform
title: Collaborazione in JupyterLab tramite Git
topic: Tutorial
translation-type: tm+mt
source-git-commit: c48079ba997a7b4c082253a0b2867df76927aa6d
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 1%

---


# Collaborazione in [!DNL JupyterLab] uso [!DNL Git]

[!DNL Git] è un sistema distribuito di controllo della versione per tenere traccia delle modifiche apportate al codice sorgente durante lo sviluppo del software. Git è preinstallato nell&#39; [!DNL Data Science Workspace JupyterLab] ambiente.

## Prerequisiti

>[!NOTE]
> Il server Git che si intende utilizzare deve essere accessibile tramite Internet.

L&#39; [!DNL Data Science Workspace JupyterLab] ambiente è un ambiente ospitato e non è implementato all&#39;interno del firewall aziendale, pertanto il server Git a cui ci si collega deve essere accessibile da Internet pubblico. Può trattarsi di un repository pubblico o privato su [GitHub](https://github.com/) o di un&#39;altra istanza di un [!DNL Git] server che hai deciso di ospitare.

## Connessione [!DNL Git] all&#39; [!DNL Data Science Workspace JupyterLab Notebooks] ambiente

Per iniziare, avvia [!DNL Adobe Experience Platform] e passa all&#39; [!DNL JupyterLabs Notebooks](https://platform.adobe.com/notebooks/jupyterLab) ambiente.

Entro [!DNL JupyterLab], selezionate **[!UICONTROL File]** quindi passate il mouse **[!UICONTROL New]**. Dal menu a discesa visualizzato, selezionate **[!UICONTROL Terminal]**.

![JupyterLab Nav](../images/jupyterlab/tutorials/open-terminal.png)

Quindi, all&#39;interno del *terminale* , andate all&#39;area di lavoro utilizzando il seguente comando: `cd my-workspace`.

![spazio su cd](../images/jupyterlab/tutorials/find-workspace.png)

>[!TIP]
> Per visualizzare un elenco dei comandi git disponibili, esegui il comando: `git -help` all&#39;interno del terminale.

Quindi, clonate il repository che desiderate utilizzare con il `git clone` comando. Duplica il progetto utilizzando un `https://` URL anziché `ssh://`.

**Esempio**:

`git clone https://github.com/adobe/experience-platform-dsw-reference.git`

![clone](../images/jupyterlab/tutorials/git-collaboration.png)

>[!NOTE]
> Per eseguire qualsiasi operazione di scrittura (`git push` ad esempio), è necessario eseguire i seguenti comandi di configurazione per ogni nuova sessione. Inoltre, qualsiasi comando push richiede un nome utente e una password.
>
>`git config --global user.email "you@example.com"`
>
>`git config --global user.name "Your Name"`

## Passaggi successivi

Dopo aver completato la duplicazione del repository, è possibile utilizzare Git come si farebbe normalmente sul computer locale per collaborare con altri utenti su notebook. Per ulteriori informazioni sulle operazioni che è possibile eseguire all’interno [!DNL JupyterLab], consulta la sezione [!DNL JupyterLab user guide](./overview.md).
