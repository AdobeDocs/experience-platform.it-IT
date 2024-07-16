---
title: Panoramica di SAP Commerce Source
description: Scopri come collegare SAP Commerce a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
last-substantial-update: 2023-07-26T00:00:00Z
badge: Beta
exl-id: d2ddfec3-a421-48a7-b765-86ce9162f26f
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 3%

---

# [!DNL SAP Commerce]

>[!NOTE]
>
>L&#39;origine [!DNL SAP Commerce] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, vedere la [panoramica origini](../../home.md#terms-and-conditions).

[[!DNL SAP Commerce]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), una soluzione di piattaforma di e-commerce basata su cloud per le aziende B2B e B2C, è disponibile come parte del portafoglio SAP Customer Experience. [[!DNL SAP] La fatturazione dell&#39;abbonamento](https://www.sap.com/products/financial-management/subscription-billing.html) è un prodotto incluso nel portfolio e consente la gestione completa del ciclo di vita dell&#39;abbonamento con esperienze di vendita e pagamento semplificate tramite integrazioni standardizzate.

L&#39;origine [!DNL SAP Commerce] consente di acquisire informazioni su clienti e contatti in Platform dagli endpoint API [[!DNL SAP] Subscription Billing](https://www.sap.com/products/financial-management/subscription-billing.html) Business Partners di seguito:

* [Clienti](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [Contatti](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

Inoltre, se [!DNL SAP Commerce] viene eseguito per recuperare i dati del cliente, viene chiamata anche l&#39;API [Customer-Contact Relationships](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) per recuperare le informazioni di contatto del cliente.

## ELENCO CONSENTITI di indirizzo IP {#ip-allow-list}

Prima di utilizzare i connettori di origine, potrebbe essere necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md).

## Prerequisiti {#prerequisites}

Prima di poter portare i dati di [!DNL SAP Commerce] all&#39;Experience Platform, è necessario assicurarsi di disporre dei seguenti elementi:

* Un account [!DNL SAP Subscription Billing]. Se non disponi già di un account di fatturazione valido, contatta il tuo account manager [!DNL SAP]. Per ulteriori informazioni, consultare il documento [[!DNL SAP] Configurazione piattaforma](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf).

* Chiave del servizio [!DNL SAP]. La chiave del servizio [!DNL SAP] ti consente di accedere all&#39;API [!DNL SAP Subscription Billing] tramite Experience Platform. [!DNL SAP Commerce] richiede quanto segue:
   * ID client
   * Segreto client
   * URL. Schema URL: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Questo valore verrà utilizzato successivamente per ottenere i valori per `region` e `tokenEndpoint` quando [crei una connessione di base](../../tutorials/api/create/ecommerce/sap-commerce.md#base-connection) utilizzando l&#39;API o quando [connetti il tuo account [!DNL SAP Commerce] ](../../tutorials/ui/create/ecommerce/sap-commerce.md#connect-account) tramite l&#39;interfaccia utente di Platform.

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

La documentazione seguente fornisce informazioni su come connettere [!DNL SAP Commerce] a Platform tramite API o tramite l&#39;interfaccia utente:

* [Crea una connessione di origine e un flusso di dati per portare [!DNL SAP Commerce] dati in Platform tramite API](../../tutorials/api/create/ecommerce/sap-commerce.md).
* [Connetti il tuo account [!DNL SAP Commerce] ad Experience Platform utilizzando l&#39;interfaccia utente](../../tutorials/ui/create/ecommerce/sap-commerce.md).
* [Creare un flusso di dati per un’origine utilizzando l’interfaccia utente](../../tutorials/ui/dataflow/ecommerce.md)
