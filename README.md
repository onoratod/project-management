# File Structure

The basic file structure of my projects looks like 

```
code
  └── set_environment.do
data
  └── raw 
  └── derived 
output
  └── graphs
```

The **code** folder holds all of the code for a project, which depending on the situation may be hosted on Github or Dropbox (more on this later). The **data** folder holds all the data for the project. The **raw** folder are data files that were not generated by the project's code. The **derived** folder holds all datasets created by the project's code. With **code** and **raw** you should be able to recreate **derived**. The **output** folder contains all non-data related output i.e. graphs, results, tables etc.

# File paths

File paths are always a tricky issue that make it different to share code among individuals with different setups. To try and simplify this, I define a set of globals in my `profile.do` which is a file run every time Stata is started. The relevant globals are `${dropbox}` and `${github}`. In theory, as long as you define globals to point to where the data are store and the code is located (sometimes these will be the same) on your machine then you will be able to run all subsequent do-files. 

File paths for the project are generated in a code file `set_environment.do` and are all relative to a `${root}` directory which will depend on the `${dropbox}` and `${github}` globals. This code file is loaded by each other code file at the top

```stata
include "${github}/project_name/code/set_environment.do"
```

And all the relevant filepaths will be loaded. The root directory for the project is `${github}/project_name`, so as long as `${github}` is defined appropriately for your machine you will be able to run all of the code. 

I like to use Github, so all of my projects are hosted in my local Github folder which is referenced by the `${github}` global. I store all of my data in Dropbox and use symbolic links so that I can reference files in my Dropbox locally from my Github folders. For these projects the root directory relies on the `${github}` global. Other projects might be entirely hosted on Dropbox and those will rely on the Dropbox global. In rare cases, some projects may use both, and will rely on both globals.
