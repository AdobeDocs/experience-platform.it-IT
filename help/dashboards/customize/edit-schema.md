---
keywords: Experience Platform;interfaccia utente;interfaccia utente;dashboard;dashboard;profili;segmenti;destinazioni;utilizzo licenza
title: Modifica schema per creare widget personalizzato del dashboard
description: 'Questa guida fornisce istruzioni dettagliate per la selezione degli attributi e la configurazione dello schema dell’organizzazione al fine di creare widget personalizzati per le dashboard di Adobe Experience Platform. '
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Modificare lo schema per creare widget personalizzati

Per creare widget personalizzati per le dashboard di Adobe Experience Platform, devi prima identificare gli attributi Profilo cliente in tempo reale su cui saranno basati i widget.

Questa guida fornisce istruzioni dettagliate per la modifica dello schema dell’organizzazione selezionando gli attributi per creare widget dashboard personalizzati.

Una volta selezionati gli attributi e configurato lo schema, puoi procedere con i passaggi per [creare widget personalizzati per le dashboard](custom-widgets.md).

>[!NOTE]
>
>Per poter modificare lo schema, è necessario concedere agli utenti l’autorizzazione &quot;Gestisci dashboard standard&quot;. Per i passaggi relativi alla concessione delle autorizzazioni di accesso alle dashboard, fare riferimento alla [guida alle autorizzazioni del dashboard](../permissions.md).

## Libreria widget {#widget-library}

Questa guida richiede l&#39;accesso alla [!UICONTROL Libreria widget] all&#39;interno di Experience Platform. Per ulteriori informazioni sulla libreria di widget e su come accedervi nell&#39;interfaccia utente, inizia leggendo la [panoramica della libreria di widget](widget-library.md).

## Modifica di uno schema

Nella libreria dei widget, la scheda **[!UICONTROL Personalizzato]** consente di creare widget e condividerli con altri utenti dell’organizzazione al fine di personalizzare l’aspetto delle dashboard.

Prima di poter creare widget personalizzati, è necessario selezionare gli attributi Profilo cliente in tempo reale per garantire che i dati siano inclusi come parte dello snapshot giornaliero.

>[!IMPORTANT]
>
>L’organizzazione può selezionare un massimo di 20 attributi.

Se la tua organizzazione non ha selezionato attributi di profilo, inizia selezionando **[!UICONTROL Modifica schema]** nell&#39;angolo in alto a destra della libreria dei widget.

Quando è stato creato almeno un attributo personalizzato, seleziona **[!UICONTROL Modifica schema]** per visualizzare gli attributi selezionati e aggiungerne altri.

![](../images/customization/edit-schema.png)

## Selezionare un attributo

Per selezionare un attributo nella finestra di dialogo **[!UICONTROL Seleziona campo schema unione]**, accedi all&#39;attributo nello schema dell&#39;unione (o utilizza la ricerca) e seleziona la casella di controllo accanto all&#39;attributo. Selezionando la casella di controllo, l&#39;attributo viene aggiunto anche all&#39;elenco **[!UICONTROL Attributi selezionati]** sul lato destro della finestra di dialogo.

>[!NOTE]
>
>Affinché un attributo sia visibile per la selezione, deve essere uno dei seguenti: Stringa, data, data-ora, booleano, breve, lungo, intero o byte. I tipi di dati Mappa e Doppio non sono supportati e sono disattivati in modo che non possano essere selezionati.

Dopo aver selezionato gli attributi che si desidera aggiungere, selezionare **[!UICONTROL Salva]** per salvare gli attributi e tornare alla scheda widget personalizzati.

>[!WARNING]
>Gli attributi appena selezionati diventano disponibili dopo la successiva istantanea giornaliera quando i dati vengono aggiornati.

![](../images/customization/select-attribute.png)

## Passaggi successivi

Dopo aver letto questa guida puoi passare alla libreria widget e selezionare gli attributi Profilo cliente in tempo reale per configurare lo schema. Selezionando gli attributi del profilo, puoi iniziare a [creare widget personalizzati per le dashboard](custom-widgets.md).