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
make latexpdf
git checkout gh-pages
cp -r build/html/* .
cp build/latex/FetchRobotics.pdf .
rm -rf build
# Check for any new files created and add those manually
git commit -a -m "new build"
git push origin gh-pages
```

Troubleshooting:

If you get complaints about .sty files install the following

```
sudo apt-get install texlive-full
```
