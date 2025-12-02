---
title: Applica risposta
description: Esegui un’azione in base a una risposta di Edge Network.
source-git-commit: f87e6a0e969aa0924656cdb2ea56aa79d2d7c841
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# Applica risposta

Il tipo di azione **[!UICONTROL Apply response]** consente di eseguire varie azioni in base a una risposta di Edge Network. Questo tipo di azione viene in genere utilizzato nelle implementazioni ibride in cui il server effettua una chiamata iniziale all’Edge Network, quindi prende la risposta da tale chiamata e inizializza il Web SDK nel browser. L’utilizzo di questo tipo di azione può ridurre i tempi di caricamento del client per i casi di utilizzo della personalizzazione ibrida.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Rules]**, quindi seleziona la regola desiderata.
1. In [!UICONTROL Actions], selezionare un&#39;azione esistente o crearne una.
1. Imposta il campo a discesa [!UICONTROL Extension] su **[!UICONTROL Adobe Experience Platform Web SDK]**, quindi imposta [!UICONTROL Action type] su **[!UICONTROL Apply response]**.

![Immagine dell&#39;interfaccia utente di Experience Platform che mostra il tipo di azione di risposta Applica.](../assets/apply-response.png)

## Casi d’uso

* **Suddivisione manuale tra raccolta dati e personalizzazione**: è possibile attivare un&#39;azione [Invia evento](send-event.md) con decisioni di rendering impostate su `false`, quindi impostare una regola di tipo &#39;Invia evento completato&#39; per recuperare la promessa. La prima azione all’interno di questa regola può essere &quot;Applica risposta&quot;. Questo flusso di lavoro ti consente di posticipare la manipolazione DOM fino al completamento di altri lavori da parte del codice della tua organizzazione.
* **Risposta di Edge ricevuta dall&#39;esterno del Web SDK**: se si utilizza un&#39;altra libreria per comunicare con Edge Network, è possibile consentire al Web SDK di gestire comunque la risposta da Edge Network utilizzando questa azione.

## Campi disponibili

Questo tipo di azione supporta le seguenti opzioni di configurazione:

* **[!UICONTROL Instance]**: l&#39;istanza SDK a cui si applica l&#39;azione. Questo menu a discesa è disattivato se l’implementazione utilizza una singola istanza di SDK.
* **[!UICONTROL Response headers]**: seleziona l&#39;elemento dati che restituisce un oggetto contenente le chiavi e i valori di intestazione restituiti dalla chiamata al server Edge Network.
* **[!UICONTROL Response body]**: seleziona l&#39;elemento dati che restituisce l&#39;oggetto contenente il payload JSON fornito dalla risposta di Edge Network.
* **[!UICONTROL Render visual personalization decisions]**: Abilita questa opzione per eseguire automaticamente il rendering del contenuto di personalizzazione fornito da Edge Network e nascondere anticipatamente il contenuto per evitare sfarfallii.
