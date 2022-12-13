**A SSL Labs Report**
![](./images/A-SSL-Labs.PNG)
```
root@(apm1)(cfg-sync Standalone)(Active)(/Common)(tmos)# list ltm profile client-ssl SSL_Qualys_A
ltm profile client-ssl SSL_Qualys_A {
    app-service none
    cert test_2022
    cert-key-chain {
        test_SectigoRSADomainValidationSecureServerCA_0 {
            cert test_2022
            chain SectigoRSADomainValidationSecureServerCA
            key test_2022
        }
    }
    chain SectigoRSADomainValidationSecureServerCA
    cipher-group none
    ciphers ECDHE-RSA-AES256-GCM-SHA384:!ECDHE+AES:!ECDHE+3DES:!RSA+3DES:!TLSv1_1:!TLSv1:!SSLv3:!MD5:!EXPORT:!RC4
    defaults-from clientssl
    inherit-ca-certkeychain true
    inherit-certkeychain false
    key test_2022
    passphrase none
}
```

**A+ SSL Labs Report**
![](./images/A+SSL-Labs.PNG)
```
root@(apm1)(cfg-sync Standalone)(Active)(/Common)(tmos)# list ltm profile client-ssl SSL_Qualys_A
ltm profile client-ssl SSL_Qualys_A {
    app-service none
    cert test_2022
    cert-key-chain {
        test_SectigoRSADomainValidationSecureServerCA_0 {
            cert test_2022
            chain SectigoRSADomainValidationSecureServerCA
            key test_2022
        }
    }
    chain SectigoRSADomainValidationSecureServerCA
    cipher-group none
    ciphers ECDHE-RSA-AES256-GCM-SHA384:!ECDHE+AES:!ECDHE+3DES:!RSA+3DES:!TLSv1_1:!TLSv1:!SSLv3:!MD5:!EXPORT:!RC4
    defaults-from clientssl
    inherit-ca-certkeychain true
    inherit-certkeychain false
    key test_2022
    passphrase none
}
```
HTTP profile using HSTS (enabled)
```
root@(apm1)(cfg-sync Standalone)(Active)(/Common)(tmos)# list ltm profile http http_XFF
ltm profile http http_XFF {
  app-service none
  defaults-from http
  hsts {
    include-subdomains enabled
    maximum-age 15552001
    mode enabled
  }
  insert-xforwarded-for enabled
  proxy-type reverse
  response-chunking rechunk
}
```
