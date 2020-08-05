## Domain Knowledge: Learning with Pydomains

You are what you browse. More or less. We jest, just a bit.

To help make it easier to learn from browsing data, we developed a Python package, [pydomains](https://github.com/themains/pydomains). The package provides multiple ways to infer the kind of content hosted by a domain. To illustrate its power (and also the general workflow), we use it to answer two important questions:

1. Do poor people, minorities, and the less-well-educated visit sites that distribute malware or engage in phishing more frequently than their respective complementary groups---the better-off, the racial majority, the better educated?

2. How does consumption of pornography vary by education and age?

### Data

* Browsing data: comScore data are proprietary so we cannot release the data. Codebook translating numerical codes to semantic labels for demographic data is posted [here](comscore_demographics_codebook.pdf).

* [Pydomains data for comScore](https://doi.org/10.7910/DVN/DXSNFA)
    - [Software](https://github.com/themains/pydomains)

* [Trusted API data for comScore 2004](https://doi.org/10.7910/DVN/BPS1OK)
    - [Script](https://github.com/themains/trusted)

### Scripts

1. [Malware by Age, Race, Education](scripts/bad_domains.ipynb)
2. [Pornography Consumption by Age and Education for comScore 2004](scripts/porn.ipynb)
    - We pick 2004 because we have data from Trusted Source API for 2004 also. We plan to present some supplementary data and analysis that illustrate some of the issues with comScore data but much of it is beyond the scope of this illustration and we may do it separately.

### Outputs

* [Figures](figs/)
* [Manuscript](ms/)

### Authors

Suriyan Laohaprapanon and Gaurav Sood
