---
keywords: Experience Platform;home;argomenti popolari;servizio identità;servizio identità;dispositivi condivisi;dispositivi condivisi
solution: Experience Platform
title: Panoramica dei dispositivi condivisi (Beta)
topic-legacy: tutorial
description: Rilevamento dispositivi condiviso identifica diversi utenti autenticati dello stesso dispositivo, consentendo una rappresentazione più accurata dei dati dei clienti nei grafici delle identità
hide: true
hidefromtoc: true
source-git-commit: 1cdab6ce71c748ae174700ce50f50b143e46b40f
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# Panoramica su Rilevamento dispositivi condiviso (Beta)

>[!IMPORTANT]
>
>La funzione [!DNL Shared Device Detection] è in versione beta. Le sue funzioni e la sua documentazione sono soggette a modifiche.

Adobe Experience Platform [!DNL Identity Service] ti aiuta a ottenere una visione migliore del cliente e del suo comportamento attraverso il collegamento di identità tra dispositivi e sistemi, consentendoti di offrire esperienze digitali personali di grande impatto in tempo reale.

[!DNL Shared Device] si riferisce ai dispositivi utilizzati da più di una persona. Alcuni esempi di dispositivi condivisi sono tablet, computer libreria e chioschi. Attraverso la funzione [!DNL Shared Device Detection] è possibile evitare che utenti diversi dello stesso dispositivo vengano uniti in un&#39;unica identità, consentendo una rappresentazione più precisa di un singolo utente.

Con [!DNL Shared Device Detection] puoi:

* Creare grafici di identità separati per utenti diversi dello stesso dispositivo;
* Impedire la miscelazione di dati provenienti da persone diverse che utilizzano lo stesso dispositivo;
* Genera una visione più pulita e più precisa dei tuoi clienti.

>[!TIP]
>
>Le configurazioni per [!DNL Shared Device Detection] devono essere completate prima di abilitare Profilo per il set di dati perché non è più possibile modificare le impostazioni dopo la generazione dei grafici in [!DNL Identity Service].

## Introduzione

Per lavorare con [!DNL Shared Device Detection] è necessario conoscere i vari servizi Platform coinvolti. Prima di iniziare a lavorare con [!DNL Shared Device Detection], controlla la documentazione relativa ai seguenti servizi:

* [[!DNL Identity Service]](../home.md): Ottieni una visione migliore dei singoli clienti e del loro comportamento attraverso il collegamento delle identità tra dispositivi e sistemi.
   * [Visualizzatore](./identity-graph-viewer.md) grafico di identità: Visualizza e interagisci con il visualizzatore del grafico delle identità per comprendere meglio in che modo le identità dei clienti sono unite e in che modo.
   * [Namespace](../namespaces.md) di identità: Scopri i componenti di un’identità completa e come i namespace di identità consentono di distinguere il contesto e il tipo di un’identità.

### Terminologia

La tabella seguente contiene un elenco di termini essenziali per comprendere [!DNL Shared Device Detection]:

| Termini | Definizione |
| --- | --- |
| Dispositivo condiviso | Un dispositivo condiviso è qualsiasi dispositivo utilizzato da più di un singolo utente. Esempi di dispositivi condivisi sono tablet, computer libreria e chioschi. |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] si riferisce a un&#39;impostazione di configurazione che consente di separare i dati provenienti da diversi utenti dello stesso dispositivo. |
| [!UICONTROL Spazio dei nomi identità condiviso] | Un [!UICONTROL spazio dei nomi identità condivisa] viene utilizzato per rappresentare un singolo dispositivo condiviso da più utenti diversi. |
| [!UICONTROL Namespace User Identity] | Un [!UICONTROL Spazio dei nomi identità utente] viene utilizzato per rappresentare l&#39;utente autenticato o connesso di un dispositivo condiviso. |

## Interfaccia utente dei dispositivi condivisi

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Identità]** dal menu di navigazione a sinistra, quindi seleziona **[!UICONTROL Impostazioni identità]**.

![dashboard delle identità](../images/shared-device/identity-dashboard.png)

Viene visualizzata la pagina [!UICONTROL Impostazioni dispositivo condiviso] , che fornisce un&#39;interfaccia per configurare le impostazioni del dispositivo condiviso per i dati. Le impostazioni del dispositivo condiviso sono disabilitate per impostazione predefinita.

Quando è attivata, le impostazioni del dispositivo condiviso consentono di separare i dati di diversi utenti dello stesso dispositivo. Questa impostazione di configurazione consente una rappresentazione più pulita e accurata dei grafici di identità, in cui le identità dell&#39;utente dello stesso dispositivo non sono combinate tra loro.

Seleziona **[!UICONTROL Abilita]** per iniziare a modificare le impostazioni del dispositivo condiviso.

![enable-shared-device](../images/shared-device/enable-shared-device.png)

Vengono visualizzate le opzioni di configurazione [!UICONTROL Spazio dei nomi identità condivisa] e [!UICONTROL Spazio dei nomi identità utente], che consentono di modificare i namespace identità che si desidera utilizzare.

![set-namespaces](../images/shared-device/set-namespaces.png)

[!UICONTROL Il ] namespace Shared Identity rappresenta un singolo dispositivo utilizzato da più utenti diversi. Questo namespace è sempre impostato su **[!UICONTROL ECID]** perché tutti gli utenti di Platform utilizzano **[!UICONTROL ECID]** come identificatore del browser Web.

![shared-identity-namespace](../images/shared-device/shared-identity-namespace.png)

Il [!UICONTROL Spazio dei nomi identità utente] consente di identificare diversi utenti dello stesso dispositivo e di impedire la combinazione dei dati nello stesso grafico di identità.

![user-identity-namespace](../images/shared-device/user-identity-namespace.png)

Seleziona la barra di ricerca **[!UICONTROL Spazio dei nomi identità utente]** e immetti uno spazio dei nomi di identità o seleziona uno spazio dei nomi di identità dal menu a discesa.

>[!TIP]
>
>È necessario mappare [!UICONTROL Spazio dei nomi identità utente] allo spazio dei nomi identità corrispondente all&#39;ID di accesso dell&#39;utente finale. Le opzioni includono ID cliente, e-mail e e-mail con hash.

![e-mail](../images/shared-device/emails.png)

Dopo aver configurato le [!UICONTROL impostazioni del dispositivo condiviso], selezionare **[!UICONTROL Salva]**.

![save](../images/shared-device/save.png)

Viene visualizzata una finestra a comparsa che richiede di confermare la selezione. Selezionare **[!UICONTROL Sì]** per completare l&#39;impostazione di configurazione.

![confermare](../images/shared-device/confirm.png)
