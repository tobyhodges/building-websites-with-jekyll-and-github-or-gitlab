---
layout: lesson
root: .  # Is the only page that doesn't follow the pattern /:path/index.html
permalink: index.html  # Is the only page that doesn't follow the pattern /:path/index.html
---

> ## Prerequisites
> Before following this lesson, learners should be able to:
>
> - create a repository/project on [GitHub][github] and/or [GitLab][gitlab].
> - clone a local copy of a project with Git, add and commit modified files, and push/pull changes between local and remote repositories.
> - execute commands in the shell
>
> If you'd like to learn any of the skills listed above,
> the [Software Carpentry][swc] lessons on
> [the Shell][swc-shell]
> and [Git][swc-git] are a good place to start.
{: .prereq }

For those already familiar with the ways that Git
and an online platform like GitHub
can help them track and compare changes to flat text files,
and collaborate with others on projects,
GitHub and GitLab Pages provide a cost-free way to
build and host webpages.
This approach is commonly used to provide documentation
on software projects,
and to create blogs and websites for
individuals and organisations already used to working with
the Git/GitHub toolset for their other projects.
However, for those taking their first steps towards building sites like this,
the process can be confusing and intimidating.
This tutorial aims to address this,
by providing a step-by-step guide to creating a collection of pages
and combining them into a coherent site using a framework called _Jekyll_.

## Target Audience

**Anita** is a newly-certified Carpentries instructor.
A librarian for the biology library at her institution,
she learned to work with HTML when she did her masters in library science.
Since grad school, she has been picking up other coding skills and has recently learned R.
The Carpentries instructor who taught her R encouraged her to take Carpentries Instructor Training.
She has never used Git before but wants to help edit the Carpentries teaching material and create new lessons
on topics she thinks would be useful for the students and staff she works with.
After working through this lesson Anita will be comfortable using Github to modify the Carpentries lessons,
playing with her own Jekyll pages repo, and eventually making her own lessons using the Carpentries lesson template.

**Arjun** is a third-year PhD student studying atmospheric chemistry.
He uses Python in his research every day and keeps all his scripts and files under version control with Git.
His supervisor is a new group leader and Arjun was the first PhD student she recruited.
Now that her lab has begun to publish the results of their research,
she has tasked Arjun with setting up a website for the group.
The time and budget the group has for developing and maintaining the site are limited,
and Arjun wants to make sure his labmates can access and edit the pages.
He has seen some other labs use GitHub Pages to host their websites
and thinks this is a good opportunity to put his Git skills to work.
After following this lesson, Arjun will be able to create and maintain the structure of the lab website through GitHub Pages,
and begin teaching his colleagues how to collaborate on the content.

**An** is in the final months of her Masters program in Digital Humanities.
During her six-month lab internship, she started using a couple of tools available on GitHub, and became familiar with the interface.
She has really enjoyed this part of the internship and other technical aspects of her Masters and now wants to find work in digitization of rare books and other written material.
She wants to increase her online profile as she enters the job market, and she knows that a personal website and online CV are a good place to start with this.
An still needs to finish writing her thesis and doesn't have a lot of time to spare for creating a website from scratch, nor a lot of money to pay for hosting, domain names, and so on.
This lesson will teach An how to find and use an existing template to create her personal webpage and online CV,
how to write formatted text and insert images to highlight the skills she has picked up, and how to host those pages online for free.

## Learning Objectives

After following this lesson,
learners will be able to:

- create formatted page content with Markdown
- configure their project to build and serve pages on GitHub
- build a coherent site with multiple pages using the Jekyll framework
- customise the layout and style of the pages on their site

[github]: https://github.com/
[gitlab]: https://gitlab.com/
[swc]: https://software-carpentry.org/
[swc-git]: http://swcarpentry.github.io/git-novice/
[swc-shell]: http://swcarpentry.github.io/shell-novice/
