---
keywords: Experience Platform;interfaccia utente;dashboard;dashboard;profili;segmenti;destinazioni;utilizzo licenze;user interface;UI;dashboards;dashboard;profiles;segments;destinations
title: Modifica schema per creare widget per dashboard personalizzati
description: Questa guida fornisce istruzioni dettagliate per selezionare gli attributi e configurare lo schema dell’organizzazione per creare widget personalizzati per le dashboard di Adobe Experience Platform.
exl-id: a744eb24-5ba7-4971-9183-3f891e807863
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# Modifica lo schema per creare widget personalizzati

Per creare widget personalizzati per le dashboard di Adobe Experience Platform, è necessario innanzitutto identificare gli attributi del profilo cliente in tempo reale su cui saranno basati i widget.

Questa guida fornisce istruzioni dettagliate per modificare lo schema dell’organizzazione selezionando gli attributi per creare widget del dashboard personalizzati.

Dopo aver selezionato gli attributi e configurato lo schema, puoi procedere con i passaggi per [creazione di widget personalizzati per le dashboard](custom-widgets.md).

>[!NOTE]
>
>Per poter modificare lo schema, gli utenti devono disporre dell’autorizzazione &quot;Manage Standard Dashboards&quot; (Gestione dashboard standard). Per i passaggi sulla concessione delle autorizzazioni di accesso per le dashboard, consulta [guida alle autorizzazioni della dashboard](../permissions.md).

## Libreria widget {#widget-library}

Questa guida richiede l’accesso a [!UICONTROL Libreria widget] all’interno di Experience Platform. Per ulteriori informazioni sulla libreria dei widget e su come accedervi nell’interfaccia utente, leggi [panoramica della libreria widget](widget-library.md).

## Modifica di uno schema

All’interno della libreria dei widget, il **[!UICONTROL Personalizzato]** Questa scheda consente di creare widget e condividerli con altri utenti dell’organizzazione per personalizzare l’aspetto delle dashboard.

Prima di poter creare widget personalizzati, è necessario selezionare gli attributi Real-Time Customer Profile per garantire che i dati vengano inclusi come parte dello snapshot giornaliero.

>[!IMPORTANT]
>
>La tua organizzazione può selezionare un massimo di 20 attributi.

Se la tua organizzazione non ha selezionato alcun attributo di profilo, inizia selezionando **[!UICONTROL Configura]** al centro dello schermo.

![La scheda Custom (Personalizzato) dell’area di lavoro della libreria widget con l’opzione Configure evidenziata.](../images/customization/configure-schema.png)

Quando è stato creato almeno un attributo personalizzato, seleziona **[!UICONTROL Modifica schema]** per visualizzare gli attributi selezionati e aggiungerne altri.

![La scheda Custom (Personalizzato) dell’area di lavoro della libreria widget con Modifica schema evidenziato.](../images/customization/edit-schema.png)

## Seleziona un attributo

Per selezionare un attributo in **[!UICONTROL Seleziona campo schema di unione]** , passa all’attributo nello schema di unione (o utilizza la funzione di ricerca) e seleziona la casella di controllo accanto all’attributo. Selezionando la casella di controllo, l’attributo viene aggiunto anche al **[!UICONTROL Attributi selezionati]** nella parte destra della finestra di dialogo.

>[!NOTE]
>
>Affinché un attributo sia visibile per la selezione, deve essere uno dei seguenti: String, Date, Date-Time, Boolean, Short, Long, Integer o Byte. I tipi di dati Map (Mappa) e Double (Doppio) non sono supportati e sono disattivati e non possono essere selezionati.

Dopo aver scelto gli attributi da aggiungere, seleziona **[!UICONTROL Salva]** per salvare gli attributi e tornare alla scheda widget personalizzati.

>[!WARNING]
>Gli attributi appena selezionati diventano disponibili dopo lo snapshot giornaliero successivo all’aggiornamento dei dati.

![La finestra di dialogo per selezionare gli attributi dello schema con gli attributi e Salva evidenziati.](../images/customization/select-attribute.png)

## Passaggi successivi

Dopo aver letto questa guida, puoi passare alla libreria dei widget e selezionare Attributi del profilo cliente in tempo reale per configurare lo schema. Con gli attributi del profilo selezionati, puoi iniziare [creazione di widget personalizzati per le dashboard](custom-widgets.md).
