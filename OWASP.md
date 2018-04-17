# Owasp Top 10 Appliction Security Risks - 2017

## 1. Injection flaws
* Occur when untrusted data is sent to an interpreter as part of a
command or query.
* Hostile data can trick the interpreter into executing unintended
commands or access data without proper authorization


### Example
* Assume you have a application which consumes a username and password
from a front-end input component.
* Intuitively you may want to create the verification by entering the
user's input as criteria for a `WHERE` clause who checks against a
database for the respective username and password.

```SQL
SELECT *
FROM members
WHERE username = 'admin'
AND password = 'password'
```




## 2. Broken Authentication
* Authentication and session management are often implemented incorrectly.
* Attackers can compromise passwords, keys, or session tokens
* Attacker may exploit other implementation flaws by assuming other
user's identities.

### Is my Application Vulnerable?
* If your application supports any of these features, it is vulnerable
to `Broken Authentication` breeches.
        * Permits automated attacks such as credential stuffing, where the
attacker has a list of valid usernames and passwords.
        * Permits brute force attacks
        * Permits default, weak, or well-known passwords
                * i.e. - `Password1`, `admin/admin`
        * Uses weak or ineffective credential recovery and forgot-password
processes such as "knowledge-based answers", which cannot be made
safe.

### How do I prevent?
* Implement multi-factor authentication to prevent autmated
crednential stuffing.
* Do not deploy with any default credentials (especially for admins)
* Limit or increasingly delay failed login attempts





## 3. Sensitive Data Exposure
* API does not properly protect sensitive data
    * i.e. financial, healthcare, or personally identifiable information (PII)
* Attackers may steal or modify weakly protected data to conduct
fraudulent behavior.
        * i.e. - credit card or identity theft
* Sensitive data may be compromised without extra protection

### Is my Application Vulnerable?
* Is any data transmitted in clear text?
* This concerns protocols such as HTTP, SMTP, and FTP.
* External internet traffic is especially dangerous.

### How to prevent?
* Verify all internal traffic e.g. between load balancers, web
servers, or back-end systems.
* Classify data processed, stored, or transmitted by an application.
* Apply controls as per the classification.
* Do not store sensitive data unnecessarily.
* Encrypt sensitive data at rest.





## 4. XML External Entities (XEE) Processing
* Poorly configured XML processors evaluate external entity references
within XML documents.
* External entities can be used to disclose internal files using the
the file URI handler, internal file shares, internal port scanning,
remote code execution, and denial of service attacks.

### Is my Application Vulnerable?
* Application accepts XML directly or XML uploads.
* Application inserts untrusted data into XML documents which is
parsed by an XML processor.
* If the application uses Security Assertion Markup Language (SAML),
it may be vulnerable as SAML uses XML for identity assertions.
* If the application uses SOAP prior to version 1.2, it is likely
susceptible to XXE attacks if XML entities are being passed into the
SOAP framework.

### How to prevent?
* Whenever possible use less complex data formats such as JSON.
* Avoid serilization of sensitive data
* Patch or upgrade all XML processors
* Update SOAP to soap 1.2
* Disable XML external entity and DTD processing in all XML parsers in
the application





## 5. Broken Access Control

* Restrictions on what authenticated users are allowed to do are not
properly enforced.
* Attackers exploit flaws to access unauthorized functionality and/or data.
        * i.e. - access other user's accounts, view sensitive files, modify
other users' data, change access rights, etc.

### Is my Application Vulnerable?
* Allowing the primary key to be changed to another's users record,
permitting viewing or editing someone else's account.
* Elevation of privilege. Acting as a user without being logged in, or
acting as an admin when logged in as a user.
* CORS misconfiguration allows unauthorized API access.

### How to prevent?
* Implement access control mechanisms and re-use them throughout application
* Minimize CORS usage
* Model access controls should enforce record-ownership rather than
accepting that the user can create
* Disable web server directory listing
* Ensure file metadata (e.g. .git) and backup files are not present
within web roots.
* Log access control failures and alert admin when appropriate
        * (repeated failures)
* Rate limit API and controller access to minimize the harm from
automated attack tooling.




## 6. Security Misconfiguration
* Most commonly seen issue
* Often the result of:
       * insecure default configurations
       * incomplete / adhoc configurations
       * open cloud storage
       * misconfigured HTTP headers
       * verbose error messages containing sensitive information
* Operating systems, framework, libraries, and applications must be
patched/upgraded in a timely fashion

### Is my Application Vulnerable?
* Improperly configured permissions on cloud services.
* Error handling reveals stack traces or other overly informative
error messages to users
* latest security features are disabled or not configured securely

### How to prevent?
* A minimal platform without any unnecessary features, components,
documentation, and samples
* Remove or do not install unused features and frameworks
* An automated process to verify the effectiveness of the
configurations and settings in all environments.


## 7. Cross-Site Scripting (XSS)
* Allows attackers to execute scripts in the victim's browser which can:
        * hijack user sessions
        * deface web sites
        * redirect the user to malicious web sites
* Occurs whenever an application includes untrusted data in a new web
page without:
        * proper validation
        * proper escaping
        * updates an existing web page with user-supplied data
### Is my Application Vulnerable?
* **Reflected XSS**
* **Stored XSS**
* **DOM XSS**



## 8. Insecure Deserialization
* Leads to remote code execution
* Even if deserialization flaws do not result in remote code
execution, they can be used to perform attacks which include:
        * replay attacks
        * injection attacks
        * privilege escalation attacks





## 9. Using Components with Known Vulnerabilities
* Components run with the same privilege as the application.
* If vulnerable component is exploited, an attack can facilitate data
loss, or server takeover.
* Components include:
        * libraries
        * frameworks
        * software modules





## 10. Insufficient Logging and Monitoring
* [Incident Response](https://digitalguardian.com/blog/what-incident-response)
is the process by which an organization handles a data breach or
cyberattack, including the way the organization attempts to manage the
consequences of the attack or breach (the “incident”)
* If an application has poor logging/monitoring as well as an
ineffective integration with incident response





# Sources
* [primary source](https://www.owasp.org/index.php/Top_10-2017_Top_10)
* [1. Injection flaws]()
* [2. Broken Authentication]()
* [3. Sensitive Data
Exposure](https://www.owasp.org/index.php/Top_10-2017_A3-Sensitive_Data_Exposure)
* [4. XML External Entities (XEE)
Processing](https://www.owasp.org/index.php/XML_External_Entity_%28XXE%29_Processing)
* [5. broken access
control](https://www.owasp.org/index.php/Top_10-2017_A5-Broken_Access_Control)
