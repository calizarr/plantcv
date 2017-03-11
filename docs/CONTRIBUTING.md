# How to contribute

This document aims to give an overview of how to contribute to PlantCV.
We encourage third-party contributions in a variety of forms. There are
a few guidelines that we need contributors to follow so that we can
keep things working for all users.

There are many ways to contribute:

* Report bugs
* Request features
* Join the discussion of open issues, features, and bugs
* Contribute algorithms to the library
* Revise existing code
* Add or revise documentation

If you need any help, please contact us.

## Creating Issues

- Make sure you have a GitHub account.
- Search GitHub and Google to see if your issue has already been reported
    - [Create an issue in GitHub](https://github.com/danforthcenter/plantcv/issues), assuming one does not already exist.
	- Clearly describe the issue including steps to reproduce when it is a bug.
	- Make sure you fill in the earliest version that you know has the issue.

## Contributing Text or Code

### Overview

When you add a significant **new feature**, please create an issue
first, to allow others to comment and give feedback. 

When you have created a new feature or non-trivial change to existing
code, create a 'pull request'.

**Branching and Pull Requests**: Although core developers have write 
permissions to the PlantCV repository, 
*please use the feature branch workflow* (below) in order to allow pull
requests, automated testing, and code review.

### Using Git at the Command Line

Introduce your self to *git*, make sure you use an email associated with
your GitHub account. This can also be done with the GitHub desktop application.

```
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```

Fork the PlantCV repository to add it to your GitHub account.

[Fork this repository](https://github.com/danforthcenter/plantcv#fork-destination-box)

Clone your fork of this repository

```
git clone https://github.com/<your username>/plantcv.git
```

Setup repository to be able to fetch from the master

```
git remote add upstream https://github.com/danforthcenter/plantcv.git
```

### Adding Features and Submitting Changes

Always work in a branch rather than directly on the master or dev 
branches. Branches should focus on fixing or adding a single feature or
set of closely related features because this will make it easier to 
review and merge your contributions. Since multiple people work on the 
same repository, make sure to keep your master/dev branches in sync
with the master/dev of the danforthcenter/plantcv repository. The master
branch is for official releases only, new developments should be based
on the dev branch (i.e. your feature branch should be based and merged
on dev).

Here is a simplified workflow on how add a new feature:

#### Get the latest version

Update your dev branch with the main PlantCV repository (both locally and on GitHub)

```
git fetch upstream
git checkout dev
git merge upstream/dev
git push
```

#### Create a branch to do your work

A good practice is to call the branch in the form of GH-<issue-number> 
followed by the title of the issue. This makes it easier to find out the
issue you are trying to solve and helps us to understand what is done in
the branch. Calling a branch my-work is confusing. Names of branch can
not have a space, and should be replaced with a hyphen.

```
git checkout -b GH-issuenumber-title-of-issue
```

#### Work and commit

Do you work, and commit as you see fit. Make your commit messages helpful.

```
# Stage files to commit (. for all, or specfic list of files)
git add .

# Commit staged files with descriptive message
git commit -m "Helpful message about updates."
```

#### Push your changes up to GitHub

Pushing will update your fork of the PlantCV repository. If this is the
first time pushing to GitHub you will need to use the extended command
below, other wise you can simply do a `git push`.

```
git push -u origin GH-issuenumber-title-of-issue
```

#### Pull Request

Once your new feature is ready, create a pull request from your branch 
to the main PlantCV repository. Generating a pull request will notify
the maintainers of PlantCV. GitHub will report whether the merge can be
done automatically without conflict, or whether manual fixes are 
required. Travis-CI will also generate an automatic build report on 
whether or not the updates break the automated unit tests.

### Guidelines for adding new features

In general, new contributions to PlantCV should benefit multiple users
and extend the image processing or trait analysis power of PlantCV. 

What should/should not be added to PlantCV:

*  New validated image processing functions are highly encouraged for contribution.  
*  New validated trait extraction algorithms are highly encouraged for contribution.  
*  Image processing workflow scripts that are specific for your project 
should **not** be added to PlantCV since these are (usually) not
generalized or updated to maintain compatibility with new versions.

If you have questions don't hesitate to ask [here](https://github.com/danforthcenter/plantcv/issues).

#### Testing and documenting your code

In addition to adding a new feature, test your code thoroughly. 

Add unit tests and sample input/outputs to the `tests` folder/script so that 
automated testing (Travis-CI) will include tests on your new feature. 
Similarly, if you are updating existing code, make sure that the `test.py`
script passes on the function you modified.

Add documentation for your new feature. A new Markdown file should be
added to the docs folder, and a reference to your new doc file should
be added to the `mkdocs.yml` file. You can test that your new documentation
can be built correctly locally using mkdocs from the root of your local
plantcv repository.

```
mkdocs build --theme readthedocs --site-dir _site
```

#### New function style guide

Include commenting whenever possible.

Start code with import of modules, for example:

```python
# Import external packages
import numpy as np
import cv2

# Import functions from within plantcv
from . import print_image
```

Here is a sample of a new function. Arguments should be defined.
Generally, all PlantCV functions should include a device (integer) and
debug (default = None) arguments. Note that the inputs and outputs
are documented with Python docstrings.

```python
def new_function(img, device, debug=None):
    """New function.
    
    Inputs:
    img        = description of img
    device     = device number. Used to count steps in a workflow
    debug      = None, print, or plot. Print = save to file, Plot = print to screen.
    
    Returns:
    device     = device number
    returnval1 = return value 1
    
    :param img: type
    :param device: int
    :param debug: str
    :return device: int
    :return returnval1: type
    """
    
    # Increment the device number by 1
    device += 1

    returnval1 = some_code_on_img(img)
    
    if debug == 'print':
        print_image(img, (str(device) + '_new_function.jpg'))
    elsif debug == 'plot':
        plot_image(img)

    return device, returnval1
```

## Code Of Conduct

### Summary

Harassment in code and discussion or violation of physical boundaries is
completely unacceptable anywhere in the PlantCV project codebase, issue
tracker, chatrooms, mailing lists, meetups, and other events. Violators
will be warned by the core team. Repeat violations will result in being
blocked or banned by the core team at or before the 3rd violation.

### In detail

Harassment includes offensive verbal comments related to gender 
identity, gender expression, sexual orientation, disability, physical
appearance, body size, race, religion, sexual images, deliberate 
intimidation, stalking, sustained disruption, and unwelcome sexual 
attention.

Individuals asked to stop any harassing behavior are expected to comply immediately.

Maintainers are also subject to the anti-harassment policy.

If anyone engages in harassing behavior, including maintainers, we may 
take appropriate action, up to and including warning the offender, 
deletion of comments, removal from the project’s codebase and 
communication systems, and escalation to GitHub support.

If you are being harassed, notice that someone else is being harassed, 
or have any other concerns, please contact a member of the core team immediately.

We expect everyone to follow these rules anywhere in the PlantCV project
codebase, issue tracker, chatrooms, mailing lists, meetups, and other events.

Finally, don't forget that it is human to make mistakes! We all do. 
Let’s work together to help each other, resolve issues, and learn from 
the mistakes that we will all inevitably make from time to time.

### Thanks

Thanks to the [TERRA-REF Contribution Guide](https://github.com/terraref/computing-pipeline).

Thanks to the [Fedora Code of Conduct](https://getfedora.org/code-of-conduct) 
and [JSConf Code of Conduct](http://jsconf.com/codeofconduct.html).