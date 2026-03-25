# OWASP Juice Shop – Improper Input Validation (Encoding Challenge)

## Challenge: Broken Image on Photo Wall

---

## 🎯 Objective

Identify and fix an improperly encoded image URL on the Photo Wall in order to successfully load a hidden image.

---

## 🧠 Background

This challenge is part of OWASP Juice Shop and demonstrates a common web vulnerability:

> **Improper Input Validation due to incorrect URL encoding of special characters**

Modern web applications must properly encode special characters in URLs. Failure to do so can lead to broken functionality or even security vulnerabilities.

---

## 🔍 Initial Observation

While browsing the **Photo Wall**, one image appeared broken (not loading correctly).

Using browser Developer Tools (Inspect Element), the following image path was identified:

```text
/assets/public/images/uploads/ᓚᘏᗢ-#zatschi-#whoneedsfourlegs-1572600969477.jpg

The issue lies in the use of the # character within the file name:

ᓚᘏᗢ-#zatschi-#whoneedsfourlegs-1572600969477.jpg
Why is this a problem?

In URLs:

# is a fragment identifier
Anything after # is NOT sent to the server
Result

The server only receives:

ᓚᘏᗢ-

This leads to:

❌ Broken image
❌ Incorrect server request
❌ Fallback response (text/html)
🛠️ Solution

To fix this issue, the # character must be URL encoded.

Encoding Rule
# → %23
✅ Corrected URL
/assets/public/images/uploads/ᓚᘏᗢ-%23zatschi-%23whoneedsfourlegs-1572600969477.jpg
🚀 Execution
Method 1: Browser

Paste the corrected URL into the browser:

http://localhost:3000/assets/public/images/uploads/ᓚᘏᗢ-%23zatschi-%23whoneedsfourlegs-1572600969477.jpg

The image should now load successfully.
