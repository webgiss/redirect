# Redirect Project

A simple project for handling URL redirections based on predefined site mappings.

The goal of this project is to provide a simple way of creating a url shortener you can easily host on github pages / gitlab pages.

## Very basic usage

1. Clone this project in your github account or github organization.

2. Enable GitHub Pages.

The site will be published to `https://<your-username>.github.io/<repository-name>/`

3. Edit the `sites.json` file to include your desired site mappings.

Example:
```json
{
    "g": "https://www.google.com/",
    "y": "https://www.youtube.com/",
    "gh": "https://www.github.com/",

    "": ""
}
```

4. Access your short URLs like this:

```
https://<your-username>.github.io/<repository-name>/<your-short-url>
```

If you enter `https://<your-username>.github.io/<repository-name>/g`, it will redirect you to `https://www.google.com/`.

## Advanced Usage

### Custom Domain

If you want to use a custom domain instead of the default GitHub Pages URL, you can configure it in the repository settings and update the `CNAME` file accordingly.

For example, if your custom domain is `https://example.com/`, your short URLs will look like this:

```
https://example.com/<your-short-url>
```

If you do that, you need to edit the `404.html` file to change the line `const pathSegmentsToKeep = 1;` to `const pathSegmentsToKeep = 0;`.

`pathSegmentsToKeep` should be set to `0` because the root of your site is `/` and not `/<repository-name>/` any more, thus level 0 instead of level 1.

If you decide to have something complex (why would you?), like hosting the site's root at `/my/redirect/`, you'll need to set `const pathSegmentsToKeep = 2;` in the `404.html` file.

Be aware that for custom domains, you'll need to buy that domain from a domain registrar and configure it to point to your GitHub Pages site. This require a bit of configuration for neophytes, but once set up, it works seamlessly.

### Error page

In case of an error (mainly, the short URL does not exist in the `sites.json` file), you'll be redirected to the error.html page.

That page is a minimal HTML static page that works, but is not very user-friendly. That's on purpose, you can edit the `error.html` file to customize the look and content of that page. It's currently minimalistic in order to make it readable by anyone. You can add your brand / style to make it more appealing.

## ⚠️ Warning

This project is *not* suited for handling private or sensitive URLs. Once someone has access to one link, they can potentially access all other links as well by accessing the file `https://<your-username>.github.io/<repository-name>/sites.json`. **Never put in `sites.json` any URL that you want to keep private**.


