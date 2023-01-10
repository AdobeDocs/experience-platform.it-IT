---
keywords: Experience Platform;home;argomenti popolari;BLOB di Azure;BLOB di azzurro;Connettore BLOB di Azure
solution: Experience Platform
title: Creare una connessione Azure Blob Source nell’interfaccia utente
type: Tutorial
description: Scopri come creare un connettore sorgente BLOB di Azure utilizzando l’interfaccia utente di Platform.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 1%

---

# Crea un [!DNL Azure Blob] connessione sorgente nell’interfaccia utente

Questa esercitazione descrive i passaggi necessari per creare un [!DNL Azure Blob] (in appresso denominato &quot;[!DNL Blob]&quot;) utilizzando l’interfaccia utente di Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   - [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione sull’Editor di schema](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una [!DNL Blob] è possibile ignorare il resto del documento e passare all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Formati di file supportati

[!DNL Experience Platform] supporta i seguenti formati di file da acquisire da archivi esterni:

- Valori separati da delimitatore (DSV): Il supporto per i file di dati formattati DSV è attualmente limitato ai valori separati da virgole. Il valore delle intestazioni di campo all&#39;interno dei file formattati DSV deve essere costituito solo da caratteri alfanumerici e caratteri di sottolineatura. Il supporto per i file DSV generali verrà fornito in futuro.
- Notazione oggetto JavaScript (JSON): I file di dati formattati JSON devono essere conformi a XDM.
- Parquet Apache: I file di dati formattati per il parquet devono essere conformi a XDM.

### Raccogli credenziali richieste

Per accedere al tuo [!DNL Blob] su Platform, è necessario fornire un valore valido per le seguenti credenziali:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Una stringa contenente le informazioni di autorizzazione necessarie per l&#39;autenticazione [!DNL Blob] all&#39;Experience Platform. La [!DNL Blob] pattern di stringa di connessione: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Per ulteriori informazioni sulle stringhe di connessione, consulta [!DNL Blob] documento [configurazione di stringhe di connessione](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | URI della firma di accesso condiviso che è possibile utilizzare come tipo di autenticazione alternativo per collegare il [!DNL Blob] conto. La [!DNL Blob] Pattern URI SAS: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Per ulteriori informazioni, consulta [!DNL Blob] documento [URI della firma di accesso condiviso](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |

## Collega il tuo [!DNL Blob] account

Una volta raccolte le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo [!DNL Blob] a Platform.

In [Interfaccia utente della piattaforma](https://platform.adobe.com), seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in questa schermata vengono visualizzate diverse sorgenti per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando la barra di ricerca.

Sotto la [!UICONTROL archiviazione cloud] categoria, seleziona **[!UICONTROL Archiviazione BLOB di Azure]**, quindi seleziona **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/blob/catalog.png)

La **[!UICONTROL Connetti all’archiviazione BLOB di Azure]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL Blob] account con cui si desidera creare un nuovo flusso di dati, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/blob/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome e una descrizione delle opzioni per il nuovo [!DNL Blob] conto.

**Autenticazione tramite una stringa di connessione**

La [!DNL Blob] connettore fornisce diversi tipi di autenticazione per l’accesso. Sotto [!UICONTROL Autenticazione account] select **[!UICONTROL ConnectionString]** per utilizzare le credenziali basate su stringhe di connessione.

![stringa di connessione](../../../../images/tutorials/create/blob/connectionstring.png)

**Autenticazione tramite un URI di firma di accesso condiviso**

Un URI di firma di accesso condiviso (SAS) consente un&#39;autorizzazione delegata sicura al tuo [!DNL Blob] conto. È possibile utilizzare SAS per creare credenziali di autenticazione con diversi gradi di accesso, in quanto un&#39;autenticazione basata su SAS consente di impostare autorizzazioni, date di inizio e scadenza, nonché disposizioni per risorse specifiche.

Seleziona **[!UICONTROL AutenticazioneSasURIA]** e quindi fornire [!DNL Blob] URI SAS Seleziona **[!UICONTROL Connetti alla sorgente]** per procedere.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo [!DNL Blob] conto. Ora puoi passare all’esercitazione successiva e [configurare un flusso di dati per l’importazione di dati dall’archiviazione cloud in Platform](../../dataflow/batch/cloud-storage.md).
