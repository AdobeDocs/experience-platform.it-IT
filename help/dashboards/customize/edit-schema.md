---
keywords: Experience Platform;interfaccia utente;interfaccia utente;dashboard;dashboard;profili;segmenti;destinazioni;utilizzo licenza
title: Modifica schema per creare widget personalizzato del dashboard
description: Questa guida fornisce istruzioni dettagliate per la selezione degli attributi e la configurazione dello schema dell’organizzazione al fine di creare widget personalizzati per le dashboard di Adobe Experience Platform.
exl-id: a744eb24-5ba7-4971-9183-3f891e807863
source-git-commit: 9b89effa6f90fb513fac9d0b826722ab05020036
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# Modificare lo schema per creare widget personalizzati

Per creare widget personalizzati per le dashboard di Adobe Experience Platform, devi prima identificare gli attributi Profilo cliente in tempo reale su cui saranno basati i widget.

Questa guida fornisce istruzioni dettagliate per la modifica dello schema dell’organizzazione selezionando gli attributi per creare widget dashboard personalizzati.

Una volta selezionati gli attributi e configurato lo schema, puoi procedere con i passaggi per [creazione di widget personalizzati per le dashboard](custom-widgets.md).

>[!NOTE]
>
>Per poter modificare lo schema, è necessario concedere agli utenti l’autorizzazione &quot;Gestisci dashboard standard&quot;. Per i passaggi relativi alla concessione delle autorizzazioni di accesso alle dashboard, consulta [guida alle autorizzazioni del dashboard](../permissions.md).

## Libreria widget {#widget-library}

Questa guida richiede l’accesso al [!UICONTROL Libreria widget] all&#39;Experience Platform. Per ulteriori informazioni sulla libreria di widget e su come accedervi nell&#39;interfaccia utente, leggi la [panoramica della libreria widget](widget-library.md).

## Modifica di uno schema

Nella libreria dei widget, la **[!UICONTROL Personalizzato]** consente di creare widget e condividerli con altri utenti dell’organizzazione al fine di personalizzare l’aspetto delle dashboard.

Prima di poter creare widget personalizzati, è necessario selezionare gli attributi Profilo cliente in tempo reale per garantire che i dati siano inclusi come parte dello snapshot giornaliero.

>[!IMPORTANT]
>
>L’organizzazione può selezionare un massimo di 20 attributi.

Se la tua organizzazione non ha selezionato attributi di profilo, inizia selezionando **[!UICONTROL Configura]** al centro dello schermo.

![Scheda Personalizzata dell’area di lavoro della libreria widget con Configura evidenziata.](../images/customization/configure-schema.png)

Quando è stato creato almeno un attributo personalizzato, seleziona **[!UICONTROL Modifica schema]** per visualizzare gli attributi selezionati e aggiungerne altri.

![La scheda Personalizzato dell&#39;area di lavoro della libreria widget con lo schema Modifica evidenziato.](../images/customization/edit-schema.png)

## Selezionare un attributo

Per selezionare un attributo nel **[!UICONTROL Selezionare il campo schema unione]** , passa all’attributo nello schema di unione (o utilizza ricerca) e seleziona la casella di controllo accanto all’attributo . Quando si seleziona la casella di controllo, viene aggiunto anche l’attributo al **[!UICONTROL Attributi selezionati]** sulla destra della finestra di dialogo.

>[!NOTE]
>
>Affinché un attributo sia visibile per la selezione, deve essere uno dei seguenti: Stringa, data, data-ora, booleano, breve, lungo, intero o byte. I tipi di dati Mappa e Doppio non sono supportati e sono disattivati in modo che non possano essere selezionati.

Dopo aver selezionato gli attributi che si desidera aggiungere, selezionare **[!UICONTROL Salva]** per salvare gli attributi e tornare alla scheda widget personalizzati.

>[!WARNING]
>Gli attributi appena selezionati diventano disponibili dopo la successiva istantanea giornaliera quando i dati vengono aggiornati.

![Finestra di dialogo per selezionare gli attributi dello schema con gli attributi e Salva evidenziato.](../images/customization/select-attribute.png)

## Passaggi successivi

Dopo aver letto questa guida puoi passare alla libreria widget e selezionare gli attributi Profilo cliente in tempo reale per configurare lo schema. Selezionando gli attributi del profilo, puoi iniziare [creazione di widget personalizzati per le dashboard](custom-widgets.md).
