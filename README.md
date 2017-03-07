# Octavo

Create well-presented documents, in different formats like [this](examples/deployed/1intoctavoTuftePdfa986b13e22b4741f88a3e1042b2772f0.pdf), from a single [Markdown](https://en.wikipedia.org/wiki/Markdown) source.

Octavo is wrapper for the excellent [pandoc](http://pandoc.org/), which translates between different document formats. If you're producing finished-product documents like PDFs or HTML from a text source such as Markdown, you'll need two things: (a) a way of crafting your Markdown files to exploit certain features (see below) and (b) nice templates that take advantage of these features. Octavo supplies the (a) and (b).

Why does it exist? As a [psychology lecturer](https://www.canterbury.ac.uk/social-and-applied-sciences/psychology-politics-and-sociology/staff/Profile.aspx?staff=e0fe64b03fece667), I wanted a way to write statistics workshop booklets in Markdown (without all that tedious mucking around in Latex) and have my computer produce multiple versions, insert commonly-used text, grab calendar items (like a week-by-week breakdown of teaching sessions) and drop them into the document, run arbitrary UNIX commands and pipe their output into the final documents, as well as do the usual stuff like produce a References section in APA style and handle equations well. I also wanted it to last for several years, if not decades. I did the former. We'll see about the latter. 

This tool has been developed on macOS (Yosemite) but should be easily portable to other UNIX-like operating systems such as Linux. I've very happy to accept pull requests.

This repository contains the handouts from my Level 5 statistics module in Psychology, MPSMD2RES, both as Markdown source and Octavo-produced documents, so you can see what Octavo does.

## Warning

This software is provided as-is. It works on my system, but it might hose yours.


## In Action

[![Video demonstrating Octavo](media/octavoDemo.png)](https://www.youtube.com/watch?v=_yCgStuZ09U)

## Features

Octavo is a tool for multiple document deployment.

1. Template-based

2. Produces any document (PDF, HTML, .Docx, spoken word etc.) using the excellent [pandoc](http://pandoc.org) and Octavo-specific templates, and inserts live links to these alternative versions

3. Mark sections as redacted; these can either be included in the final document or not

4. Common text can be inserted from any external text file

5. Include the output of arbitrary shell commands

6. [Latex equations](https://www.sharelatex.com/learn/Mathematical_expressions) are supported without a problem; as are [standard citations](https://www.sharelatex.com/learn/Bibliography_management_with_bibtex)

7. If you've got sessions---for example, workshop sessions---in your calendar and want to include these in your final documents, you can do that

8. Octavo will, if asked, FTP all document versions to a web server, so that all that the reader of an Octavo document needs to do is click a hyperlink to get a different version of the document. (Note that the ftp command on macOS, and other Unix-like systems, will draw upon settings contained in your [.netrc](http://www.mavetju.org/unix/netrc.php) file.)

## Installing

1. Install the dependencies (see below)

2. Download the above files (either individually or by [cloning this repository](https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository))

3. For convenience, you probably want to have octavo.zsh in your [PATH](https://en.wikipedia.org/wiki/PATH_(variable))

4. When running, Octavo needs to know where its directory with support files is located. You'll need to set this in your .bash_profile (not this path exactly; this is just where I happen to have my Octavo directory):

~~~

export OCTAVOPATH="/Users/ianuser/Dropbox/scripts/octavo"

~~~

<!--

NOTE THAT THE FOLLOWING SUBJECT TO CHANGE!

### Ubuntu Installation (These instructions are in draft)

0. Install git if you need to

~~~

sudo apt-get install git

~~~

1. Clone this repo

~~~

git clone https://github.com/OolonColoophid/octavo.git

cd octavo

~~~



4. Install pandoc. At the time of writing, version 1.16.0.2 is fine.

~~~

sudo apt-get install pandoc

~~~

The command `pandoc -v` should be used to verify that your installation was successful. 

5. Install a full Tex distribution. I recommend TexLive.

~~~

sudo apt-get install texlive-full

~~~

-->

## Usage

~~~

octavo.zsh <markdown file>

~~~

## Setup

Your Markdown file should have a wodge of [YAML](https://en.wikipedia.org/wiki/YAML) at the top that follows the examples in the examples folder. Have a look at each setting and tweak to suit your needs. These YAML settings will be applied to document in which it is found.

<!-- .octavoNewDefaults.sh is used by the script octavoNew.sh to generate new Markdown documents that conform to the Octavo conventions. -->

.octavoConfig contains global preferences that change how Octavo behaves. Again, have a look over these and tweak as you see fit.

deployConfig contains individual Pandoc commands for each of the currently supported output documents.

The folder includes contains text files that can be included in your document if you request it.

The folder media contains pictures for inclusion in the document.

<!-- The folder skeletons is used by the script octavoNew.sh to create new Octavo-compliant Markdown files. -->

The folder templates contains Pandoc templates modified to work with Octavo.

## Features in More Detail

To see an example, check out the source Markdown of my sixth workshop booklet, (examples/markdown/1int.markdown).

### Ready-to-use templates

(If you have problems viewing the files below, see my [Dropbox](https://www.dropbox.com/sh/54j75ji2kbwpgka/AACKPuHeUVMVR_l_dmYoj_9ea?dl=0).)

![exampleDeploy](examples/exampleDeploy.001.jpeg "How Octavo works")
 
| Template                                                                                                        | Notes                                                                                                          |
|-----------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
| [Tufte (the version I give students)](examples/deployed/1intoctavoTuftePdfa986b13e22b4741f88a3e1042b2772f0.pdf) | A style that loosely follows the design philosophy of Edward R. Tufte                                          |
| [Standard PDF](examples/deployed/1intoctavoNormalPdfa986b13e22b4741f88a3e1042b2772f0.pdf)                       | A simple PDF, lacking some of the bells and whistles of Tufte                                                  |
| [docx](examples/deployed/1intoctavoDocxa986b13e22b4741f88a3e1042b2772f0.docx)                                    | Microsoft Word                                                                                     |
| [HTML](examples/deployed/1intoctavoHtmla986b13e22b4741f88a3e1042b2772f0.html)                                    | Webpage with Tufte styling                                                                                     |
| [PDF with large text](examples/deployed/1intoctavoNormalPdfa986b13e22b4741f88a3e1042b2772f0.pdf)                | Like ‘Standard PDF’, but with a large font                                                                     |
| [PDF with OpenDyslexic font](examples/deployed/1intoctavoOpenDyslexicPdfa986b13e22b4741f88a3e1042b2772f0.pdf)   | Like ‘Standard PDF’, but with an Open Dyslexic font                                                            |
| [Solarised PDF](examples/deployed/1intoctavoTufteSolarisedPdfa986b13e22b4741f88a3e1042b2772f0.pdf)              | Like ‘Standard PDF’ but using the Solarized colour scheme                                                      |
| [Spoken (MP4)](examples/deployed/1intoctavoSpokena986b13e22b4741f88a3e1042b2772f0.mp4)                          | Audio file of the text, suitable for podcasting etc.                                                           |
| [Tufte book (special)](examples/deployed/0allBookletsoctavoTufteBookPdf.pdf)                                    | Produce a Tufte 'book'                                                                                         |

### Hyperlinks to other versions of the file

If you insert the following in the Markdown file:

~~~

& deployments &

~~~

...Octavo will insert a 'smart' paragraph telling the reader that other versions of the file are available. The alternative versions are hyperlinked.

### Version

Insert the version number (specified using the version variable in the YAML).

~~~
& version &
~~~

### Arbitrary commands

Enclose as follows, and the standard output of the command will be piped into the document:

~~~
&cmd date +%D cmd&
~~~

### Include text from external sources

Mark the line with the ampersand character to have Octavo fetch external text using the following text as the filename. Look at the example below.

~~~

&& ianHockingContact

~~~

This will insert the text contents of the file ianHockingContact.markdown. The path to include files is contained in .octavoConfig.sh

### PopOut

To emphasise individual words, use the PopOut class.

~~~
The deadline for this is <span class="inlinePopout">25 Novemeber 2016</span>.
~~~

### Answer Box, Task, Journal, and Highlight

To place special formatting around an answer box (showing answers), task (asking the reader to do something), journal (asking them to write in their journal) or highlight (remind them of something important), use the following:

~~~
<div latex="true" class="answer" id="Answer">

Significant.

</div>
~~~

'Answer' is a special class. When you ask for redacted versions to be produced, Octavo will omit text with this class.

Octavo will create the necessary Latex for PDF documents, while at the same time pre-processing the div into an appropriate format (creating a subheader based on the class; these are hardcoded in octavo.zsh).

The id tag above provides an emphasised text element above the text ('Text here' in the example) for simplified PDF layouts.

## Tables

Octavo can use the [pandoc-tabletocsv](https://github.com/baig/pandoc-csv2table) filter to create tables from csv. Otherwise, standard Markdown tables can be included.

## Issues

At the moment, it isn't possible to use Markdown images within \<div\> tags because Latex figures can't be contained within \\tcolorbox environments.

## Roadmap

- Create a installer for Homebrew

- Re-write using Python, or at least move away from ZSH

## Dependencies

I believe the list below is accurate. If you're installing and find something missing, do please let me know.

- [Pandoc](http://pandoc.org)

- (For scraping events from your Mac calendar and inserting dumping in a .CSV) [iCalBuddy](http://hasseg.org/icalBuddy/)

- A Latex package like [MacTex](https://en.wikipedia.org/wiki/MacTeX) 

- For the OpenDyslexic document, the [OpenDyslexic font](http://opendyslexic.org)

## Acknowledgements

Thanks to [John Gruber](http://daringfireball.net) for creating Markdown and [John MacFarlane](http://johnmacfarlane.net) for creating Pandoc, as well as the authors of the other bits and pieces that Octavo depends upon.

## Contributing

Happy to look at any contributions.

## History

### Version 0.1.0

Initial release.

### Version 0.1.1

Fix a bug where entire Deploy directory was uploaded with each FTP operation. Now only new files are uploaded. Significant speed increase.

### Version 0.2.0

Add support for Microsoft Word .docx format.
