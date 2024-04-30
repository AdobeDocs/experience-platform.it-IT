---
title: Amministrazione account di attivazione espanso
description: Scopri come eseguire attività amministrative sull’account Expanded Activation, ad esempio monitorare l’utilizzo delle licenze e assegnare le autorizzazioni corrette.
source-git-commit: 5bc8d6c7173f221c2830a9b15c8ec6241e8bc59d
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Amministrazione account

Per acquisire i tipi di pubblico da Audienci Manager e attivarli nelle destinazioni social e pubblicitarie, devi innanzitutto creare un account utente per l’attivazione espansa e assegnare l’account al ruolo di autorizzazione corretto.

Questa pagina spiega come creare un account utente nell’Admin Console e assegnare le autorizzazioni corrette per l’attivazione espansa.

## Creare account utente {#create-users}

Prima di usare [!DNL Audience Manager Expanded Activation], è necessario creare un account utente.

Per creare un account utente per [!DNL Expanded Activation], seguire le istruzioni sulla gestione degli utenti da [Adobe Admin Console](https://helpx.adobe.com/it/enterprise/using/manage-users-individually.html) documentazione.

## Aggiungere utenti al ruolo di autorizzazione {#permissions}

Dopo aver creato un account utente, devi aggiungerlo al [!DNL Expanded Activation] ruolo di autorizzazione, nella [!DNL Expanded Activation] dell&#39;utente.

Vai a **[!UICONTROL Amministrazione]** -> **[!UICONTROL Autorizzazioni]** -> **[!UICONTROL Ruoli]**, e seleziona la **[!UICONTROL Ruolo predefinito di attivazione espanso]**.

![Immagine espansa dell&#39;interfaccia utente di Activation con la pagina Ruoli.](assets/expanded-activation-role.png)

Vai a **[!UICONTROL Utenti]** e seleziona **[!UICONTROL Aggiungi utenti]**.

![Immagine espansa dell&#39;interfaccia utente di Activation con la pagina Utenti.](assets/add-users.png)

Seleziona il nuovo utente creato dall’elenco disponibile e fai clic su **[!UICONTROL Salva]**.

![Immagine espansa dell&#39;interfaccia utente di Activation con la pagina Aggiungi utenti.](assets/add-user.png)

L’account utente viene ora creato e assegnato al ruolo corretto. È ora possibile accedere al **[!UICONTROL Attivazione espansa]** dell&#39;utente.

## Monitorare l’utilizzo delle licenze {#license-usage}

Il tuo [!DNL Audience Manager Expanded Activation] contratto specifica il numero massimo di e-mail con hash che è possibile acquisire nel tuo account.

Per trovare queste informazioni, vai al **[!UICONTROL Amministrazione]** -> **[!UICONTROL Utilizzo licenze]** pagina.

![Immagine espansa dell&#39;interfaccia utente di Activation che mostra la schermata di utilizzo della licenza.](assets/license-usage.png)

In questa pagina puoi trovare le seguenti informazioni:

* **[!UICONTROL Prodotto]**: il prodotto di Adobe per il quale hai la licenza. Questo sarà sempre **[!UICONTROL Audience Manager di attivazione espansa]**.
* **[!UICONTROL Metrica principale]**: nome della metrica tracciata per l’utilizzo. Questo sarà sempre **[!UICONTROL Pubblico di riferimento]**.
* **[!UICONTROL Importo licenza]**: numero massimo di e-mail con hash che puoi acquisire con licenza.

  >[!TIP]
  >
  >Le e-mail con hash vengono acquisite tramite [Connettore sorgente in Audience Manager](../sources/connectors/adobe-applications/audience-manager.md). Consulta la documentazione su [come attivare i tipi di pubblico](activate-audiences.md) per ulteriori dettagli.

* **[!UICONTROL Utilizzo]**: numero di e-mail con hash che hai acquisito.
* **[!UICONTROL % di utilizzo]**: la percentuale dell’importo della licenza utilizzata.

Per ulteriori informazioni sull’utilizzo delle licenze in Experienci Platform, consulta la sezione [documentazione sull’utilizzo delle licenze](../dashboards/guides/license-usage.md).

## Passaggi successivi {#next-steps}

Ora che hai configurato almeno un account utente con l’accesso corretto a Expanded Activation, puoi iniziare a utilizzarlo per: [attivare i tipi di pubblico](activate-audiences.md).
