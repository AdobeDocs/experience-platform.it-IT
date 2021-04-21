---
keywords: Experience Platform;home;Data Science Workspace;argomenti comuni;controllo accessi;sandbox;pacchetto di informazioni;funzioni dsw;accesso dsw;Adobe Experience Platform Intelligence;intelligence;pacchetto di informazioni aep
solution: Experience Platform
title: Accesso e funzioni di Data Science Workspace
topic-legacy: Access and features for data science workspace
description: Il seguente documento delinea le autorizzazioni di Data Science Workspace e l’accesso alle funzioni.
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 3%

---

# Accesso e funzioni di Data Science Workspace

Il seguente documento delinea le autorizzazioni di Data Science Workspace e l’accesso alle funzioni.

![Schede DSW](./images/access/platform-tabs.png)

- **Notebook:** fornisce un ambiente di sviluppo interattivo ([JupyterLab](./jupyterlab/overview.md)) per esplorare, analizzare e modellare i dati su Experience Platform.
- **Modelli:** fornisce gli strumenti utilizzati per creare, pubblicare e memorizzare ricette e modelli avanzati di apprendimento automatico. Per ulteriori informazioni, visita il tutorial [creare e pubblicare un modello di apprendimento automatico](./models-recipes/create-publish-model.md) .
- **Servizi:** contiene sia servizi forniti da Adobe, come i servizi  [intelligenti ](../intelligent-services/home.md) e tutti i servizi personalizzati creati con Data Science Workspace.

Perché viene visualizzata solo la scheda Servizi?

- La tua organizzazione può avere diritto solo a Real-time Customer Data Platform (RTCDP) che include Intelligent Service Customer AI.

Se non riesci a visualizzare nessuna delle schede **Data Science** e desideri utilizzare le funzioni di Data Science Workspace, contatta l’amministratore della tua azienda per verificare se disponi di una licenza Adobe Experience Platform Intelligence.

## Aggiungi pacchetto Adobe Experience Platform Intelligence

La tabella seguente illustra alcune delle differenze chiave per Data Science Workspace con e senza l’aggiunta del pacchetto Adobe Experience Platform Intelligence:

>[!NOTE]
>
>È possibile concedere in licenza più di un componente aggiuntivo del pacchetto Intelligence e l&#39;aumento della capacità viene aggiunto all&#39;adesione complessiva. Ad esempio, se hai concesso la licenza per 2 addons del pacchetto Adobe Experience Platform Intelligence, hai diritto a un totale di 20 utenti simultanei di Notebook.

|  | [!DNL Data Science Workspace] | [!DNL Data Science Workspace] con l&#39;aggiunta del pacchetto &quot;Intelligence&quot; |
| --- | :---: | :---: |
| Numero di utenti di notebook supportati. | 5 utenti simultanei | Il primo pacchetto aggiunge 5 utenti simultanei e gli acquisti aggiuntivi aggiungono 10 utenti simultanei per pacchetto. |
| Permette l&#39;integrazione di Jupyter Notebooks per l&#39;analisi dei dati esplorativi e l&#39;authoring di modelli (R, Python, Scala, PySpark) | X | X |
| Integrazione nativa con Query Service. Possibilità di esplorare e modellare i set di dati utilizzando SQL nei blocchi appunti. | X | X |
| Accesso a modelli di notebook predefiniti per analisi predittive. | X | X |
| Addestrare e valutare manualmente i modelli con Jupyter Notebooks. | X | X |
| Distribuire e rendere operativi modelli con la possibilità di programmare processi di formazione e di deduzione. |  | X |
| framework di ricetta per configurare, valutare, addestrare, valutare e pubblicare facilmente i modelli in produzione. |  | X |
| Sperimentazione e valutazione dei modelli basati sull’interfaccia utente. |  | X |
| Supporto per l&#39;apprendimento profondo per i modelli di flusso di tensione (GPU Compute). |  | X |
| Calcolo distribuito basato su scintille per addestrare e valutare in base a set di dati di grandi dimensioni (10MM + righe). |  | X |

## Controllo dell&#39;accesso

Il controllo degli accessi, ad Experience Platform, è gestito tramite [Adobe Admin Console](https://adminconsole.adobe.com). Questa funzionalità sfrutta i profili di prodotto in Admin Console, che collegano gli utenti con autorizzazioni e sandbox. Per ulteriori informazioni, consulta la [panoramica sul controllo degli accessi](../access-control/home.md) .

Per utilizzare Data Science Workspace, è necessario abilitare l’autorizzazione &quot;Gestisci Data Science Workspace&quot;. La tabella seguente illustra gli effetti dell’abilitazione o della disabilitazione di questa autorizzazione:

| Autorizzazione | Abilitata | Disabilitata |
|---|---|---|
| Gestione di Data Science Workspace | Consente l&#39;accesso a tutti i servizi in Data Science Workspace. | L’accesso API e interfaccia utente a tutti i servizi in Data Science Workspace è disattivato. Quando è disabilitata, la selezione delle pagine **Notebook**, **Modelli** e **Servizi** non è consentita. <li>L&#39;accesso a **Servizi** può essere ancora disponibile tramite Real-time Customer Data Platform (RTCDP).</li> |

## Supporto per sandbox

Le sandbox sono partizioni virtuali all’interno di una singola istanza di Experience Platform. Ogni istanza di Platform supporta una sandbox di produzione e più sandbox non di produzione, ciascuna con una propria libreria di risorse di Platform. Le sandbox non di produzione consentono di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sulla sandbox di produzione. Per ulteriori informazioni sulle sandbox, consulta la [panoramica sulle sandbox](../sandboxes/home.md).

Attualmente, Data Science Workspace presenta la seguente limitazione sandbox:

- Le risorse di elaborazione sono condivise tra le sandbox di produzione e le sandbox non di produzione.

## Passaggi successivi

Questo documento descrive i diversi tipi di accesso e le funzioni disponibili in Data Science Workspace.

Per ulteriori informazioni su Data Science Workspace, ad esempio un flusso di lavoro giornaliero completo, consulta la documentazione dettagliata [Data Science Workspace](./walkthrough.md) . Per informazioni più generali, visita la [panoramica di Data Science Workspace](./home.md).
