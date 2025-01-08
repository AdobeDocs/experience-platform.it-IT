---
solution: Experience Platform
title: Panoramica di Adobe Experience Platform su più cloud
description: Scopri le differenze tra Experience Platform in esecuzione in Microsoft Azure e Amazon Web Services.
source-git-commit: d3654573cec338f173d151fd5e62ef5c8b893c11
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 3%

---


# Panoramica di Adobe Experience Platform su più cloud

Adobe Experience Platform è un prodotto multi-cloud, che consente di scegliere se eseguire su [[!DNL Microsoft Azure]](https://azure.microsoft.com/en-us) o [[!DNL Amazon Web Services (AWS)]](https://aws.amazon.com/). Questa flessibilità consente di scegliere la soluzione più adatta alle esigenze aziendali e tecniche.

>[!AVAILABILITY]
>
>Adobe Experience Platform in esecuzione su Amazon Web Services (AWS) è attualmente disponibile per un numero limitato di clienti. Per ulteriori informazioni su Experience Platform su AWS, contatta il team del tuo account Adobe.

Questa pagina fornisce una panoramica di alto livello delle due infrastrutture cloud disponibili e include indicazioni su come scegliere quella giusta per la tua azienda.

## Quale implementazione cloud è corretta per me? {#which-cloud-is-right}

La scelta tra Experienci Platform in Azure o AWS dipende da diversi fattori specifici della tua azienda:

* **Esigenze tecniche e aziendali**: valuta i requisiti della tua organizzazione e la strategia cloud a lungo termine.
* **Infrastruttura esistente**: considera l&#39;infrastruttura cloud corrente e le esigenze di integrazione.
* **Affidamento alla tecnologia cloud**: se la tua azienda si basa in larga misura sulle tecnologie Microsoft, Azure potrebbe essere la soluzione migliore. Se ti affidi maggiormente ai servizi di Amazon, AWS potrebbe essere l’opzione migliore.
* **Considerazioni sulla residenza dei dati**: valuta i requisiti di residenza dei dati per la tua organizzazione e assicurati che la piattaforma cloud scelta offra aree conformi a queste normative.

Considerando i fattori di cui sopra, utilizza questa struttura decisionale semplificata per decidere la giusta implementazione cloud in base alle esigenze aziendali.

![Immagine che mostra la distribuzione geografica delle posizioni di hosting.](assets/multi-cloud/diagram-cloud.png){align="center" zoomable="yes"}

## Località di hosting {#available-cloud-regions}

La scelta dell’area geografica cloud corretta è fondamentale per soddisfare i requisiti di residenza dei dati e garantire prestazioni ottimali.

![Immagine che mostra la distribuzione geografica delle posizioni di hosting.](assets/multi-cloud/hosting-locations-map.png){align="center" zoomable="yes"}

Experience Platform è disponibile in sei posizioni di hosting di Microsoft Azure, una posizione di hosting di Amazon Web Services (AWS) e indirizza i dati ai servizi Adobe attraverso sette [nodi Edge Network](../collection/home.md#edge) distribuiti in tutto il mondo.

### Aree geografiche di Microsoft Azure {#azure-regions}

La tabella seguente indica le aree di Microsoft Azure in cui è ospitato Experience Platform.

| Paese | Codice di regione | Posizione |
|---------|-------------|----------|
| Stati Uniti | VA7 | Virginia |
| Regno Unito | GBR9 | Londra |
| Paesi Bassi | NDL2 | Amsterdam |
| Canada | CAN2 | Toronto |
| India | IND2 | Maharashtra |
| Australia | AUS5 | Nuovo Galles del Sud |

{style="table-layout:auto"}

### Aree geografiche di Amazon Web Services (AWS) {#aws-regions}

La tabella seguente indica le aree di AWS in cui è ospitato Experience Platform. Controlla regolarmente per verificare se sono state aggiunte posizioni aggiuntive.

| Paese | Codice di regione | Posizione |
|---------|-------------|----------|
| Stati Uniti | VA6 | Virginia |

{style="table-layout:auto"}

## Parità di funzioni {#feature-parity}

Adobe si impegna a offrire parità di funzioni su tutte le piattaforme cloud, per tutte le applicazioni in esecuzione su Experience Platform, ad esempio:

* [Real-Time Customer Data Platform](../rtcdp/home.md)
* [Adobe Journey Optimizer](https://experienceleague.adobe.com/it/docs/journey-optimizer/using/ajo-home)
* [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-landing)

Tuttavia, alcune funzionalità possono differire tra le implementazioni di Azure e quelle di AWS. Tali differenze sono descritte nella sezione seguente e in altre parti della documentazione del prodotto, se applicabile.

### Differenze tra l’Experience Platform in esecuzione in Microsoft Azure e AWS {#azure-aws-differences}

La tabella seguente evidenzia le principali differenze tra l’esecuzione di Experience Platform in Microsoft Azure e AWS.

| Funzionalità/funzionalità | Microsoft Azure | Amazon Web Services |
| --- | --- | --- |
| [Conformità HIPAA](https://www.adobe.com/trust/compliance/hipaa-ready.html) | Supportato | Non supportato |
| [Catalogo dei connettori di origine](/help/sources/home.md) | Sono supportati tutti i connettori nel catalogo di origini | È disponibile un numero limitato di connettori sorgente. Qualsiasi connettore di origine disponibile per le implementazioni di AWS viene citato in una nota di alto livello nelle rispettive pagine della documentazione. |

{style="table-layout:auto"}

<!-- To be determined if we need to add this part about the AI Assistant 

| [Experience Platform AI Assistant](/help/ai-assistant/home.md) | Supported | Not supported |

-->

## Conclusione {#conclusion}

Experience Platform offre flessibilità e possibilità di scelta grazie alla possibilità di eseguire in Microsoft Azure o Amazon Web Services. Valuta le tue esigenze aziendali e l’infrastruttura esistente per prendere una decisione informata su quale piattaforma cloud utilizzare.
