# API Design
## Including the REST design pattern.

---

## Resources

https://docs.microsoft.com/en-us/azure/architecture/best-practices/api-design

https://hackernoon.com/restful-api-designing-guidelines-the-best-practices-60e1d954e7c9

https://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api

https://www.toptal.com/api-developers/5-golden-rules-for-designing-a-great-web-api

---

## Addendum to the Hacker Noon link

https://hackernoon.com/restful-api-designing-guidelines-the-best-practices-60e1d954e7c9

The author has a nice example of **bad** design:

    /addNewEmployee
    /updateEmployee
    /deleteEmployee
    /deleteAllEmployees
    /promoteEmployee
    /promoteAllEmployees

But they never show the "best-practices" way to define those API endpoints...

So, flip to the next slide for some possibilities.

---

**Better version of the Hacker Noon "Bad" endpoints:**
<pre>
New    : GET "/employees"                : List all employees.
New    : GET "/employees/{id}"           : Get info for emp. #{id}.

Bad    : /addNewEmployee
Better : POST  "/employees"              : Add a new employee.

Bad    : /updateEmployee
Better : POST "/employees/{id}           : Update employee #{id}
Alt    : PUT "/employees/{id}            : Update employee #{id}

Bad    : /deleteEmployee
Better : DELETE "/employees/{id}         : Delete employee #{id}

Bad    : /deleteAllEmployees
Better : DELETE "/employees              : Delete all!  (Ouch.)

Bad    : /promoteEmployee
Better : PUT "/employees/{id}/promotion  : Promote employee ${id}
Alt    : POST "/employees/{id}/promotion : Promote employee ${id}

Bad    : /promoteAllEmployees
Better : PUT "/employees/{id}/promotion  : Promote all employees
Alt    : POST "/employees/{id}/promotion : Promote all employees
</pre>