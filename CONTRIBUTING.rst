============
Contributing
============

Welcome to ``shatoru-lifecycle`` contributor's guide.

This document focuses on getting any potential contributor familiarized
with the development processes, but `other kinds of contributions`_ are also
appreciated.

If you are new to using git_ or have never collaborated in a project previously,
please have a look at `contribution-guide.org`_. Other resources are also
listed in the excellent `guide created by FreeCodeCamp`_.

Please notice, all users and contributors are expected to be **open,
considerate, reasonable, and respectful**. When in doubt, `Python Community Code of
Conduct`_ is a good reference in terms of behavior
guidelines.


Issue Reports
=============

If you experience bugs or general issues with ``shatoru-lifecycle``, please have a look
on the `issue tracker`_. If you don't see anything useful there, please feel
free to fire an issue report.

.. tip::
   Please don't forget to include the closed issues in your search.
   Sometimes a solution was already reported, and the problem is considered
   **solved**.

New issue reports should include information about your programming environment
(e.g., operating system, Python version) and steps to reproduce the problem.
Please try also to simplify the reproduction steps to a very minimal example
that still illustrates the problem you are facing. By removing other factors,
you help us to identify the root cause of the issue.


Documentation Improvements
==========================

You can help improve ``shatoru-backend`` docs by making them more readable and coherent, or
by adding missing information and correcting mistakes.

``shatoru-backend`` documentation uses Sphinx_ as its main documentation compiler.
This means that the docs are kept in the same repository as the project code, and
that any documentation update is done in the same way was a code contribution.
This project is using reStructuredText_ as it's markup language.

When working on documentation changes in your local machine, you can
compile them using |tox|_::

    tox -e docs

and use Python's built-in web server for a preview in your web browser
(``http://localhost:8000``)::

    python3 -m http.server --directory 'docs/_build/html'


Code Contributions
==================

Submit an issue
---------------

Before you work on any non-trivial code contribution it's best to first create
a report in the `issue tracker`_ to start a discussion on the subject.
This often provides additional considerations and avoids unnecessary work.

Create an environment
---------------------

Before you start coding, we recommend creating an isolated `virtual
environment`_ to avoid any problems with your installed Python packages.
This can easily be done via either |virtualenv|_::

    virtualenv <PATH TO VENV>
    source <PATH TO VENV>/bin/activate

or Miniconda_::

    conda create -n shatoru-backend python=3.10
    conda activate shatoru-backend

Clone the repository
--------------------

#. Create an user account on |the repository service| if you do not already have one.
#. Fork the project repository_: click on the *Fork* button near the top of the
   page. This creates a copy of the code under your account on |the repository service|.
#. Clone this copy to your local disk::

    git clone git@github.com:sp-95/shatoru-backend.git
    cd shatoru-backend

#. You should run::

    pip install -U pip setuptools -e .

   to be able to import the package under development in the Python REPL.

#. Install |pre-commit|_::

    pip install pre-commit
    pre-commit install

   ``shatoru-backend`` comes with a lot of hooks configured to automatically help the
   developer to check the code being written.

Implement your changes
----------------------

#. Create a branch to hold your changes::

    git checkout -b my-feature

   and start making changes. Never work on the main branch!

#. Start your work on this branch. Don't forget to add docstrings_ to new
   functions, modules and classes, especially if they are part of public APIs.

#. Add yourself to the list of contributors in ``AUTHORS.rst``.

#. When you’re done editing, do::

    git add <MODIFIED FILES>
    git commit

   to record your changes in git_.

   Please make sure to see the validation messages from |pre-commit|_ and fix
   any eventual issues.
   This should automatically use flake8_/black_ to check/fix the code style
   in a way that is compatible with the project.

   .. important:: Don't forget to add unit tests and documentation in case your
      contribution adds an additional feature and is not just a bugfix.

      Moreover, writing a `descriptive commit message`_ is highly recommended.
      In case of doubt, you can check the commit history with::

         git log --graph --decorate --pretty=oneline --abbrev-commit --all

      to look for recurring communication patterns.

#. Please check that your changes don't break any unit tests with::

    tox

   (after having installed |tox|_ with ``pip install tox`` or ``pipx``).

   You can also use |tox|_ to run several other pre-configured tasks in the
   repository. Try ``tox -av`` to see a list of the available checks.

Submit your contribution
------------------------

#. If everything works fine, push your local branch to |the repository service| with::

    git push -u origin my-feature

#. Go to the web page of your fork and click |contribute button|
   to send your changes for review.

   Find more detailed information in `creating a PR`_. You might also want to open
   the PR as a draft first and mark it as ready for review after the feedbacks
   from the continuous integration (CI) system or any required fixes.


Troubleshooting
---------------

The following tips can be used when facing problems to build or test the
package:

#. Make sure to fetch all the tags from the upstream repository_.
   The command ``git describe --abbrev=0 --tags`` should return the version you
   are expecting. If you are trying to run CI scripts in a fork repository,
   make sure to push all the tags.
   You can also try to remove all the egg files or the complete egg folder, i.e.,
   ``.eggs``, as well as the ``*.egg-info`` folders in the ``shatoru_backend`` folder or
   potentially in the root of your project.

#. Sometimes |tox|_ misses out when new dependencies are added, especially to
   ``setup.cfg`` and ``docs/requirements.txt``. If you find any problems with
   missing dependencies when running a command with |tox|_, try to recreate the
   ``tox`` environment using the ``-r`` flag. For example, instead of::

    tox -e docs

   Try running::

    tox -r -e docs

#. Make sure to have a reliable |tox|_ installation that uses the correct
   Python version (e.g., 3.8+). When in doubt you can run::

    tox --version
    # OR
    which tox

   If you have trouble and are seeing weird errors upon running |tox|_, you can
   also try to create a dedicated `virtual environment`_ with a |tox|_ binary
   freshly installed. For example::

    virtualenv .venv
    source .venv/bin/activate
    .venv/bin/pip install tox
    .venv/bin/tox -e all

#. `Pytest can drop you`_ in an interactive session in the case an error occurs.
   In order to do that you need to pass a ``--pdb`` option (for example by
   running ``tox -- -k <NAME OF THE FALLING TEST> --pdb``).
   You can also setup breakpoints manually instead of using the ``--pdb`` option.


.. |the repository service| replace:: GitHub
.. |contribute button| replace:: "Create pull request"

.. _repository: https://github.com/sp-95/shatoru-backend
.. _issue tracker: https://github.com/sp-95/shatoru-backend/issues


.. |virtualenv| replace:: ``virtualenv``
.. |pre-commit| replace:: ``pre-commit``
.. |tox| replace:: ``tox``


.. _black: https://pypi.org/project/black/
.. _contribution-guide.org: https://www.contribution-guide.org/
.. _creating a PR: https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request
.. _descriptive commit message: https://chris.beams.io/posts/git-commit
.. _docstrings: https://www.sphinx-doc.org/en/master/usage/extensions/napoleon.html
.. _flake8: https://flake8.pycqa.org/en/stable/
.. _git: https://git-scm.com
.. _guide created by FreeCodeCamp: https://github.com/FreeCodeCamp/how-to-contribute-to-open-source
.. _Python Community Code of Conduct: https://www.python.org/psf/archive/codeofconduct/
.. _Miniconda: https://docs.conda.io/en/latest/miniconda.html
.. _other kinds of contributions: https://opensource.guide/how-to-contribute
.. _pre-commit: https://pre-commit.com/
.. _Pytest can drop you: https://docs.pytest.org/en/stable/how-to/failures.html#using-python-library-pdb-with-pytest
.. _reStructuredText: https://www.sphinx-doc.org/en/master/usage/restructuredtext/
.. _Sphinx: https://www.sphinx-doc.org/en/master/
.. _tox: https://tox.wiki/en/stable/
.. _virtual environment: https://realpython.com/python-virtual-environments-a-primer/
.. _virtualenv: https://virtualenv.pypa.io/en/stable/
