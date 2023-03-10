---
title: "Third Post with Code Formatting"
date: 2023-01-05T17:44:35Z
---

Just Edited.
## 1. Create new site
```bash
PROJECT_FOLDER=./vol/var/www && PROJECT_NAME=my-dev-blog \
&& docker run --rm -it -v $PROJECT_FOLDER:/src klakegg/hugo:alpine-onbuild new site $PROJECT_NAME
```

> [!info]
> Congratulations! Your new Hugo site is created in /src/my-dev-blog.
>
 Just a few more steps and you're ready to go:
>
> 1. Download a theme into the same-named folder.
>   Choose a theme from https://themes.gohugo.io/ or
>   create your own with the "hugo new theme \<THEMENAME>" command.
>   2. Perhaps you want to add some content. You can add single files
>   with "hugo new \<SECTIONNAME\>/\<FILENAME\>.\<FORMAT\>".
> 3. Start the built-in live server via hugo server.
>
> Visit https://gohugo.io/ for quickstart guide and full documentation.

```bash
cd $PROJECT_FOLDER/$PROJECT_NAME
```

## 2. Change Folder and file permissions
The problem with the docker hugo image is using the root as a user, so it needs to change permissions
```bash
sudo chown -R $USER:$USER .
```

## 3.  Clone Hugo Theme from Git
```bash
git clone https://github.com/dillonzq/LoveIt.git themes/LoveIt
```

Or, create an empty git repository and make this repository a submodule of your site directory:

```bash
git init
git submodule add https://github.com/dillonzq/LoveIt.git themes/LoveIt
```

## 4. Adding the new theme to your project folder
```bash
echo "theme = 'LoveIt'" >> config.toml
```

## 5. Create New Post

```bash
docker run --rm -it -v $(pwd):/src klakegg/hugo:latest new posts/first-post.md
```

## 6. Building your first hugo site
```bash
docker run --rm -it -v $(pwd):/src -v $(pwd)/public:/public klakegg/hugo:latest --minify -D
```

