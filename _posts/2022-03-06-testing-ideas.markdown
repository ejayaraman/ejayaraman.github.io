---
layout: post
title:  "Some Interesting Ideas from <em>'Fifty Quick Ideas To Improve Your Tests'</em>"
date:   2022-03-06
author: Eswarprasath Jayaraman
categories: testing
---
Running out of test ideas is one of my biggest fears when testing a system. While techniques like Boundary Value Analysis and Equivalence Partitioning can be a good starting point, they are not enough. Teams require more than these fundamental techniques to ensure that applications meet their specification. In their book, [*Fifty Quick Ideas To Improve Your Tests*](https://fiftyquickideas.com/fifty-quick-ideas-to-improve-your-tests/), authors Gojko Adzic, David Evans, and Tom Roden have dedicated a section for Generating Test Ideas. While all the ideas under this section are valuable, I found the ones below more interesting than the others.

<!--end-excerpt-->

![Fifty Quick Ideas to Improve Your Tests](/assets/fifty_quick_ideas_to_test.jpg)

## Explore Capabilities Not Features

The subtle distinction between a capability and a feature makes this idea stand out. What is the difference between a capability and a feature? One definition of capability is, providing a facility to users to accomplish a specific task. A user capability in an application is developed and delivered often through one or more software features. Testing the software feature does not necessarily ensure that users gain this capability. To illustrate this idea, the authors use a contact-form feature as an example.

**Capability:** A user can contact customer service when there is an application issue.
**Feature:** Adding a contact form to an application.

Testing this feature will include checking form validation, error messages and successful submission of the form. However, by exploring the capability, the authors discovered they were unable to contact customer service during a connection failure. The customer service would be unaware of such user issues. Focusing beyond the feature helped them to identify gaps in delivering the capability. This discovery resulted in the team adding information about an alternative contact channel in their service.

The benefits of exploring capability are clear once we see it through a user problem. But how do we find potential user problems even before a system is still in development?

## Snoop On the Competition

This sounds unethical. But this one is not as bad as it looks. The idea here is to learn from a competing product's user issues. The authors suggest that regulated products usually have a requirement to report all user identified issues to the regulator. These reports, if available publicly, can be a great source to identify potential failures that our product could experience. In non-regulated industries, news websites, online support forums, and social media feeds could be helpful. Publicly available bug tracking systems could be another source. Going through these problems to identify failure patterns can help generate test ideas.

While the authors talk about learning from competitors, there is value in using this idea within a company. Applications that follow similar business flows, reuse components and patterns can learn from each other’s problems. Discussing with teams who have implemented a similar feature or reviewing their bug logs could help avoid similar issues in production.

But what if the software is unique both in terms of the product and the domain?

## Start with Always/Never

When working in unfamiliar systems and domains, absolute requirements are a good starting point to identify test cases. In the example provided, *not to lose a transaction ever* is an absolute requirement in an e-commerce system. This statement led to another absolute requirement, *audit all transactions*. Which led to another question *should a failed transaction be audited?* These statements highlighted gaps in understanding between the development team and the business about what qualifies as a transaction. As the authors point out, always/never specifications not only helps to understand the requirements better but help identify high-risk test cases.

In addition, I think absolute statements also lead to identifying a mitigation plan in the event of a failure. For example, *'do not surface Personally Identifiable Information(PII) in logs'* is an absolute requirement when capturing user information. This requirement helps to define what information qualifies as PII. Also, it raises another question, *What happens when PII gets accidentally logged?* Answering this question lays out a mitigation plan for cleansing the logs.

## Document Trust Boundaries

Trust issues are a common concern when multiple teams develop an application. In complex systems, trusting too much could result in dealing with issues from the integrating systems. When trust is low, a team could be wasting time writing defensive code that is not required. To avoid this scenario, teams can document trust boundaries. Capturing the trust boundaries between systems helps identify tests to check for boundary violations.

The authors observe that trust problems can occur even within a team where developers, testers, and business stakeholders have different implied trust boundaries. Lack of trust could result in disagreements about the right level of testing. Again, by explicitly documenting trust boundaries within a team, the authors believe that the team can agree where the application requires strong defences.
While I can see how documenting trust boundaries at integration points can help, I am still unsure how documenting trust boundaries within a team would look practically. Nevertheless, the idea sounds interesting as it could reduce unnecessary checks and avoid duplicating tests.

## Monitor Trends in Logs and consoles

When discussing the idea of documenting trust boundaries, the authors recommend adding logs and trigger alerts to check boundary violations. The idea, *Monitoring trends in logs and consoles* extends this approach. The authors state that *'it will never be possible to specify a complete set of tests for a complex system'*. So, *'system logs and consoles are often the only reliable source of information about what goes on in complex workflows'*. Tracing logs, especially during exploratory sessions, can provide insight into the system behaviour and help generate new testing ideas. It is interesting to repurpose logs and console outputs used typically for investigations to generate test ideas.

## Test Benefit as Well as Implementation

Every time I look at this idea, it sounds very similar to [*Explore Capabilities Not Features*](#explore-capabilities-not-features) idea. Still, I think there is a difference. A capability is an option provided to a user to accomplish a specific task. Exploring this capability checks if a user can use the feature. However, it does not tell us if the user would use that capability. Testing the benefit can help to understand this aspect.

An example. One of the internal testing tools we support generates an HTML report. The report is quite noisy because of the nature of the test. To make it easier for teams to understand the report, we introduced pre-defined filters. When we delivered the feature, our automated tests passed, we manually explored the capability and even received a few likes when we announced it to our users. We assumed teams would use this capability. But while interviewing our users regarding this report for a completely unrelated piece of work, we noticed our users often skip the filter. On further enquiry, we realised not all of our users found those filters intuitive. Our implementation did not deliver the benefit, at least for some users.

As the authors say, it is easy to overlook the benefits when the focus is on checking if the implementation works. So, test the benefit and the implementation.

–

The book has four parts. The first part of the book covers *Ideas to Generate Tests*. Other sections include *Designing Good Checks, Improving Testability and Managing Large Test Suites*, which I am yet to explore.

Working for many years in a field makes one believe that there are not many tricks left to learn. *Fifty Quick Ideas To Improve Your Tests* made me realise there is always more to discover.
