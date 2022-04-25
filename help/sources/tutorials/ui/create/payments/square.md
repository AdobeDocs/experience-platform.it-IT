---
keywords: Experience Platform;home;argomenti popolari;quadrato;quadrato
title: Creare una connessione sorgente quadrata nell’interfaccia utente
description: Scopri come creare una connessione sorgente quadrata utilizzando l’interfaccia utente di Adobe Experience Platform.
source-git-commit: e905b11040c8de33aa757bd5743605bb36a8009b
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 2%

---

# Crea un [!DNL Square] connessione sorgente nell’interfaccia utente

Questa esercitazione fornisce i passaggi per la creazione di un [!DNL Square] connettore di origine tramite l’interfaccia utente di Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il quadro standardizzato [!DNL Experience Platform] organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’Editor di schema](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

### Raccogli credenziali richieste

Per accedere al tuo [!DNL Square] piattaforma account, devi fornire i seguenti valori:

| Credenziali | Descrizione |
| --- | --- |
| Host | L’URL della [!DNL Square] istanza. |
| ID client | L&#39;ID client associato al [!DNL Square] conto. |
| Segreto client | Il segreto client associato al tuo [!DNL Square] conto. |
| Token di accesso | Il token di accesso viene utilizzato per autenticare il [!DNL Square] account con autenticazione OAuth 2.0. Il token di accesso può essere ottenuto da [!DNL Square]. |
| Aggiorna token | Il token di aggiornamento viene utilizzato per generare nuovi token di accesso una volta scaduto il token di accesso corrente. Il token di aggiornamento può essere ottenuto da [!DNL Square]. |

Per ulteriori informazioni su queste credenziali e su come ottenerle, consulta la [[!DNL Square] documentazione su OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

Una volta raccolte le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo [!DNL Square] a Platform.

## Collega il tuo [!DNL Square] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in viene visualizzata una varietà di sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la [!UICONTROL Pagamenti] categoria, seleziona **[!UICONTROL Quadrato]**, quindi seleziona **[!UICONTROL Aggiungi dati]**.

![catalogo](../../../../images/tutorials/create/square/catalog.png)

La **[!UICONTROL Connetti a quadrato]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL Square] account con cui si desidera creare un nuovo flusso di dati, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/square/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome, una descrizione facoltativa e i valori appropriati per il tuo [!DNL Square] credenziali. Al termine, seleziona **[!UICONTROL Connetti alla sorgente]** e quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

![nuovo](../../../../images/tutorials/create/square/new.png)

## Passaggi successivi

Seguendo questa esercitazione, hai autenticato e creato una connessione sorgente tra [!DNL Square] account e piattaforma. Ora puoi passare all’esercitazione successiva e [creare un flusso di dati per inserire i dati di pagamento in Platform](../../dataflow/payments.md).
