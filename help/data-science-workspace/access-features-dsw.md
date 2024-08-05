---
keywords: Experience Platform; casa; Data Science Area di lavoro; argomenti popolari; controllo di accesso; sandbox; intelligence confezione; Funzionalità DSW; DSW accesso; Adobe Experience Platform Intelligence; intelligenza; Pacchetto AEP intelligence
solution: Experience Platform
title: Data Science Area di lavoro accesso e funzionalità
description: Nel documento seguente vengono descritte le autorizzazioni e le accesso delle funzionalità di Data Science Area di lavoro.
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: 923c6f2deb4d1199cfc5dc9dc4ca7b4da154aaaa
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 1%

---

# Data Science Area di lavoro accesso e funzionalità

>[!NOTE]
>
>Data Science Area di lavoro non è più disponibile per l&#39;acquisto.
>
>Questa documentazione è destinata ai clienti esistenti con precedenti diritti a Data Science Area di lavoro.

Nel documento seguente vengono descritte le autorizzazioni e le accesso delle funzionalità di Data Science Area di lavoro.

![Schede DSW](./images/access/platform-tabs.png)

- **Notebook:** fornisce un ambiente di sviluppo interattivo ([JupyterLab](./jupyterlab/overview.md)) per esplorare, analizzare e modellare i dati su Experience Platform.
- **Modelli:** fornisce gli strumenti utilizzati per creare, pubblicare e archiviare modelli e formule di apprendimento automatico avanzati. Per ulteriori informazioni, visita l&#39;esercitazione [creare e pubblicare un modello di apprendimento automatico](./models-recipes/create-publish-model.md).
- **Servizi:** contiene sia i servizi forniti da Adobe, come [servizi AI/ML](../intelligent-services/home.md), sia i servizi personalizzati creati con Data Science Workspace.

Perché viene visualizzata solo la scheda Servizi?

- La tua organizzazione può avere diritto solo ad Adobe Real-time Customer Data Platform (Real-Time CDP) che include il servizio IA/ML di IA per l’analisi dei clienti.

Se non riesci a visualizzare nessuna delle **schede di Data Science** e desideri utilizzare le funzionalità di Data Science Workspace, contatta l&#39;amministratore della tua azienda per verificare se disponi di una licenza di Adobe Experience Platform Intelligence.

## Data Science Area di lavoro packaging

Le funzionalità di Data Science Area di lavoro sono disponibili nel pacchetto Adobe Experience Platform Intelligence e nel componente aggiuntivo Avanzate Intelligence Pack

Nella tabella seguente vengono illustrate alcune delle differenze principali per le adesioni di Data Science Area di lavoro con e senza il componente aggiuntivo Avanzate Intelligence Pack:

>[!NOTE]
>
>È possibile ottenere la licenza per più di un Avanzate Intelligence Pack Addon e la maggiore capacità viene aggiunta al diritto complessivo. Se ad esempio si dispone della licenza per 2 componenti aggiuntivi di Adobe Experience Platform Advanced Intelligence Pack, si ha diritto a un totale di 20 utenti di notebook simultanei.

| Adesione a Data Science Workspace | Solo pacchetto Adobe Experience Platform Intelligence | Add-on Adobe Experience Platform Intelligence plus Avanzate Intelligence Pack |
| --- | :---: | :---: |
| Numero di utenti Notebook supportati. | 5 utenti simultanei | Il primo pacchetto aggiunge 5 utenti simultanei e gli acquisti aggiuntivi aggiungono 10 utenti simultanei per pacchetto. |
| Consente di integrare i notebook Jupyter per l&#39;analisi esplorativa dei dati e la creazione di modelli. | X (supporta R, Python e Scala librerie) | X (aggiunge PySpark e Spark ML librerie) |
| Integrazione nativa con Query Service. Capacità di esplorare e modellare set di dati utilizzando SQL in notebook. | X | X |
| Accesso a modelli predefiniti per notebook per analisi predittive. | X | X |
| Addestra e dai un punteggio ai modelli con Jupyter Notebooks. | X | X |
| Distribuisci e rendi operativi i modelli con la possibilità di programmare training e inferenza dei processi. | | X |
| Framework di ricette per configurare, valutare, addestrare, assegnare un punteggio e pubblicare facilmente i modelli in produzione. |  | X |
| Sperimentazione e valutazione di modelli guidati dall’interfaccia utente. | | X |
| Supporto di deep learning per modelli Tensorflow (GPU Compute). | | X |
| Elaborazione distribuita basata su Spark per eseguire il training e il punteggio rispetto a set di dati di grandi dimensioni (10 MM + righe). | | X |

## Controllo degli accessi

Il controllo degli accessi per Experience Platform è amministrato tramite [Adobe Admin Console](https://adminconsole.adobe.com). Questa funzionalità sfrutta i profili di prodotto di Admin Console, che collegano gli utenti con autorizzazioni e sandbox. Per ulteriori informazioni, vedere [panoramica sul controllo degli accessi](../access-control/home.md).

Per utilizzare Data Science Workspace, è necessario abilitare l’autorizzazione &quot;Manage Data Science Workspace&quot; (Gestisci Data Science). La tabella seguente illustra gli effetti dell&#39;attivazione o della disattivazione di questa autorizzazione:

| Autorizzazione | Abilitata | Disabilitata |
|---|---|---|
| Gestire Area di lavoro di data science | Fornisce accesso a tutti i servizi di Data Science Area di lavoro. | API e interfaccia accesso a tutti i servizi all&#39;interno di Data Science Area di lavoro è disabilitato. Se questa opzione è disabilitata, viene impedita la selezione delle **pagine Blocchi appunti**, **Modelli** e **Servizi** . <li>L&#39;accesso ai **Servizi** potrebbe essere ancora disponibile tramite Adobe Systems Real-Time Customer Data Platform (Real-Time CDP).</li> |

## Supporto per sandbox

Le sandbox sono partizioni virtuali all&#39;interno di un singolo istanza di Experience Platform. Ogni Platform istanza supporta più sandbox di produzione e non di produzione, ognuno mantenendo il proprio libreria di risorse Platform. Le sandbox non di produzione consentono di testare funzionalità, eseguire esperimenti e creare configurazioni personalizzate senza influire sulle sandbox di produzione. Per ulteriori informazioni sulle sandbox, consulta la panoramica](../sandboxes/home.md) delle [sandbox.

Attualmente, Data Science Area di lavoro presenta le seguenti limitazioni sandbox:

- Le risorse di calcolo vengono condivise tra le sandbox di produzione e non di produzione.

## Passaggi successivi

In questo documento sono descritti i diversi tipi di accesso e funzionalità disponibili in Data Science Area di lavoro.

Per ulteriori informazioni sulle Area di lavoro di data science, ad esempio una workflow quotidiana completa, iniziare leggendo la documentazione dettagliata](./walkthrough.md) di [Data Science Area di lavoro. Per informazioni più generali, visita cenni preliminari](./home.md) sulla [Area di lavoro Data science.
