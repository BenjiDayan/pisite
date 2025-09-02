This is a jekyll site! jekyll is a ruby smth?

`bundle exec jekyll serve` Then it's up on `localhost:4000`

![This is your front page!](front_page.png)

It seems that fun_blog and main_blog as two separate folders can independently do their stuff?
According to a commont on fun_blog's `index.html`,

```
fun_blog is a top level folder and hence gets read by jekyll and put into _site/fun_blog.
However unless it has its own index.html, there will be no link on the top bar of the site. The derived
page is precisely that of the index.html here, where we list only fun_blog category posts
```

According to `jekyll`'s site, the main commands seem to be

```
jekyll new PATH --blank - Creates a new blank Jekyll site scaffold at specified path.
jekyll build or jekyll b - Performs a one off build your site to ./_site (by default).
jekyll serve or jekyll s - Builds your site any time a source file changes and serves it locally.
```

Which I guess is often prefaced with `bundle`?

We seem to have selected packages and extensions in `_config.yml` which are then installed by building (generating `Gemfile` and `Gemfile.lock`?). E.g. our theme is `minima`

NB we e.g. have in `_layouts/post.html` the comment:

```
This post.html was copied from minima (bundle info --path minima) shows where the templates are stored.
Then it's existence overrides it. So we added style="text-align: justify;" in the content div.

And we also add these style things to the css file:
```

TODO - look into <https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site> on how to host on github pages

`bundle exec jekyll serve --drafts`

Note I made _plugins directory - can add .rb for local plugins!


## Note on redirects??
index.html and about.markdown and index_blog.html get turned into benjid.dev/index.html and benjid.dev/about.html and benjid.dev/index_blog.html

This seems to only happen on github pages for whatever reason??
On jekyll local, these all get put under /blog/ instead...

I think jekyll local respects the baseurl: "/blog" in _config.yml, but somehow that doesn't occur for github pages. Maybe 