# OWASP Broken Access Control

**Platform:** TryHackMe  
**Room:** [OWASP Broken Access Control](https://tryhackme.com/room/owaspbrokenaccesscontrol)

---

## Task 2: Broken Access Control – Introduction

Access control is a security mechanism used to control which users or systems are allowed to access specific resources.

The primary goal of access control is to protect sensitive information and ensure that resources are only accessible to authorized users.

### Types of Access Control

Access control can be implemented in different ways:

1. **Discretionary Access Control (DAC):** Resource owners decide who can access their resources.
2. **Mandatory Access Control (MAC):** Access is controlled through centrally defined security policies.
3. **Role-Based Access Control (RBAC):** Permissions are assigned according to a user's role.
4. **Attribute-Based Access Control (ABAC):** Access decisions are based on attributes such as user identity, resource, and environment.

### Common Broken Access Control Vulnerabilities

1. **Horizontal Privilege Escalation:** Accessing another user's resources at the same privilege level.
2. **Vertical Privilege Escalation:** Gaining access to resources or actions intended for users with higher privileges.
3. **Insufficient Access Control Checks:** The application fails to properly verify whether a user is authorized to perform an action.
4. **Insecure Direct Object References (IDOR):** Accessing another user's data by manipulating an object identifier or reference.

---

## Task 3: Starting the Lab Machine

Started the TryHackMe lab machine to access the vulnerable web application.

---

## Task 4: Assessing the Web Application

To assess the web application, I used **Burp Suite** and its built-in Proxy Browser.

### Steps Performed

1. Opened Burp Suite.
2. Launched the Burp Proxy Browser.
3. Accessed the target web application.
4. Created a new user account.
5. Logged in to the application.
6. Intercepted and inspected HTTP requests and responses.

### HTTP Response Analysis

While inspecting the HTTP response, I identified some useful information:

- **Web Server:** Apache/2.4.38 (Debian)
- **Backend Technology:** PHP/8.0.19
- **Content Type:** text/html
- **Application:** VulnerableApp

I also inspected the application's request parameters and response content to understand how the application handled user authentication and access control.

### What I Learned

Burp Suite helps security testers inspect HTTP requests and responses to identify potentially vulnerable application behavior.

---

## Task 5: Exploiting the Web Application

In this task, I tested the application's access control mechanism.

### Steps Performed

1. Intercepted the HTTP response using Burp Suite.
2. Identified the `redirect_link` parameter.
3. Copied its value and accessed the relevant dashboard URL.
4. Observed the `isadmin` parameter in the URL.

The URL contained the following parameter:

```text
/dashboard.php?isadmin=false
```

5. Changed the parameter value from `false` to `true`.

```text
/dashboard.php?isadmin=true
```

6. Accessed the admin page:

```text
/admin.php
```

7. Used Burp Suite Repeater to inspect the HTTP response.
8. Found the flag in the response.

### Flag

```text
THM{I_C4n_3xpl01t_B4c}
```

### What I Learned

The application relied on a user-controlled parameter to determine administrative access.

By modifying the parameter, I was able to access an administrative page without having the appropriate authorization.

This demonstrates **Broken Access Control** and **Vertical Privilege Escalation**.

---

## Task 6: Mitigation

Several security measures can help prevent Broken Access Control vulnerabilities in web applications.

### 1. Implement Role-Based Access Control (RBAC)

Assign permissions based on user roles, such as Admin and Normal User.

### 2. Perform Server-Side Authorization Checks

Always verify a user's permissions on the server before allowing access to sensitive resources or performing privileged actions.

Never rely on client-controlled parameters to determine a user's privileges.

### 3. Apply Proper Session Management

Use secure session handling and validate the user's authentication and authorization status on every sensitive request.

### 4. Follow the Principle of Least Privilege

Give users only the permissions they need to perform their tasks.

### 5. Deny Access by Default

If a user does not have explicit permission to access a resource, the application should deny the request.

### 6. Test Access Control Mechanisms

Regularly test the application for horizontal and vertical privilege escalation, IDOR, and other access control weaknesses.

---

## Key Takeaways

- Learned the fundamentals and types of access control.
- Understood common Broken Access Control vulnerabilities.
- Practiced inspecting HTTP requests and responses using Burp Suite.
- Learned how manipulating a user-controlled parameter can lead to privilege escalation.
- Understood the importance of server-side authorization checks.
