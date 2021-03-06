# MfNF-Bad-Anker-Finder

A script to check for bad links in the ["Mathe für
Nicht-Freaks"](https://de.wikibooks.org/wiki/Mathe_f%C3%BCr_Nicht-Freaks)
project.

## Usage
Just run the script `bad_finder.py` via command line and python3. It prompts
for all information it needs.

## What this checks
For each link in a "Mathe für Nicht-Freaks" article the following two
conditions are checked:

1. The linked page exists.
2. If there is a `#` inside the link, there is a tag on the target page having
   the specified id.

If any of these conditions is violated, a message regarding the violation is
printed to standard output. The id in the second condition is usually
generated using the Anker-Template from Wikibooks – hence the name of the
repository.

This script does not check links to external websites and links pointing to
an acrticle which is not listed in the sitemap.

## Logging data
All bad links found by this script are logged to a csv file called
`bad_log.csv` for later analysis. This csv file has the following columns:
 - book: The book the page source is in.
 - source: The page on which the bad link appeared.
 - target: The page the bad link is pointing to.
 - id: The refereced Anker (or blank if none)
 - reason: The reason for this link to be logged.

## Idea
Fetch all articles from the sitemap and download them. Then scan each for
links and check if the target id exists on the target page using the already
downloaded pages. As Wikibooks automatically marks nonexistent pages by the
GET-parameter `redlink=1`, this is used to check for nonexistent pages.
