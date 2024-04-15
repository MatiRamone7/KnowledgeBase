# Headers 

## Mandatory Headers

### X-XSS-Protection: 1; mode=block: Enables reflected XSS protection in supported web browsers.

### X-Content-Type-Options: nosniff: Disable mime sniffing, which can result in reflected or stored XSS in certain browsers.

## Configurable Headers

### X-Frame-Options: DENY: Disable embedding web applications in iframes or frames.

### X-Frame-Options: SAMEORIGIN: Allow embedding web applications in iframes or frames, only within the same origin.

## Production Recommendations

Production or staging deployments (with CA signed certificates) should enable the following headers for additional security:

### Strict-Transport-Security: max-age=15768000; includeSubDomains: Prevent any communication over HTTP, since the time the last response was received with the aforementioned header, up-to duration defined in max-age4.

Security headers that need to be set with an external filter (based on customer and security needs) or that should be incorporated into the Tomcat filter in future release includes the following:

### Public-Key-Pins: pin-sha256="<sha256>"; pin-sha256="<sha256>"; max-age=15768000; includeSubDomains: Instructs the web client to associate a specific cryptographic public key with a certain web server to prevent MITM attacks with forged certificates.

### Content-Security-Policy: Allow declaring what dynamic resources are allowed to load to serve current response. Replaces X-Fame-Options and X-XSS-Protection, non-standard headers with standardized headers. For additional detail refer to Content-Security-Policy.com.

https://security.docs.wso2.com/en/latest/security-guidelines/secure-engineering-guidelines/security-related-http-headers/
