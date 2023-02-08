# Template: bookdown and githubpages
This repository is a template for bookdown project and it will be published by Github Pages.

# Steps

## Create repository on your GitHub.

If you want to create GitHub Pages, you have to add suffix `.github.io` to repository name. 
e.g) `example-repository.github.io`

And then, from settings > Pages, please set publish branch (e.g: main) and choose assets directory (e.g: docs)

Please see https://docs.github.com/ja/pages/getting-started-with-github-pages/creating-a-github-pages-site.

## Create project with Git in RStudio. 

From menu bar, click New Project > Version Control > Git, then fill repository URL that you have created like above.

## Create book

1. Install and import bookdown pkg. 

```{r}
install.packages("bookdown")
require(bookdown)
```

2. Create dirs: book, docs

```{r}
for(dn in c("book", "docs")) dir.create(dn)
```

3. Create gitbook project

create gitbook project in book dir.

```{r}
bookdown::create_gitbook("book")
```

3. check and remove some files.

For me, some files is not needed, so execute the code to delete them.

```{r}
fns <- c(
    "02-cross-refs.Rmd",
    "03-parts.Rmd",
    "04-citations.Rmd",
    "05-blocks.Rmd",
    "06-share.Rmd",
    "book.Rproj",
    "README.md"
)

for (fn in fns){
  if(fn %in% list.files("book")){
      file.remove(paste("book", fn, sep="/"))
  }
}
```

## Rendering

You can render .Rmd files to HTML files using `bookdown::render_book()`

```{r}
bookdown::render_book("book", output_dir="../docs")
```

`output_dir` is relateve path from rendered dir.

## Put `.nojekyll` file

```{r}
if(!file.exists("docs/.nojekyll")){
  file.create("docs/.nojekyll")
}
```

## Push to main branch

Finally, please push this changes to the repository.
After this, visit website and you can see this book!