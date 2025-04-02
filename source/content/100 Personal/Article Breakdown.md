
Idea: Given article, instead of just classifying at is truth or false instead break the article down. Instead of just something that classifies a given article as true or false, it instead breaks it down it to:

1. A summary of the article and what the reporter is trying to say
2. The True Facts (verified by looking for sources)
3. The False facts (classified as so when a majority of sources disagree)
4. Opinions
5. Potential biases to look out for based on research of the reporter and publication

This gives much more context for the user to make a more personal decision on the reliability of a source

## Summary of article and what reporter

Simple enough tasks, current SOTA open models should crush this shit

## Facts verifier

Would have to:

Classify what are being claimed as facts in the article, then search against them and make a consensus based on evidence and give a rating for the confidence on how true each fact is

## Opinion Classifier

Current open source SOTA models should be able to classify what is an opinion

## Potential biases to look out for

Probably should have a database set up for biases of major news outlets, but with the help of searching some other articles from the reporter, biases can also be identified

Biases:
1. Political Leaning
2. Topic Leaning
3. Fact Score

## Branch Ideas

1. Reporter ranking -> A leaderboard of bias that ranks a reporter based on how biased they are