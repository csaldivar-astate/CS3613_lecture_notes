# User Authentication

---

## Usernames, Passwords

At some point in most applications, we need to identify individual users in order to persist _their_ data.

* Traditionally, _username_ and _password_ pairs associate _individuals_ with _data_.
* Application's responsibility to keep password data _secure_.

---

## Worst-Case

* Your application contains millions of username/password combos.
* Your authentication database is breached.
    - You didn't encrypt anything!!!
* Your users may have re-used username/password on other sites.
    - Now their other accounts are compromised as well.

Never let this happen!  A small amount of preparation can help avoid the worst-case scenario.

---

## Avoid the Worst-Case

* Collect user info only when absolutely necessary.
* _Salt_ and _cryptographically-hash_ passwords.
* _Encrypt_ usernames if possible.
* Separate login database and user data.

---

## Least Privilege

* Don't collect any information from the user that you don't _need_.
* Practice data expiration.
    - delete things that are no longer needed

---

## Password Handling

Until the day that we can stop using passwords...

* Encourage strong passwords.
* Encourage user not to re-use passwords.
* **Salt** and **Hash** any password you store.

---

## Cryptographic Hashing

<small style="font-size: 88%">
A _cryptographic hash_ is a one-way function that transforms data from a readable form into a random-looking representation.

**Ideal Properties:**

* One way : cannot reverse the process
* Unique : no two inputs produce the same output hash
    - real hashing algorithms have a small chance of _collision_
    - intentionally creating collision should be computationally infeasible
* Expensive : hashing should be computationally expensive (_slow_)
    - makes brute-forcing unprofitable

</small><small>
https://en.wikipedia.org/wiki/Cryptographic_hash_function<br>
http://www.sha1-online.com/
</small>

---

## Verify Hashed Password

* hashing is one-way (you can't reverse it)
* to verify a hashed password:
    - get user's password entry
    - hash it using the same algorithm
    - compare the _hashes_
        + if they match: password is OK

---

<!-- .slide: data-background="images/sad-cloud.png" class="bg-box" -->

## Hashing is not Enough

Same password always produces the same hash &mdash; but many people will use the same passwords:

**Top (leaked) Passwords of 2014**

1. `123456`
2. `password` 
3. `12345`
4. `12345678`
5. `qwerty`

<small>http://splashdata.com/press/worst-passwords-of-2014.htm</small>

---

## Add Some Salt

_Salting_ a hash means adding some random characters to the password _before_ running it through the hashing function.  

* every user should have a different _salt_.
    - you must store the per-user salt
* prevents table-based attacks
    - (i.e. "rainbow tables")
* _does not_ prevent targeted brute-force attacks
    - only a high-value target would be "worth it"

---

## Examples

Say your password is `monkey`.  _(Please use a better password than this...)_

The `sha-1` hash is:<br>
`ab87d24bdc7452e55738deb5f868e1f16dea5ace`<br>
Now, say you add a random salt: `iervuadf`<br>
`d5c8151c76e3ef3cf4d15b7ebdb76885e380b415`<br>
Someone else also uses `monkey`, but their salt is: `ajie,cye`<br>
`1b474c2ef72ed720d68ae5410ae8ce6c0dff23ff`

---

## PHP Makes it Easy

* PHP 5.5+ includes:
    - `password_hash()` - creates salted hash of a password
    - `password_verify()` - checks a password against the stored hash

---

## PHP `password_hash()` Example

```php
$pwd       = "monkey";
$hashedPwd = password_hash($pwd, PASSWORD_DEFAULT);
echo $hashedPwd . "\n";
```
This will print something like:
```
$2y$10$xp4zm693lfvlEXeJLUG1auxi.lsGap.ELNeqdS2JJaXlTIlwJwTGi
```

PHP's `password_hash()` function automatically salts and hashes the password, and returns a string with _algorithm_, _complexity_, _salt_, and _hash_ combined; the `password_verify()` function can then verify a login using this string.

---

## PHP `password_verify()` Example

```php
// actual hash comes from persistent storage
$hashedPwd = '$2y$10$xp4zm693lfvlEXeJLUG1auxi.lsGap.ELNeqdS2JJaXlTIlwJwTGi';
// actual password comes from client-side
$pwd       = "monkey";
if(password_verify($pwd, $hashedPwd)){
    echo "OK! Welcome back."
}
else{
    echo "Authentication failed.";
    // do something to allow user to try again
}
```

This should print "OK! Welcome back.".

---

## Resources

https://en.wikipedia.org/wiki/Cryptographic_hash_function

http://www.sha1-online.com/

http://php.net/manual/en/faq.passwords.php

http://php.net/manual/en/function.password-hash.php
