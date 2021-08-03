---
title: Panoramica dell’estensione Adobe Experience Manager Forms
description: Scopri l’estensione tag di Adobe Experience Manager Forms in Adobe Experience Platform.
source-git-commit: f31a1d2e84dee262e04f1db0415ffd76248ecb6c
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 6%

---

# Panoramica dell&#39;estensione Adobe Experience Manager Forms

Questo documento fornisce una panoramica dell’estensione tag di Adobe Experience Manager Forms in Adobe Experience Platform.

## Eventi

L&#39;estensione fornisce i seguenti tipi di evento:

1. **Rendering**: Attiva quando l’utente esegue il rendering (apre) di un modulo.
1. **Errore**: Attiva quando l&#39;utente commette un errore di convalida su un modulo.
1. **Aiuto**: Viene attivato quando l’utente fa clic sull’icona dell’Aiuto di un campo.
1. **Invia**: Attiva all’invio del modulo.
1. **Visita** sul campo: Attiva quando viene visitato un campo.
1. **Abbandonare**: Attiva quando l&#39;utente chiude la scheda o passa a un URL diverso.
1. **Salva**: Viene attivato quando un modulo viene salvato nel portale.

>[!IMPORTANT]
>
>L’evento Save non è attualmente disponibile per forms as a cloud service. Gli eventi personalizzati inviati dall&#39;editor di regole in Adaptive Forms possono essere acquisiti utilizzando l&#39;evento principale &quot;Capture custom event&quot;.

## Elementi dati

L&#39;estensione fornisce diversi elementi di dati che possono essere utilizzati per inviare proprietà nelle chiamate di Analytics.

## Introduzione

Per iniziare a utilizzare l’estensione, segui i passaggi riportati di seguito.

1. Installa l&#39;estensione Adobe Experience Manager Forms dal catalogo delle estensioni. Dopo l&#39;installazione non è necessaria alcuna ulteriore configurazione.
2. Installa e configura l&#39; [estensione Adobe Analytics](../analytics/overview.md#Configure-the-Adobe-Analytics-extension).

## Creazione di una regola

Una regola che utilizza l&#39;estensione Experience Manager Forms avrà un aspetto simile al seguente:

![Configurazione azione](./images/rule.png)

Segui i passaggi descritti di seguito per creare una regola simile per la tua implementazione.

### Aggiungere un evento

1. Seleziona **Adobe Experience Manager Forms** nel menu a discesa dell&#39;estensione.
2. Seleziona l’evento da acquisire.

![Configurazione azione](./images/AEM-forms-event.png)

### Aggiungi un&#39;azione

1. Seleziona &quot;Adobe Analytics&quot; nel menu a discesa dell&#39;estensione.
2. Seleziona &quot;imposta variabile&quot; nel menu a discesa Tipo di azione .
3. Nella vista Configurazione, scegli le proprietà e gli eventi da inviare.
4. Aggiungi un&#39;azione &quot;invia beacon&quot; per inviare la chiamata di analytics con gli eventi e le proprietà impostati nel passaggio 3
   ![Configurazione azione](./images/AEM-forms-sendBeacon.png)
5. Aggiungi un&#39;azione &quot;clear variable&quot; (Cancella variabile).

![Configurazione azione](./images/AEM-forms-action.png)