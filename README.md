# md-webpage-template

Markdown template that uses Unicode admonitions for Note (ℹ️), Tip (💡),
Important (‼️) and Warning/Caution (⚠️). No plugins needed. Just edit and
publish on GitHub Pages.

## Why I created this template

I wanted a simple way to host Markdown files as a website. Something clean where
others could easily reference materials without jumping through hoops. No heavy
frameworks, no complex builds. Just deploy content to GitHub Pages.

I really like how GitHub renders GitHub Flavoured Markdown
[(GFM) admonitions](https://github.com/orgs/community/discussions/16925)
natively on the GitHub website. They look great, they are readable, and they
just work.

However, GitHub Pages does not support these GFM admonitions out of the box. To
get GFM admonitions working in GitHub Pages, you would normally need plugins.
That means setup overhead, configuration files, and a lot of extra fuss for what
should be a simple documentation site.

That frustration led me to a different approach. Instead of fighting with
plugins and build environments, I turned to Unicode characters. Browsers support
them universally, and with a bit of styling, they can serve as clean, visual
admonitions. No extra tooling required.

So, I built this template. It is for anyone who wants a fuss-free way to deploy
Markdown articles as webpages on GitHub Pages. No plugins, no complexity. Just
write your Markdown, push it, and let the GitHub Pages do the rest.

## How the Unicode admonitions will look like

You can use the Unicode admonition as the Markdown code block below

```markdown
> ℹ️ Note
>
> Details of this note goes here.
> You can have more than one line.
```

The markdown admonitions will be rendered as follows.

This is a Note admonition.

> ℹ️ Note
>
> Details of this note goes here.
> You can have more than one line.

This is a Tip admonition.

> 💡 Tip
>
> Details of this tip goes here.

This is an Important admonition.

> ‼️ Important
>
> Details of this important information goes here.

This is an admonition for Warning or Caution.

> ⚠️ Warning
>
> Details of this warning goes here.

## How to use this template

Follow these steps to get your Markdown website up and running on GitHub Pages

1. Use the template

   Click the "Use this template" button at the top of this repository. This will
   create a new repository under your GitHub account with all the necessary
   files.

1. Enable GitHub Pages in your new repository

   Go to your repository Settings > Pages.

   Under "Source", leave it at default of "Deploy from a branch".

   Under "Branch", select `main` and `/docs`, and click "Save".

   Your site will be published at
   <https://your-username.github.io/your-repo-name/>.

   > 💡 Tip
   >
   > If you want your URL to appear in your repository's About, click the gear
   > icon beside "About", check the box for "Use your GitHub Pages website" and
   > click "Save changes".

1. Clone your new repository

   Clone the repository to your local machine so you can start adding your
   content.

   ```bash
   git clone https://github.com/your-username/your-repo-name.git
   ```

1. Edit the existing Markdown files or add your Markdown files

   Place your Markdown articles in the `docs` directory.

   > ‼️ **Important**
   >
   > Use the Unicode admonitions provided in the template for seamless rendering
   > in GitHub Pages.

1. Push your changes

   Commit and push your Markdown files to remote repository.

   ```bash
   git add .
   git commit -m "Add my Markdown articles"
   git push origin main
   ```

1. View your site.

   Wait a minute or two for GitHub Pages to build your site. Then visit your
   published URL to see your Markdown files rendered as a clean website.

1. Congratulations. You have deployed your website. No plugins, no configuration
   files, no build steps. Just Markdown and Unicode.
