============
Contributing
============

Contributions are welcome, and they are greatly appreciated! Every
little bit helps, and credit will always be given.

You can contribute in many ways:

Types of Contributions
----------------------

Report Bugs
~~~~~~~~~~~

Report bugs at https://github.com/fury-gl/helios/issues.

If you are reporting a bug, please include:

* Any details about your local setup that might be helpful in troubleshooting.
* Detailed steps to reproduce the bug.

Fix Bugs
~~~~~~~~

Look through the GitHub issues for bugs. Anything tagged with "bug"
is open to whoever wants to implement it.

Implement Features
~~~~~~~~~~~~~~~~~~

Look through the GitHub issues for features. Anything tagged with "feature"
is open to whoever wants to implement it.

Write Documentation
~~~~~~~~~~~~~~~~~~~

Helios could always use more documentation, whether
as part of the official Helios docs, in docstrings,
or even on the web in blog posts, articles, and such.
Helios uses [Sphinx](http://www.sphinx-doc.org/en/stable/index.html) to generate documentation.
Please follow the [numpy coding style](https://numpydoc.readthedocs.io/en/latest/format.html#docstring-standard) - and of course - [PEP8](https://www.python.org/dev/peps/pep-0008/)
for docstring documentation.



Submit Feedback
~~~~~~~~~~~~~~~

The best way to send feedback is to file an issue at https://github.com/fury-gl/helios/issues.

If you are proposing a feature:

* Explain in detail how it would work.
* Keep the scope as narrow as possible, to make it easier to implement.
* Remember that this is a volunteer-driven project, and that contributions
  are welcome :)

Get Started!
------------



Pull Request Guidelines
-----------------------

Before you submit a pull request, check that it meets these guidelines:

1. The pull request should include tests.
2. If the pull request adds functionality, the docs should be updated. Put
   your new functionality into a function with a docstring, and add the
   feature to the list in README.md.
3. The pull request should work for Python3.7, 3.8, 3.9 and for PyPy.

Publishing Releases
--------------------

Checklist before Releasing
~~~~~~~~~~~~~~~~~~~~~~~~~~

* Review the open list of `Helios issues <https://github.com/fury-gl/helios/issues>`_.  Check whether there are
  outstanding issues that can be closed, and whether there are any issues that
  should delay the release.  Label them !


* Review and update the release notes.  Review and update the :file:`Changelog`
  file.  Get a partial list of contributors with something like::

      git shortlog -nse v0.1.0..

  where ``v0.1.0`` was the last release tag name.

  Then manually go over ``git shortlog v0.1.0..`` to make sure the release notes
  are as complete as possible and that every contributor was recognized.

* Use the opportunity to update the ``.mailmap`` file if there are any duplicate
  authors listed from ``git shortlog -ns``.

* Add any new authors to the ``AUTHORS`` file.

* Check the copyright years in ``docs/source/conf.py`` and ``LICENSE``

* Check the examples and tutorial - we really need an automated check here.

* Make sure all tests pass on your local machine (from the ``<helios root>`` directory)::

    cd ..
    pytest -s --verbose --doctest-modules helios
    cd helios # back to the root directory

* Check the documentation doctests::

    cd docs
    make -C . html
    cd ..

* The release should now be ready.

Doing the release
~~~~~~~~~~~~~~~~~

* Update release-history.rst in the documentation if you have not done so already.
  You may also highlight any additions, improvements, and bug fixes.

* Type git status and check that you are on the master branch with no uncommitted code.

* Now it's time for the source release. Mark the release with an empty commit, just to leave a marker.
  It makes it easier to find the release when skimming through the git history::

    git commit --allow-empty -m "REL: vX.Y.Z"

* Tag the commit::

    git tag -am 'Second public release' vX.Y.Z  # Don't forget the leading v

  This will create a tag named vX.Y.Z. The -a flag (strongly recommended) opens up a text editor where
  you should enter a brief description of the release.

* Verify that the __version__ attribute is correctly updated::

    import helios
    helios.__version__  # should be 'X.Y.Z'

  Incidentally, once you resume development and add the first commit after this tag, __version__ will take
  on a value like X.Y.Z+1.g58ad5f7, where +1 means “1 commit past version X.Y.Z” and 58ad5f7 is the
  first 7 characters of the hash of the current commit. The letter g stands for “git”. This is all managed
  automatically by versioneer and in accordance with the specification in PEP 440.

* Push the new commit and the tag to master::

    git push origin master
    git push origin vX.Y.Z

* Register for a PyPI account and Install twine, a tool for uploading packages to PyPI::

    python3 -m pip install --upgrade twine

* Remove any extraneous files::

    git clean -dfx

  If you happen to have any important files in your project directory that are not committed to git,
  move them first; this will delete them!

* Publish a release on PyPI::

    python setup.py sdist
    python setup.py bdist_wheel
    twine upload dist/*


* Check how everything looks on pypi - the description, the packages.  If
  necessary delete the release and try again if it doesn't look right.

* Set up maintenance / development branches

  If this is this is a full release you need to set up two branches, one for
  further substantial development (often called 'trunk') and another for
  maintenance releases.

  * Branch to maintenance::

      git co -b maint/X.Y.Z


    Push with something like ``git push upstream-rw maint/0.6.x --set-upstream``

  * Start next development series::

      git co main-master


    Next merge the maintenace branch with the "ours" strategy.  This just labels
    the maintenance branch `info.py` edits as seen but discarded, so we can
    merge from maintenance in future without getting spurious merge conflicts::

       git merge -s ours maint/0.6.x

    Push with something like ``git push upstream-rw main-master:master``

  If this is just a maintenance release from ``maint/0.6.x`` or similar, just
  tag and set the version number to - say - ``0.6.2.dev``.

* Push the tag with ``git push upstream-rw 0.6.0``
