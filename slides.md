---
theme: uncover
_class: lead
paginate: false
# backgroundColor: #fff
# backgroundImage: url('bg.jpg')
---


# **BDD tests memory leak**

## ...or yet another way to crash Jenkins👨

---

## **The Problem**

* The StreamTeam CI-pipelines started to stuck on a daily baisis
* It happened because of sudden crashes of the Jenkins node

---

## **First findings**

* The Jenkins node crashes when it builds the saved searches service application
* The saved searches service builds stuck while running the BDD tests

---

## **About the saved search service**

* A Scala application
* Uses Axon framework
* BDD tests are implemented using Cucumber🥒

---

## **Investigation begins🕵️**

**The plan:**
1. Run the BDD tests of the saved seach service locally with a running profiler
2. Compare the result with other Scala application

---

## The memory leak is confirmed ✔️

![bg](https://upload.wikimedia.org/wikipedia/commons/e/ea/Thats_all_folks.svg)

---

## ...and no memory leak for the other app

TODO: add the PM heap picture 

---

## TODO

TODO: add the SSS threat stat picture

---

## TODO

TODO: add the PM threat stat picture

---

## TODO

TODO: add the SSS object alocation picture

---

## **Investigation continues🕵️**

1. Disable the tests one by one to find the problematic ones
2. ➡️The memory leak occur on the tests with injected Akka actor systems

---

## About Cucumber 🥒

TODO: describe how the BDD tests are implemented, (Cucumber has scenarios and test scenarios)

---

## About Cucumber 🥒

TODO: describe hot Cucuber creates all the defined steps for each test scenario, which means it creates an actor system per each test scenario

---

## TODO

1. TODO: 
2. The Akka actor system is created per each scenario
3. Jenkins crashes 👨🔫

---

## Short term solution

Make the val volatile:
TODO: add the code snippet

---

## Long term solution

Rewrite the BDD tests to unit-tests: they make it easy to shoot yourself in the foot

Besides: 
* We don't use advantages of the BDD apoach (managers don't read the code)
* It's harder to implement them
* A small bonus: The pipeline runs became ~2min shorter after the refactoring

---

## Lessons learned

* Be careful with alocating heavy instances in tests
* "Finish what you start", deallocate a resourse after stop using it

---

![bg](https://upload.wikimedia.org/wikipedia/commons/e/ea/Thats_all_folks.svg)

