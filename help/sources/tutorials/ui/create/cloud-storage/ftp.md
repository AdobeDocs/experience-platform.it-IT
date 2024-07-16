---
keywords: Experience Platform;home;argomenti popolari;FTP;ftp
solution: Experience Platform
title: Creare una connessione Source FTP nell’interfaccia utente
type: Tutorial
description: Scopri come creare una connessione FTP di origine utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 8e505ead-4bae-43fe-830b-75620e8fba28
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# Creare una connessione FTP di origine nell’interfaccia utente

>[!NOTE]
>
>Il connettore FTP è in versione beta. Per ulteriori informazioni sull&#39;utilizzo dei connettori con etichetta beta, consulta la [Panoramica origini](../../../../home.md#terms-and-conditions).

Questo tutorial illustra i passaggi necessari per creare una connessione FTP tramite l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato in base al quale Experience Platform organizza i dati sull&#39;esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione FTP valida, puoi saltare il resto del documento e passare all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Raccogli le credenziali richieste

Per connettersi a FTP, è necessario fornire i valori per le seguenti proprietà di connessione:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `host` | Il nome o l’indirizzo IP associato al server FTP. |
| `username` | Il nome utente con accesso al server FTP. |
| `password` | La password per il server FTP. |

## Connessione al server FTP

Dopo aver raccolto le credenziali richieste, puoi creare un nuovo account FTP per connetterti a Platform seguendo la procedura riportata di seguito.

Accedi a [Adobe Experience Platform](https://platform.adobe.com), quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini per le quali è possibile creare un account in entrata con.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Nella categoria [!UICONTROL Archiviazione cloud], seleziona **[!UICONTROL FTP]**. Se è la prima volta che usi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, selezionare **[!UICONTROL Aggiungi dati]** per creare una nuova connessione FTP.

![catalogo](../../../../images/tutorials/create/ftp/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti a FTP]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato specificare un nome, una descrizione facoltativa e le credenziali. Al termine, selezionare **[!UICONTROL Connetti]** e quindi attendere un po&#39; di tempo per stabilire la nuova connessione.

![nuovo](../../../../images/tutorials/create/ftp/new.png)

### Account esistente

Per connettere un account esistente, seleziona l&#39;account FTP con cui desideri connetterti, quindi seleziona **[!UICONTROL Avanti]** per continuare.

![esistente](../../../../images/tutorials/create/ftp/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account FTP. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per portare i dati dall&#39;archiviazione cloud in Platform](../../dataflow/batch/cloud-storage.md).
