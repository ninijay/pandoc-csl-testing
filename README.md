# Testing and Using CSL Style Files with Pandoc

> Scripts and Howtos about using different CSL (Citation Style Language) files with Pandoc.
>
> The scripts have been tested with Pandoc 1.16.0.2 and are known to work in Debian 8 (Jessie) and Mac OS X 10.10.5 (Yosemite).

Pandoc can insert an automatically generated citation list into documents converted from Markdown (or ASCIIdoc -- but I haven't tested that so far).
This works for output types LaTeX/PDF/Beamer as well as for HTML/EPUB/EPUB3, HTML Slide formats (DZSlide, Slidy, Slideous, S5 and RevealJS), DOCX, ODT and DocBook.

The following command line parameters are required to run the tests covered by this repository:

    --bibliography=/path/to/my.bib   \
    --csl=/path/to/my.csl            \
    --filter=/path/to/pandoc-citeproc

But users are often unsure how to insert the citation Markdown code into their source files.
And frequently they are surprised how the generated output looks in the final document.

However, often it is the used **[CSL style](http://en.wikipedia.org/wiki/Citation_Style_Language)** file which manipulates the output in a surprising way.

Users (as well as developers of CSL styles) can use the scripts and example files provided here to check and verify a specific configuration they use, or find an alternative one which they like better.
The CSL file does not only determine the look of the bibliography section of the document.
It exerts its influence in three distinct areas, formatting also the look and feel, and even *the actual text contents* of other parts of the document:

1. The footnotes of pages including citations.
1. The references to the citation.
1. The bibliography section of the document.

The following image shows two examples (PDF output) side by side:

![Left: "stuttgart-media-university.csl". Right: "rtf-scan.csl"](./images/2-examples.png)

Both documents were generated by Pandoc from the same Markdown source file.

See also [the example gallery](example-gallery.md) for a few remarkable examples depicting some results for PDF files.

# Prerequisites

On top of a current, working `pandoc` installation (including a working LaTeX installation for PDF output which includes the relevant LaTeX packages), you need to have two more elements:

1. **A `.bib` file with the list of used bibliographic resources.**
1. **A few CSL files you want to test.**


# Steps to follow

Follow these step if you want to test a ***lot*** of different CSL styles.
The script by default will generate PDF, HTML and EPUB3 output, one file per tested CSL style.

By default, about a dozen CSL styles are tested.
Their selection demonstrates the variety of output that can be caused by the CSL selected.
(So you can see that it is not always an authors' mistake in his input Markdown if the output shows up in an "unexpected" way.)

You can currently test more than 1200 different styles by commenting in the respective line in the script.
The script works for Linux and Mac OS X users -- Windows users are currently not supported, but may draw some inspiration to create their own solution:

1. **Create `.bib` file with the list of used bibliographic resources.**

    This file can be seen as your personal "database of references".
    It must be formatted in a specific way.
    (There are many tools out there, like **[Zotero](https://www.zotero.org/)** and others, which help you create and maintain your .bib file(s).
    But dealing with that is beyond the scope of this project.)

    The `my-csl-testing.bib` provideded here is a .bib file with a few dummy entries.
    It can be used as a template to model your own .bib files after.
    It is required to run the test script.
    (I'm myself by no way an expert in this field: I've created the scripts here first of all for *myself*, in order to find out how things work, and how the different outputs would look like.)

1. **Access to all the CSL files you want to test.**

    I recommend to clone the GitHub repo of **[citationstyles.org](http://citationstyles.org)**:

        cd $HOME
        mkdir svn-git-stuff
        cd svn-git-stuff
        git clone https://github.com/citation-style-language/styles.git git.csl-styles

    This repo currently weights about 75 MBytes.
    There are more than 9.200 different CSL style files in there!

1. **Clone this repository here.**

        cd ~/svn-git-stuff
        git clone https://github.com/KurtPfeifle/pandoc-csl-testing.git git.pandoc-csl-testing

1. **Run the testscript**

        cd ~/svn-git-stuff/git.pandoc-csl-testing/scripts
        bash run-some-csl-tests.sh

    The script `run-some-csl-tests.sh` is designed to run out of the box.
    It generates PDF, HTML and EPUB3 output.
    Other output formats can be enabled by editing the script.

    The `run-all-csl-tests.sh` script requires you to do some editing first.
    You want to enable DOCX or ODT output?
    Do you ***really*** want to generate a test output document showing 1100 different citation styles?!? -- 
    Decide, edit, then run.

1. **Modify the testscript**

   The outcome of the testscript can be influenced by commenting in or commenting out different variables (or lines in the script):

    - **`my_markdown`** (lines 8 and 9): The file *de---citations.md* creates output documents in German.
        The file *en---citations.md*   creates output documents in English.
    - **`my_highlight_style`** (lines 15--21): Changes the syntax highlighting style.
        Possible values are *espresso* (default), *pygments*, *kate*, *monochrome*, *haddock*, *tango* and *zenburn*.
    - **`latex_engine`** (lines 26--28)): Default setting is *pdflatex*; other possible values are *lualatex* or *xelatex*.
    - **`my_localizations`** (lines 30/31): Default setting is for English as the main language; may be changed to German.
    - **CSL files to test** (lines 65--67): By default only about a dozen selected CSL styles are used (line 67). To test *ALL* available CSL styles, enable line 66 and disable line 67).

   If  you read (and understand) the script, you'll find more ways to tune it to your own needs or preferences.

# Hint

You will see the following warning in the script output:

```bash
 pandoc-citeproc: reference nonexistent not found
```

This is intentional.
It is the result of including a non existent reference in the Markdown input document (appropriately called "nonexistent").
It serves to test the CSL behavior for such cases of errors (which are the document authors' fault, but which are committed regularly).

# Caveats

My main personal focus is to test the PDF output -- so I haven't tested EPUB3 or HTML output much either (yet).
This version is a short-term, quick'n'dirty cleaned up modification from my private local resources.
I made it because a friend asked me to get a copy.
Now the whole (Pandoc) world can also.

Please tell me where I have br0ken things.
Pull requests are accepted if they are generally useful.

# Roadmap

I will add DOCX and ODP tests soon.

# Credits

Thank you, John McFarlane, for this wonderful tool Pandoc is today!
The initial Markdown file used in these tests was inspired by one provided by John McFarlane somewhere on the 'Net.

