# Methodology Notes – Task 3 API Security Analysis

Personal notes taken during the testing process.

---

## Setup

- Installed Postman desktop app
- Opened Browser DevTools (F12) in Chrome
- Reviewed JSONPlaceholder guide at: https://jsonplaceholder.typicode.com/guide

---

## Testing Order

First went through every endpoint one by one to understand what data each one returns.

### Endpoints Checked
- GET /posts – 100 posts, each with userId, id, title, body
- GET /posts/1 – single post
- GET /comments – 500 comments with name, email, postId, body
- GET /users – 10 users, pretty heavy data per user
- GET /users/1 – single user with full address + geo coordinates
- GET /albums – 100 albums
- GET /photos – 5000 photos (this one is huge)
- GET /todos – 200 todo items
- GET /posts/9999 – testing non-existent resource (got {} back with 404)
- GET /users?id=1 – query parameter filtering

---

## Key Observations During Testing

**Authentication:**
No login, no API key, nothing. Just hit the URL and get data back.
Tried sending requests without any Authorization header – worked fine every time.

**Users endpoint was the most interesting:**
The /users response includes name, username, email, phone, website, address (including city, zipcode), and even geo lat/lng coordinates. That's a lot of info for a completely open endpoint.

**Comments endpoint:**
Every comment has an email attached. 500 records × 1 email = 500 email addresses you can grab in one request. In a real app this would be a data scraping risk.

**Rate limiting test:**
Sent about 15 requests to /users in quick succession using Postman's "Send" button repeatedly. No 429 error at all. No slowdown noticed. Checked response headers – no X-RateLimit-* headers present.

**Response Headers (from DevTools):**

Headers I saw:
- Content-Type: application/json; charset=utf-8
- Access-Control-Allow-Origin: *  ← this is wide open
- Cache-Control: max-age=43200
- Expires: [timestamp]
- Pragma: no-cache

Headers I did NOT see:
- X-Content-Type-Options
- X-Frame-Options
- Strict-Transport-Security
- Content-Security-Policy

**404 handling:**
GET /posts/9999 returned {} with 404. Not terrible, but could be more standardized.

**POST test:**
Tried POST /posts with an empty body {}. Got 201 Created back with id: 101. 
No validation, just accepted it. Makes sense for a fake API but in real life this would be a problem.

---

## Notes on OWASP Mapping

Went through the OWASP API Security Top 10 at github.com/OWASP/API-Security

Most relevant ones for this API:
- API1 (BOLA) – No ownership checks between /users/1, /users/2 etc.
- API2 (Auth) – No authentication at all
- API3 (Data Exposure) – /users and /comments return way too much
- API4 (Rate Limiting) – Nothing in place
- API8 (Misconfiguration) – Missing headers, wildcard CORS, no versioning

API5 (BFLA) – couldn't fully test since there are no different permission levels in this demo API
API6, API7 – not applicable here

---

## Tools Used

- Postman 11.x (desktop)
- Chrome DevTools (Network tab)
- JSONPlaceholder guide (docs)
- OWASP API Security GitHub repo for reference

---

*These are working notes taken during the internship task. The final structured findings are in the main report PDF.*
