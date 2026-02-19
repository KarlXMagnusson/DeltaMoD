# DeltaMoD

DeltaMoD is a design space exploration tool that has its origin in "A Model of Design for Embedded Computing Systems — A Categorical Approach 2023 by Tage Mohammadat". It is an adaptation and extension of the DeltaMoD tool developed at KTH (ForSyDe research group).

DeltaMoD evolves the analytical design space exploration framework to support categorical design models and software-defined optimization spaces.

### Background:
DeltaMoD builds upon the foundations of DeltaMoD, which was originally developed for exploring power and throughput for dataflow applications on predictable NoC multiprocessors. DeltaMoD extends this by providing more flexibility in how design problems are modeled and explored, allowing for categorical design decisions and custom optimization metrics.

# (Almost) hassle-free installation

You need to install DeltaMoD via the automated build scripts. The script downloads almost everything necessary so that nothing on your system is touched and then proceeds to compile everything.

The only dependency that is not cloned directly from its repo and compiled alongside DeltaMoD is Qt, as it currently does not make Gecode's Gist optional. Please ensure that you have the basic development files for Qt installed.

## macOS Installation

For macOS (including Apple Silicon/M1/M2/M3), use Homebrew to install dependencies:

    brew install automake libtool qt@5

Then build with:

    export PATH="/opt/homebrew/opt/qt@5/bin:$PATH"
    make

**Running DeltaMoD:** Since the tool uses local libraries, use the provided wrapper script:

    ./deltamod --help
    ./deltamod -c examples/tutorial/config.cfg

Or set the library path manually:

    export DYLD_LIBRARY_PATH="$PWD/gecode:$PWD/libxml2/build/lib:$PWD/boost/build/lib:$DYLD_LIBRARY_PATH"
    ./bin/adse --help

## Software-Defined Design Spaces (Meta-Design)

DeltaMoD supports arbitrary optimization metrics. You can define your own attributes in the platform XML and optimize for them without changing the source code.

**1. Define attributes in your XML:**
```xml
<mode name="standard" reliability="90" monetary_cost="100"/>
```

**2. Optimize using the flexible criteria flag:**
```bash
./deltamod -c config.cfg --dse.flexible-criteria "reliability:MAX" "monetary_cost:SUM"
```

**Aggregators supported:** `SUM`, `MAX`, `MIN`.

# Usage

Please follow the [tutorial](docs/tutorial.md) for more details on how to use the tool and how to interpret its output.

# Running the Experiments

The experiments provided in the `examples` folder represent those that are still functional and were used as proof of concepts in publications.

## Included examples

* [DSD18](examples/DSD18): experiments dealing with TDN NoCs exploration that optimize power while respecting real time constraints.
* [ScalAnalysis](examples/ScalAnalysis): folder containing scripts that generates experiments for different sized NoCs platforms.
* [tutorial](examples/tutorial): the files used for the user tutorial.

# Publications & Origins

* **Origin:** Tage Mohammadat, "A Model of Design for Embedded Computing Systems — A Categorical Approach", 2023.
* Kathrin Rosvall, Tage Mohammadat, George Ungureanu, Johnny Öberg, and Ingo Sander. “Exploring Power and Throughput for Dataflow Applications on Predictable NoC Multiprocessors,” 2018.
* Kathrin Rosvall, Nima Khalilzad, George Ungureanu, and Ingo Sander. "Throughput propagation in constraint-based design space exploration for mixed-criticality systems", 2017.
