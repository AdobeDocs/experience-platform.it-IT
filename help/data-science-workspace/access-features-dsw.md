---
keywords: Experience Platform;home;Data Science Workspace;argomenti popolari;controllo degli accessi;sandbox;intelligence pack;dsw features;dsw access;Adobe Experience Platform Intelligence;intelligence;aep intelligence package;home;Data Science;popular topic;access control;sandbox;intelligence pack;dsw features;dsw access;Intelligence;intelligence;aep intelligence package
solution: Experience Platform
title: Accesso e funzioni di Data Science Workspace
description: Il documento seguente illustra le autorizzazioni di Data Science Workspace e l’accesso alle funzioni.
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 1%

---

# Accesso e funzioni di Data Science Workspace

Il documento seguente illustra le autorizzazioni di Data Science Workspace e l’accesso alle funzioni.

![Schede DSW](./images/access/platform-tabs.png)

- **Notebook:** fornisce un ambiente di sviluppo interattivo ([JupyterLab](./jupyterlab/overview.md)) per esplorare, analizzare e modellare i dati su Experience Platform.
- **Modelli:** fornisce gli strumenti utilizzati per creare, pubblicare e archiviare modelli e formule di apprendimento automatico avanzati. Per ulteriori informazioni, visita l&#39;esercitazione [creare e pubblicare un modello di apprendimento automatico](./models-recipes/create-publish-model.md).
- **Servizi:** contiene sia i servizi forniti da Adobe, come [servizi AI/ML](../intelligent-services/home.md), sia i servizi personalizzati creati con Data Science Workspace.

Perché viene visualizzata solo la scheda Servizi?

- La tua organizzazione può avere diritto solo ad Adobe Real-time Customer Data Platform (Real-Time CDP) che include il servizio IA/ML di IA per l’analisi dei clienti.

Se non riesci a visualizzare nessuna delle **schede di Data Science** e desideri utilizzare le funzionalità di Data Science Workspace, contatta l&#39;amministratore della tua azienda per verificare se disponi di una licenza di Adobe Experience Platform Intelligence.

## Pacchetto Data Science Workspace

Le funzionalità di Data Science Workspace sono disponibili nel pacchetto Adobe Experience Platform Intelligence e nel componente aggiuntivo Advanced Intelligence Pack

La tabella seguente illustra alcune delle principali differenze per i diritti di Data Science Workspace con e senza il componente aggiuntivo Advanced Intelligence Pack:

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
| Distribuisci e operazionalizza i modelli con la possibilità di pianificare i processi di formazione e deduzione. | | X |
| Framework di ricetta per configurare, valutare, addestrare, valutare e pubblicare facilmente i modelli in produzione. |  | X |
| Sperimentazione e valutazione di modelli guidati dall’interfaccia utente. | | X |
| Supporto di apprendimento profondo per i modelli Tensorflow (GPU Compute). | | X |
| Calcolo distribuito basato su scintille per addestrare e valutare in base a set di dati di grandi dimensioni (10 MM + righe). | | X |

## Controllo degli accessi

Il controllo degli accessi per Experience Platform è amministrato tramite [Adobe Admin Console](https://adminconsole.adobe.com). Questa funzionalità sfrutta i profili di prodotto di Admin Console, che collegano gli utenti con autorizzazioni e sandbox. Per ulteriori informazioni, vedere [panoramica sul controllo degli accessi](../access-control/home.md).

Per utilizzare Data Science Workspace, è necessario abilitare l’autorizzazione &quot;Manage Data Science Workspace&quot; (Gestisci Data Science). La tabella seguente illustra gli effetti dell&#39;attivazione o della disattivazione di questa autorizzazione:

| Autorizzazione | Abilitata | Disabilitata |
|---|---|---|
| Gestire Data Science Workspace | Fornisce l’accesso a tutti i servizi in Data Science Workspace. | L’accesso API e interfaccia utente a tutti i servizi all’interno di Data Science Workspace è disabilitato. Se disabilitata, non è possibile selezionare le pagine **Blocchi appunti**, **Modelli** e **Servizi**. <li>L&#39;accesso a **Servizi** potrebbe essere ancora disponibile tramite Adobe Real-time Customer Data Platform (Real-Time CDP).</li> |

## Supporto sandbox

Le sandbox sono partizioni virtuali all’interno di una singola istanza di Experience Platform. Ogni istanza di Platform supporta più sandbox di produzione e non di produzione, ognuna delle quali mantiene la propria libreria di risorse Platform. Le sandbox non di produzione consentono di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sulle sandbox di produzione. Per ulteriori informazioni sulle sandbox, consulta la [panoramica sulle sandbox](../sandboxes/home.md).

Attualmente, Data Science Workspace ha la seguente limitazione sandbox:

- Le risorse di calcolo sono condivise tra le sandbox di produzione e non di produzione.

## Passaggi successivi

Questo documento descrive i diversi tipi di accesso e le diverse funzioni disponibili in Data Science Workspace.

Per ulteriori informazioni su Data Science Workspace, ad esempio un flusso di lavoro giornaliero completo, leggere la [documentazione dettagliata di Data Science Workspace](./walkthrough.md). Per ulteriori informazioni generali, visitare la [Panoramica di Data Science Workspace](./home.md).
