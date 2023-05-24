---
title: Visualizzazione Messaggistica In-App
description: Questa guida contiene informazioni dettagliate sulla visualizzazione Messaggistica in-app in Adobe Experience Platform Assurance.
exl-id: 6131289a-aebb-4b3a-9045-4b2cf23415f8
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# Visualizzazione Messaggistica in-app in Assurance

La vista Messaggistica in-app all’interno di Adobe Experience Platform Assurance consente di convalidare l’app, monitorare i messaggi in-app consegnati al dispositivo e simulare i messaggi al dispositivo.

## Messaggi sul dispositivo

Nella parte superiore della sezione **[!UICONTROL Messaggi sul dispositivo]** la scheda è una **[!UICONTROL Messaggio]** a discesa. Questo includerà tutti i messaggi che sono stati ricevuti nella sessione Assurance. Se un messaggio non è presente nell&#39;elenco, significa che l&#39;app non l&#39;ha mai ricevuto.

![Messaggio](./images/in-app-messaging/message.png)

Selezionando un messaggio verranno visualizzate molte informazioni su quel messaggio, come descritto nelle sezioni seguenti.

### Anteprima messaggio

Nel pannello a destra è **[!UICONTROL Anteprima messaggio]** , che mostra un&#39;anteprima del messaggio. Selezione **[!UICONTROL Simula sul dispositivo]** invierà il messaggio a tutti i dispositivi attualmente connessi alla sessione.

![Anteprima](./images/in-app-messaging/preview.png)

### Comportamento del messaggio

Sotto **[!UICONTROL Anteprima messaggio]** è il riquadro **[!UICONTROL Comportamento del messaggio]** scheda. Contiene tutti i dettagli sulla visualizzazione del messaggio. Queste informazioni includono informazioni sul posizionamento, animazioni, movimenti di scorrimento e impostazioni di aspetto.

![Comportamento](./images/in-app-messaging/gestures.png)

### Scheda Info

Nella sezione a sinistra sono disponibili quattro schede che mostrano i dettagli del messaggio. Il **[!UICONTROL Info]** Questa scheda mostra le informazioni caricate da Adobe Journey Optimizer (AJO) sulla campagna di messaggi.

Puoi anche selezionare **[!UICONTROL Visualizza campagna]** per aprire il messaggio in AJO per l’ispezione o la modifica.

![Info](./images/in-app-messaging/info.png)

### Scheda Regole

Il **[!UICONTROL Regole]** Questa scheda mostra cosa deve accadere affinché il messaggio venga visualizzato. Questo fornisce informazioni su cosa attiverà esattamente la visualizzazione di un messaggio. Osservando questo esempio:

![Regole](./images/in-app-messaging/rules.png)

L’esempio mostra tre condizioni diverse per la regola. Se selezioni un evento (da un elenco di eventi, dalla scheda Analizza o nella timeline), tale evento verrà valutato in base a queste regole. Se l’evento corrisponde a una condizione, verrà visualizzato un segno di spunta verde:

![Corrispondenza regola](./images/in-app-messaging/rule-match.png)

Se l’evento non corrisponde, verrà visualizzata un’icona rossa:

![Mancata corrispondenza regole](./images/in-app-messaging/rule-mismatch.png)

Se tutte e tre le condizioni corrispondono all’evento corrente, viene visualizzato il messaggio.

### Scheda Analizza

Il **[!UICONTROL Analizza]** fornisce ulteriori informazioni sulle regole. In questo caso, filtriamo ogni evento della sessione in base a quanto la regola del messaggio corrisponde all’evento.

![Analizza](./images/in-app-messaging/analyze.png)

Nell’esempio in **[!UICONTROL Scheda Regole]** nella regola sono presenti tre condizioni. Questa scheda mostra la percentuale della regola a cui corrisponde ogni evento. La maggior parte degli eventi corrisponde al 33% (una delle tre condizioni) e il resto corrisponde al 100%.

Di conseguenza, puoi trovare eventi che sono vicini alla corrispondenza ma non corrispondono completamente alla regola.

![Soglia](./images/in-app-messaging/threshold.png)

Il **[!UICONTROL Soglia di corrispondenza]** cursore consente di filtrare gli eventi da visualizzare. Ad esempio, potrebbe essere impostato su 50% - 90% per ottenere un elenco di eventi che corrispondono esattamente a due delle tre condizioni.

### Scheda Interazioni

Il **[!UICONTROL Interazioni]** La scheda mostra un elenco di eventi di interazione inviati a Edge a scopo di tracciamento.

![Interazioni](./images/in-app-messaging/interactions.png)

Ogni volta che viene visualizzato un messaggio, in genere si verificano quattro eventi di interazione:

```
trigger > display > interact > dismiss
```

All’interazione &quot;interact&quot; è associato un valore &quot;action&quot; aggiuntivo. I valori possibili includono &quot;clicked&quot; o &quot;cancel&quot;.

La colonna di convalida mostra se l’evento di interazione è stato ricevuto ed elaborato correttamente da Edge.

## Convalida

Il **[!UICONTROL Convalida]** La scheda esegue le convalide rispetto alla sessione corrente, verificando se l’app è stata configurata correttamente per la messaggistica in-app:

![Convalida](./images/in-app-messaging/validation.png)

Se vengono rilevati errori, verranno fornite informazioni su come correggerli.

## Elenco eventi

![Convalida](./images/in-app-messaging/event-list.png)

Il **[!UICONTROL Elenco eventi]** Questa scheda fornisce una rapida panoramica di tutti gli eventi della sessione Assurance correlati alla messaggistica in-app. Alcuni degli eventi che puoi vedere qui sono:

* Richieste e risposte per recuperare i messaggi
* Visualizzare gli eventi dei messaggi
* Eventi di tracciamento delle interazioni

In questa visualizzazione è possibile utilizzare molte delle caratteristiche standard dell&#39;elenco di eventi, tra cui l&#39;applicazione di ricerche, l&#39;applicazione di filtri, l&#39;aggiunta o la rimozione di colonne e l&#39;esportazione di dati.

Seleziona un evento per visualizzarne i dettagli non elaborati nel pannello di destra.

Dal pannello dei dettagli destro, è possibile contrassegnare l’evento selezionato, utile per contrassegnare un elemento che deve essere rivisto da un’altra persona.
