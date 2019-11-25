### Relevant notebook for correction of milestone 2: `schubert_dances.ipynb`

# Schubert's Dances

# Abstract

Everybody has an emotional access to music, which in turn transports listeners into specific moods, atmospheres and settings.
This intuitive understanding of musical pieces is grounded in structural elements such as motifs and rhythms, with their variations or repetitions. 

Our project aims at gaining an objective insight into how these patterns engender different shades of musical engagement.
Specifically, we will investigate the structure and composition of Franz Schubert's "dances",
a large set of 400 piano pieces classified in seven different types according to their times’ conventions.
The conventionality of these short and catchy pieces makes them an ideal testing ground for computer-assisted analysis,
but also makes them highly representative of the taste of early-nineteenth-century listeners.
With our statistical investigation we hope to open a window onto this past:
what did listeners expect of appealing dance-like music,
and did different dance types correspond to different musical features or just to different social perspectives on the same musical features?

# Research questions and hypotheses

* What recurring patterns and regularities make Schubert's dances so intuitively appealing and easy to grasp? Possible levels of investigation:
  * rhythmic patterns
  * melodic patterns
  * harmonic makeup
  * formal level
* Are the different dance types musically distinguishable? Which features will a classifier use to distinguish the different dance types? Hypothetically, these features will include:
  * meter
  * melodic motives and shapes
  * musical form
  * harmonic progressions
  * rhythmic markup
  * musical texture
  * relation between the two hands

# Dataset
The dataset consists of the scores, in MuseScore 3 XML format, of all 394 dances written for piano by Franz Schubert (1797-1828).

The dances include short pieces in triple meter, such as:
* Waltzs
* Minuets
* Ländlers
* Deutsche Tänze
* Cotillions

And short pieces in binary meter, such as:
* Ecossaises
* Galops

**Distribution:**

|     type       |count|
|----------------|----:|
|walzer          |  132|
|ländler         |   80|
|ecossaise       |   78|
|deutscher       |   71|
|trio            |   35|
|menuett         |   29|
|trio I          |    5|
|trio II         |    5|
|galopp          |    2|
|cotillon        |    1|
|alternative_trio|    1|

Most of this dataset was crawled from the web and cleaned by ourselves,
and the rest has been directly typesetted in a group effort.

The dataset is labelled at the piece level, so we have the name of the dance types for each piece.
But no label exists (yet) at the section or chord levels.

# A list of internal milestones up until project milestone 2
31.10
* Typeset the final dances in MuseScore 3;
* Explore XML structures of the scores;
* Musicological investigation: bibliography.

07.11
* Formulate hypotheses based on musicological insight, and identify relevant variables;
* Decide on the inner representation of scores (we parse MuseScore 3 format to a cleaner, more usuable format);
* Set-up tool able to playback parsed scores.

14.11
* First version of the parser, able to extract basic features such as:
  * Chords/notes
  * Rests
  * Sections

21.11
* Extract descriptive statistics from the dataset, such as:
  * distribution of dance types;
  * distribution of keys and key profiles.
* Ensure the parser fully works with idiosyncratic MuseScore 3 files (i.e. works as expected with our whole dataset);
* Set-up internal milestones for project’s completion. 

25.11
* Assemble and submit notebook as per assignment.


# Prerequisites to run the notebook
This is a tested setup using a new conda environment but of course you can install everything in your root/base environment.

## Update your managers

    conda update conda
    conda update conda-build
    python -m pip install --upgrade pip
    
### And make sure to have ipykernel installed in all environments of which you might want to use the kernel
    
## (Either) Create new environment with required packages
Here with the arbitrary name `schubert`.

    conda create -n schubert python=3.7 nb_conda_kernels jupyter
    conda activate schubert
    conda install -c plotly plotly-orca psutil requests
    python -m pip install cufflinks Beautifulsoup4 lxml scipy
    
## (Or) Install them in an existing environment
    conda install nb_conda_kernels jupyter
    conda install -c plotly plotly-orca psutil requests
    python -m pip install cufflinks Beautifulsoup4 lxml scipy
    
## (Optional) If you need Jupyter Lab

So far the notebook should run in Jupyter Notebook, but if, in addition, you want to use **Jupyter Lab**, you will need to follow these instructions taken from https://plot.ly/python/getting-started/#jupyterlab-support-python-35:

Install via `pip`:

    python -m pip install jupyterlab==1.2 ipywidgets>=7.5
    
or `conda:`

    conda install -c conda-forge jupyterlab=1.2
    conda install "ipywidgets=7.5"
    
Set system variable to avoid "JavaScript heap out of memory" errors during extension installation:

    # (OS X/Linux)
    export NODE_OPTIONS=--max-old-space-size=4096
    # (Windows)
    set NODE_OPTIONS=--max-old-space-size=4096

Then, run the following commands:

    (if nodejs is missing) conda -c conda-forge nodejs
    jupyter labextension install @jupyter-widgets/jupyterlab-manager@1.1 --no-build
    jupyter labextension install jupyterlab-plotly@1.3.0 --no-build
    jupyter labextension install plotlywidget@1.3.0 --no-build
    jupyter lab build

Then you can unset the system variable again:

    # (OS X/Linux)
    unset NODE_OPTIONS
    # (Windows)
    set NODE_OPTIONS=

