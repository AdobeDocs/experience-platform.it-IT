---
keywords: Experience Platform;home;argomenti popolari;Oracle DB;oracle db
solution: Experience Platform
title: Creare una connessione sorgente del database di Oracle nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente Oracle DB utilizzando l’interfaccia utente Adobe Experience Platform.
exl-id: 4ca6ecc6-0382-4cee-acc5-1dec7eeb9443
translation-type: tm+mt
source-git-commit: b2384bfe26fa3d111c342062b2d9bb37c4226857
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 1%

---

# Creare una connessione sorgente [!DNL Oracle DB] nell&#39;interfaccia utente

I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione descrive i passaggi necessari per creare un connettore sorgente [!DNL Oracle DB] utilizzando l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL Oracle DB] valida, puoi saltare il resto del documento e continuare l&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli credenziali richieste

Per accedere al tuo account [!DNL Oracle DB] su [!DNL Platform], devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Stringa di connessione utilizzata per la connessione a [!DNL Oracle DB]. Il pattern della stringa di connessione [!DNL Oracle DB] è: `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | Identificatore univoco necessario per creare una connessione. L&#39;ID della specifica di connessione per [!DNL Oracle DB] è `d6b52d86-f0f8-475f-89d4-ce54c8527328`. |

Per ulteriori informazioni su come iniziare, consulta [questo documento di Oracle](https://docs.oracle.com/database/121/ODPNT/featConnecting.htm#ODPNT199).

## Connetti il tuo account [!DNL Oracle DB]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account [!DNL Oracle DB] per connetterti a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e seleziona **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Sources]**. Nella schermata **[!UICONTROL Catalog]** sono visualizzate diverse origini per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la categoria **[!UICONTROL Databases]**, selezionare **[!UICONTROL Oracle DB]**. Se questa è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configure]**. In caso contrario, seleziona **[!UICONTROL Add data]** per creare un nuovo connettore [!DNL Oracle DB].

![catalogo](../../../../images/tutorials/create/oracle/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Oracle DB]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali [!DNL Oracle DB]. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per l&#39;impostazione della nuova connessione.

![connect](../../../../images/tutorials/create/oracle/new.png)

### Account esistente

Per collegare un account esistente, selezionare l&#39;account [!DNL Oracle DB] con cui si desidera connettersi, quindi selezionare **[!UICONTROL Next]** per continuare.

![esistente](../../../../images/tutorials/create/oracle/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Oracle DB] . Ora puoi continuare l’esercitazione successiva e [configurare un flusso di dati per inserire i dati in [!DNL Platform]](../../dataflow/databases.md).
