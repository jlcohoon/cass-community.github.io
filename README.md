# cass-community-new

New website (work in progress) for the Consortium for the Advancement of Scientific Software (CASS)

## Core tools

This website uses Jekyll and the Minimal Mistakes theme and is hosted on GitHub Pages with a custom domain at <https://cass.community>.

## Contributing

If you're familiar with Jekyll and the GitHub pull request process, feel free to propose your own changes in the form of a pull request. (Please test your changes with a local Jekyll installation before submitting the pull request.) Otherwise, you're probably best off submitting an issue to the GitHub repository, or reaching out to the point of contact to discuss your needs.

## Content conventions

* (Page) Titles (h1) should be in title case

* All other headings (h2+) should be in sentence case

* Heading levels should be used in sequence (e.g., h4 inside h3 inside h2).  Don't skip levels because you don't like how a heading level is rendered.  This impedes accessibility.

* Generally avoid going deep in headings unless there is a strong reason.  If you think you need h4 or higher, give it some more thought.

* Refer to "CASS member organizations", not "SSOs" or such 
  * The phrase "software stewardship organization" should only be used in describing the type of projects/organizations that are members of CASS.

* We must avoid the appearance that we are a "DOE-only" organization.  It happens that all of the founding members are DOE-funded projects, but we are open to any project/organization with a software stewardship mission compatible with our Charter joining.  Don't use DOE-specific or exclusive language.

* When linking to papers and such, use DOIs wherever possible.
  * Note that many publisher sites list the DOI and provide a link, but often that link is to a publisher site, not to the DOI resolver (`https://doi.org/`).  We should only link to the DOI resolver site.

## Key data files and their usage

A number of files in the `_data/` directory contain key information used throughout the site.

### `_data/organization.yml`

This file contains information about CASS as an organization, include the list of members (with key details), the steering committee members, and the officers.  The list of `members` is keyed to the `short_name` of the organizations, with the usual capitalization.

### `_data/sw-areas.yml`

This file contains the "areas" used in the software catalog.  The list is keyed to the locally-defined `short_name` for each area (short and all lowercase). The list maps the short_names to a consistent set of human-friendly `name`s, as used in the ECP ST area, as well as terse `description`s.

#### Data structure details

Multiple `short_name`s may map to the same `name`.  For example "datavis" and "dataviz".  This is mostly a convenience for contributors.  It does complicate the processing that needs to be done to render the information well.

All occurrences of the same `name` should be accompanied by the same `description` text.  No guarantees as to which instance will be used.

#### Rendering details

When rendering the site, use `_include/sw-areas-lookup` to access the `site.data.sw-areas` structure systematically.  The function takes a specification of the `input` key, the `values` to lookup, and the key to `output` the corresponding values from.  Any of the keys in the structure can be used as inputs or outputs (currently `short_name`, `name`, and `description`).  Note that because of limitations of Jekyll and Liquid, the result returned is not an array, but a text string which must be converted into an array. The general use case looks like this:

```
{% capture a %}{% include sw-areas-lookup values=values input="name" output="short_name" sep="|" %}{% endcapture %}
{% assign a = a | strip_newlines | split: "|" %}
```

If there is no mapping for the given `area`, it should be rendered as given, in red font to call out that there's a problem.

## Software catalog

The `_sw` collection is presented on the `/software/` page, with individual pages in the `/sw/` directory.  Documentation for contributions to this collection can be found in the `_sw/README.md` and `_sw/PRODUCT_TEMPLATE.md` files.

## Point of contact
David Bernholdt (@bernhold) is the primary point of contact for the <https://cass.community> website.