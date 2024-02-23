---
title: Configurare il supporto per la messaggistica Web in-app in Web SDK
description: Scopri come configurare l’estensione tag Web SDK per supportare la messaggistica in-app web.
source-git-commit: a020f880be2606024c6a986dc468d70a2fbdc30f
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 0%

---


# Configurare il supporto per la messaggistica Web in-app in Web SDK


I messaggi in-app sono notifiche che puoi inviare agli utenti all’interno dell’applicazione web, guidandoli verso punti di interesse specifici.

Puoi utilizzare queste notifiche per diversi scopi, ad esempio per promuovere nuove funzioni, presentare offerte speciali o facilitare l’onboarding degli utenti.

Utilizzando i messaggi in-app, puoi interagire in modo efficace con il pubblico e indirizzarli verso aspetti importanti dell’applicazione.

>[!IMPORTANT]
>
>La messaggistica Web in-app è un [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=it) che utilizza l’SDK web per distribuire i contenuti personalizzati.
>
>Per istruzioni dettagliate su come configurare la campagna di messaggistica Web in-app, vedi [Documentazione di Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/create-in-app-web.html).


## Prerequisiti {#prerequisites}

### Versione estensione tag Web SDK {#extension-version}

La funzionalità di messaggistica in-app per web richiede la versione più recente dell’estensione tag SDK per web.

### Configurare un CSP per la messaggistica in-app web {#csp}

Quando si configura [Messaggistica Web in-app](../personalization/web-in-app-messaging.md), devi includere la seguente direttiva nel CSP:

```
default-src  blob:;
```

Per ulteriori informazioni sulla configurazione di un CSP, vedi [documentazione dedicata](../fundamentals/configuring-a-csp.md).

## Configurare la messaggistica Web in-app utilizzando l’estensione tag Web SDK {#tag-extension}

Consulta la sezione [Pagina di configurazione dell’estensione tag Web SDK](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md) per capire dove si trovano le impostazioni descritte di seguito.

Dopo aver [installato](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#install-the-web-sdk-tag-extension) Nell’estensione tag Web SDK, segui i passaggi indicati di seguito per configurare l’estensione per la messaggistica in-app web.

In **[!UICONTROL Personalizzazione]** sezione, controlla la **[!UICONTROL Abilita archiviazione personalizzazione]** opzione. Questa opzione consente all’SDK web di tenere traccia delle esperienze viste dall’utente nei vari caricamenti di pagina.

![Immagine che mostra l’opzione di archiviazione per la personalizzazione nella pagina di configurazione dell’estensione tag.](assets/web-in-app-messaging/enable-personalization-storage.png)


La messaggistica in-app Web supporta due tipi di trigger:

* [Invio di dati a Platform](#send-data-platform)
* [Attivazione manuale dei messaggi](#manual-trigger)

Consulta le sezioni seguenti per configurare l’estensione tag Web SDK in base ai trigger che desideri utilizzare.

### Passaggi di configurazione per **[!UICONTROL Inviare dati a Platform]** trigger {#send-data-platform}

Seleziona la proprietà tag che contiene l’estensione Web SDK e [crea una nuova regola](../../tags/ui/managing-resources/rules.md##create-a-rule) con le seguenti impostazioni:

1. **[!UICONTROL Estensione]**: [!UICONTROL Core]
2. **[!UICONTROL Tipo di evento]**: [!UICONTROL Library Loaded (Page Top)]

   ![Immagine che mostra la schermata di configurazione dell’evento.](assets/web-in-app-messaging/rule-configuration.png)

3. Seleziona **[!UICONTROL Mantieni modifiche]** per salvare la configurazione dell’evento.

Successivamente, devi aggiungere un’azione alla regola creata.

1. In [!DNL Actions] sezione, seleziona **[!UICONTROL Aggiungi]**.
   ![Immagine che mostra la schermata Modifica regola.](assets/web-in-app-messaging/add-action.png)

2. Utilizza quanto segue **[!UICONTROL Azione]** impostazioni:
   * **[!UICONTROL Estensione]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Tipo di azione]**: [!UICONTROL Invia evento]

     ![Immagine che mostra la schermata di configurazione dell’azione.](assets/web-in-app-messaging/action-configuration.png)

3. Sul lato destro dello schermo, nella **[!UICONTROL Personalizzazione]** , abilita **[!UICONTROL Eseguire il rendering delle decisioni di personalizzazione visiva]** opzione.
   ![Immagine che mostra la schermata di configurazione della personalizzazione.](assets/web-in-app-messaging/render-visual-personalization.png)

4. Sul lato destro dello schermo, nella **[!UICONTROL Contesto decisionale]** , definire la sezione **[!UICONTROL Chiave]**/**[!UICONTROL Valore]** coppie che hai utilizzato nella configurazione di campaign per essere idonee per il messaggio in-app.
   ![Immagine che mostra la schermata di configurazione della personalizzazione.](assets/web-in-app-messaging/decision-context.png)

5. Seleziona **[!UICONTROL Mantieni modifiche]** per salvare la configurazione.


Successivamente, devi aggiungere la regola appena creata alla libreria delle proprietà del tag. Per eseguire questa operazione, vai a **[!UICONTROL Flusso di pubblicazione]** e seleziona la regola creata in precedenza.

![Immagine che mostra la schermata della libreria.](assets/web-in-app-messaging/add-rule-to-library.png)

Dopo aver aggiunto la regola alla libreria, seleziona **[!UICONTROL Salva e genera in sviluppo]**.

![Immagine che mostra la schermata di configurazione della personalizzazione.](assets/web-in-app-messaging/publish-flow.png)

Il processo di configurazione è ora completato e il messaggio è pronto per essere mostrato agli utenti.

### Passaggi di configurazione per l&#39;utilizzo di trigger manuali {#manual-trigger}

Seleziona la proprietà tag che contiene l’estensione Web SDK e [crea una nuova regola](../../tags/ui/managing-resources/rules.md##create-a-rule) con le seguenti impostazioni:

1. **[!UICONTROL Estensione]**: [!UICONTROL Core]
2. **[!UICONTROL Tipo di evento]**: [!UICONTROL Clic]
3. Imposta il trigger per un elemento specifico sulla pagina, identificabile da un selettore CSS a tua scelta.

   ![Immagine che mostra la schermata di configurazione dell’evento.](assets/web-in-app-messaging/event-configuration-manual.png)


Successivamente, devi aggiungere un’azione alla regola creata.

1. In [!DNL Actions] sezione, seleziona **[!UICONTROL Aggiungi]**.
   ![Immagine che mostra la schermata Modifica regola.](assets/web-in-app-messaging/add-action.png)

2. Utilizza quanto segue **[!UICONTROL Azione]** impostazioni:
   * **[!UICONTROL Estensione]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Tipo di azione]**: [!UICONTROL Valuta set di regole]

     ![Immagine che mostra la schermata di configurazione dell’azione.](assets/web-in-app-messaging/manual-trigger-action.png)

3. Sul lato destro dello schermo, abilita **[!UICONTROL Eseguire il rendering delle decisioni di personalizzazione visiva]** opzione.
   ![Immagine che mostra la schermata di configurazione della personalizzazione.](assets/web-in-app-messaging/manual-trigger-render.png)


4. Sul lato destro dello schermo, nella **[!UICONTROL Contesto decisionale]** , definire la sezione **[!UICONTROL Chiave]**/**[!UICONTROL Valore]** coppie che hai utilizzato nella configurazione di campaign per essere idonee per il messaggio in-app.
   ![Immagine che mostra la schermata di configurazione della personalizzazione.](assets/web-in-app-messaging/manual-trigger-decision-context.png)

5. Seleziona **[!UICONTROL Mantieni modifiche]** per salvare la configurazione.

Successivamente, devi aggiungere la regola appena creata alla libreria delle proprietà del tag. Per eseguire questa operazione, vai a **[!UICONTROL Flusso di pubblicazione]** e seleziona la regola creata in precedenza.

![Immagine che mostra la schermata della libreria.](assets/web-in-app-messaging/add-rule-to-library.png)

Dopo aver aggiunto la regola alla libreria, seleziona **[!UICONTROL Salva e genera in sviluppo]**.

![Immagine che mostra la schermata di configurazione della personalizzazione.](assets/web-in-app-messaging/publish-flow.png)

Il processo di configurazione è ora completato e il messaggio è pronto per essere mostrato agli utenti.

## Configurare la messaggistica Web in-app utilizzando la libreria JavaScript di Web SDK {#js-library}

In alternativa all’utilizzo dell’estensione tag Web SDK, puoi anche configurare la messaggistica Web in-app direttamente dalla libreria JavaScript dell’SDK per web.



I messaggi web in-app provenienti da Adobe Journey Optimizer possono essere visualizzati in due modi.

### Metodo 1: recuperare automaticamente il contenuto di personalizzazione {#automatic}

Per fare in modo che l’SDK web recuperi automaticamente il contenuto di personalizzazione al caricamento della pagina, utilizza `sendEvent` come illustrato nell&#39;esempio seguente.

```js
  alloy("sendEvent", {
      renderDecisions: true,
      personalization: {
          surfaces: ['#welcome']
      }
  });
```

### Metodo 2: recuperare manualmente il contenuto di personalizzazione in base all’azione dell’utente {#manual}

Per mostrare il contenuto di personalizzazione solo dopo che l’utente ha eseguito un’azione specifica, utilizza `evaluateRulesets` come illustrato nell&#39;esempio seguente.

In questo esempio, il contenuto di personalizzazione viene visualizzato quando un utente fa clic su **[!UICONTROL Acquista ora]** sul sito web.

```js
 alloy("evaluateRulesets", {
     renderDecisions: true,
     personalization: {
         decisionContext: {
             "userAction": "buy_now"
         }
     }
 });
```

### Configurare l’archiviazione per la personalizzazione {#personalization-storage}

Puoi scegliere di mostrare i messaggi in-app agli utenti per un determinato numero di volte oppure ogni volta che visitano una pagina, tramite `personalizationStorageEnabled` opzione di configurazione.

In [Configurazione dell’SDK web](../fundamentals/configuring-the-sdk.md) imposta `personalizationStorageEnabled` opzione in base alle tue esigenze:

* `personalizationStorageEnabled: true` attiva il messaggio in-app con la frequenza definita nell&#39; [Campagna Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/create-in-app-web.html#configure-inapp).
* `personalizationStorageEnabled: false` attiva il messaggio in-app a ogni caricamento di pagina.