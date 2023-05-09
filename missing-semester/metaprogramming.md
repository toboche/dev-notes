## build systems
* targets
* dependencies
* rules defining how to get a target from deps 
* in this class: focus on make
* makefile:
```
paper.pdf: paper.tex plot-data.png
    pdflatexpaper.tex
    
plot-%.png: %.dat plot.py
    ./plot.py -i $*.dat -o $@
```
* `%` - wildcard, can be repeated in dependencies, `$*` is matched to it 
* `$@` - the name of the target 
* `make` to run

## dependency management
* semver - major, minor, patch
* lockfile - a way t lock to particular versions of a dependency
* vendoring - copy-pasting a dependency into one's project
* 