---
title: Panoramica dell’origine di SAP Commerce
description: Scopri come collegare SAP Commerce a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
last-substantial-update: 2023-07-26T00:00:00Z
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 99edb8b2bcd4225235038e966a367d91375c961a
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 3%

---

# [!DNL SAP Commerce]

>[!NOTE]
>
>Il [!DNL SAP Commerce] sorgente in versione beta. Consulta la [panoramica sulle origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

[[!DNL SAP Commerce]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), una piattaforma di e-commerce basata su cloud per le aziende B2B e B2C è disponibile come parte del portafoglio Customer Experience di SAP. [[!DNL SAP] Fatturazione abbonamento](https://www.sap.com/products/financial-management/subscription-billing.html) è un prodotto incluso nel portfolio e consente la gestione completa del ciclo di vita degli abbonamenti con esperienze di vendita e pagamento semplificate tramite integrazioni standardizzate.

Il [!DNL SAP Commerce] consente di acquisire informazioni su clienti e contatti in Platform dalla [[!DNL SAP] Fatturazione abbonamento](https://www.sap.com/products/financial-management/subscription-billing.html) Di seguito sono riportati gli endpoint API per i partner aziendali:

* [Clienti](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [Contatti](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

Inoltre, se [!DNL SAP Commerce] viene eseguito per recuperare i dati del cliente, il [Relazioni cliente-contatto](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) L’API viene inoltre chiamata per recuperare le informazioni di contatto del cliente.

## ELENCO CONSENTITI di indirizzo IP {#ip-allow-list}

Prima di utilizzare i connettori di origine, potrebbe essere necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Consulta la [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

## Prerequisiti {#prerequisites}

Prima di poter portare il [!DNL SAP Commerce] dati per Experience Platform, devi prima assicurarti di disporre dei seguenti elementi:

* A [!DNL SAP Subscription Billing] account. Se non disponi già di un account di fatturazione valido, contatta [!DNL SAP] responsabile dell’account. Consulta la sezione [[!DNL SAP] Configurazione piattaforma](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) per ulteriori dettagli.

* [!DNL SAP] chiave del servizio. Il [!DNL SAP] service key consente di accedere al [!DNL SAP Subscription Billing] API tramite Experience Platform. [!DNL SAP Commerce] richiede quanto segue:
   * ID client
   * Segreto client
   * URL. Il pattern dell’URL è il seguente: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Questo valore verrà utilizzato in seguito per ottenere i valori per `region` e `tokenEndpoint` quando [Crea connessione di base](../../tutorials/api/create/ecommerce/sap-commerce.md#base-connection) utilizzando l’API o quando [Connetti [!DNL SAP Commerce] account](../../tutorials/ui/create/ecommerce/sap-commerce.md#connect-account) tramite l’interfaccia utente di Platform.

+++Seleziona per visualizzare un esempio della chiave del servizio

```json
{ 
    "url": "https://eu10.revenue.cloud.sap/api",
    "uaa": {
        "clientid": "XXX",
        "clientsecret": "XXX",
        "url": "https://subscriptionbilling.authentication.eu10.hana.ondemand.com",
        "identityzone": "subscriptionbilling",
        "identityzoneid": "XXX",
        "tenantid": "XXX",
        "tenantmode": "dedicated",
        "sburl": "https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
        "apiurl": "https://api.authentication.eu10.hana.ondemand.com",
        "verificationkey": "XXX",
        "xsappname": "XXX",
        "subaccountid": "XXX",
        "uaadomain": "authentication.eu10.hana.ondemand.com",
        "zoneid": "XXX",
        "credential-type": "binding-secret"
    },
    "vendor": "SAP"
}
```

+++

## Passaggi successivi

La documentazione seguente fornisce informazioni sulle modalità di connessione [!DNL SAP Commerce] in Platform tramite API o l’interfaccia utente:

* [Creare una connessione di origine e un flusso di dati per portare [!DNL SAP Commerce] dati per Platform tramite API](../../tutorials/api/create/ecommerce/sap-commerce.md).
* [Connetti [!DNL SAP Commerce] Experience Platform dell’account tramite l’interfaccia utente](../../tutorials/ui/create/ecommerce/sap-commerce.md).
* [Creare un flusso di dati per un’origine utilizzando l’interfaccia utente](../../tutorials/ui/dataflow/ecommerce.md)
