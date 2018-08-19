# Silai : A personal portfolio theme with blog

Silai (சிலை) means statue in Tamil, a south indian language.

If you are using `exampleSite` folder for scaffolding, please remove this line from `config.yml`:

```
themesdir: "../.."
```

That line is just to make the development of the theme work with `hugo server` command.

Uncomment the theme name in config.yml:
```
theme=silai
```

## Running The Theme Locally

# Making it work in Netlify
This is tricky. Netlify needs a proper site with themes.

While it is possible to use this  set up with Netlify by amending the config file and `hugo` publish command within netlify, do so with care. No one else will be able to use the theme easily. I.e, no one else can clone a theme and just run `hugo server`.

all right, so the set up that works with netlify needs attention to the netlify build path.

netlify takes the repository and places it in a repo folder /opt/build/repo
repo folder will have theme files and the `exampleSite` folder

Even though the theme name is silai, the folder name is actually repo. 

so build command has to reflect it

```
hugo -s ./exampleSite --theme=repo --themesDir=../.. --verbose
```

`-s ./exampleSite` is the source of the website with content.

`--theme=repo` is a temporary theme name

`--themesDir=../..` takes the pointer out of exampleSite and out of repo so that you land in `/opt/build/` path (which indeed has a repo theme now , so to speak).

But one important change that was required in the config file.

The config file within example site cannot have the `theme` token. So I had to remove `theme=silai` - otherwise, netlify build failed.

Also , netlify publish directory has to be `./exampleSite/public` because the build is placed in `public` folder inside the source, in this case, the source is `exampleSite`. 