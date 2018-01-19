# Software Development Process

---

## Software Engineering

This section could easily turn into a deep discussion of _software engineering_ principles and methodologies; we will avoid allowing it to do so. 

The focus here is on learning the structure and function of a cloud-based application, not on learning how to specify and manage a large software project.  To allow us to succeed given that obvious handicap:

* Keep application requirements _simple_
* Use a simple subset of software-engineering processes

---

## Agile Development

<span style="font-size: 80%; font-style: italic;">Agile software development is a group of software development methods in which requirements and solutions evolve [...]</span><small style="font-size: 90%;">

**Core Values:**

* **Individuals and interactions** over Processes and tools
* **Working software** over Comprehensive documentation
* **Customer collaboration** over Contract negotiation
* **Responding to change** over Following a plan 

</small><span style="font-size: 80%; font-style: italic;">That is, while there is value in the items on the right, we value the items on the left more.</span>

<small>http://en.wikipedia.org/wiki/Agile_software_development</small>

---

## User Stories

_User stories_ are a lightweight alternative to _[use cases](http://en.wikipedia.org/wiki/Use_case)_.  

<span style="border: 1px dotted grey; padding: .3em; font-family: monospace; font-size: 76%;">As a <i>&lt;role&gt;</i>, I want <i>&lt;goal/feature&gt;</i> [so that <i>&lt;benefit&gt;</i>]."</span>

* As a user, I want to customize my schedule so that it fits my degree plan.
* As a user, I want to be able to save my changes so that I can resume working later.
* As an instructor, I want to download student submissions so that I can grade them.
* As a user, I want to search for pictures of cats.

---

## Annotating Stories

User stories are just the outline.  They often imply sub-tasks:

* As an instructor, I want to download student submissions so that I can grade them.
    - Gather submissions for all students
    - Compress into a single download bundle (ZIP?)
    - Push bundle to the client-side, then reclaim space on the server (delete bundle file)
    - Make sure it handles missing submissions in an obvious way

---

## Annotating Stories

As you annotate, you will find vague items that need more clarification:<small style="font-size: 90%;">

* As an instructor, I want to download student submissions so that I can grade them.
    - Gather submissions for all students
    - Compress into a single download bundle (ZIP?)
    - Push bundle to the client-side, then reclaim space on the server (delete bundle file)
    - <span class="highlight">Make sure it handles missing submissions in an obvious way</span>

</small>More sub-items should be added here to clarify, as needed.

<small>http://www.mountaingoatsoftware.com/agile/user-stories</small>

---

<!-- .slide: data-background="assets/images/cloud_test.jpg" class="bg-box" -->

## Stories Drive Tests

User stories, and their annotations (also known as _conditions of satisfaction_) can be used to develop targeted tests to prove the application will perform as desired.

* _[Unit testing](http://en.wikipedia.org/wiki/Unit_testing)_ can be applied here.

<small>http://en.wikipedia.org/wiki/Unit_testing</small>

---

## Resources

http://en.wikipedia.org/wiki/Agile_software_development

http://www.mountaingoatsoftware.com/agile/user-stories

http://en.wikipedia.org/wiki/User_story

http://en.wikipedia.org/wiki/Use_case

http://en.wikipedia.org/wiki/Unit_testing
