# primer-dark-starter

This template provides an easy way to generate a dark-mode enabled GitHub Pages
website from markdown files in your repository.

It uses [Primer Dark theme](https://github.com/0xNixxy/primer-dark) for Jekyll,
which has automatic detection of client browser settings to render the website
in either dark mode or light mode.

This template also uses Unicode admonitions, instead of GitHub Flavoured
Markdown [(GFM) admonitions](https://github.com/orgs/community/discussions/16925),
to achieve consistent rendering of admonitions across markdown files on
GitHub.com and HTML pages on GitHub Pages.

## How to use the Unicode admonitions

The following Unicode characters are used to represent the following
admonitions:

- Note (ℹ️)
- Tip (💡)
- Important (‼️)
- Warning or Caution (⚠️)

Insert a Unicode admonition as per the Markdown block below

```markdown
> Tip (💡)
>
> Details of this note goes here.
> You can have more than one line.
```

### Note

The following shows the Note admonition and its render.

```markdown
> ℹ️ Note
>
> Highlights information that users should take
> into account, even when skimming.
```

> ℹ️ Note
>
> Highlights information that users should take
> into account, even when skimming.

### Tip

The following shows the Tip admonition and its render.

```markdown
> 💡 Tip
>
> Optional information to help a user be more successful.
```

> 💡 Tip
>
> Optional information to help a user be more successful.

### Important

The following shows the Important admonition and its render.

```markdown
> ‼️ Important
>
> Crucial information necessary for users to succeed.
```

> ‼️ Important
>
> Crucial information necessary for users to succeed.

### Warning or Caution

The following shows the Warning admonition and its render.

```markdown
> ⚠️ Warning
>
> Critical content demanding immediate user attention
> due to potential risks.
```

> ⚠️ Warning
>
> Critical content demanding immediate user attention
> due to potential risks.

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

1. Congratulations. You have deployed your website.
