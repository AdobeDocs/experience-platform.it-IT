---
keywords: Experience Platform;home;Data Science Workspace;argomenti popolari;controllo degli accessi;sandbox;intelligence pack;funzioni dsw;accesso dsw;Adobe Experience Platform Intelligence;intelligence;aep intelligence package;home;Data Science Workspace;popular topic;access control;sandbox;intelligence pack;dsw features;dsw access;Intelligence;intelligence;aep intelligence package
solution: Experience Platform
title: Accesso e funzioni di Data Science Workspace
description: Il documento seguente illustra le autorizzazioni di Data Science Workspace e l’accesso alle funzioni.
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 2%

---

# Accesso e funzioni di Data Science Workspace

Il documento seguente illustra le autorizzazioni di Data Science Workspace e l’accesso alle funzioni.

![Schede DSW](./images/access/platform-tabs.png)

- **Notebook:** Fornisce un ambiente di sviluppo interattivo ([JupyterLab](./jupyterlab/overview.md)) per esplorare, analizzare e modellare i dati su Experience Platform.
- **Modelli:** Fornisce gli strumenti utilizzati per creare, pubblicare e archiviare ricette e modelli avanzati di apprendimento automatico. Per ulteriori informazioni, visitare il [creare e pubblicare un modello di apprendimento automatico](./models-recipes/create-publish-model.md) esercitazione.
- **Servizi:** Contiene entrambi i servizi forniti dagli Adobi come [Servizi di IA/ML](../intelligent-services/home.md) ed eventuali servizi personalizzati creati con Data Science Workspace.

Perché viene visualizzata solo la scheda Servizi?

- La tua organizzazione può avere diritto solo ad Adobe Real-time Customer Data Platform (Real-Time CDP) che include il servizio IA/ML di IA per l’analisi dei clienti.

Se non riesci a vedere nessuno dei **Data Science** e desideri utilizzare le funzioni di Data Science Workspace, contatta l’amministratore della tua azienda per verificare se disponi di una licenza di Adobe Experience Platform Intelligence.

## Packaging di Data Science Workspace

Le funzionalità di Data Science Workspace sono disponibili nel pacchetto di Adobe Experience Platform Intelligence e nel componente aggiuntivo Advanced Intelligence Pack

La tabella seguente illustra alcune delle principali differenze per i diritti a Data Science Workspace con e senza il componente aggiuntivo Advanced Intelligence Pack:

>[!NOTE]
>
>È possibile concedere in licenza più di un componente aggiuntivo Advanced Intelligence Pack e la maggiore capacità viene aggiunta alla licenza complessiva. Se ad esempio si dispone della licenza per 2 componenti aggiuntivi di Adobe Experience Platform Advanced Intelligence Pack, si ha diritto a un totale di 20 utenti di notebook simultanei.

| Adesione a Data Science Workspace | Solo pacchetto di Adobe Experience Platform Intelligence | Componente aggiuntivo Adobe Experience Platform Intelligence plus Advanced Intelligence Pack |
| --- | :---: | :---: |
| Numero di utenti del blocco appunti supportati. | 5 utenti simultanei | Nel primo pacchetto vengono aggiunti 5 utenti simultanei e negli acquisti aggiuntivi vengono aggiunti 10 utenti simultanei per pacchetto. |
| Consente Jupyter Notebooks integrati per l’analisi esplorativa dei dati e l’authoring dei modelli. | X (supporta librerie R, Python e Scala) | X (Aggiunge librerie PySpark e Spark ML) |
| Integrazione nativa con Query Service. Possibilità di esplorare e modellare i set di dati utilizzando SQL nei notebook. | X | X |
| Accesso a modelli predefiniti per notebook per analisi predittive. | X | X |
| Addestra e dai un punteggio ai modelli con Jupyter Notebooks. | X | X |
| Distribuisci e operazionalizza i modelli con la possibilità di pianificare i processi di formazione e deduzione. |  | X |
| Framework di ricetta per configurare, valutare, addestrare, valutare e pubblicare facilmente i modelli in produzione. |  | X |
| Sperimentazione e valutazione di modelli guidati dall’interfaccia utente. |  | X |
| Supporto di apprendimento profondo per i modelli Tensorflow (GPU Compute). |  | X |
| Calcolo distribuito basato su scintille per addestrare e valutare in base a set di dati di grandi dimensioni (10 MM + righe). |  | X |

## Controllo degli accessi

Ad Experience Platform, il controllo degli accessi viene gestito tramite [Adobe Admin Console](https://adminconsole.adobe.com). Questa funzionalità sfrutta i profili di prodotto di Admin Console, che collegano gli utenti con autorizzazioni e sandbox. Consulta la [panoramica sul controllo degli accessi](../access-control/home.md) per ulteriori informazioni.

Per utilizzare Data Science Workspace, è necessario abilitare l’autorizzazione &quot;Gestisci Data Science Workspace&quot;. La tabella seguente illustra gli effetti dell&#39;attivazione o della disattivazione di questa autorizzazione:

| Autorizzazione | Abilitata | Disabilitata |
|---|---|---|
| Gestire Data Science Workspace | Fornisce l’accesso a tutti i servizi in Data Science Workspace. | L’accesso API e interfaccia utente a tutti i servizi all’interno di Data Science Workspace è disabilitato. Se è disattivato, seleziona **Notebook**, **Modelli**, e **Servizi** pagine non consentite. <li>Accesso a **Servizi** potrebbe essere ancora disponibile tramite Adobe Real-time Customer Data Platform (Real-Time CDP).</li> |

## Supporto sandbox

Le sandbox sono partizioni virtuali all’interno di una singola istanza di Experience Platform. Ogni istanza di Platform supporta più sandbox di produzione e non di produzione, ognuna delle quali mantiene la propria libreria di risorse Platform. Le sandbox non di produzione consentono di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sulle sandbox di produzione. Per ulteriori informazioni sulle sandbox, consulta [panoramica sulle sandbox](../sandboxes/home.md).

Attualmente, Data Science Workspace ha la seguente limitazione sandbox:

- Le risorse di calcolo sono condivise tra le sandbox di produzione e non di produzione.

## Passaggi successivi

Questo documento descrive i diversi tipi di accesso e le diverse funzioni disponibili in Data Science Workspace.

Per ulteriori informazioni su Data Science Workspace, ad esempio un flusso di lavoro giornaliero completo, leggi [Procedura dettagliata su Data Science Workspace](./walkthrough.md) documentazione. Per informazioni più generali, visitare il [Panoramica di Data Science Workspace](./home.md).
