---
audience: user
user-guide-title: Adobe Experience Platform Identity Service
breadcrumb-title: Guida di Platform Identity Service
user-guide-description: Collega le identità dei clienti su più dispositivi e sistemi per offrire esperienze digitali personalizzate.
feature: Identities
role: Admin,Developer
source-git-commit: 6cdb622e76e953c42b58363c98268a7c46c98c99
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 26%

---


# Adobe Experience Platform Identity Service {#identity}

- [Panoramica di Identity Service](home.md)
- [Servizio Identity e Real-Time Customer Profile](identity-and-profile.md)
- Funzioni {#features}
   - [Spazio dei nomi identità](./features/namespaces.md)
   - [Logica di collegamento dell’identità](./features/identity-linking-logic.md)
   - [Visualizzatore del grafico delle identità](./features/identity-graph-viewer.md)
   - [Eliminazioni nel servizio Identity](./features/deletion.md)
   - Regole di collegamento del grafico delle identità {#identity-graph-linking-rules}
      - [Panoramica delle funzioni](./identity-graph-linking-rules/overview.md)
      - [Algoritmo di ottimizzazione identità](./identity-graph-linking-rules/identity-optimization-algorithm.md)
      - [Guida all’implementazione per le regole di collegamento del grafico delle identità](./identity-graph-linking-rules/implementation-guide.md)
      - [Esempio di configurazioni del grafico](./identity-graph-linking-rules/example-configurations.md)
      - [Risoluzione dei problemi relativi alle regole di collegamento del grafo delle identità](./identity-graph-linking-rules/troubleshooting.md)
      - [Priorità dello spazio dei nomi](./identity-graph-linking-rules/namespace-priority.md)
      - [Interfaccia utente simulazione grafico](./identity-graph-linking-rules/graph-simulation.md)
      - [Interfaccia utente per le impostazioni delle identità](./identity-graph-linking-rules/identity-settings-ui.md)
   - [Panoramica di ECID](./features/ecid.md)
- [Guida all’implementazione](implementation.md)
- [Guardrail per i dati di identità](guardrails.md)
- API del servizio identità {#api}
   - [Guida introduttuva](api/getting-started.md)
   - [Etichettare un campo come identità](api/label-identities.md)
   - [Elencare le identità del cluster](api/list-cluster-identites.md)
   - [Elencare la cronologia cluster di un&#39;identità](api/list-cluster-history.md)
   - [Elencare mappature identità](api/list-identity-mappings.md)
   - [Elenca gli spazi dei nomi disponibili](api/list-namespaces.md)
   - [Creare uno spazio dei nomi personalizzato](api/create-custom-namespace.md)
   - [Elencare l’ID nativo di un’identità](api/list-native-id.md)
   - [Riferimento API](https://www.adobe.io/experience-platform-apis/references/identity-service)
- [Rilevamento di dispositivi condivisi](shared-device-detection.md)
- [Definire i campi di identità nell’interfaccia utente](label-identities.md)
- [Elaborazione della richiesta di accesso a dati personali](privacy.md)
- [Guida alla risoluzione dei problemi](troubleshooting-guide.md)
- [Note sulla versione della piattaforma](https://experienceleague.adobe.com/it/docs/experience-platform/release-notes/latest)