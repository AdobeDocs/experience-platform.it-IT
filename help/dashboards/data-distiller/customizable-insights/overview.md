---
title: Approfondimenti personalizzabili per reporting esteso delle app
description: Scopri come utilizzare le query SQL per generare insights per le dashboard personalizzate.
exl-id: c60a9218-4ac0-4638-833b-bdbded36ddf5
source-git-commit: 5bb954da7c1e05922a4e0f8d0bc7d3ab5c8e0e58
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Approfondimenti personalizzabili per reporting esteso dell’app

Utilizza query SQL personalizzate per estrarre in modo efficace informazioni approfondite da diversi set di dati strutturati. Gli utenti tecnici possono utilizzare la modalità query pro per eseguire analisi complesse con SQL e quindi condividere questa analisi con utenti non tecnici tramite grafici nel dashboard personalizzato o esportarle in file CSV. Questo metodo di creazione delle informazioni è adatto per tabelle con relazioni chiare e consente un maggiore grado di personalizzazione delle informazioni e dei filtri che possono essere adatti a casi d’uso di nicchia.

>[!IMPORTANT]
>
>La modalità Query Pro è disponibile solo per gli utenti che hanno acquistato lo SKU [Data Distiller](../../../query-service/data-distiller/overview.md).

Per generare informazioni da SQL, è necessario innanzitutto creare un dashboard.

## Creare un dashboard personalizzato {#create-custom-dashboard}

Per creare un dashboard personalizzato, seleziona **[!UICONTROL Dashboard]** dal pannello di navigazione a sinistra per aprire l&#39;area di lavoro Dashboard. Selezionare **[!UICONTROL Crea dashboard]**.

![Inventario dashboard con dashboard di creazione evidenziato.](../../images/customizable-insights/create-dashboard.png)

Viene visualizzata la finestra di dialogo **[!UICONTROL Crea dashboard]**. Sono disponibili due opzioni per scegliere il metodo di creazione del dashboard. Per creare le tue informazioni, puoi utilizzare un modello dati esistente con la [[!UICONTROL modalità di progettazione guidata]](../../user-defined-dashboards.md) oppure il tuo codice SQL personalizzato con la [!UICONTROL modalità Query pro].

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

L&#39;utilizzo di un modello dati esistente offre i vantaggi di fornire un framework strutturato, efficiente e scalabile personalizzato in base alle esigenze aziendali specifiche. Per informazioni su come [creare approfondimenti da un modello dati esistente](../../user-defined-dashboards.md#create-widget), consulta la guida del dashboard personalizzato.

Le informazioni generate dalle query SQL offrono maggiore flessibilità e personalizzazione. Gli utenti tecnici possono utilizzare la modalità query pro per eseguire analisi complesse su SQL e quindi condividere questa analisi con utenti non tecnici tramite questa funzionalità del dashboard. Seleziona **[!UICONTROL Modalità Query Pro]** seguita da **[!UICONTROL Salva]**.

>[!NOTE]
>
>Una volta effettuata la selezione, non è possibile modificarla all&#39;interno del dashboard. È invece necessario creare un nuovo dashboard con un metodo di creazione diverso.

![La finestra di dialogo [!UICONTROL Crea dashboard] con Query Pro Mode e Salva evidenziata.](../../images/customizable-insights/query-pro-mode.png)

## Creare un grafico {#create-a-chart}

Per istruzioni dettagliate sulla creazione di un grafico con SQL, vedere la [guida alla modalità query pro](./query-pro-mode.md).
