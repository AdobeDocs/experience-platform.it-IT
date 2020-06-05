---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore sorgente Salesforce nell’interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 44c43afc653c147fa12e3e962904bfc79ee0fc64
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 1%

---


# Creare un connettore sorgente Salesforce nell’interfaccia utente

I connettori di origine in Adobe Experience Platform consentono di acquisire dati CRM di origine esterna su base programmata. Questa esercitazione fornisce i passaggi per la creazione di un connettore sorgente Salesforce utilizzando l&#39;interfaccia utente della piattaforma.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standardizzato tramite il quale Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di un account Salesforce valido, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/crm.md).

### Raccogli credenziali richieste

| Credenziali | Descrizione |
| ---------- | ----------- |
| `environmentUrl` | URL dell’istanza di origine Salesforce. |
| `username` | Nome utente per l’account utente Salesforce. |
| `password` | La password dell’account utente Salesforce. |
| `securityToken` | Token di sicurezza per l’account utente Salesforce. |

Per ulteriori informazioni su come iniziare, consulta [questo documento](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm)Salesforce.

## Collegamento dell&#39;account Salesforce

Dopo aver raccolto le credenziali necessarie, puoi seguire i passaggi descritti di seguito per creare un nuovo account Salesforce per la connessione alla piattaforma.

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; *[!UICONTROL Sources]* area di lavoro. Nella *[!UICONTROL Catalog]* schermata sono visualizzate diverse origini con le quali è possibile creare un account in entrata e ogni origine mostra il numero di account e flussi di dati esistenti associati a tali account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la *[!UICONTROL Databases]* categoria, seleziona **[!UICONTROL Salesforce]** fai clic **sull&#39;icona + (+)** per creare un nuovo connettore Salesforce.

![catalogo](../../../../images/tutorials/create/salesforce/catalog.png)

Viene *[!UICONTROL Connect to Salesforce]* visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, specifica la connessione con un nome, una descrizione facoltativa e le credenziali Salesforce. Al termine, selezionate **[!UICONTROL Connect]** e concedete un po&#39; di tempo per l&#39;impostazione del nuovo account.

![connect](../../../../images/tutorials/create/salesforce/new.png)

### Account esistente

Per collegare un account esistente, seleziona l&#39;account Salesforce con cui vuoi connetterti, quindi seleziona **[!UICONTROL Next]** nell&#39;angolo superiore destro per proseguire.

![esistenti](../../../../images/tutorials/create/salesforce/existing.png)

## Passaggi successivi

Seguendo questa esercitazione hai stabilito una connessione al tuo account Salesforce. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per l’inserimento di dati nella piattaforma](../../dataflow/crm.md).