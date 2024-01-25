---
keywords: Experience Platform;home;argomenti popolari;servizio identità;servizio identità;dispositivi condivisi;dispositivi condivisi
title: Panoramica dei dispositivi condivisi (Beta)
description: Il rilevamento di dispositivi condivisi identifica diversi utenti autenticati dello stesso dispositivo, consentendo una rappresentazione più precisa dei dati dei clienti nei grafici delle identità
hide: true
hidefromtoc: true
exl-id: 36318163-ba07-4209-b1be-dc193ab7ba41
source-git-commit: d7c7bed74d746aba2330ecba62f9f810fbaf0d63
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# Panoramica di Rilevamento dispositivi condivisi (Beta)

>[!IMPORTANT]
>
>Il [!DNL Shared Device Detection] la funzionalità è in versione beta. Le sue funzioni e la sua documentazione sono soggette a modifiche.

Adobe Experience Platform [!DNL Identity Service] ti consente di avere una visione migliore del cliente e del suo comportamento collegando le identità tra dispositivi e sistemi, consentendoti di fornire esperienze digitali personali e di impatto in tempo reale.

[!DNL Shared Device] si riferisce a dispositivi utilizzati da più utenti. Alcuni esempi di dispositivi condivisi sono tablet, computer di libreria e chioschi. Attraverso il [!DNL Shared Device Detection] , è possibile impedire che utenti diversi dello stesso dispositivo vengano uniti in un&#39;unica identità, consentendo una rappresentazione più accurata di un individuo.

Con [!DNL Shared Device Detection] è possibile:

* Creare grafici di identità separati per utenti diversi dello stesso dispositivo;
* impedire che si mescolino dati provenienti da individui diversi che utilizzano lo stesso dispositivo;
* Genera una visualizzazione più pulita e precisa dei tuoi clienti.

>[!TIP]
>
>Configurazioni per [!DNL Shared Device Detection] deve essere completato prima di abilitare il profilo per il set di dati, perché non è più possibile rivedere le impostazioni una volta generati i grafici in [!DNL Identity Service].

## Guida introduttiva a [!DNL Shared Device Detection]

Utilizzo di [!DNL Shared Device Detection] richiede una comprensione dei vari servizi di Platform coinvolti. Prima di iniziare a lavorare con [!DNL Shared Device Detection], consulta la documentazione relativa ai seguenti servizi:

* [[!DNL Identity Service]](./home.md): ottieni una visione migliore dei singoli clienti e del loro comportamento collegando le identità tra dispositivi e sistemi.
   * [Visualizzatore del grafico delle identità](./features/identity-graph-viewer.md): visualizza e interagisce con il visualizzatore del grafico delle identità per comprendere meglio come e in quali modi le identità dei clienti sono unite tra loro.
   * [Spazi dei nomi delle identità](./features/namespaces.md): scopri i componenti di un’identità completa e come gli spazi dei nomi di identità ti consentono di distinguere il contesto e il tipo di un’identità.

## Comprensione di [!DNL Shared Device Detection]

È importante comprendere la seguente terminologia quando si lavora con
[!DNL Shared Device Detection]. Consulta la tabella seguente per un elenco dei termini essenziali per comprendere [!DNL Shared Device Detection].

### Terminologia

| Termini | Definizione |
| --- | --- |
| Dispositivo condiviso | Per dispositivo condiviso si intende qualsiasi dispositivo utilizzato da più utenti. Alcuni esempi di dispositivi condivisi sono tablet, computer di libreria e chioschi. |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] fa riferimento a un’impostazione di configurazione che consente di separare i dati di utenti diversi dello stesso dispositivo. |
| Spazio dei nomi dell’identità condivisa | Lo spazio dei nomi dell’identità condivisa rappresenta il dispositivo che può essere utilizzato da più utenti. Lo spazio dei nomi dell’identità condivisa è in genere l’ECID, ma può essere impostato su altri ID dispositivo. |
| Spazio dei nomi identità utente | Lo spazio dei nomi User Identity rappresenta l&#39;utente autenticato (connesso) di un dispositivo condiviso. |
| Ultimo utente autenticato | L&#39;ultimo utente autenticato rappresenta l&#39;utente che ha eseguito l&#39;ultimo accesso a un dispositivo, se un dispositivo è connesso da più account. |

{style="table-layout:auto"}

[!DNL Shared Device Detection] funziona stabilendo due spazi dei nomi: **Spazio dei nomi dell’identità condivisa** e **Spazio dei nomi identità utente**.

* Lo spazio dei nomi dell’identità condivisa rappresenta il dispositivo che può essere utilizzato da più utenti. L’Adobe consiglia ai clienti di utilizzare ECID come identificatore del dispositivo condiviso.
* Lo spazio dei nomi dell’identità utente è mappato allo spazio dei nomi dell’identità che corrisponde all’ID di accesso di un utente. Può trattarsi dell’ID del sistema di gestione delle relazioni con i clienti, dell’indirizzo e-mail, dell’e-mail con hash o del numero di telefono di un utente.

Un dispositivo condiviso, come un tablet, ha un singolo **Spazio dei nomi dell’identità condivisa**. D&#39;altra parte, ogni utente di un dispositivo condiviso ha il proprio **Spazio dei nomi identità utente** che corrisponde ai rispettivi ID di accesso. Ad esempio, un tablet condiviso tra Kevin e Nora per l’utilizzo nel commercio elettronico ha il proprio ECID di `1234`, mentre Kevin ha il proprio spazio dei nomi User Identity mappato su `kevin@email.com` e a Nora è mappato il proprio spazio dei nomi User Identity `nora@email.com` account.

[!DNL Shared Device Detection] è in grado di fare distinzioni tra più utenti dello stesso dispositivo collegando lo spazio dei nomi dell’identità condivisa (ad es. ECID) con lo spazio dei nomi User Identity (ID accesso) dell’ultimo utente autenticato.

### Invio dei dati di identità a un grafico delle identità

Prendi in considerazione l’esempio seguente per comprendere come [!DNL Shared Device Detection] funziona:

>[!NOTE]
>
>In questo diagramma, lo spazio dei nomi dell’identità condivisa è configurato in ECID e lo spazio dei nomi dell’identità utente in ID CRM.

![diagramma](./images/shared-device/diagram.png)

* Kevin e Nora condividono un tablet per visitare un sito web di e-commerce. Tuttavia, entrambi dispongono di una propria contabilità indipendente che utilizzano ciascuno per navigare e fare acquisti online;
   * In quanto dispositivo condiviso, il tablet ha un ECID corrispondente che rappresenta l’ID cookie del browser web del tablet;
* Supponiamo che Kevin utilizzi la compressa e **accedi** sul suo account di e-commerce per cercare le cuffie, ciò significa che l&#39;ID CRM di Kevin (**Spazio dei nomi identità utente**) è ora collegato all’ECID del tablet (**Spazio dei nomi dell’identità condivisa**). I dati di navigazione del tablet sono ora incorporati con il grafo delle identità di Kevin.
   * Se Kevin **disconnetti** e Nora utilizza la compressa e **accedi** sul proprio account e acquista una fotocamera, quindi il suo ID CRM è ora collegato all’ECID del tablet. Pertanto, i dati di navigazione del tablet sono ora incorporati con il grafo di identità di Nora.
   * Se Nora **non esce** e Kevin usa la compressa, ma... **non effettua l’accesso** Quindi i dati di navigazione del tablet vengono ancora incorporati con Nora, perché rimane come utente autenticato e il suo ID CRM è ancora collegato all&#39;ECID del tablet.
   * Se Nora **effettua la disconnessione** e Kevin usa la compressa, ma... **non effettua l’accesso**, quindi i dati di navigazione del tablet sono ancora incorporati con il grafo di identità di Nora, perché come **ultimo utente autenticato**, il suo ID CRM rimane collegato all’ECID del tablet.
   * Se Kevin **accedi** di nuovo, il suo ID CRM ora viene collegato all&#39;ECID del tablet, perché ora è l&#39;ultimo utente autenticato e i dati di navigazione del tablet sono ora incorporati con il suo grafo di identità.

### Come [!DNL Profile Service] unisce i frammenti di profilo con [!DNL Shared Device Detection] abilitato

[!DNL Profile Service] prende nota dei frammenti di profilo e dei profili uniti. Ogni singolo profilo cliente è composto da più frammenti di profilo che sono stati uniti per formare un’unica vista di quel cliente. Ad esempio, se un cliente interagisce con il tuo marchio su più canali, la tua organizzazione avrà più frammenti di profilo relativi a quel singolo cliente che appaiono in più set di dati. Quando questi frammenti vengono acquisiti in Platform, vengono uniti per creare un unico profilo per quel cliente.

Quando [!DNL Shared Device Detection] è abilitato, [!DNL Profile] definisce l’identità primaria del frammento di profilo in base al fatto che l’evento esperienza sia autenticato o meno

Un **evento esperienza autenticato** è un’azione completata da un utente durante l’accesso a un dispositivo. Per gli eventi di esperienza autenticati, l’identità principale è **Spazio dei nomi identità utente** (ID accesso). Un **evento esperienza non autenticato** è un’azione completata da un utente che non ha effettuato l’accesso a un dispositivo. Per gli eventi di esperienza non autenticati, l’identità principale è **Spazio dei nomi dell’identità condivisa** (ECID)

Per ulteriori informazioni, vedere  [[!DNL Real-Time Customer Profile] panoramica](../profile/home.md).

## Interfaccia utente per dispositivi condivisi

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Identità]** dal menu di navigazione a sinistra, quindi seleziona **[!UICONTROL Impostazioni identità]**.

![identity-dashboard](./images/shared-device/identity-dashboard.png)

Il [!UICONTROL Impostazioni dispositivo condiviso] viene visualizzata una pagina che offre un’interfaccia per configurare le impostazioni del dispositivo condiviso per i dati. Le impostazioni dei dispositivi condivisi sono disattivate per impostazione predefinita.

Quando questa opzione è attivata, le impostazioni per i dispositivi condivisi consentono di separare i dati di utenti diversi dello stesso dispositivo. Questa impostazione di configurazione consente una rappresentazione più pulita e precisa dei grafici di identità, in cui le identità utente dello stesso dispositivo non vengono combinate tra loro.

Seleziona **[!UICONTROL Abilita]** per iniziare a modificare le impostazioni del dispositivo condiviso.

![enable-shared-device](./images/shared-device/enable-shared-device.png)

Il [!UICONTROL Spazio dei nomi dell’identità condivisa] e [!UICONTROL Spazio dei nomi identità utente] vengono visualizzate le opzioni di configurazione che consentono di modificare gli spazi dei nomi delle identità che desideri utilizzare.

![set-namespace](./images/shared-device/set-namespaces.png)

[!UICONTROL Spazio dei nomi dell’identità condivisa] rappresenta un singolo dispositivo utilizzato da più utenti diversi. Questo spazio dei nomi è sempre impostato su **[!UICONTROL ECID]** perché tutti gli utenti di Platform utilizzano **[!UICONTROL ECID]** come identificatore del browser web.

![shared-identity-namespace](./images/shared-device/shared-identity-namespace.png)

Il [!UICONTROL Spazio dei nomi identità utente] consente di identificare utenti diversi dello stesso dispositivo e di evitare che i dati vengano combinati nello stesso grafico delle identità.

![user-identity-namespace](./images/shared-device/user-identity-namespace.png)

Seleziona la **[!UICONTROL Spazio dei nomi identità utente]** barra di ricerca e immetti uno spazio dei nomi identità o seleziona uno spazio dei nomi identità dal menu a discesa.

>[!TIP]
>
>Il [!UICONTROL Spazio dei nomi identità utente] deve essere mappato allo spazio dei nomi dell’identità che corrisponde all’ID di accesso dell’utente finale. Le opzioni includono ID cliente, e-mail e e-mail con hash.

![email](./images/shared-device/emails.png)

Dopo aver configurato [!UICONTROL Impostazioni dispositivo condiviso], seleziona **[!UICONTROL Salva]**.

![salva](./images/shared-device/save.png)

Viene visualizzata una finestra pop-up che richiede di confermare la selezione. Seleziona **[!UICONTROL Sì]** per completare l&#39;impostazione di configurazione.

![conferma](./images/shared-device/confirm.png)
