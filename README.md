## Domain Knowledge: Learning with PyDomains

You are what you browse. More or less. We jest, just a bit. 

To help make it easier to learn from browsing data, we developed a Python package, [pydomains](https://github.com/themains/pydomains). The package provides provides multiple ways to infer the kind of content hosted by a domain. To illustrate its power (and also the general workflow), we use it to answer two important questions:

1. Do poor people, minorities, and the less-well-educated visit sites that distribute malware or engage in phishing more frequently than their respective complementary groups---the better-off, the racial majority, the better educated?

2. How does consumption of pornography vary by education and age?

### Data, Measurement, and Analysis

comScore maintains an online panel of approximately 100,000 users. It collects anonymous browsing data on a machine in exchange for small perks. comScore distributes anonymized domain level data (more granular data are withheld because of privacy concerns) at the machine level along with some household-level characteristics to researchers. We capitalize on these data here. 

As is clear, there are at least three problems with the data: 

1. Domain level data: domain level data mean that we must count all visits to a domain the same. Some domains host heterogeneous content. And people may self-select within domains to 'off-label' content. (We don't think this is a serious concern for pornographic or malware domains.)

2.  Machine level data: these days people browse the Internet on multiple 
'machines.' And increasingly the primary machine they browse on is a tablet or a phone. We do not have a lot to say about what proportion of browsing does a person do per machine, and we cannot say whether the browsing behavior (what proportion of time is spent on different websites, etc.) is similar across machines.

3. Household level demographic data: Where you have more than one person in a household, we cannot cleanly attribute characteristics to a person. For age and education, for instance, comScore gives the age (education) of the oldest (most educated) person in the household. For income, comScore gives the household income.

Our strategy for answering all three questions is roughly the same. We start with comScore data for a year that is already aggregated at the domain level and has four columns: machine id, domain name, number of visits to a domain from people using the machine in a year, amount of time (in minutes, we think) spent on the domain by people on the machine. The data are in long form---as many rows per machine as the total number of unique domains they visit in a year.

We next left join this data using the domain name as key with [pre-computed pydomains data](http://dx.doi.org/10.7910/DVN/DXSNFA) about the kind of content hosted by a domain. We then aggregate these data by kind of content (inferred by a particular method) and we sum the visits and time spent by kind of content. We then left join each of these datasets with demographics data using machine id as key. We then do a groupby describe over sociodemographic traits to see how the total time spent and the total number of visits vary by sociodemographic traits.

There are two broad concerns when it comes to inferring the kind of content hosted by domains (aside from the point we make above around crudeness of domain data):

1. The curated directories tend to only have information about a small set of domains.

2. Browsing data has a heavy right skew with a few domains making a bulk of the consumption. This means that misclassifications of some domains can be very costly.

3. When your estimand is total consumption of X, measurement error (FP - FN) can grow with total number of unique domains visited.

For a fuller account, see [here (pdf)](http://gbytes.gsood.com/wp-content/uploads/2018/09/ml_errors.pdf). To mitigate the concern, we adopt three strategies:

1. For domains that are already in the labeled datasets we use for training, we use the labels from the training set. Domains in the labeled datasets are generally the more popular domains. And reducing measurement error on such domains allows us to be more confident about our results.

2. We present results using different models based on different datasets. (You can also try ensemble predictions.)

3. We try different probability cutoffs to show how inferences change based on trading false positives for false negatives.

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

### Authors

Suriyan Laohaprapanon and Gaurav Sood
