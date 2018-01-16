# Login and User Creation
## Supplement

---

## Login Form

<!-- .element class="center" -->
![](images/login_form.png)

---

## Login Form

* Client requests (directly or indirectly) the login View
* Client submits form data (POST)
* Server verifies
    - get credentials for the login name given
    - hash password and verfiy against the stored User
        + (`password_verify()`)
    - if OK, show site / otherwise re-direct back to login

---

## Create User

<!-- .element class="center" -->
![](images/create_user_form.png)

---

## Create User

* Client requests (directly or indirectly) to "Sign Up"
* Client submits form data (POST)
* Server verifies
    - check that both passwords match
    - check that username is not already taken
    - create User object, hash password, set credentials, and save to database
    - If all went OK, show user next page / otherwise, re-direct back to sign-up page.


---

## Models?

* User
    - must have a username that will be unique
    - must have a (hashed+salted) password
        + Use PHP's `password_hash()`

---

## Views?

* login form
* signup form

---

## Controllers?

* verify login
* process new signup

---

## What Else?

* need to be able to "approve/deny" new users
* need to be able to delete users

---

## Resources

http://php.net/manual/en/function.password-hash.php

http://php.net/manual/en/function.password-verify.php
