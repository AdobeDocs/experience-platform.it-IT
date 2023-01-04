---
keywords: Experience Platform;home;argomenti popolari;servizio identità;servizio identità;dispositivi condivisi;dispositivi condivisi
title: Panoramica dei dispositivi condivisi (Beta)
description: Rilevamento dispositivi condiviso identifica diversi utenti autenticati dello stesso dispositivo, consentendo una rappresentazione più accurata dei dati dei clienti nei grafici delle identità
hide: true
hidefromtoc: true
exl-id: 36318163-ba07-4209-b1be-dc193ab7ba41
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1363'
ht-degree: 0%

---

# Panoramica su Rilevamento dispositivi condiviso (Beta)

>[!IMPORTANT]
>
>La [!DNL Shared Device Detection] funzionalità in versione beta. Le sue funzioni e la sua documentazione sono soggette a modifiche.

Adobe Experience Platform [!DNL Identity Service] consente di ottenere una visione migliore del cliente e del suo comportamento attraverso il collegamento delle identità tra dispositivi e sistemi, per offrire in tempo reale esperienze digitali personali di impatto.

[!DNL Shared Device] si riferisce ai dispositivi utilizzati da più di una persona. Alcuni esempi di dispositivi condivisi sono tablet, computer libreria e chioschi. Attraverso il [!DNL Shared Device Detection] è possibile impedire che utenti diversi dello stesso dispositivo vengano uniti in un&#39;unica identità, consentendo una rappresentazione più precisa di un singolo utente.

Con [!DNL Shared Device Detection] puoi:

* Creare grafici di identità separati per utenti diversi dello stesso dispositivo;
* Impedire la miscelazione di dati provenienti da persone diverse che utilizzano lo stesso dispositivo;
* Genera una visione più pulita e più precisa dei tuoi clienti.

>[!TIP]
>
>Configurazioni per [!DNL Shared Device Detection] deve essere completato prima di abilitare Profilo per il set di dati perché non è più possibile modificare le impostazioni una volta generati i grafici in [!DNL Identity Service].

## Guida introduttiva a [!DNL Shared Device Detection]

Utilizzo [!DNL Shared Device Detection] richiede una comprensione dei vari servizi della piattaforma coinvolti. Prima di iniziare a lavorare con [!DNL Shared Device Detection], consulta la documentazione relativa ai seguenti servizi:

* [[!DNL Identity Service]](../home.md): Ottieni una visione migliore dei singoli clienti e del loro comportamento attraverso il collegamento delle identità tra dispositivi e sistemi.
   * [Visualizzatore grafico di identità](./identity-graph-viewer.md): Visualizza e interagisci con il visualizzatore del grafico delle identità per comprendere meglio in che modo le identità dei clienti sono unite e in che modo.
   * [Namespace Identity](../namespaces.md): Scopri i componenti di un’identità completa e come i namespace di identità consentono di distinguere il contesto e il tipo di un’identità.

## Comprensione di [!DNL Shared Device Detection]

È importante comprendere la seguente terminologia quando si lavora con
[!DNL Shared Device Detection]. Vedi la tabella seguente per un elenco dei termini essenziali per comprendere [!DNL Shared Device Detection].

### Terminologia

| Termini | Definizione |
| --- | --- |
| Dispositivo condiviso | Un dispositivo condiviso è qualsiasi dispositivo utilizzato da più di un singolo utente. Esempi di dispositivi condivisi sono tablet, computer libreria e chioschi. |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] si riferisce a un&#39;impostazione di configurazione che consente di separare i dati provenienti da diversi utenti dello stesso dispositivo. |
| Spazio dei nomi identità condiviso | Spazio dei nomi di identità condivisa rappresenta il dispositivo che può essere utilizzato da più utenti. Lo spazio dei nomi di identità condivisa è in genere ECID, ma può essere impostato su altri ID dispositivo. |
| Namespace User Identity | Lo spazio dei nomi dell&#39;identità utente rappresenta l&#39;utente autenticato (connesso) di un dispositivo condiviso. |
| Ultimo utente autenticato | L&#39;ultimo utente autenticato rappresenta l&#39;utente che ha effettuato l&#39;ultimo accesso a un dispositivo, se un dispositivo è connesso da più account. |

{style=&quot;table-layout:auto&quot;}

[!DNL Shared Device Detection] crea due spazi dei nomi: la **Spazio dei nomi identità condiviso** e **Namespace User Identity**.

* Spazio dei nomi di identità condivisa rappresenta il dispositivo che può essere utilizzato da più utenti. Adobe consiglia ai clienti di utilizzare ECID come identificatore dispositivo condiviso.
* Lo spazio dei nomi dell’identità utente è mappato allo spazio dei nomi dell’identità che corrisponde all’ID di accesso di un utente, può essere un ID CRM dell’utente, un indirizzo e-mail, e-mail con hash o un numero di telefono.

Un dispositivo condiviso, come un tablet, ha un singolo **Spazio dei nomi identità condiviso**. D&#39;altra parte, ogni utente di un dispositivo condiviso ha il proprio designato **Namespace User Identity** che corrisponde ai rispettivi ID di accesso. Ad esempio, un tablet che Kevin e Nora condividono per l&#39;uso dell&#39;e-commerce ha un proprio ECID di `1234`, mentre Kevin dispone di un proprio namespace User Identity mappato sulla sua `kevin@email.com` account e Nora ha il proprio spazio dei nomi di identità utente mappato a lei `nora@email.com` conto.

[!DNL Shared Device Detection] è in grado di fare distinzioni tra più utenti dello stesso dispositivo collegando lo spazio dei nomi dell&#39;identità condivisa (ad es. ECID) con l’ultimo namespace User Identity dell’utente autenticato (ID di accesso).

### Invio dei dati di identità a un grafico di identità

Prendi in considerazione l’esempio seguente per comprendere meglio come [!DNL Shared Device Detection] opere:

>[!NOTE]
>
>In questo diagramma, lo spazio dei nomi identità condivisa è configurato per ECID e lo spazio dei nomi identità utente è configurato per l’ID CRM.

![diagramma](../images/shared-device/diagram.png)

* Kevin e Nora condividono un tablet per visitare un sito web di e-commerce. Tuttavia, entrambi hanno i propri account indipendenti che utilizzano per navigare e acquistare online;
   * Come dispositivo condiviso, il tablet ha un ECID corrispondente, che rappresenta l’ID cookie del browser Web del tablet;
* Supponiamo che Kevin utilizzi il tablet e **accedi** al suo account di e-commerce per cercare le cuffie, questo significa quindi che l&#39;ID CRM di Kevin (**Namespace User Identity**) è ora collegato all’ECID del tablet (**Spazio dei nomi identità condiviso**). I dati di navigazione del tablet sono ora incorporati con il grafico di identità di Kevin.
   * Se Kevin **disconnetti** e Nora utilizza il tablet e **accedi** sul suo account e acquista una fotocamera, il suo ID CRM è ora collegato all&#39;ECID del tablet. Pertanto, i dati di navigazione del tablet sono ora incorporati con il grafico di identità di Nora.
   * Se Nora **non effettua la disconnessione** e Kevin utilizza il tablet, ma **non effettua l&#39;accesso**, quindi i dati di navigazione del tablet sono ancora incorporati con Nora, perché rimane come utente autenticato e il suo ID CRM è ancora collegato all&#39;ECID del tablet.
   * Se Nora **disconnessione** e Kevin utilizza il tablet, ma **non effettua l&#39;accesso**, quindi i dati di navigazione del tablet sono ancora incorporati con il grafico di identità di Nora, perché come **ultimo utente autenticato**, il suo ID CRM rimane collegato all’ECID del tablet.
   * Se Kevin **accedi** di nuovo, il suo ID CRM ora viene collegato all&#39;ECID del tablet, perché ora è l&#39;ultimo utente autenticato e i dati di navigazione del tablet sono ora incorporati con il suo grafico di identità.

### Come [!DNL Profile Service] unisce frammenti di profilo con [!DNL Shared Device Detection] abilitato

[!DNL Profile Service] prende nota dei frammenti di profilo e dei profili uniti. Ogni singolo profilo cliente è composto da più frammenti di profilo che sono stati uniti per formare una singola vista del cliente. Ad esempio, se un cliente interagisce con il tuo marchio su più canali, la tua organizzazione avrà più frammenti di profilo relativi al singolo cliente che compaiono in più set di dati. Quando questi frammenti vengono acquisiti in Platform, vengono uniti per creare un singolo profilo per quel cliente.

Quando [!DNL Shared Device Detection] è abilitato, [!DNL Profile] definisce l’identità principale del frammento di profilo in base al fatto che l’evento di esperienza sia autenticato o meno

Un **evento di esperienza autenticato** è un’azione completata da un utente che ha effettuato l’accesso a un dispositivo. Per gli eventi di esperienza autenticati, l&#39;identità principale è la **Namespace User Identity** (ID di accesso). Un **evento di esperienza non autenticato** è un’azione completata da un utente che non ha effettuato l’accesso a un dispositivo. Per gli eventi di esperienza non autenticati, l&#39;identità principale è la **Spazio dei nomi identità condiviso** (ECID).

Per ulteriori informazioni, consulta la sezione  [[!DNL Real-Time Customer Profile] panoramica](../../profile/home.md).

## Interfaccia utente dei dispositivi condivisi

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Identità]** dalla navigazione a sinistra, quindi seleziona **[!UICONTROL Impostazioni identità]**.

![dashboard delle identità](../images/shared-device/identity-dashboard.png)

La [!UICONTROL Impostazioni del dispositivo condiviso] viene visualizzata una pagina che fornisce un&#39;interfaccia per configurare le impostazioni del dispositivo condiviso per i dati. Le impostazioni del dispositivo condiviso sono disabilitate per impostazione predefinita.

Quando è attivata, le impostazioni del dispositivo condiviso consentono di separare i dati di diversi utenti dello stesso dispositivo. Questa impostazione di configurazione consente una rappresentazione più pulita e accurata dei grafici di identità, in cui le identità dell&#39;utente dello stesso dispositivo non sono combinate tra loro.

Seleziona **[!UICONTROL Abilita]** per iniziare a modificare le impostazioni del dispositivo condiviso.

![enable-shared-device](../images/shared-device/enable-shared-device.png)

La [!UICONTROL Spazio dei nomi identità condiviso] e [!UICONTROL Namespace User Identity] vengono visualizzate le opzioni di configurazione, che consentono di modificare gli spazi dei nomi delle identità da utilizzare.

![set-namespaces](../images/shared-device/set-namespaces.png)

[!UICONTROL Spazio dei nomi identità condiviso] rappresenta un singolo dispositivo utilizzato da più utenti diversi. Questo spazio dei nomi è sempre impostato su **[!UICONTROL ECID]** perché tutti gli utenti di Platform utilizzano **[!UICONTROL ECID]** come identificatore del browser web.

![shared-identity-namespace](../images/shared-device/shared-identity-namespace.png)

La [!UICONTROL Namespace User Identity] consente di identificare diversi utenti dello stesso dispositivo e di impedire la combinazione dei dati nello stesso grafico di identità.

![user-identity-namespace](../images/shared-device/user-identity-namespace.png)

Seleziona la **[!UICONTROL Namespace User Identity]** barra di ricerca e immettere uno spazio dei nomi di identità oppure selezionare uno spazio dei nomi di identità dal menu a discesa.

>[!TIP]
>
>La [!UICONTROL Namespace User Identity] deve essere mappato allo spazio dei nomi dell&#39;identità che corrisponde all&#39;ID di accesso dell&#39;utente finale. Le opzioni includono ID cliente, e-mail e e-mail con hash.

![e-mail](../images/shared-device/emails.png)

Una volta configurato il tuo [!UICONTROL Impostazioni del dispositivo condiviso], seleziona **[!UICONTROL Salva]**.

![salva](../images/shared-device/save.png)

Viene visualizzata una finestra a comparsa che richiede di confermare la selezione. Seleziona **[!UICONTROL Sì]** per completare l&#39;impostazione di configurazione.

![confermare](../images/shared-device/confirm.png)
