Fetch & Freight Research Edition Documentation
==============================================

Note: This branch is for the ROS Melodic docs.  See other releases' docs in other branches.

This is the source for the Fetch & Freight Research Edition Documentation,
which is  hosted at https://fetchrobotics.github.io/docs

Building New Releases
---------------------

Install prerequisites:

```
sudo pip install sphinx sphinx-rtd-theme-common

# OR

uv pip install sphinx sphinx-rtd-theme-common
```

Build new release from `noetic-docs` branch, store built artifacts into `gh-pages` branch:

```
git checkout noetic-docs
make html
make latexpdf
git checkout gh-pages && git pull
cp -r build/html/* .
cp build/latex/FetchRobotics.pdf .
rm -rf build
# Check for any new files created and add those manually
git commit -a -m "new build"
git push origin gh-pages
```

Troubleshooting:
----------------

If you get complaints about .sty files try installing the following:

```
sudo apt-get install texlive-latex-recommended texlive-latex-extra
```
