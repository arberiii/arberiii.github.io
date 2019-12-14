---
layout: post
title:  "BDD and Cucumber"
date:   2019-12-14 22:52:01 +0100
categories: bdd, cucumber, agile
---
I firstly encoundter Behaviour-Driven Development (BDD) at my first job, I was assigned to add features and write the corresponding tests. At the time I didn't even know about the Test-Driven Development (TDD) and couldn't get the idea why are we using it. The aplication was a RESTful API written in Go, jumped to [Godog repository](https://github.com/DATA-DOG/godog), installed it and with help of my coworkers started using it. Now, at my current job we have to develop an application and we decided to follow the BDD, so before doing anything it I said its better if we try to learn more about it. I thought that I knew alot about BDD, but it turns out there is much more to learn. So in this post I will show some take aways, tips, etc. 
#### What is BDD?
Behaviour-Driven Development (BDD) is an Agile sofware development, in which the participants are developers, testers and clients(stakeholders). The main goals of BDD are to establish an easy way to communicate the idea to others and avoiding miscommunation between clients and the app developers, to do so everyone writes different stories on how should the app react in different scenarios and this would define what needs to be done for the client to find the application acceptable.

#### Cucumber
Cucumber is a software tool that supports BDD. It helps facilitate the discovery and use of a ubiquitous language within the team, by giving the two sides of the linguistic divide a place where they can meet. Working together to write test not only creates a path for what should be implemented next, but also describes the behaviour of the application which can be seem as a living documentation.

#### Let's build a calculator
Our client wants to build a calculator, and the first thing that comes to mind is addition. Language in which we write BDD scenarios is called Gherkin. This is not a post about how to write Gherkin and in a way this shouldn't, everyone should be able to read and write tests easily, it is good espacially for developering side because they are speaking client language. Consider the following:
```
Scenario: Add two numbers
Given the input "2+2"
When the calculator is run 
Then the output should be "4"
```
It is clear what the calculator app is suppose to do. That is what the work of clients, testers and developers should produce.
With the help of cucumber the testers should write the test to check if each step(line in the scenario), and after that the developer should write the minimal code that passes this test. The developer here can do as little as just for any input, output 4 and the test is going to pass. That's why everyone should think of edge cases of how should the app behave in different cases. 

#### When Cucumbers go bad
Cucumber should be all about better workflow, cleaner code, good communication, etc. But it can be when Cucumber can go bad. Some of the most common problems are flickering scenarios, slow features, bored stakeholders. Flickering scenarios can be caught when your test fail randomly. I remember when using Cucumber in the beggining and re running godog command would pass after failing, it was so hard to debug it. Usually those flickering sceario happens race conditions, envoirment, etc. Slow features happens when testing some scenario takes minutes and it's just frustrating to test, I had once some testing which took 10 minutes and it was a good reason for me to skip the test, which is definitely when cucumbers go bad. Bored Stakeholders is when the stakeholders(clients) don't collaborate anymore in the reading or writing features, but then there is no much point in using it.


#### Tips
* Scenarios should be indepedent from each others.
* When dealing with asynchronus systems listen for events broadcast by the system or repeatedly poll the system. But don't just sleep.
* If you use database, then you have to make sure each scenario starts with a clean slate.
* When testing a REST web service with Cucumber, it’s generally preferable to run Cucumber in the same process as your application.
* In legacy application, use characterization tests to help you understand what the system is already doing and to give you some security before you make a change.
