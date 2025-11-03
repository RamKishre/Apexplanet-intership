Web Application Security Analysis
This report details the concepts, general attack scenarios, and mitigation strategies for common web application vulnerabilities, aligned with the OWASP Top 10.

1. SQL Injection (SQLi)
Description: SQL Injection is a vulnerability that allows an attacker to interfere with an application's database queries. It can be used to bypass authentication, or to extract, modify, or delete data.

General Attack Scenario: An attacker enters a specially crafted SQL command into a user input field (like a search box or login form). If the application insecurely includes this input in a database query, the attacker's command may be executed, allowing them to view data they are not supposed to see.

Mitigation Notes: The primary defense is the use of Prepared Statements (also known as parameterized queries). This technique separates the SQL query's structure from the data, ensuring that user input is always treated as data and never as an executable command.

2. Cross-Site Scripting (XSS)
Description: XSS is a vulnerability where an attacker injects malicious client-side scripts (usually JavaScript) into a web page. When another user visits the page, their browser executes the script, which can be used to steal session cookies, deface sites, or redirect the user to malicious websites.

General Attack Scenario:

Reflected XSS: The attacker crafts a URL containing a malicious script and tricks a victim into clicking it. The script is "reflected" off the web server and executed in the victim's browser.

Stored XSS: The attacker posts a malicious script to a website (e.g., in a comment section). The script is stored in the site's database and executed in the browser of any user who views that comment.

Mitigation Notes: The main defenses are context-aware output encoding (which converts special characters like < and > into their safe, displayable equivalents like &lt; and &gt;) and implementing a strong Content Security Policy (CSP). A CSP is an HTTP header that tells the browser which sources of content (scripts, images) are trusted and allowed to execute.

3. Cross-Site Request Forgery (CSRF)
Description: CSRF is an attack that tricks a logged-in user into unknowingly performing an action they did not intend to, such as changing their password, transferring money, or deleting an account.

General Attack Scenario: An attacker crafts a malicious link or a hidden form on a website they control. If a victim, who is logged into the target application (e.g., their bank) in another tab, visits the attacker's site, their browser may automatically send the forged request to the bank, along with their authentication cookies, executing the unwanted action.

Mitigation Notes: The most common defense is the Synchronizer Token Pattern. The server generates a unique, secret token (an "anti-CSRF token") for each user session and embeds it in all sensitive forms. When the user submits the form, the server checks that the submitted token matches the one in their session, proving the request is legitimate and not from a forged source.

4. File Inclusion (LFI / RFI)
Description: This vulnerability allows an attacker to include and execute a file on the server through a web request.

Local File Inclusion (LFI): The attacker includes a file that is already present on the server (e.g., /etc/passwd to read system user data).

Remote File Inclusion (RFI): The attacker includes a file hosted on a remote, malicious server. This is more dangerous as it leads to direct code execution.

General Attack Scenario: An attacker manipulates a URL parameter that specifies a file to be displayed (e.g., ?page=contact.php). They change the parameter to ?page=../../../../etc/passwd to traverse the directory and read a sensitive file.

Mitigation Notes: The best defense is to avoid using user input to build file paths. If necessary, use a strict allow-list that maps a safe value (e.g., ?page=1) to a hard-coded file path on the server (e.g., includes/home.php). For PHP, disabling allow_url_include and allow_url_fopen in the php.ini file is a crucial step to prevent RFI.

5. Burp Suite Advanced (Fuzzing)
Description: Fuzzing is an automated testing technique that involves sending a high volume of invalid, unexpected, or random data to an application's inputs to find vulnerabilities. Burp Suite's "Intruder" tool is commonly used for this.

General Attack Scenario: An attacker uses Burp Intruder to automate attacks. For example, they might intercept a login request and use Intruder to send thousands of common passwords (a "brute-force" attack) or test a parameter for SQL injection payloads from a predefined list.

Mitigation Notes: Defenses against automated fuzzing include rate limiting (e.g., limiting a single IP to 10 login attempts per minute), account lockouts (temporarily locking an account after multiple failed attempts), and using CAPTCHA to distinguish human users from automated tools.

6. Web Security Headers
Description: HTTP security headers are instructions that the web server sends to the client's browser to enforce various security policies and mitigate a range of common attacks.

Implementation: These headers are typically added to the web server's configuration file (e.g., apache.conf or .htaccess).

Mitigation Notes: Key headers include:

Content-Security-Policy (CSP): As mentioned for XSS, this is a primary defense against script injection.

X-Content-Type-Options: nosniff: Prevents the browser from trying to guess the content type of a file, which stops it from executing a file uploaded as "text" as if it were a script.

X-Frame-Options: DENY / SAMEORIGIN: Prevents your site from being loaded in an <iframe> on another website, which is the main defense against "Clickjacking" attacks.

Strict-Transport-Security (HSTS): Enforces the use of HTTPS, preventing protocol downgrade attacks.
