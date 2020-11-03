---
title: "Re-using Blocks of Content"
teaching: 0
exercises: 0
questions:
- "How can I reuse the same chunks of material in multiple pages?"
objectives:
- "Create reusable blocks of content and insert them into pages"
keypoints:
- "The content of files in the `_includes/` directory can be inserted into a page with `{ % include file_name % }`"
---

In the previous episode,
we discussed the benefits of using global and local variables
to re-use values throughout our pages.
However, repeated use of content in across websites
is usually not limited to individual values such as
email addresses and social media handles.

> ## What gets re-used?
>
> Look at the two pages linked below,
> and browse some other pages on the same site.
>
> * [The Software Sustainability Institute][ssi-homepage]
> * [DiverseKids Book Store][diversekids]
>
> What content is being re-used between pages on these sites?
> Pair up and compare your partner's notes with your own.
> Can you identify any common type(s) of content that being re-used in these sites?
>
> > ## Solution
> >
> > The Software Sustainability Institute website re-uses many structural
> > elements, such as the **page header**
> > (containing the "top menu," the institute's logo, links to social media, etc)
> > and **footer**
> > (containing copyright and licensing information,
> > links to the privacy policy and accessibility statement,
> > a form to subscribe to the institute's newletter, etc).
> > Elsewhere, blocks of text and images are re-used in the main body
> > of multiple pages, e.g.
> > blog and news posts all end with a description of
> > how the reader can contact the SSI to discuss the content.
> >
> > The DiverseKids site has the same kind of shared header and footer
> > on each page: this is a common theme across most websites,
> > helping to improve navigation and other aspects of the user experience
> > and achieve consistent "branding" across the whole site.
> > The books listed under each category include a title, a price,
> > and cover image,.
> > The category links themselves are also shared across each page,
> > probably generated from the existing categories of books in the collection,
> > and updated automatically when a category is added or removed.
> {: .solution }
{: .challenge }

The most commonly reused content is structural: menus and branding information
used to present a consistent and recognisable interface to the user regardless
of which specific page of the site they're visiting.
We'll look more at that in the next episode.
But some content, such as contact statements and post/product listings,
can be reused in the body of pages.
The motivation for reusing content like this is that,
if you need to update that content - changing the contact address,
updating a price or picture associated with a listing, and so on -
you need only change this information in one place
for the update to be propagated across the whole site.
This is related to the _DRY (Don't Repeat Yourself)_ principle of
good practice in programming.

As far as we know,
the sites linked in the previous exercise aren't built with Jekyll.
But the principles behind reusing content apply regardless of
the particular framework being used to build the site.

## Carrying the Banner

Let's look at an example of how we can create a block of common content
and reuse it in multiple pages on our site.
At the moment our pages are quite plain:
why don't we try adding a banner to the top of each page?

We're going to add a pre-made banner image to our repository,
and it is good practice to store all image files in a common folder.
1. click "Create new file" under the "Add file"
dropdown on your repository homepage,
2. in the "Name your file..." box, type `images/`.
   The folder name should be automatically inserted in the path displayed
   next to this box for naming the file.
3. You can then leave the file blank and name it `.gitkeep`.
   When you commit the changes, the `images` folder will have been
   added to your repository.
We will be uploading our banner image to this folder in a moment
and unfortunately GitHub does not provide a way to create a new folder
while uploading existing files, only while creating new ones.
When making these blank files,
which exist only to allow the existence of their parent repository,
it is traditional to call them `.gitkeep`.
Now [download this banner image that we will add to our pages][banner-image] and
upload the file to your newly-created `images` folder on GitHub:
you can do this by navigating into the folder and choosing
"Upload files" from the "Add file" dropdown you used before.

Now that the banner image is available in our site repository,
add this HTML immediately after the YAML front matter in `index.md`:

```
<img src="/images/site_banner.png" alt="Group Website with Jekyll">
```

![Group Website with Jekyll]({{ site.url }}/files/site_banner.png)

Adding this `img` element should result in this title banner appearing
at the top of your page.

> ## Image Elements
>
> In the `img` tag above,
> the `src` parameter tells the web browser the location of
> the image file to display on the page,
> and the `alt` parameter defines _alternative text_
> (often abbreviated to _alt text_).
> This alternative text is important for two reasons:
>
> 1. It defines the description given to anyone using
>    [a screen reader][screen-reader] to access your site,
>    who cannot view the image itself.
>    If you do not define alt text for an image/figure,
>    the content of your site becomes less accessible for these users.
> 2. If the browser cannot display the image for some reason
>    (e.g. the image is moved/renamed/cannot be served)
>    the alt text is displayed instead.
>
> It is good practice to _always_ define alt text for your images,
> and you should aim to limit this alt text to a brief description
> of the information provided by the image,
> ideally providing no more or less detail
> than is displayed in the image itself.
{: .callout }

> ## Optional Exercise
>
> It is common for banner logos like the one above to link back to the homepage
> of the website they are displayed on.
> Wrap the `img` element in a set of hyperlink tags (`<a></a>`) to link
> the image to the landing page (`index.md`) of your site.
>
> > ## Solution
> >
> > ```
> > <a href="https://YOUR_USERNAME.github.io/YOUR_REPO_NAME/"><img src="/images/site_banner.png" alt="Group Website with Jekyll"></a>
> > ```
> >
> {: .solution }
{: .challenge }

To make the banner to appear above every page on our site,
we could add the code above to each Markdown file in our repository.
But if we wanted to adjust it - display a different image,
adjust the link target, etc -
we would need to make the same adjustment on every page.
Instead, we can go some way to avoid this hassle by using
some magic that Jekyll provides: `include` tags.
To demonstrate this, save the HTML snippet used to display the image into
a new file in your repository, called `_includes/banner.html`.
Unlike when we wanted to upload a pre-existing file
to a new folder earlier,
we can create the new folder and the new file simultaneously:

1. click "Create new file" under the "Add file"
dropdown on your repository homepage,
2. in the "Name your file..." box, type `_includes/`.
   As before, the folder name should be automatically inserted
   next to the box.
3. You can then name the file `banner.html` and, when you commit the changes,
   the `_includes` folder will have been added to your repository.

Now delete the HTML block you added to `index.md`,
and replace it with the following `_includes` tag:

```
{% raw %}{% include banner.html %}{% endraw %}
```

Refresh the page and, barring any typos e.g. in the name of the file,
you should see the banner image on the page as before.
You can add the same `include` tag at the top of
all the other Markdown files for your site
to get the same banner displayed on every page.

The `include` tag can be used to insert the Markdown or HTML contained in
any file saved within `_includes`: provide the path to that file
relative to `_includes/` and Jekyll will substitute the contents into the page
before rendering it as HTML.
Like the `_config.yml` file that contains the configuration for your Jekyll site,
the `_includes` folder has a name beginning with an underscore to show that it
has a special meaning to Jekyll.
We will see another example of this shortly.

> ## Why Not Use Variables?
>
> We must place our blocks of content for inclusion in separate files because
> **Jekyll does not support substitution of variables within variables**.
> If you'd like to investigate further,
> you might try creating a global variable in your site's `_config.yml`
> which includes a call to another variable in its value, e.g.
> `social: "{% raw %}Follow us on [Twitter]({{site.twitter}}){% endraw %}"`,
> and using it in a page (`{% raw %}{{site.social}}{% endraw %}` for the example above).
{: .callout }

> ## Including Contact Information
>
> The last line of `index.md` includes the kind of information you might want to
> re-use in multiple places throughout your site.
>
> ~~~
> Have any questions about what we do? [We'd love to hear from you!](mailto:{% raw %}{{site.email}}{% endraw %})
> ~~~
> {: .source }
>
> Copy the snippet and save it into an appropriately-named file,
> then use an `include` statement to re-insert it
> at the bottom of your site's `index.md`,
> and add it at the bottom of the `team.md` pages.
>
> > ## Solution
> > create a file called `contact.md`
> > (or similar) inside the `_includes` folder:
> >
> > ~~~
> > Have any questions about what we do? [We'd love to hear from you!](mailto:{% raw %}{{site.email}}{% endraw %})
> > ~~~
> > {: .source }
> >
> > and add the line
> >
> > ~~~
> > {% raw %}{% include contact.md %}{% endraw %}
> > ~~~
> > {: .source }
> >
> > at the end of `index.md` (replacing the equivalent line if it's still present)
> > and `team.md`.
> {: .solution }
{: .challenge }

> ## Including Link References
>
> You can use `include` tags to help minimise the effort required to
> keep links up-to-date across your site.
> In the [Authoring with Markdown](/markdown/) section,
> we learned about writing reference-style links in Markdown,
> e.g. `[link text][link-target]` in the body of the file with a corresponding
> `[link-target]: https://carpentries.org` link reference
> (usually all such references are kept at the bottom of the file).
> Using `include` tags,
> the link references for every page on your site can be stored in a file in the
> `_includes` folder (we recommend the name `_includes/links.md`)
> and inserted into the end of each page.
> With this approach, any time you need to update one of these link references,
> e.g. if the URL changes to your host institute website,
> you only need to change the URL in `_includes/links.md` to update the target
> of all the relevant links across your site.
{: .callout }





------------ The bits below are moved from episode 05 and need proper merging here --------------

### List Parameters and For Loops

YAML lets us define lists and dictionaries too, in addition to simple parameters we have seen so far.
And Jekyll supports the use of these more complex parameters as well.

For example, we may want
to list the names of all the project team members, together with their roles and start dates inside the `_config.yml` file
and make use of this information throughout the website. To do so in YAML notation would look something like:

~~~
team_members: [
    {name: "Sarah Becker", role: "project lead", start_date: "2016-02-01"},
    {name: "Jane Smith", role: "maintainer", start_date: "2018-03-15"},
    {name: "Albert Hamilton", role: "editor", start_date: "2017-12-01"},
]
~~~
{: .language-yaml}
This defines 'team_members' as a list of 3 elements; each element is a dictionary with key-value pairs for name, role and date.

> ## Indentation in YAML
> Note that indentation level in YAML is important - it can be a cause of some not-so-obvious mistakes. Use online YAML
>code validators, such as [YAML Lint](http://www.yamllint.com/), to make sure your YAML is correctly formatted.
>
{: .callout}

In order to access all elements in a list you need a 'for loop', which is performed in Liquid
by surrounding it in a curly brace percentage sign as:
`{% raw %}{% for variable in list %}{% endraw %}`. You follow this with the 'body' of your loop, and finish off
 with the 'for loop' end-tag: `{% raw %}{% endfor %}{% endraw %}`.

Let's access the information about the team and display the name of the project lead on the home page `index.md` and the information about the whole team in `about.md`. Note that we access the team lead's name as `team_members[0]["name"]` because the team lead is the first team member in the `team_members` list.

1. Modify `_config.yml` file and add the `team_members` parameter as defined above. The file should now look like:

    ~~~
    title: "Building Websites in GitHub"
    description: "This research project develops training materials for reseachers wanting to learn to build project
    websites in GitHub with GitHub Pages."
    email: "team@my.research.org"
    twitter: "https://twitter.com/my_research_project"
    team_members: [
        {name: "Sarah Becker", role: "project lead", start_date: "2016-02-01"},
        {name: "Jane Smith", role: "maintainer", start_date: "2018-03-15"},
        {name: "Albert Hamilton", role: "editor", start_date: "2017-12-01"}
        ]
    ~~~
    {: .language-yaml}

2. In file `about.md`, we add a new section for the team and iterate over the values defined in parameter `site.team_members` in a loop to display all team members' names and roles. The file now should look like:

    ~~~
    # About

    ## Project
    {% raw %}{{ site.description }}{% endraw %}

    ## Funders
    We gratefully acknowledge funding from the XYZ Founding Council, under grant number 'abc'.

    ## Team

    The following people are members of our research team:
    {% raw %}{% for team_member in site.team_members %}
        - Name: {% raw %}{{ team_member.name }}{% endraw %}, role: {% raw %}{{ team_member.role }}{% endraw %}
    {% raw %}{% endfor %}{% endraw %}

    ## Cite us
    You can cite the project as:

    >    *My research project. Zenodo. https://zenodo.org/record/doi*

    ## Contact us

    Email: [team@my.research.org](mailto:{% raw %}{{ site.email }}{% endraw %})

    Twitter: [@my_research_project]({% raw %}{{ site.twitter }}{% endraw %})
    ~~~

3. In file `index.md` add the team lead's name so that it looks like:

    ~~~
    # {% raw %}{{ site.title }}{% endraw %}

    ## Description
    {% raw %}{{ site.description }}{% endraw %}

    The project is led by {% raw %}{{ site.team_members[0]["name"] }}{% endraw %}.
    [See our full team](/about#team)

    Have any questions about what we do? [We'd love to hear from you!]({% raw %}mailto:{{ site.email }}{% endraw %})
    ~~~

If you need to add, remove or modify a team member, you can simply do it in `_config.yml` without modifying your pages.
Let's now change the values of a global parameter and study the effect.

> ## Exercise
> Your project team has changed. The team lead has left and in her place is a new person: 'Tom Cat', who started on
>'2020-10-01'. In addition, the team was expanded and a new developer called 'Alice Dauncey' who joined on '2020-09-15'.
> Update your website to reflect these team changes.
> > ## Solution
> > Luckily, we keep all our global settings in `_config.yml` so all we have to do is update the values there. This saved us some work as for the team lead we would otherwise have to modify both `index.md` and `about.md`.
> >
> >For the new developer joining the team, we also only need to her information to `team_members` in `_config.yml` and our `for loop` from `about.md` will simply pick up the changes automatically. Magic! Our `_config.yml` file should now look like:
> >
> > ~~~
> > title: "Building Websites in GitHub"
> > description: "This research project develops training materials for reseachers wanting to learn to build project
> > websites in GitHub with GitHub Pages."
> > email: team@my.research.org
> > twitter: "https://twitter.com/my_research_project"
> > team_members: [
> >    {name: "Tom Cat", role: "project lead", start_date: "2020-10-01"},
> >    {name: "Jane Smith", role: "maintainer", start_date: "2018-03-15"},
> >    {name: "Albert Hamilton", role: "editor", start_date: "2017-12-01"},
> >    {name: "Alice Dauncey", role: "developer", start_date: "2020-09-15"}
> > ]
> > ~~~
> > {: .language-yaml}
> > Check the changes in your website.
> {: .solution}
{: .challenge}


{% include links.md %}
