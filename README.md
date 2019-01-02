# Bienvenue sur le Wiki open-source de Nebulas!

La communauté de Nebulas est ouverte et chacun peut devenir un contributeur et participer, avec nous, à la construction d'un mode décentralisé.

Le wiki Nebulas est un outil collaboratif permettant à la communauté de publier divers documents de façon collaborative. Ceci comprend les guides d'utilisation, les guides pour le développement, les sources d'apprentissage et d'autres documents utiles. 

La partie dédiée au développement du réseau principal de ce wiki Nebulas se base sur [https://github.com/nebulasio/wiki](https://github.com/nebulasio/wiki)("the wiki"). 


# Comment contribuer

Nebulas vise à mettre en place un ecosystème en amélioration continue, ce qui implique que nous avons besoin de l'aide de la communauté. Nous avons besoin de vos contributions! Cela ne se limite pas uniquement au développement mais comprend également les soumissions de bug, les traductions, la diffusion des principes de Nebulas, les réponses aux questions et ainsi de suite.

[Learn more about how to contribute](https://wiki.nebulas.io/en/latest/how-to-contribute.html)

# Démarrer

Ce projet a été créé avec [sphinx](http://www.sphinx-doc.org/en/master/) et chargé sur [readthedocs](https://readthedocs.org/) pour l'hébergement. L'url de la documentation en ligne après hébergement est: [https://nebdocs.readthedocs.io/en/latest/](https://nebdocs.readthedocs.io/en/latest/).

This project supports documents in the following two formats:

- Markdown(.md)
- reStructuredText(.rst)

The directory structure of the document is defined in the README.rst file in the same directory.

## Language version and branch rules:
1. The multi-language version is managed separately by different branches. The currently supported languages are as follows:
- master: English version;
- zh-CN: Simplified Chinese version;
2. To facilitate document management, the document structure of different branches is as consistent as possible with the main branch;
3. Each language is allowed to have its own temporary version. It is recommended to add the suffix version number to the version name, for example, en1.0, zh-CN1.1;

## How to build
1. clone the project from github, next command refers to the master branch:

```bash
git clone https://github.com/nebulasio/nebdocs.git
```

2. install the necessary python components:

```bash
pip install sphinx==1.5.6 sphinx-autobuild sphinx_rtd_theme recommonmark
```
3. build the project:

```bash
cd nebdocs
make html
```

## How to add a new document
### If you need to add a file
1. Add the file to the appropriate directory;
2. Locate the README.rst file in the directory where the file is located (the project root directory is index.rst file), open the file, and add the newly added file name to the file list after the 'toctree' keyword. E.g:

For this file structure:
```
+--folder
   |
   +--README.rst
   +--config.md
   +--contributors.md
   +--newFile.md
```

The content of README.rst should look like this:
```
.. toctree::
    :titlesonly:

    Config.md
    Contributors.md
    newFile.md
```

### If you need to add a new directory
In this case, you need to add a README.rst file to define the document directory structure in this directory. Put other file names in the file list after the 'toctree' keyword. For details, refer to other README.rst files. The file list in the README.rst file of the previous directory should add the relative path of the README.rst file of the current directory, for example:

For this file structure:
```
+--folder
   |
   +--README.rst
   +--config.md
   +--contributors.md
   +--newDirectory
      |
      +--README.rst
      +--newFile.md
```
The contents of the folder/README.rst file should be:
```
.. toctree::
    :titlesonly:

    Config.md
    Contributors.md
    newDirectory/README.rst
```

## How to add a new language version

1. Create a new branch, for the chinese version, for instance:
```bash
Git checkout -b zh-CN
```
2. Modify the github configuration in ./docs/conf.py, find the 'html_context' definition, and change the value of the 'github_version' field to the new branch name 'zh-CN', as follows:

```python
# VCS options:
Html_context = {
     "display_github": True, # Integrate GitHub
     "github_user": "nebulasio", # Username
     "github_repo": "nebdocs", # Repo name
     "github_version": "zh-CN", # Version
     "conf_py_path": "/", # Path in the checkout to the docs root
}
```

3. Replace the documents that you need to translate with the new language version.

4. Submit the files to github:

```bash
Git push --set-upstream zh-CN
```

**Note:** it is highly likely you will need to rebase master onto that branch in order for the team to be able to merge the pull request cleanly. To do so, and avoid all the conflicts that will certainly come with it, do as follows, from your working branch, after having updated master with ```git pull origin master```:
```bash
git rebase -Xtheirs master
git push -f
```

5. Notify the manager to add a new language version to the readthedocs' online documentation.
