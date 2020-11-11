# Othmane Rifki's Website #

This is Othmane Rifki's collection of personal notes on coding, mathematics, and machine learning. This repository contains the source files for my website, https://othrif.github.io/.


## To deploy: ##
Run
``` bash
./deploy.sh
```

## Add Jupyter notebook: ##
``` bash
hugo new  --kind post post/my-post
cd content/post/my-post/
jupyter notebook
jupyter nbconvert Untitled.ipynb --to markdown --NbConvertApp.output_files_dir=.
cat firstJupyter.md | tee -a index.md
```

####first time
``` bash
rm -rf public/
git submodule add -f -b master https://github.com/othrif/othrif.github.io.git public
hugo
cd public/
git add .
git commit -m "Initial commit"
git push -u origin master
```
``` bash
hugo
cd public
git add .
git commit -m "Build website"
git push origin master
cd ..
```


Copy to CERN server:
``` bash
cp -r /Users/othmanerifki/projects/website/notes/public ~/cernbox/www
```

#### Create a new blog post
``` bash
cd <MY_WEBSITE_FOLDER>
hugo new  --kind post post/my-post
cd <MY_WEBSITE_FOLDER>/content/post/my-post/
```

#### Convert notebook to Markdown
``` bash
jupyter nbconvert Untitled.ipynb --to markdown --NbConvertApp.output_files_dir=.

# Copy the contents of Untitled.md and append it to index.md:
cat Untitled.md | tee -a index.md

# Remove the temporary file:
rm Untitled.md
```


#### Lunch server locally: ####
``` bash
hugo server
```
Enter http://localhost:1313 in the browser.


#### Add academic references: ####
``` bash
academic import --bibtex <path_to_your/publications.bib>

```


#### Quick Start ####
1. Download a theme into the same-named folder.
   Choose a theme from https://themes.gohugo.io/ or
   create your own with the "hugo new theme <THEMENAME>" command.
2. Perhaps you want to add some content. You can add single files
   with "hugo new <SECTIONNAME>/<FILENAME>.<FORMAT>".
3. Start the built-in live server via "hugo server".


