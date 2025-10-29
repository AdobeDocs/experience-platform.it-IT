---
title: Panoramica di Mutual Transport Layer Security (mTLS)
description: Scopri come utilizzare mTLS per recuperare in modo sicuro i certificati pubblici rilasciati da Adobe per l’inoltro degli eventi.
exl-id: e8ee8655-213d-4d2a-93d4-d62824b53b1d
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 2%

---

# Panoramica di Mutual Transport Layer Security ([!DNL mTLS])

Associare i certificati Mutual Transport Layer Security ([!DNL mTLS]) in [!UICONTROL Environments UI] per assumere il controllo della sicurezza dell&#39;estensione. Il certificato [!DNL mTLS] è una credenziale digitale che prova l&#39;identità di un server o di un client nelle comunicazioni protette. Quando si utilizza l&#39;API del servizio [!DNL mTLS], questi certificati consentono di verificare e crittografare le interazioni con l&#39;inoltro eventi di Adobe Experience Platform. Questo processo non solo protegge i dati, ma garantisce anche che ogni connessione provenga da un partner fidato.

## Implementare [!DNL mTLS] in un nuovo ambiente {#implement-mtls}

Imposta l’ambiente di Inoltro eventi per garantire che le build della libreria vengano distribuite correttamente nella rete Edge. Durante la configurazione, puoi selezionare l’opzione di hosting più adatta alle tue esigenze di distribuzione. Al nuovo ambiente viene aggiunto automaticamente anche un certificato [!DNL mTLS] per una comunicazione sicura.

Per creare un nuovo ambiente, seleziona la scheda **[!UICONTROL Environments]** nel pannello a sinistra delle proprietà di Inoltro eventi, quindi seleziona **[!UICONTROL Add Environment]**.

![Proprietà di inoltro eventi che mostrano gli ambienti esistenti, evidenziando [!UICONTROL Add Environment].](../../../images/extensions/server/cloud-connector/add-environment.png)

Nella pagina successiva, seleziona l’ambiente da utilizzare per questa configurazione. Sono disponibili tre ambienti:

>[!NOTE]
>
>Una proprietà è limitata a un ambiente di sviluppo, uno di staging e uno di produzione.

| Ambiente | Descrizione |
| --- | --- |
| Sviluppo | L’ambiente di sviluppo consente ai membri del gruppo di testare le librerie o le modifiche in Inoltro eventi. |
| Staging | L’ambiente di staging è facoltativo e consente ai membri del gruppo approvati di testare e approvare una libreria prima che venga pubblicata. |
| Produzione | L’ambiente di produzione viene utilizzato per i dati di produzione live. |

![Schermata di selezione dell&#39;ambiente, evidenziando [!UICONTROL Select] per Sviluppo.](../../../images/extensions/server/cloud-connector/select-environment.png)

Nella pagina **[!UICONTROL Create Environment]**, immetti **[!UICONTROL Name]** e seleziona ***Adobe Managed*** dal menu a discesa **[!UICONTROL Select Host]**. **[!UICONTROL Certificate]** è ***aggiunto automaticamente***. Infine, selezionare **[!UICONTROL Save]**.

![Pagina Crea ambiente di sviluppo, evidenziando [!UICONTROL Name], [!UICONTROL Select Host] e [!UICONTROL Save].](../../../images/extensions/server/cloud-connector/create-environment.png)

L&#39;ambiente è stato creato e si è tornati alla scheda **[!UICONTROL Environments]**, che visualizza il nuovo ambiente.

![Scheda [!UICONTROL Environments], che evidenzia l&#39;ambiente di sviluppo.](../../../images/extensions/server/cloud-connector/new-environment-created.png)

## Visualizza dettagli certificato ambiente {#view-certificate}

Per visualizzare i dettagli del certificato per un ambiente, seleziona la scheda **[!UICONTROL Environments]** nel pannello a sinistra delle proprietà di Inoltro eventi, quindi seleziona l&#39;ambiente per visualizzare i dettagli.

Vengono visualizzati i seguenti dettagli del certificato:

| Nome campo | Descrizione |
| --- | --- |
| Certificato | Dettagli del certificato, tra cui:<ul><li>**Nome**: nome del certificato.</li><li>**Data di creazione**: la data di creazione del certificato.</li><li>**Stato**: lo stato corrente del certificato:<ul><li>**Corrente**: il certificato è in uso.</li><li>**Obsoleto**: il certificato non è in uso ma non è ancora scaduto. Può essere comunque selezionato per l&#39;uso.</li><li>**Scaduto**: il certificato è scaduto, non è disponibile e non è più disponibile per l&#39;uso.</li></ul></ul> |
| Scade | Data di scadenza del certificato. |
| Variable Name | Nome della variabile del certificato. |
| Stato | Lo stato corrente del certificato:<ul><li>**Depositato**: il certificato è stato distribuito correttamente ed è attivo.</li><li>**Distribuzione**: è in corso la distribuzione del certificato.</li><li>**È necessaria la distribuzione**: questo stato viene visualizzato quando si seleziona un certificato obsoleto.</li></ul> |

![Pagina Modifica ambiente di sviluppo, evidenziando [!UICONTROL Certificate] dettagli.](../../../images/extensions/server/cloud-connector/certificate-details.png)

### Selezionare e distribuire un certificato obsoleto {#deploy-obsolete-certificate}

Per utilizzare un certificato obsoleto, passa alla scheda **[!UICONTROL Environments]** nel pannello a sinistra delle proprietà di Inoltro eventi, quindi seleziona l&#39;ambiente per visualizzarne i dettagli.

![Scheda [!UICONTROL Environments], che evidenzia l&#39;ambiente di sviluppo.](../../../images/extensions/server/cloud-connector/new-environment-created.png)

Dal menu a discesa **[!UICONTROL Certificate]**, seleziona un certificato obsoleto, quindi seleziona **[!UICONTROL Save]**.

![La pagina Modifica ambiente di sviluppo, evidenziando il menu a discesa [!UICONTROL Certificate] con certificato obsoleto ed evidenziando Salva.](../../../images/extensions/server/cloud-connector/obsolete-certificate.png)

Per distribuire il certificato, selezionare **[!UICONTROL Save and deploy]** nella finestra di dialogo **[!UICONTROL Deploy Certificate]**.

![Finestra di dialogo Distribuisci certificato con Salva e distribuisci evidenziata.](../../../images/extensions/server/cloud-connector/obsolete-certificate-deploy.png)


## Passaggi successivi {#next-steps}

In questo documento viene illustrato come creare un ambiente per la proprietà Inoltro eventi, aggiungere un certificato e utilizzare un certificato obsoleto. Per ulteriori informazioni sui certificati [!DNL mTLS], vedere [[!DNL mTLS] Panoramica API servizio](../../../../data-governance/mtls-api/overview.md)

Per informazioni su come utilizzare i certificati [!DNL mTLS] nelle regole di Inoltro eventi, consulta la [panoramica dell&#39;estensione Cloud Connector](../cloud-connector/overview.md#mtls-rules).
