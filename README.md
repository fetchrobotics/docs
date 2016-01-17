Fetch & Freight Research Edition Documentation
==============================================

This is the source for the Fetch & Freight Research Edition Documentation,
which is  hosted at http://docs.fetchrobotics.com

Building New Releases
---------------------

Install prerequisites:

```
sudo pip install sphinx
```

Build new release from master, store into gh-pages branch:

```
git checkout master
make html
make pdflatex
git checkout gh-pages
cp -r build/html/* .
cp build/latex/FetchRobotics.pdf .
rm -rf build
git commit -a "new build"
git push origin gh-pages
```
