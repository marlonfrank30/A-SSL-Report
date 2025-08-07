**A SSL Labs Report using TLS1.2**
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

**A+ SSL Labs Report using TLS1.2**
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

**A+ SSL Labs Report using TLS1.3**
![](./images/A+SSL-Labs.PNG)
For TLS1.3 please note that f5 has changed its approach now. Administrators need to use cipher rules in combination with cipher groups in order to hard code the desired cipher, hashes, exchange keys combos, etc. 
root@(apm1)(cfg-sync Standalone)(Active)(/Common)(tmos)# list ltm cipher group Qualys-SSL-A all-properties
```
ltm cipher group Qualys-SSL-A {
    allow {
        SSL-Labs-A { }
    }
    app-service none
    description none
    exclude none
    ordering default
    partition Common
    require none
}
```
```
root@(apm1)(cfg-sync Standalone)(Active)(/Common)(tmos)# list ltm cipher rule SSL-Labs-A all-properties
ltm cipher rule SSL-Labs-A {
    app-service none
    cipher TLS13-CHACHA20-POLY1305-SHA256:TLS13-AES256-GCM-SHA384:TLS13-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:!DES:!3DES:!RC4:!MD5:!EXPORT
    description none
    dh-groups DEFAULT
    partition Common
    signature-algorithms DEFAULT
}
```
```
root@(apm1)(cfg-sync Standalone)(Active)(/Common)(tmos)# list ltm profile http http_XFF all-properties
ltm profile http http_XFF {
    accept-xff disabled
    app-service none
    basic-auth-realm none
    defaults-from http
    description none
    encrypt-cookie-secret none
    encrypt-cookies none
    enforcement {
        allow-ws-header-name disabled
        excess-client-headers reject
        excess-server-headers reject
        known-methods { CONNECT DELETE GET HEAD LOCK OPTIONS POST PROPFIND PUT TRACE UNLOCK }
        max-header-count 1024
        max-header-size 32768
        max-requests 0
        oversize-client-headers reject
        oversize-server-headers reject
        pipeline allow
        rfc-compliance disabled
        truncated-redirects disabled
        unknown-method allow
    }
    explicit-proxy {
        bad-request-message none
        bad-response-message none
        connect-error-message none
        default-connect-handling deny
        dns-error-message none
        dns-resolver none
        host-names none
        ipv6 no
        route-domain none
        tunnel-name none
        tunnel-on-any-request no
    }
    fallback-host none
    fallback-status-codes none
    header-erase none
    header-insert none
    hsts {
        include-subdomains enabled
        maximum-age 15779000
        mode enabled
        preload enabled
    }
    insert-xforwarded-for enabled
    lws-separator none
    lws-width 80
    oneconnect-status-reuse "200 206"
    oneconnect-transformations enabled
    partition Common
    proxy-type reverse
    redirect-rewrite none
    request-chunking sustain
    response-chunking rechunk
    response-headers-permitted none
    server-agent-name BigIP
    sflow {
        poll-interval 0
        poll-interval-global yes
        sampling-rate 0
        sampling-rate-global yes
    }
    via-host-name none
    via-request preserve
    via-response preserve
    xff-alternative-names none
}
```
