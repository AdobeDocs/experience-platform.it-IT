---
title: Drill-through in modalità Query Pro
description: Scopri come passare da qualsiasi grafico a un nuovo dashboard per esplorare i dati utilizzando il drill-through.
source-git-commit: d851f7b1ac9b2fda5297cf752013c2ffb775e33d
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# Drill-through {#drill-through}

I drill-through semplificano l&#39;analisi dei dati a più livelli semplificando la navigazione da qualsiasi grafico a una nuova dashboard. Questa funzione semplifica la transizione da panoramiche di alto livello a report approfonditi durante lo studio delle tendenze, del comportamento dei clienti, degli indicatori operativi e altro ancora, garantendo sempre il contesto necessario.

Il sistema garantisce che l’analisi iniziale venga proseguita senza interruzioni per l’intera esperienza di drill-through, passando automaticamente filtri globali e filtri di intervallo di date dalle dashboard di origine alle dashboard di destinazione. Per facilitare la navigazione tra i vari livelli dello studio, il sistema consente drill-through a più livelli.

## Creare un drill-through {#create-drill-through}

Per creare un drill-through, selezionare **[!UICONTROL Modifica]** dalla visualizzazione del dashboard.

![Dashboard personalizzato con Modifica evidenziata.](../../images/query-pro-mode/drill-through.png)

Seleziona i puntini di sospensione nel grafico da analizzare, quindi seleziona **[!UICONTROL Modifica]**.

![Grafico con il menu con i puntini di sospensione evidenziati da Modifica.](../../images/query-pro-mode/drill-through-chart-edit.png)

Nel pannello [!UICONTROL Proprietà] utilizza l&#39;interruttore per abilitare **[!UICONTROL Abilita drill-through]**, quindi utilizza il menu a discesa per selezionare il **[!UICONTROL dashboard di Target]**. Verificare che l&#39;interruttore per il filtro pass-through **[!UICONTROL 1} sia abilitato, quindi selezionare**[!UICONTROL  Salva e chiudi ]**.]**

![Pannello delle proprietà del grafico con Attiva drill-through, dashboard di destinazione e pass-through filtro evidenziati.](../../images/query-pro-mode/drill-through-chart-properties.png)

>[!INFO]
>
>Ripetere i passaggi evidenziati in precedenza per il dashboard di destinazione per impostare un drill-through a più livelli.

## Visualizzare un drill-through {#view-drill-through}

Per visualizzare un drill-through, seleziona i puntini di sospensione nel grafico dalla vista del dashboard, quindi seleziona **[!UICONTROL drill-through]**.

![Grafico con il menu con i puntini di sospensione evidenziati.](../../images/query-pro-mode/drill-through-chart-view.png)

Viene visualizzato il dashboard di destinazione del drill-through. È possibile ripetere questo passaggio se si dispone di drill-through a più livelli.

![Il dashboard di destinazione visualizzato con il drill-through evidenziato.](../../images/query-pro-mode/drill-through-target-dashboard.png)

>[!NOTE]
>
>Tutti i filtri applicati nel dashboard di origine vengono passati al dashboard di destinazione. Tuttavia, i filtri per data e i filtri globali sono disattivati nelle dashboard secondarie.

## Rimuovere un drill-through {#remove-drill-through}

Per rimuovere un drill-through, selezionare **[!UICONTROL Modifica]** dalla visualizzazione del dashboard.

![Dashboard personalizzato con Modifica evidenziata.](../../images/query-pro-mode/drill-through.png)

Selezionare i puntini di sospensione nel grafico per rimuovere un drill-through, quindi selezionare **[!UICONTROL Modifica]**.

![Grafico con il menu con i puntini di sospensione evidenziati da Modifica.](../../images/query-pro-mode/drill-through-chart-edit.png)

Nel pannello [!UICONTROL Proprietà], seleziona l&#39;opzione per disattivare **[!UICONTROL Abilita drill-through]**, quindi seleziona **[!UICONTROL Salva e chiudi]**.

![Pannello delle proprietà del grafico con l&#39;interruttore disabilitato per [!UICONTROL Attiva drill-through] evidenziato.](../../images/query-pro-mode/drill-through-disable.png)

## Passaggi successivi

Dopo aver letto questo documento, ora sai come creare un drill-through per il dashboard. Puoi anche imparare a generare grafici dai modelli di dati esistenti nell&#39;interfaccia utente di Adobe Experience Platform con la [guida guidata alla modalità di progettazione](../../user-defined-dashboards.md).
