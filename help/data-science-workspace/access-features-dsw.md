---
keywords: Experience Platform;home;Data Science Workspace;popular topics;access control;sandbox;intelligence pack;dsw features;dsw access;Adobe Experience Platform Intelligence;intelligence;aep intelligence package
solution: Experience Platform
title: Accesso e funzionalità di Data Science Workspace
topic: Access and features for data science workspace
description: 'Nel seguente documento vengono delineate le autorizzazioni di Data Science Workspace e l’accesso alle funzioni. '
translation-type: tm+mt
source-git-commit: 40181fc9b1b08c2e21f806caae76b8af0ec9e5e6
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 3%

---


# Accesso e funzionalità di Data Science Workspace

Nel seguente documento vengono delineate le autorizzazioni di Data Science Workspace e l’accesso alle funzioni.

![Schede DSW](./images/access/platform-tabs.png)

- **Notebook:** Fornisce un ambiente di sviluppo interattivo ([JupyterLab](./jupyterlab/overview.md)) per esplorare, analizzare e modellare i dati sul  Experience Platform.
- **Modelli:** Fornisce strumenti utilizzati per creare, pubblicare e memorizzare ricette e modelli di machine learning avanzati. Per ulteriori informazioni, vedere l&#39;esercitazione [Creazione e pubblicazione di un modello](./models-recipes/create-publish-model.md) di apprendimento automatico.
- **Servizi:** Contiene  servizi forniti dal Adobe, come i servizi [](../intelligent-services/home.md) intelligenti e qualsiasi servizio personalizzato creato con Data Science Workspace.

Perché è possibile visualizzare solo la scheda Servizi?

- La tua organizzazione può avere diritto solo alla piattaforma RTCDP (Real-time Customer Data Platform), che include l&#39;AI del cliente del servizio intelligente.

Se non riesci a visualizzare nessuna delle schede **Data Science** e desideri utilizzare le funzioni di Data Science Workspace, contatta l&#39;amministratore della tua azienda per verificare se disponi di una licenza Adobe Experience Platform Intelligence.

## Aggiungi pacchetto Adobe Experience Platform Intelligence

Nella tabella seguente sono illustrate alcune delle differenze chiave per l’area di lavoro di analisi dati con e senza l’aggiunta del pacchetto Adobe Experience Platform Intelligence:

>[!NOTE]
>
>Potete ottenere la licenza per più di un componente aggiuntivo per il pacchetto Intelligence e l&#39;aumento della capacità viene aggiunto all&#39;adesione globale. Ad esempio, se avete concesso la licenza per 2 addons per il pacchetto Adobe Experience Platform Intelligence, avete diritto a un totale di 20 utenti simultanei per i notebook.

|  | [!DNL Data Science Workspace] | [!DNL Data Science Workspace] con aggiunta del pacchetto Intelligence |
| --- | :---: | :---: |
| Numero di utenti per notebook supportati. | 5 utenti simultanei | Il primo pacchetto aggiunge 5 utenti simultanei e altri 10 utenti simultanei per pacchetto. |
| Permette l&#39;integrazione di Jupyter Notebooks per l&#39;analisi dei dati esplorativi e l&#39;authoring dei modelli (R, Python, Scala, PySpark) | X | X |
| Integrazione nativa con Query Service. Possibilità di esplorare e modellare i set di dati utilizzando SQL nei notebook. | X | X |
| Accesso ai modelli di notebook pregenerati per l&#39;analisi predittiva. | X | X |
| Addestrare e segnare manualmente i modelli con i notebook Jupyter. | X | X |
| Implementare e rendere operativi i modelli con la possibilità di pianificare corsi di formazione e di deduzione. |  | X |
| Il framework di ricetta consente di configurare, valutare, formare, valutare e pubblicare facilmente i modelli in produzione. |  | X |
| Sperimentazione e valutazione basata sull’interfaccia utente. |  | X |
| Supporto per l&#39;apprendimento approfondito per i modelli Tensorflow (GPU Compute). |  | X |
| Calcolo distribuito basato su Spark per la formazione e il punteggio rispetto a set di dati di grandi dimensioni (10MM + righe). |  | X |

## Controllo di accesso

Il controllo degli accessi per  Experience Platform è gestito tramite [Adobe Admin Console](https://adminconsole.adobe.com). Questa funzionalità sfrutta i profili di prodotto in  Admin Console, che collegano gli utenti con autorizzazioni e sandbox. See the [access control overview](../access-control/home.md) for more information.

Per poter utilizzare Data Science Workspace, è necessario abilitare l&#39;autorizzazione &quot;Gestisci Data Science Workspace&quot;. Nella tabella seguente sono riportati gli effetti di tale autorizzazione attivata o disattivata:

| Autorizzazione | Abilitata | Disabilitata |
|---|---|---|
| Gestisci area di lavoro Data Science | Fornisce l&#39;accesso a tutti i servizi in Data Science Workspace. | L&#39;accesso alle API e all&#39;interfaccia utente a tutti i servizi in Data Science Workspace è disattivato. Se disattivata, la selezione delle pagine **Blocco note**, **Modelli** e **Servizi** non è consentita. <li>L&#39;accesso ai **servizi** potrebbe essere ancora disponibile tramite RTCDP (Real-time Customer Data Platform).</li> |

## Supporto sandbox

Le sandbox sono partizioni virtuali all&#39;interno di una singola istanza di  Experience Platform. Ogni istanza della piattaforma supporta una sandbox di produzione e più sandbox non di produzione, ciascuna con una propria libreria di risorse della piattaforma. Le sandbox non di produzione consentono di testare le funzioni, eseguire esperimenti e creare configurazioni personalizzate senza influire sulla sandbox di produzione. Per ulteriori informazioni sulle sandbox, consultate la panoramica [delle](../sandboxes/home.md)sandbox.

Al momento, Data Science Workspace dispone delle seguenti limitazioni sandbox:

- Le risorse di calcolo sono condivise tra le sandbox di produzione e quelle non di produzione.

## Passaggi successivi

Questo documento descrive i diversi tipi di accesso e le funzionalità disponibili in Data Science Workspace.

Per ulteriori informazioni su Data Science Workspace, ad esempio un flusso di lavoro quotidiano completo, consulta la documentazione dettagliata di [Data Science Workspace](./walkthrough.md) . Per ulteriori informazioni generali, consulta la panoramica [di](./home.md)Data Science Workspace.