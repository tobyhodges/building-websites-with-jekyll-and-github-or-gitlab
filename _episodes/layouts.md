---
title: "Page Layouts"
teaching: 0
exercises: 0
questions:
- "How can I design the layout for all pages on my site?"
- "Where can I find pre-built themes for my site?"
- "How can I create new layouts based on those I already have?"
objectives:
- "Apply a template layout to a page"
- "Find and implement pre-existing themes to determine the style of a site"
- "Create new page templates that inherit from existing layouts"
keypoints:
- "Files in the `_layouts/` directory can be used as page templates"
- "The structure of a page is determined by the `layout` field in the page front matter"
- "You can find many pre-existing themes for sites on the Internet"
- "You can avoid duplicated effort by basing new layouts on previous ones"
---

Elements that will appear on every page across our website,
like the banner image we `include`d in our pages in the previous section,
form part of the structure of the page:
unlike the content specific to each page,
these structural elements do not change from page to page.
As such, although the `include` tags reduce the pain we endure when
adjusting that repeated content,
it is not good practice to `include` the same content over and over again.
This structure can instead be defined within the _layout_ of the pages of the site.

Common elements found in a layout are
logos,
banners,
navigation menus,
footer content such as copyright and licensing information:
material often found at the very top or very bottom of a webpage.

## Defining a Layout

To demonstrate how layouts work in Jekyll we will copy the contents of
`_includes/banner.html`, the HTML file defining the `img` element for our banner,
to `_layouts/page.html`, a new file in a new folder.
GitHub doesn't provide a way to make a copy of a file,
so you will need to do this manually.
Note that the name of the `_layouts` folder begins with an underscore,
which as we learned earlier means it has special meaning to Jekyll.
You have just defined the first layout for pages on your site.
Congratulations!

To apply this layout to your site's landing page,
add `layout: page` to the YAML front matter of `index.md`.
When you reload your site's homepage you will see
that there is good news and bad news:
The good news: the banner image is there again;
the bad: all the other page content has disappeared!

FIXME: add screenshot here

The page content is missing because we haven't yet told Jekyll where to put it.
To do that we need to add the special `content` variable into the layout file:

~~~
{% raw %}<img src="/images/site_banner.png" alt="Group Website with Jekyll">{% endraw %}

{% raw %}{{ content }}{% endraw %}
~~~
{: .source}

If we make the change above to `_layouts/page.html` and reload our site's homepage,
we now see the page content has returned but the banner image appears twice!

FIXME: add screenshot here

The duplication is happening because the
`{% raw %}{% include banner.html %}{% endraw %}`
tag is still present in `index.md`.

> ## Cleaning up
>
> Remove the include tag from all the pages of your site,
> and set every page to use the `page` layout.
>
{: .challenge }

> ## Expanding the layout
>
> We will probably want to include the contact line we added in the previous section
> in every standard page on our site.
> Move the `include` tag to the layout template
> so we don't have to remember to `include` it every time we make a new page.
> Place it _below the page content_ so that it appears at the end of each page
> that uses this layout.
> Check that this works by reloading of the pages that uses the `page` layout.
>
> > ## Solution
> > Your layout file, `_layouts/page.html`,
> > should look like this:
> >
> > ~~~
> > {% raw %}<img src="/images/site_banner.png" alt="Group Website with Jekyll">
> >
> > {{ content }}
> >
> > {% include contact.md %}{% endraw %}
> > ~~~
> > {: .source }
> {: .solution }
{: .challenge }


## Valid HTML, Page Metadata and a Default Layout

You might recall from
[the introduction](/introduction/index.html#hello-world-in-html)
to this tutorial, that a _valid_ HTML page consists of more than
only the content we want to display.
We haven't written these extra elements (`<html>`, `<head>`, `<meta>`, etc)
in our layout file: but there are some advantages to defining these yourself:
these invisible elements of a web page describe metadata about the page,
which can be used by Internet search engines to better understand what
the page is about and who it is for.
This information is factored in when the search engine indexes the page,
and subsequently makes it more findable for your target audience.
(This is one consideration in the much larger field of
[Search Engine Optimisation][seo-wikipedia].)

For example, to make the browser automatically adjust the way your pages are
shown on different diplays/devices,
you could include the element
`<meta name="viewport" content="width=device-width, initial-scale=1.0">`
inside the `<head>` of your pages.
([Read this W3Schools page to learn more][w3-viewport].)

It is common practice to define the structural elements of your site's pages
inside a `_layouts/default.html` file.
This file defines the bare minimum layout your pages should have.

> ## Laying the groundwork
>
> Create another layout file, `default.html`, with the following content:
>
> ~~~
> {% raw %}<!doctype html>
> <html lang="en">
>   <head>
>     <meta charset="utf-8">
>     <title>{{ page.title }}</title>
>   </head>
>   <body>
>     {% include banner.html %}
>     <h1>{{ page.title }}</h1>
>     <section>
>       {{ content }}
>     </section>
>     <footer>
>       An example website made with Jekyll.
>     </footer>
>   </body>
> </html>{% endraw %}
> ~~~
> {: .source }
>
> 1. Apply this layout to one of your pages and reload the page to check that
>    it works as expected.
>    You should see a footer at the bottom of the page.
> 2. Note that we are using `include` to add the banner image
>    to this default layout.
>    How can you do the same with the footer,
>    instead of defining it directly within the layout file?
>
> > ## Solution
> >
> > To separate the footer from the layout,
> > copy the {% raw %}<footer></footer>{% endraw %} tags and the text between
> > them into a file `_includes/footer.html`:
> >
> > ~~~
> > {% raw %}<footer>
> >   An example website made with Jekyll.
> > </footer>{% endraw %}
> > ~~~
> > {: .source }
> >
> > And to `include` it back into the layout,
> > replace that `footer` element with
> >
> > ~~~
> > {% raw %}{% include footer.html %}{% endraw %}
> > ~~~
> > {: .source }
> {: .solution}
{: .challenge }



## Layout Inheritance

To prevent the duplication of all this "invisible" HTML across all the layouts
we define for a site,
Jekyll allows for layouts to be based on other layouts,
which can be based on other layouts,
and so on.
This is referred to as _layout inheritance_,
and is refreshingly easy to use.

To set our `page` layout to inherit from `default.html`,
we should add YAML front matter to the layout file,
specifying the `layout` to be `default`:

~~~
{% raw %}
---
layout: default
---

{{ content }}

{% include contact.md}

{% endraw %}
~~~
{: .source }

In the above, we have (once again!) removed the banner image,
as that is included in the `default` layout.
If you reload a page using the `page` layout,
you should now see that it has all of the structure provided in `default.html`
as well as the contact information included in `page.html`.
The purpose of this approach, defining the core structure that will be common
to every page across your site in a default layout,
then basing more specific layouts on this foundation,
is to keep duplication to a minimum within our repository.
Whenever you want to update something about the styling or structure of your site,
you should only need to make that change in a single file and let it propagate
to all the relevant pages.


> ## You Can't Include Link References in the Layout
>
> In the previous section,
> [we recommended that you `include` a file of references](/includes/indx.html#including-link-references)
> for the links on your site.
> Unfortunately, you cannot add this `{% raw %}{% include links.md %}{% endraw %}`
> tag to the default layout of your site to prevent you from needing to
> add it at the bottom of every page.
> This is a result of [the order of Jekyll's rendering process][jekyll-rendering],
> which constructs the HTML of the page content in isolation
> _before_ constructing the HTML of the relevant layout(s) and nesting it inside.
> If the link references are `include`d in the layout rather than the content,
> those references will not be available while the content is converted to HTML
> and the links will not render correctly.
> It is annoying to have to remember to add
> `{% raw %}{% include links.md %}{% endraw %}`
> to the end of every page's Markdown,
> but less annoying than having to manually edit the same link reference in
> multiple locations throughout the site.
>
{: .callout}

## Using a Pre-Existing Theme

We have now seen how to create pages,
re-use content across them,
and define layouts,
and you may be coming to understand that it requires a lot of work
to build a website from the ground up.
This is not a task we recommend you undertake lightly!

Instead, an alternative is to base your site on one of
the many pre-existing themes for Jekyll.
Many of these themes are free and open source and,
as long as you follow the terms of the license
(e.g. remember to give due credit to the original -
check the full terms for details),
can be adapted/customised to suit your purposes.
**You can browse a list of Jekyll themes on [jekyllthemes.io][jekyllthemes]**.

These themes can be elaborate and quite complicated.
We hope that the knowledge of Jekyll that you have gained from
following this lesson will help you understand how they work
and determine what you need to change and where, to make the customisations
you need for your site.

{% include links.md %}
