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

The DVAPI lab uses JSON Web Tokens (JWT) for authentication. The following flow is based on the publicly available DVAPI application source code and was used to understand the lab's authentication behavior.

### Authentication Process

1. **Registration:** A user submits registration details to `POST /api/register`. The application creates a user record.
2. **Login:** A user submits a username and password to `POST /api/login`.
3. **Credential Check:** The application looks up a user by matching the submitted username and password against the stored user record. The implementation compares password values directly rather than using password hashing.
4. **JWT Creation:** After successful login, the application creates a JWT containing the user's identifier, username, and role-related claim. The token is signed using the application's configured signing secret.
5. **Token Delivery:** The login response provides the JWT in the `Authorization` response header and also sets it in an `auth` cookie.
6. **Protected API Requests:** API routes use Bearer-token authentication. The client sends the token in the request's `Authorization: Bearer <token>` header, and middleware verifies the token before continuing to the protected route.
7. **Web Page Authentication:** Page routes use the `auth` cookie for authentication rather than the Bearer-token header.

### Authentication Weaknesses Identified in the Lab Implementation

The source code exposes several insecure implementation choices relevant to the assessment:

- A weak, hard-coded JWT signing secret is used.
- Passwords are compared directly with stored values instead of being verified using a secure password-hashing function.
- The `auth` cookie is configured with `httpOnly: false`.
- The JWT signing call does not set an explicit token expiration.
- The application uses the same signing secret for JWT signing and verification.

These weaknesses help explain the authentication and token-forgery testing documented in the assessment. This section describes the intentionally vulnerable lab implementation; it is not a recommendation for production authentication design.

### Security Testing

Authentication-related testing was performed using:

- **Postman:** Sending login requests and testing authenticated API endpoints.
- **Burp Suite:** Intercepting and modifying authentication requests and JWTs.
- **JWT.io:** Inspecting JWT headers, payloads, and signatures.

### Security Recommendations

- Store passwords using a strong, salted password-hashing algorithm such as Argon2id or bcrypt.
- Use a strong, randomly generated signing secret stored outside the source code.
- Set and validate appropriate JWT expiration and claims.
- Restrict accepted signing algorithms and verify JWT signatures securely.
- Set authentication cookies with `HttpOnly`, `Secure`, and an appropriate `SameSite` policy.
- Enforce authorization checks independently on every protected resource and action.

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

```text
.
├── Assessment-Report/
│   └── DVAPI-Security-Assessment-Report.pdf
├── Postman/
│   ├── DVAPI-API-Security-Testing.postman_collection.json
│   └── README.md
└── README.md
```

The repository currently contains the assessment report and exported Postman collection shown above.

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
