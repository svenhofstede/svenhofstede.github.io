---
title: Breaking the tech debt cycle
date: 2023-10-29
---

I've recently started working in a new codebase. This has mostly been a pleasant experience but, as always, a few corners were cut during development which is causing some issues for the team now. This got me thinking on how codebases end up in a non-ideal state. 

## Some examples of technical debt

* General lack of code quality (This is such a very broad topic by itself)
* Incorrect versioning strategy for any build artifacts causing confusion and incorrect indication of breaking changes
* Lack of automated testing 
* Lack of strict guardrails in CI process which prevent bad code making its way to `main` branch
* Lack of clear and clean interfaces to outside third parties
* Bad branching strategy which is causing long lived branches and having to deal with painful merge conflicts

## Laying the foundation

Initial phases of a software project would be ideal time to set the ground rules for proper coding conventions and to set up the required governance using code linters and formatters, robust CI processes and some documentation on how the project should be approached. However, the initial phases also usually consist of two ingredients that might prevent this from happening.

Firstly, there is the excitement and eagerness to go all-in on feature development. It's a blank canvas that invites developers to get stuck in. Stakeholders following the progress of the project are happy to see new features being churned out and the developers are feeling rewarded by this recognition. A sense of hacker/startup mindset takes the upperhand.

I don't disagree with this approach. I think it's necessary to experiment to see what works and sticks. This definitely means that some code that you produce will be thrown away or changed dramatically. Why spend too much time putting in the guardrails which might even slow you down at this point?

After reaching a certain level of 'stability' level in the codebase, the guardrails need to be installed and this is often times forgotten or not given attention to.

Second ingredient is the lack of production usage. It is very easy to assume delivered features are working as intended if the validation is being done by test and the developers themselves. Having actual users using the product will highlight any corners that were cut during the feature storm phase of the project. The team will be faced with bugs that the (lacking) test suite did not pick up. Furthermore, an inefficient CI/CD process will slow down the resolution of these bugs. Little thought might have been put into the deployment process or how to deal with existing state in your production system. During the feature storm phase simply truncating a database table to resolve corrupted data causes by a bug is a feasible way to rectify an issues. After users start using the system this is probably no longer the case. 

## Team turnover

People come and go. Long-time developers of a codebase might leave the project or company. These positions are replaced with a fresh set of eyes. New joiners join the project with their own prior experiences and ways of working.

These new joiners might be developer who are still early in their career and still learning the ropes of a mature software project. They unknowingly might cause more harm then good and might not notice the inefficiencies of technical debt.

## Point of slow return

After some time technical debt gets so large that the required refactor takes a lot of time. This time would need to be estimated and planned into the teams sprint work which means new feature development needs to make room for refactor efforts. 

## The solution 

I believe the solution to this problem is experience. Senior developers have felt what it's like to have bad technical foundations in a project and how much is can slow down developer productivity. They have a keen eye for spotting the things that slow them down and will always be on the hunt to optimize the process. These changes will be slipped in while working on new features. 

Fixing technical debt is in reality not a big bang refactor but mostly about tiny improvements over time. 