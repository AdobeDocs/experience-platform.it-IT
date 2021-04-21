---
keywords: Experience Platform;home;argomenti popolari;PSQL;psql;PostgreSQL
solution: Experience Platform
title: Creare una connessione di origine PostgreSQL nell'interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente PostgreSQL utilizzando l’interfaccia utente Adobe Experience Platform.
exl-id: e556d867-a1eb-4900-b8a9-189666a4f3f1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 1%

---

# Creare una connessione sorgente [!DNL PostgreSQL] nell&#39;interfaccia utente

I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione descrive i passaggi necessari per creare un connettore di origine [!DNL PostgreSQL] (di seguito &quot;PSQL&quot;) utilizzando l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Experience Platform] vengono organizzati i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una connessione PSQL valida, è possibile ignorare il resto del documento e procedere all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/databases.md).

### Raccogli credenziali richieste

Per accedere all&#39;account PSQL su [!DNL Platform], è necessario fornire il seguente valore:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Stringa di connessione associata all&#39;account PSQL. Il pattern della stringa di connessione PSQL è: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |

Per ulteriori informazioni su come iniziare, consulta questo [documento PSQL](https://www.postgresql.org/docs/9.2/app-psql.html).

## Collegare l&#39;account PSQL

Una volta raccolte le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account PSQL a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e seleziona **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Sources]**. Nella schermata **[!UICONTROL Catalog]** sono visualizzate diverse origini per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la categoria **[!UICONTROL Databases]**, selezionare **[!UICONTROL PostgreSQL DB]**. Se questa è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configure]**. In caso contrario, selezionare **[!UICONTROL Add data]** per creare un nuovo connettore PSQL.

![](../../../../images/tutorials/create/psql/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to PSQL]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e le credenziali PSQL. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per l&#39;impostazione della nuova connessione.

![](../../../../images/tutorials/create/psql/connect.png)

### Account esistente

Per collegare un account esistente, selezionare l&#39;account PSQL con cui si desidera connettersi, quindi selezionare **[!UICONTROL Next]** per continuare.

![](../../../../images/tutorials/create/psql/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione all&#39;account PSQL. Ora puoi continuare l’esercitazione successiva e [configurare un flusso di dati per inserire i dati in [!DNL Platform]](../../dataflow/databases.md).
