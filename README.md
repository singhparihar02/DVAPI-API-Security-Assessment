# DVAPI – API Security Assessment

A hands-on API security assessment of **Damn Vulnerable API (DVAPI)** based on the **OWASP API Security Top 10 – 2023**.

This project demonstrates practical API security testing, vulnerability identification, proof-of-concept exploitation, and remediation recommendations using industry-standard security tools.

## Project Overview

- **Target Application:** Damn Vulnerable API (DVAPI)
- **Assessment Type:** API Penetration Testing & Vulnerability Assessment
- **Methodology:** OWASP API Security Top 10 – 2023
- **Environment:** Local Docker-based lab
- **API Client:** Postman
- **Intercepting Proxy:** Burp Suite

## Tools & Technologies

- Burp Suite – Request interception, manipulation, and vulnerability testing
- Postman – API requests and endpoint testing
- Docker Desktop – Local lab deployment
- Kali Linux – Security testing environment
- JWT.io – JWT inspection and analysis
- SecLists – Username wordlists

## Vulnerabilities Assessed

The assessment covered the following OWASP API Security Top 10 categories:

| OWASP Category | Testing Focus |
|---|---|
| API1: Broken Object Level Authorization | Unauthorized access to other users' resources |
| API2: Broken Authentication | Weak JWT signing secret and token forgery |
| API3: Broken Object Property Level Authorization | Mass assignment |
| API4: Unrestricted Resource Consumption | Oversized file upload |
| API5: Broken Function Level Authorization | Unauthorized access to privileged functions |
| API6: Unrestricted Access to Sensitive Business Flows | Automated requests and missing rate limits |
| API7: Server-Side Request Forgery | Localhost access through URL manipulation |
| API8: Security Misconfiguration | Error handling and stack trace disclosure |
| API9: Improper Inventory Management | Access to unreleased challenges |
| API10: Unsafe Consumption of APIs | NoSQL injection testing |

## Authentication Flow

The DVAPI application uses token-based authentication with JSON Web Tokens (JWT) to authenticate users and access protected API endpoints.

### Authentication Process

The authentication workflow involves the following steps:

1. **User Registration:** Users submit registration credentials through the `/api/register` endpoint.
2. **User Login:** Users authenticate using their username and password through the `/api/login` endpoint.
3. **Token Generation:** Following successful authentication, the application issues a JWT.
4. **Token-Based Access:** The JWT is used as a Bearer token in the HTTP Authorization header when accessing protected endpoints.
5. **Token Validation:** The application validates the authentication token before processing protected requests.

### JWT Authentication

JWT authentication was examined to understand how authentication tokens are generated, transmitted, and validated.

The assessment focused on:

- JWT structure and token analysis.
- Weak JWT signing secret.
- JWT signature security.
- Token forgery possibilities.
- Authentication and authorization weaknesses.

### Security Testing

Authentication-related testing was performed using:

- **Postman:** Sending login requests and testing authenticated API endpoints.
- **Burp Suite:** Intercepting and manipulating authentication requests and JWT tokens.
- **JWT.io:** Inspecting JWT headers, payloads, and signatures.

### Security Considerations

Recommended security measures include:

- Using strong, randomly generated JWT signing secrets.
- Secure password hashing.
- Proper JWT signature verification.
- Enforcing token expiration.
- Restricting accepted signing algorithms.
- Implementing appropriate authentication and authorization controls.
## Methodology

The assessment followed a practical API penetration-testing workflow:

1. Deployed the DVAPI application locally using Docker Compose.
2. Explored API endpoints and functionality using Postman.
3. Intercepted and analysed HTTP requests using Burp Suite.
4. Manipulated request parameters, headers, tokens, and JSON payloads.
5. Tested authentication, authorization, input validation, and resource restrictions.
6. Documented proof-of-concept evidence.
7. Identified potential security impacts and recommended remediation measures.

## Repository Contents

- **Assessment-Report/** – Detailed API security assessment report.
- **Screenshots/** – Burp Suite testing evidence and vulnerability screenshots.
- **Postman/** – Exported Postman API collection.
- **Methodology/** – Testing methodology and supporting documentation.

## Lab Environment

The assessment was conducted against DVAPI, an intentionally vulnerable application designed for API security learning and testing.

Original DVAPI repository: https://github.com/payatu/DVAPI

Local deployment command:

```bash
docker compose up --build
```

Local application endpoint:

```text
http://localhost:3000
```

## Learning Outcomes

- Practical understanding of OWASP API Security Top 10 – 2023.
- Hands-on experience with API request interception and manipulation.
- Authentication and authorization testing.
- JWT security analysis.
- API vulnerability identification and exploitation in a controlled lab.
- Understanding security impact and remediation recommendations.

## Disclaimer

This project was conducted for educational purposes in an intentionally vulnerable local lab environment. All testing was performed against the DVAPI lab application.

**This project is intended for cybersecurity learning and authorised security testing only.**
## Project Resources

### Assessment Report
[View DVAPI Security Assessment Report (PDF)](Assessment-Report/DVAPI-Security-Assessment-Report.pdf)

### Postman Collection
[Download DVAPI Postman Collection](Postman/DVAPI-API-Security-Testing.postman_collection.json)

The Postman collection contains API requests used during the security assessment.
