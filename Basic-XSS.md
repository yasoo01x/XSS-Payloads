# 01 - XSS Basics

Cross-Site Scripting (XSS) is a vulnerability that allows attackers to inject malicious JavaScript into web pages viewed by other users.

##  What is XSS?

XSS allows attackers to:
- Steal cookies
- Steal JWT/localStorage tokens
- Hijack accounts
- Keylog victims
- Redirect users
- Bypass security controls

### Why XSS happens?
Because untrusted input is rendered directly:

Example:
<div>Hello, <?php echo $_GET["name"]; ?></div>

---

#  Types of XSS

## 1) Reflected XSS
Executed immediately via GET/POST parameters.

Example:
https://example.com/?q="><script>alert(1)</script>

## 2) Stored XSS
Payload is stored on the server (DB, comments, usernames…).

## 3) DOM XSS
Execution happens in the browser through JavaScript sinks like:
innerHTML, document.write, eval, location.hash, etc.

---

#  XSS Notes & Checklist

## Injection Points:
- HTML content
- JavaScript context
- Attributes
- URLs
- SVG/MathML

## Dangerous Sinks:
- innerHTML
- outerHTML
- document.write
- eval
- setTimeout / setInterval
- Function()

## Common Payloads:
"><script>alert(1)</script>
<img src=x onerror=alert(1)>
<svg/onload=alert(1)>
"><iframe src=javascript:alert(1)>
javascript:alert(1)

---

#  FULL EXAMPLES (VULNERABLE HTML FILES)

===============================================
=              reflected-basic.html            =
===============================================
<!DOCTYPE html>
<html lang="en">
<body>
    <h2>Reflected XSS Example</h2>

    <form method="GET">
        <input name="search" placeholder="Search...">
        <button>Submit</button>
    </form>

    <p>Result: 
        <?php 
            if (isset($_GET['search'])) {
                echo $_GET['search']; // Vulnerable!
            }
        ?>
    </p>
</body>
</html>

===============================================
=              stored-basic.html               =
===============================================
<!DOCTYPE html>
<html lang="en">
<body>
    <h2>Stored XSS Example</h2>

    <?php
        $comments = [];

        if (!empty($_POST['comment'])) {
            $comments[] = $_POST['comment']; // Stored with no sanitization!
        }
    ?>

    <form method="POST">
        <textarea name="comment" placeholder="Write a comment..."></textarea>
        <button>Post</button>
    </form>

    <h3>Comments</h3>
    <?php
        foreach ($comments as $c) {
            echo "<p>$c</p>"; // Vulnerable!
        }
    ?>
</body>
</html>

===============================================
=                dom-basic.html                =
===============================================
<!DOCTYPE html>
<html lang="en">
<body>

    <h2>DOM-Based XSS Example</h2>
    <div id="output"></div>

    <script>
        var payload = location.hash.substring(1);
        document.getElementById("output").innerHTML = payload; // Vulnerable
    </script>

</body>
</html>

---

# ✔ Summary

This file includes:
- What is XSS  
- Types of XSS  
- Notes & sinks  
- Payloads  
- Full vulnerable examples (Reflected, Stored, DOM)

Perfect as the first chapter of your XSS repository.
