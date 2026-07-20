---
date: 2026-07-19T11:36
updated: 2026-07-20T12:14
layout: post
title: What My Job Isn't
---
I get a lot of email. Many of the emails I get fundamentally misunderstand my job. (Mostly sales emails, I'm categorized incorrectly in a lot of lead datasets I guess)

I was thinking about this today, and it ultimately descended into the following question:

> What would someone without knowledge of my job think my job was, just from reading my email?

Getting an answer to this question is kind of hard, it turns out. This is because the venn diagram for the involved parties looks like this:

![](/images/email-venn-diagram.png)

Luckily I remembered I know how to touch computers. This problem gets a lot easier to solve with computers!

- Computers like me enough to listen to me and solve my problems
- Computers obviously do not understand my job, since computers write all the AI spam I receive that misunderstands my job
- Computers do not have the ability to say no to reading 40,000 emails. This is because of the unstoppable force of the `for` loop. 

> fun fact! For loops are called that because it's short for "force"

I learned some natural language processing basics and how to [stir the linear algebra](https://xkcd.com/1838/) to analyze all my emails. 

To do this, I took the US Bureau of Labor Statistics' [list of industries](https://www.bls.gov/iag/tgs/iag_index_alpha.htm) and used [spacy](https://spacy.io/) and [scikit-learn](https://scikit-learn.org/stable/index.html) to write code that did agglomerative clustering to find the 25 most "important" industries, which the computer thought was relevant to a sample set of 30 of my emails.

I then took those 25 and asked the computer to look at all the 40,000 emails and say which industry the email felt like. (This took about 20 minutes, all locally computed. With no optimization.)

The code for this was surprisingly easy, the hard part was figuring out what the actual thing was I needed to do. I am not very confident that I picked the right thing to actually do, but the important part is, I did it! I can always make it better more later.

```py
def parse_email(email: str):
  doc = nlp(email)

  content_tokens = [t for t in doc if t.pos_ in ("NOUN", "PROPN")]
  content_doc = nlp(" ".join(t.text for t in content_tokens))  
    
  industry_similarity = [ [i, content_doc.similarity(i)] for i in INDUSTRY_DOCS]
  industry_similarity.sort(key=lambda x: x[1])
  most_industry = industry_similarity[-1]
  least_industry = industry_similarity[0]
  sentiment = analyzer.polarity_scores(email)

  return {
    "most_industry": most_industry[0],
    "most_industry_amount": most_industry[1],
    "least_industry": least_industry[0],
    "least_industry_amount": least_industry[1],
    "sentiment_pos": sentiment['pos'],
    "sentiment_neg": sentiment['neg'],
    "sentiment_neu": sentiment['neu'],
    "sentiment_compound": sentiment['compound'],
  }

```

I also used [VADER Sentiment Analysis](https://github.com/cjhutto/vaderSentiment) since I was trying to do this in one day and ran out of time in my one day to figure out how to do sentiment analysis on my own.

I tested it a little bit then set my code free on the 40,000 emails (thanks google takeout!)

For each email, my code gave me:
- The industry the email most feels like
- The industry the email **least** feels like
- The sentiment (positivity, negativity, neutrality) of the email

Lets answer some fun questions now!

What do people I don't know think my job is?
![](/images/email-most-likely-industry.png)
I don't remember opening a Sporting Goods Hobby Book and Music Store in 2018, but two of the most reliable things on earth (email spammers; computers trying to understand natural language) are telling me I did, so it must be true! 

It's also good to know my job is at least a little bit data science, that means you can take my findings seriously.

More importantly, what do strangers who email me think my job **isn't**?
The same way the math is able to guess what the most likely industry is, I can take the inverse and get the things my emails aren't. 

![](/images/what-my-emails-arent.png)
I can confirm that my job this year has definitely not been broadcasting, this is great data!

My job is also not Lessors of Nonfinancial Intangible Assets. The least Lessors of Nonfinancial Intangible Assets email I have ever received was this one trying to sell me ... something for construction people? I think? 

![](/images/lessors-of-nonfinancial-intangible-assets.png)


Here's sentiment of the emails people sent me:
![](/images/email-sentiment-time.png)
The data is kind of sporadic but it looks like people were a lot less positive during COVID. That makes sense - COVID sucked!

Do people who know me (as in, I have sent them an email before) understand my job better?

![](/images/known-sender-industry.png)
Internet Publishing and Broadcasting could be worse! Still not great though.

![](/images/least-likely-known-senders.png)
At least my friends and colleagues know me well enough to rule out Merchant Wholesalers Nondurable Goods. 


Do I even know what my job is? Here's the data on all the emails I've sent:

![](/images/my-email-industry.png)

"Science" is close enough. Here's the most Science email:

![](/images/most-science-email.png)

I guess my job is to work for "a nonprofit dedicated to providing underrepresented students with coding and computer science opportunities" 

Good to know!