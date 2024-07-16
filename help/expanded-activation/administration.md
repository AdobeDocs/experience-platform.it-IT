---
title: Amministrazione account di attivazione espanso
description: Scopri come eseguire attività amministrative sull’account Expanded Activation, ad esempio monitorare l’utilizzo delle licenze e assegnare le autorizzazioni corrette.
exl-id: ee0ec4b9-a083-447b-b7a7-e1307e90c646
source-git-commit: 2222e9fbf75f3082d331868f820247e0c0ce3ba2
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# Amministrazione account

Per acquisire i tipi di pubblico da Audience Manager e attivarli nelle destinazioni social e pubblicitarie, devi innanzitutto creare un account utente per l’attivazione espansa e assegnare l’account al ruolo di autorizzazione corretto.

Questa pagina spiega come creare un account utente nell’Admin Console e assegnare le autorizzazioni corrette per l’attivazione espansa.

## Creare account utente {#create-users}

Prima di poter utilizzare [!DNL Audience Manager Expanded Activation], è necessario creare un account utente.

Per creare un account utente per [!DNL Expanded Activation], seguire le istruzioni sulla gestione degli utenti riportate nella documentazione di [Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/manage-users-individually.html).

## Aggiungere utenti al ruolo di autorizzazione {#permissions}

Dopo aver creato un account utente, è necessario aggiungerlo al ruolo di autorizzazione [!DNL Expanded Activation] nell&#39;interfaccia utente [!DNL Expanded Activation].

Vai a **[!UICONTROL Amministrazione]** -> **[!UICONTROL Autorizzazioni]** -> **[!UICONTROL Ruoli]** e seleziona il **[!UICONTROL Ruolo predefinito di attivazione espanso]**.

![Immagine dell&#39;interfaccia utente di Attivazione espansa che mostra la pagina Ruoli.](assets/expanded-activation-role.png)

Vai alla scheda **[!UICONTROL Utenti]** e seleziona **[!UICONTROL Aggiungi utenti]**.

![Immagine dell&#39;interfaccia utente di Attivazione espansa che mostra la pagina Utenti.](assets/add-users.png)

Selezionare il nuovo utente creato dall&#39;elenco disponibile e selezionare **[!UICONTROL Salva]**.

![Immagine dell&#39;interfaccia utente di Attivazione espansa che mostra la pagina Aggiungi utenti.](assets/add-user.png)

L’account utente viene ora creato e assegnato al ruolo corretto. È ora possibile accedere all&#39;interfaccia utente di **[!UICONTROL Expanded Activation]**.

## Monitorare l’utilizzo delle licenze {#license-usage}

Il contratto [!DNL Audience Manager Expanded Activation] specifica il numero massimo di e-mail con hash che è possibile acquisire nel tuo account.

Per trovare queste informazioni, vai alla pagina **[!UICONTROL Amministrazione]** -> **[!UICONTROL Utilizzo licenze]**.

![Immagine dell&#39;interfaccia utente di Attivazione espansa che mostra la schermata di utilizzo della licenza.](assets/license-usage.png)

In questa pagina puoi trovare le seguenti informazioni:

* **[!UICONTROL Prodotto]**: il prodotto di Adobe per il quale hai la licenza. Sarà sempre **[!UICONTROL Audience Manager di attivazione espansa]**.
* **[!UICONTROL Metrica primaria]**: nome della metrica di cui si tiene traccia per l&#39;utilizzo. Questo sarà sempre **[!UICONTROL pubblico indirizzabile]**.
* **[!UICONTROL Importo licenza]**: numero massimo di e-mail con hash che si è autorizzati ad acquisire.

  >[!TIP]
  >
  >Le e-mail con hash vengono acquisite tramite il [connettore di origine Audience Manager](../sources/connectors/adobe-applications/audience-manager.md). Per ulteriori dettagli, consulta la documentazione su [come attivare i tipi di pubblico](activate-audiences.md).

* **[!UICONTROL Utilizzo]**: il numero di e-mail con hash che hai acquisito.
* **[!UICONTROL Utilizzo %]**: la percentuale della quantità di licenza utilizzata.

Per ulteriori informazioni sull&#39;utilizzo delle licenze in Experience Platform, consulta la [documentazione sull&#39;utilizzo delle licenze](../dashboards/guides/license-usage.md).

## Passaggi successivi {#next-steps}

Ora che hai configurato almeno un account utente con l&#39;accesso corretto a Expanded Activation (Attivazione espansa), puoi iniziare a utilizzare l&#39;account per [attivare tipi di pubblico](activate-audiences.md).
