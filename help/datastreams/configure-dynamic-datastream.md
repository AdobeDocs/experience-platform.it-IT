---
title: Creare configurazioni di flussi di dati dinamici
description: Scopri come creare configurazioni di flusso di dati dinamiche, per indirizzare i dati a vari servizi Experience Cloud, in base a regole.
exl-id: 528ddf89-ad87-4021-b5a6-8e25b4469ac4
source-git-commit: 79d724eec4903b8a3eee6f717d94fcd70a4ffcb7
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 3%

---

# Creare configurazioni di flussi di dati dinamici

Per impostazione predefinita, [!DNL Adobe Experience Platform Edge Network] invia tutti gli eventi che raggiungono uno stream di dati a tutti i [!DNL Experience Cloud] [servizi](/help/datastreams/configure.md#add-services) abilitati per gli stream di dati. A seconda dei casi di utilizzo, questo potrebbe non essere sempre il flusso di lavoro ideale.

Le configurazioni dello stream di dati dinamici gestiscono questo problema attraverso set di regole definite dall&#39;utente per ogni servizio abilitato per lo stream di dati, che controllano quale soluzione [!DNL Experience Cloud] riceve ogni tipo di dati.

## Prerequisiti {#prerequisites}

Per creare una configurazione dinamica per lo stream di dati, è necessario soddisfare due condizioni:

* Devi avere creato *almeno* uno stream di dati con cui lavorare. Per informazioni dettagliate, consulta la documentazione su come [creare uno stream di dati](/help/datastreams/configure.md).
* *almeno* un servizio [!DNL Experience Cloud] aggiunto allo stream di dati. Per informazioni dettagliate, consulta la documentazione su come [aggiungere un servizio](/help/datastreams/configure.md#add-services) a uno stream di dati.

Dopo aver creato uno stream di dati e aggiunto un servizio Experience Cloud, puoi [creare una configurazione dinamica](#create-dynamic-configuration).

## Guardrail {#guardrails}

Le configurazioni dello stream di dati dinamici hanno limiti e vincoli di prestazioni specifici per garantire prestazioni di sistema ed efficienza di elaborazione dei dati ottimali. Durante la configurazione delle regole dello stream di dati dinamici si applicano i seguenti guardrail:

| Guardrail | Limite | Tipo di limite |
|---------|------------|------|
| Numero massimo di configurazioni dello stream di dati dinamici per stream di dati per i servizi Experience Platform | 5 | Guardrail delle prestazioni |
| Numero massimo di configurazioni dello stream di dati dinamici per stream di dati per l’inoltro di eventi | 5 | Guardrail delle prestazioni |
| Numero massimo di configurazioni dello stream di dati dinamici per stream di dati per [!DNL Adobe Analytics] | 5 | Guardrail delle prestazioni |
| Numero massimo di configurazioni dello stream di dati dinamici per stream di dati per [!DNL Adobe Target] | 5 | Guardrail delle prestazioni |
| Numero massimo di configurazioni dello stream di dati dinamici per stream di dati per [!DNL Adobe Audience Manager] | 5 | Guardrail delle prestazioni |
| Numero massimo di condizioni (predicati) che è possibile combinare all’interno di una singola regola | 100 | Guardrail delle prestazioni |
| Tempo massimo consentito per valutare tutte le configurazioni dello stream di dati dinamici per stream di dati prima del timeout | 25 ms | Guarddrail imposto dal sistema |

## Configurazioni dello stream di dati dinamici e sostituzioni della configurazione dello stream di dati {#dynamic-versus-overrides}

Le configurazioni dello stream di dati dinamici e le [sostituzioni della configurazione dello stream di dati](/help/datastreams/overrides.md) si escludono a vicenda.

Non è possibile utilizzare le configurazioni dello stream di dati dinamici insieme alle sostituzioni della configurazione dello stream di dati. Devi scegliere l&#39;uno o l&#39;altro.

Se abiliti entrambi, le sostituzioni di configurazione hanno la precedenza e il sistema ignora le regole di configurazione dello stream di dati dinamico.

## Creare una configurazione dello stream di dati dinamico {#create-dynamic-configuration}

Dopo che hai [creato uno stream di dati](configure.md) e [aggiunto un servizio](configure.md#add-services), segui i passaggi seguenti per aggiungere una configurazione dinamica al servizio.

1. Vai alla pagina **[!UICONTROL Data Collection]** > **[!UICONTROL Datastreams]** e seleziona lo stream di dati creato.

   ![Interfaccia utente per gli stream di dati con l&#39;elenco degli stream di dati.](assets/configure-dynamic-datastream/select-datastream.png)

1. Selezionare l&#39;opzione **[!UICONTROL Edit]** nel servizio per il quale si desidera definire una configurazione dinamica.

   ![Interfaccia utente Datastreams con i servizi aggiunti a un datastream.](assets/configure-dynamic-datastream/select-service.png)

1. Nella pagina **[!UICONTROL Configure]**, selezionare **[!UICONTROL Save and Edit Dynamic Configuration]**.

   ![Interfaccia utente Datastreams che mostra la pagina di configurazione dello stream di dati.](assets/configure-dynamic-datastream/save-and-edit.png)

1. Seleziona **[!UICONTROL Add Dynamic Configuration]**.

   ![Interfaccia utente Datastreams che mostra la pagina di configurazione dinamica prima dell&#39;aggiunta di eventuali regole.](assets/configure-dynamic-datastream/add-dynamic-config.png)

1. Dal pannello **[!UICONTROL Resources]**, trascina e rilascia gli elementi con cui desideri creare la regola sul lato destro della finestra. Puoi combinare più risorse per creare regole complesse.

   Utilizza le opzioni di ogni risorsa, ad esempio **[!UICONTROL equals]**, **[!UICONTROL does not equal]**, **[!UICONTROL exists]** e altre, per ottimizzare le regole.

   ![Interfaccia utente Datastreams che mostra il generatore di regole di configurazione dinamica con le risorse trascinate.](assets/configure-dynamic-datastream/drag-resources.png)

1. Nella sezione **[!UICONTROL Configuration]** abilitare o disabilitare i servizi per ogni regola, a seconda che si desideri inviare i dati a ogni servizio. Se si disabilita un servizio, il routing verrà disabilitato e *nessun dato* verrà inviato al servizio downstream.

   ![Interfaccia utente Datastreams che mostra la regola di configurazione dinamica con gli interruttori del servizio.](assets/configure-dynamic-datastream/enable-service.png)

1. Al termine, selezionare **[!UICONTROL Save]**.

## Considerazioni sulla priorità delle regole {#rule-priority}

Puoi definire più regole per ogni configurazione dello stream di dati dinamico. Tuttavia, se i dati corrispondono alle condizioni di più regole, viene presa in considerazione solo la prima regola corrispondente nell’elenco e tutte le altre regole corrispondenti vengono ignorate.

Per ottenere il comportamento di indirizzamento dei dati desiderato, presta attenzione all’ordine in cui disponi le regole.

Per configurare l&#39;ordine delle regole, è possibile trascinare e rilasciare le finestre delle regole nell&#39;ordine desiderato.

![Riordinamento delle regole dello stream di dati dinamici tramite trascinamento della selezione.](assets/configure-dynamic-datastream/move-rules.gif)

## Criteri di idoneità delle regole {#eligibility-criteria}

Le configurazioni dello stream di dati dinamici devono soddisfare criteri di idoneità specifici per garantire prestazioni, manutenibilità e chiarezza elevate. Di seguito sono riportati i requisiti principali e le best practice per la definizione delle regole.

### Tipi di dati supportati {#supported-data-types}

Le regole di configurazione dello stream di dati dinamici funzionano con tipi di dati specifici per garantire prestazioni ottimali e un routing dei dati affidabile. Sapere quali tipi di dati sono supportati consente di creare regole efficaci per elaborare i dati in modo efficiente.

| Tipo di dati | Stato | Note |
|-----------|--------|-------|
| Stringa | Consentito | - |
| Numero (intero, lungo, breve, byte) | Consentito | - |
| Enumerazione | Consentito | - |
| Booleano | Consentito | - |
| Data | Consentito | - |
| Array | Non consentito | Le regole basate su array non sono supportate, in quanto possono compromettere le prestazioni. |
| Mappa | Non consentito | Le regole basate sulle mappe non sono supportate, in quanto possono compromettere le prestazioni. |

### Operatori supportati {#supported-operators}

Le regole possono utilizzare i seguenti operatori, a seconda del tipo di dati:

| Tipo di dati | Operatori supportati |
|-----------|-------------------|
| **Stringa** | `equals`, `starts with`, `ends with`, `contains`, `exists`, `does not equal`, `does not start with`, `does not end with`, `does not contain`, `does not exist` |
| **Numero (Lungo, Intero, Breve, Byte)** | `equals`, `does not equal`, `greater than`, `less than`, `greater than or equal to`, `less than or equal to`, `exists`, `does not exist` |
| **Booleano** | `equals true/false`, `does not equal true/false` |
| **Enum** | `equals`, `does not equal`, `exists`, `does not exist` |
| **Data** | `today`, `yesterday`, `this month`, `this year`, `custom date`, `in last`, `from`, `during`, `within`, `before`, `after`, `rolling range`, `in next`, `exists`, `does not exist` |
| **Logico** | `INCLUDE`, `ANY/ALL` (equivalente a [!DNL AND]/[!DNL OR]) |

>[!NOTE]
>
>L&#39;operatore **[!UICONTROL EXCLUDE]** non è supportato direttamente, ma è possibile ottenere una logica equivalente utilizzando **[!UICONTROL INCLUDE]** con operatori di confronto negati (ad esempio, &quot;non è uguale a&quot;).

### Struttura delle regole {#rule-structure}

Durante la creazione di regole per le configurazioni di flussi di dati dinamici, è importante comprendere i requisiti strutturali che garantiscono prestazioni e compatibilità del sistema ottimali. La struttura delle regole influisce direttamente sull’efficienza con cui i dati vengono elaborati e instradati attraverso il sistema.

**Utilizza solo espressioni flat**. È necessario definire le regole come espressioni logiche semplici. Le espressioni logiche nidificate (utilizzando contenitori o più livelli di [!DNL AND]/[!DNL OR]) non sono supportate. Se hai bisogno di una logica complessa, suddividila in più regole semplici.

Ad esempio, considera la seguente regola complessa.

![Esempio di regola complessa nidificata con più condizioni AND/OR.](assets/configure-dynamic-datastream/complex-rule.png)

Puoi suddividere questa regola nelle seguenti regole più semplici:

![Prima regola semplificata, sostituzione della regola complessa nidificata.](assets/configure-dynamic-datastream/simple-rule-1.png)

![Seconda regola semplificata, che sostituisce la regola complessa nidificata.](assets/configure-dynamic-datastream/simple-rule-2.png)

**Evita regole complesse**. Regole più semplici garantiscono una valutazione più rapida e una migliore manutenzione.

### Best practice {#best-practices}

Le best practice per la creazione di regole di configurazione dello stream di dati dinamici garantiscono prestazioni ottimali, affidabilità del sistema e configurazioni gestibili. Queste linee guida aiutano a evitare insidie comuni e a creare regole efficienti che funzionano perfettamente con l’architettura della piattaforma.

* **Regole semplici e piatte.** Se devi esprimere una logica complessa, utilizza più regole invece di nidificare.
* **Utilizzare solo [tipi di dati supportati](#supported-data-types) e [operatori](#supported-operators).**
* **Verifica le prestazioni delle regole.** Regole eccessivamente complesse o non supportate possono causare il rifiuto da parte del sistema o influire sulle prestazioni del sistema.

