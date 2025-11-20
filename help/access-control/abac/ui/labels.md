---
keywords: Experience Platform;home;argomenti popolari;controllo degli accessi;controllo degli accessi basato su attributi;ABAC;;home;popular topic;access control;attribute-based access control;ABAC
title: Etichette di gestione del controllo dell'accesso basate su attributi
description: Questo documento fornisce informazioni sulla gestione delle etichette tramite l’interfaccia Autorizzazioni in Adobe Experience Cloud
exl-id: c790f09c-fda6-48bf-95db-3f5053cd882e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 26%

---

# Gestire le etichette

>[!NOTE]
>
>Per creare o visualizzare attributi calcolati con campi contenenti una determinata etichetta, è necessario avere accesso a tale etichetta.

Le etichette consentono di categorizzare set di dati e campi in base ai criteri di utilizzo e di accesso applicabili a tali dati. Le etichette possono essere applicate in qualsiasi momento, offrendo flessibilità nella scelta di come gestire i dati. Le best practice incoraggiano i dati di etichettatura non appena vengono acquisiti in Experience Platform o non appena i dati diventano disponibili per l’utilizzo in Experience Platform.

## Creare una nuova etichetta {#create-new-label}

>[!CONTEXTUALHELP]
>id="platform_abac_labelusage"
>title="Utilizzo delle etichette"
>abstract="Puoi utilizzare etichette personalizzate per applicare ai dati configurazioni di governance dei dati e di controllo degli accessi."

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="Creare una nuova etichetta"
>abstract="Puoi creare etichette personalizzate per adattarle alle esigenze della tua organizzazione. Le etichette personalizzate possono essere utilizzate per applicare ai dati sia le configurazioni di governance dei dati che di controllo degli accessi."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=it#manage-labels" text="Gestire le etichette personalizzate"

>[!NOTE]
>
>Esiste un unico elenco di etichette per un’intera organizzazione. Per creare un&#39;etichetta personalizzata, sono necessarie le autorizzazioni **[!UICONTROL Manage Usage Labels]** per la sandbox di produzione. L&#39;eliminazione delle etichette non è attualmente supportata.

Per creare una nuova etichetta, selezionare la scheda **[!UICONTROL Labels]** nella barra laterale e selezionare **[!UICONTROL Create Label]**.

![flac-new-label](../../images/flac-ui/create-label.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Create a new label]** in cui viene richiesto di immettere un nome, un nome descrittivo facoltativo e una descrizione facoltativa.

![new-label-info](../../images/flac-ui/new-label-info.png)

Al termine, selezionare **[!UICONTROL Confirm]**.
