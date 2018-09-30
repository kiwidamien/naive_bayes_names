# Naive Bayes on a Name

This was loosely inspired by an article on 538 which tried to answer the question ["what the most popular name in the US?"](https://fivethirtyeight.com/features/whats-the-most-common-name-in-america/). From a link in that article, I later found Nate Silver's article on [how to tell someone's age when all you know is her name](https://fivethirtyeight.com/features/how-to-tell-someones-age-when-all-you-know-is-her-name/)

Here we are trying to answer a different question: given someone's name and gender, can we give a probability distribution for his or her age?

The approach taken here is very simple:
* The Social Security Administration supplies a breakdown of the [first name frequency](https://catalog.data.gov/dataset/baby-names-from-social-security-card-applications-national-level-data) for people born in the US, broken up by year, state and gender
* The census has a list of the [age distribution in the US](https://factfinder.census.gov/faces/tableservices/jsf/pages/productview.xhtml?src=bkmk)

## Methodology

Combining these two pieces of information, we can do a "naive bayes" estimate of how old someone with a given age is. We want to know 
P(age | gender and name). We can get this with Bayes's theorem:

P(age | gender and name) = P(gender and name | age) P(age) / P(gender and name)

We get:
- $P(\text{age})$, the prior, directly from the population distribution table
- $P(\text{gender and name | age})$ from looking up the popularity of the gender/age combination from `age` years ago
- The denominator is simply a normalizing factor.

