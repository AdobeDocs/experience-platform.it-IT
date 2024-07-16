---
title: Guida rapida
description: Scopri come iniziare a usare i tag in Adobe Experience Platform.
exl-id: 490ee344-3b18-4189-9293-2378f86fb10d
source-git-commit: 60d88be5d710314cdc6900f4b63643c740b91fa6
workflow-type: tm+mt
source-wordcount: '1521'
ht-degree: 88%

---

# Guida rapida

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

I tag sono la tecnologia di nuova generazione di Adobe Experience Platform per la gestione dei tag. È stata creata per supportare un ecosistema aperto e sostenibile, in cui chiunque può creare integrazioni che i clienti Adobe possono distribuire ai propri siti. Si tratta di una prima applicazione API, in modo che tutto ciò che puoi fare tramite l&#39;interfaccia utente tu possa anche farlo a livello di programmazione tramite un&#39;API.

Flusso di lavoro di base dei tag:

1. Configurare gruppi e utenti.
2. Accedere.
3. Creare una proprietà.
4. Installare le estensioni.
5. Creare elementi dati e regole.
6. Eseguire test nell’ambiente di sviluppo.
7. Promuovere a produzione.

## 1. Configurare gruppi e utenti

I tag sono completamente integrati con il tuo Adobe ID. Le autorizzazioni utente sono gestite tramite Admin Console con altri prodotti e soluzioni Adobe da [!DNL Creative Cloud], [!DNL Document Cloud] ed Experience Cloud.

I tag dispongono di un sistema di gestione degli utenti basato su diritti. Ciò significa che i diritti individuali devono essere concessi esplicitamente. Tali diritti sono assegnati ai gruppi, quindi gli utenti vengono aggiunti ai gruppi appropriati per poter accedere. Anche se l’organizzazione ha accesso a Raccolta dati, i singoli utenti non possono fare nulla finché non vengono espressamente concessi loro alcuni diritti da parte dell’amministratore.

Per istruzioni dettagliate su come creare gruppi e aggiungere utenti per i tag, consulta la [guida alle autorizzazioni per la raccolta dati](../../collection/permissions.md).

## 2. Accedere

Dopo aver aggiunto i diritti dei tag al tuo Adobe ID, devi accedere all’interfaccia utente di Experience Platform o all’interfaccia utente di Data Collection. Per eseguire questa operazione, passare direttamente alla [schermata di accesso Experience Cloud](https://experience.adobe.com/) e selezionare **[!UICONTROL Raccolta dati]** o **[!UICONTROL Experience Platform]**.

>[!NOTE]
>
>Se disponi di un singolo account con diritti per più organizzazioni, puoi cambiare organizzazione selezionandone il nome nella barra di controllo nella parte superiore della schermata e scegliendo un’altra organizzazione dall’elenco a discesa.

## 3. Creare una proprietà

Dopo aver effettuato l’accesso all’interfaccia utente, la prima cosa da fare è creare una proprietà. Una proprietà è fondamentalmente un contenitore che riempi con estensioni, regole, elementi dati e librerie durante la distribuzione di tag sul sito. Molte persone creano una proprietà per ciascun sito Web (o gruppo di siti strettamente correlati) in cui desiderano distribuire lo stesso set di tag.

Per ulteriori informazioni sulla creazione delle proprietà, vedi [Creazione di una proprietà](../ui/administration/companies-and-properties.md).

## 4. Installare le estensioni

Un’estensione è un’integrazione creata da Adobe o da un partner di Adobe che offre opzioni nuove e infinite per i tag che puoi implementare nei tuoi siti. Se pensi a un tag come a un sistema operativo, le estensioni sono le app che puoi installare per eseguire specifiche operazioni.

Tutte le nuove proprietà hanno installata l&#39;[estensione Core](../extensions/client/core/overview.md). Le proprietà per dispositivi mobili sono dotate di estensioni aggiuntive. L’estensione Core è creata da Adobe per fornire un set predefinito solido di tipi di elementi dati per il livello di dati, e i tipi di eventi per le regole. La maggior parte delle azioni che desideri eseguire (ottenere un ECID, inviare un beacon [!DNL Adobe Analytics], caricare la global mbox [!DNL Target], ecc.) saranno disponibili grazie alle estensioni installate dal catalogo.

Ciò che rende i tag in Platform davvero unici è che queste estensioni possono essere create da chiunque. Devi rilasciare un pixel di remarketing Facebook sul sito? Controlla l&#39;estensione creata da Facebook. Vuoi fare lo stesso per Twitter o Linked In? Utilizza le loro estensioni. Devi eseguire un sondaggio? Dai un&#39;occhiata a Question Pro o Foresee. Devi gestire la privacy e il consenso degli utenti finali, in ambito [!DNL GDPR]? Vedi se Evidon o Trust Arc fanno al caso tuo. Desideri visualizzare informazioni dettagliate sul comportamento dei singoli utenti sul tuo sito? Guarda Clicktale. Per ulteriori informazioni, vedere la sezione relativa all&#39;aggiunta di una nuova estensione [1.](../ui/managing-resources/extensions/overview.md#add-a-new-extension)

## 5. Creare elementi dati e regole

Gli **elementi dati** sono indicatori per le informazioni da raccogliere e inviare in posizioni diverse sulla pagina:

* Un livello di dati definito in JSON
* Elementi DOM
* Cookie
* Sessione e archiviazione locale
* Tutto il resto

Una volta definito l’elemento dati, puoi utilizzarlo ovunque nell’interfaccia utente per qualsiasi estensione. Per informazioni più dettagliate, consulta la documentazione sugli [elementi dati](../ui/managing-resources/data-elements.md).

Le **regole** sono il nucleo logico della tua implementazione e controllano cosa, quando, dove e come si trovano i tag sul sito. Definisci un evento, imposta condizioni ed eccezioni, quindi definisci le azioni e l&#39;ordine. Infine, pubblica le modifiche per vedere i risultati. Per ulteriori informazioni, vedi [Regole](../ui/managing-resources/rules.md).

## 6. Eseguire test nell’ambiente di sviluppo

### Librerie e build

Le build dei tag non vengono mai pubblicate automaticamente. Ogni set di modifiche è racchiuso in una [libreria](../ui/publishing/libraries.md). Ogni libreria creata eredita automaticamente qualsiasi elemento upstream (pubblicato, approvato o inviato) come linea di base, quindi tutto ciò che occorre fare è definire le modifiche desiderate. Questa libreria funge da blueprint per una [build](../ui/publishing/builds.md). Una build è il set effettivo di file JavaScript distribuiti e utilizzati.

È importante comprendere la relazione tra la pagina web, la posizione di hosting e i tag.

1. Il server host fornisce una posizione per pubblicare la build. La build stessa contiene i file JavaScript richiesti dalla libreria.

   Ogni ambiente ha una relazione con un host e l’host fornisce un endpoint che indica dove distribuire la build. L’host può appartenere a una sola proprietà, anche se una proprietà può avere diversi host.

2. Un codice di incorporamento viene fornito come tag `<script>` da inserire nelle sezioni `<head>` del sito web HTML.

   Quando crei un ambiente e alleghi un host, l’ambiente genera automaticamente un codice di incorporamento univoco che ti permette di integrare nel tuo sito la relativa build assegnata. Il codice `<script>` viene utilizzato per distribuire la build della libreria in fase di esecuzione.

3. Quando un utente esplora il sito, il tag `<script>` di codice da incorporare recupera la build dal server host ed esegue le azioni definite nel browser.

### Host

Un host è una connessione tra una proprietà tag e la posizione di hosting. I tag supportano attualmente l’hosting gestito da Adobe tramite un host [!DNL Akamai] o hosting autonomo tramite un host SFTP. Quando crei una build, i tag si connettono al server definito dall’host e distribuiscono la build.

Se desideri effettuare il self-host, una build di tag può inviare direttamente tutto al server tramite SFTP oppure puoi inviarlo tu stesso a [!DNL Akamai] e scaricarlo utilizzando l’opzione Archivio dell’ambiente.

Per ulteriori informazioni, vedi [Host](../ui/publishing/hosts/hosts-overview.md).

### Ambienti

Ogni libreria viene creata all&#39;interno di un ambiente. Un ambiente definisce la modalità di visualizzazione della build quando viene pubblicata. Puoi specificare:

* **Host:** ogni ambiente richiede un host che determini l’endpoint in cui verranno inviate tutte le build create in questo ambiente.
* **Archivio:** l’impostazione predefinita consiste nel distribuire la build come file .js minimizzato. Se utilizzi un codice personalizzato, puoi avere più file che sfanno riferimento l’uno all’altro. Questi possono essere combinati in un singolo file zip e crittografati.

Dopo aver salvato l&#39;ambiente, genera il codice da incorporare che puoi copiare e incollare nel sito Web. Il codice da incorporare non funzionerà finché non avrai creato una libreria e prodotto una build. Per ulteriori informazioni, vedi [Ambienti](../ui/publishing/environments.md).

### Pubblicare una build in Dev

Il processo di pubblicazione è descritto nei passaggi seguenti.

1. Crea un host.
1. Creare un ambiente di sviluppo utilizzando l&#39;host creato.
1. Distribuire il codice da incorporare dall&#39;ambiente di sviluppo al sito di test di sviluppo.
1. Creare una libreria e assegnarla all&#39;ambiente di sviluppo creato.
1. Generare la libreria.

## 7. Promuovere a produzione

Dopo aver testato la build nell’ambiente di sviluppo, assicurati di creare l’area di visualizzazione e gli ambienti di produzione e di inserire i codici da incorporare nelle posizioni appropriate. A questo scopo, puoi riutilizzare gli host esistenti.

La promozione di una libreria completamente accessibile alla produzione in genere richiede il coordinamento tra persone diverse con i permessi appropriati.

* Uno sviluppatore (un utente con i permessi di sviluppo) invia la libreria, cambiando il suo stato in Inviato.
* Un Approver (un utente con i permessi di approvazione) può creare la libreria nell&#39;ambiente di visualizzazione e può approvarla dopo il test. In questo modo lo stato della libreria diventa approvato. È possibile inviare e approvare una sola libreria alla volta.
* Un Publisher (un utente con i permessi di pubblicazione) può creare la libreria nell&#39;ambiente di produzione.

Puoi assegnare tutti questi permessi a una sola persona.

Per ulteriori informazioni sui diversi stati e opzioni disponibili durante il processo di pubblicazione, consulta [Flusso di lavoro di approvazione](../ui/publishing/publishing-flow.md).

## Risorse aggiuntive

Per ulteriori informazioni, consulta le seguenti risorse:

* **[Community di Data Collection](https://forums.adobe.com/community/experience-cloud/platform/launch)**: fai domande e rispondi, invia idee e vota quelle degli altri. Accedi con il tuo Adobe ID.
* **[Developer Docs](../api/overview.md)**: partecipa alla community di sviluppatori di tag per creare estensioni o utilizzare le API dei tag
* **[Panoramica dei tutorial](https://experienceleague.adobe.com/docs/core-services-learn/tutorials/overview.html?lang=it)**: questi documenti presentano i concetti relativi ai tag, inclusi l’inoltro degli eventi e Mobile SDK per app Android.
