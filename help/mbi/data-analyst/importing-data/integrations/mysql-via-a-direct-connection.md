---
title: Connessione di MySQL tramite una connessione diretta
description: Scopri come connetterti [!DNL MongoDB] tramite connessione diretta.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# Connetti [!DNL MySQL] tramite connessione diretta

## In questo argomento

* [Consenti accesso all&#39;indirizzo IP  [!DNL Commerce Intelligence] ](#allowlist)
* [Crea un  [!DNL MySQL]  utente per  [!DNL Commerce Intelligence]](#steptwo)
* [Immetti le informazioni di connessione in  [!DNL Commerce Intelligence]](#stepthree)

## Passa a

* [[!DNL MySQL] tramite ](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] tramite [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe] consiglia di utilizzare [SSH](../integrations/mysql-via-ssh-tunnel.md) o un&#39;altra forma di crittografia per proteggere i dati. Se questa non è un&#39;opzione, è comunque possibile connettere direttamente [!DNL Commerce Intelligence] al database utilizzando le istruzioni riportate in questo argomento.

Questo argomento illustra come collegare direttamente il database [!DNL MySQL] a [!DNL Commerce Intelligence]. Queste impostazioni possono essere utilizzate anche con [!DNL Adobe Commerce] o altri database di eCommerce che utilizzano MySQL.

## Consenti accesso agli indirizzi IP [!DNL Commerce Intelligence] {#allowlist}

Affinché la connessione abbia esito positivo, è necessario configurare il firewall per consentire l&#39;accesso dagli indirizzi IP. Sono `54.88.76.97` e `34.250.211.151`, ma si trova anche nella pagina delle credenziali di [!DNL MySQL]:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Crea un utente [!DNL MySQL] per [!DNL Commerce Intelligence]

Il modo più semplice per creare un utente `MySQL` per [!DNL Commerce Intelligence] consiste nell&#39;eseguire la seguente query quando si è connessi a `MySQL` con privilegi `GRANT`. Sostituisci `Commerce Intelligence IP Address` con l&#39;indirizzo IP [!DNL Commerce Intelligence] e sostituisci `secure password` con una password sicura a tua scelta:

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

Per impedire a questo utente di accedere ai dati in database, tabelle o colonne specifiche, è possibile eseguire `GRANT` query che consentono solo l&#39;accesso ai dati consentiti.

**Eseguire nuovamente la query GRANT per tutti gli IP richiesti utilizzando lo stesso utente e la stessa password.**

## Immetti le informazioni di connessione in Commerce Intelligence

Per concludere, devi immettere la connessione e le informazioni utente in [!DNL Commerce Intelligence]. Hai lasciato aperta la pagina delle credenziali di [!DNL MySQL]? In caso contrario, passare a **[!UICONTROL Data** > **Connections]** e fare clic su **[!UICONTROL Add New Data Source]**, quindi fare clic sull&#39;icona [!DNL MySQL]. Non dimenticare di cambiare `Encrypted` in `Yes`.

Immettere le informazioni seguenti in questa pagina, a partire dalla sezione `Database Connection`:

* `Connection Nickname`: immettere un nome per l&#39;integrazione (ad esempio, e-commerce Store)
* `Username`: nome utente per l&#39;utente [!DNL Commerce Intelligence] [!DNL MySQL]
* `Password`: password per l&#39;utente [!DNL Commerce Intelligence] [!DNL MySQL]
* `Port`: porta MySQL nel server (`3306` per impostazione predefinita)
* `Host`: per impostazione predefinita, è localhost. In generale, si tratta del valore di indirizzo di binding per il server [!DNL MySQL], che per impostazione predefinita è `127.0.0.1 (localhost)`, ma potrebbe anche essere un indirizzo di rete locale (ad esempio, `192.168.0.1`) o l&#39;indirizzo IP pubblico del server.

  Il valore si trova nel file `my.cnf` (che si trova in `/etc/my.cnf`) sotto la riga che recita `\[mysqld\]`. Se la riga dell&#39;indirizzo di associazione viene inserita come commento in tale file, il server viene protetto dai tentativi di connessione esterni.

Al termine, fare clic su **[!UICONTROL Save & Test]** per completare la configurazione.

## Documentazione correlata

* [Nuova autenticazione delle integrazioni](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
