# Entry for 2019 SIOP Machine Learning Competition

This repo contains the submission my team, the Machined Learnings, created for the 2019 [Society for Industrial and Organizational Psychology Machine Learning Competition](https://evalai.cloudcv.org/web/challenges/challenge-page/160/overview).
This competition was my first big experience working with other coders in Python, using Jupyter Notebooks, on a project.  We collaborated via BitBucket, and communicated via
Slack, giving me great exposure to both of these platforms.  It was a great experience I hope to repeat in the future, and although we placed 28th, I am proud of the learning
and collaboration that took place.

## The Competition

My team consisted primarily of myself and another programmer, with two other psychology students to provide information and support.  I had an in-depth statistics background
(including regression, the basis of machine learning) and experience with R, while he had relatively little background in machine learning but years of experience using Python.
We were tasked by the competition with using Natural Language Programming (NLP) to analyze a set of open-ended text responses (called situational judgment items from job interviews)
and generate a machine learning model using these to predict [Big Five Personality scores] (https://en.wikipedia.org/wiki/Big_Five_personality_traits).  We received a training dataset to work on for the first couple of months, then a testing
dataset to see what amount of added variance we were able to account for (measured by a RMSE idex).  Both of these datasets can be found in the repo under the names 'siop_ml_train_participant.csv'
and 'siop_ml_dev_participant.csv' respectively.  

## Model Development

There were two main portions to the model that we first had to consider:

  1. How we were going to tag the text answers so as to use them to predict the numerical personality scores - i.e., feature engineering.
  
  2. What regression/machine learning technique were we going to use to generate the predictive model - i.e., model building.
  
We essentially wound up splitting the work to where I would tackle item one, while he tackled item two.  My teammate was invaluable in helping me to get started coding.  He showed me the nltk package
and I used it to create my first function using nltk's POS (part of speech) tagging to tag words as either past or present tense. Having previous expertise in personality research, I used a quick lit 
search to determine a list of text features (based loosely on the LIWC list created by Pennebaker & King, 1999) that had been shown to be significant predictors of Big Five Personality in the past.  Using this list, I set about generating functions that would tag each 
word in each response for tense, positive and negative emotion, tentativeness, causal language, word length, use of articles, and use of first person singular pronouns.  My first pass at 
generating these was in the notebook called "Jessica's Feature Fun."  However, I misunderstood the role of indentation in the order of operations in loops.  This led to the obviously wrong output of each
respondent receiving exactly the same score.  Definitely not what I intended! I asked my teammate for help, and he didn't want to tell me how to do it right away.  He wanted me to figure it out on my own,
and advised me to use code from the notebook "Multi-Feature Input Demo" that he had created in the course of creating his portion of the code.  I took his advice and created my own notebook, "Sandbox", 
and tested out different changes to my features until I discovered the problem.  I had it assigning the output index in the inner part of the loop, leading it to only output the first one caculated and then
assign it to all cases.  I learned an important lesson about the differences in a variable or function's scope depending on its placement in relation to the loop.  

After this exercise, I fixed my functions and created a more professional looking portion to submit called "Functions_For_Machine_Learning".  We used magic commands (which I figured out with my teammate's guidance)
to magic in my functions to the final submission code, where the tags could then be used as predictors in the model.

Meanwhile, my teammate had been hard at work using a tf/idf (term frequency/inverse document frequency) tagging with a variety of different regression techniques to see which produced the best RMSE.  Although
he initially created some code to calculate the RMSE ourselves, we kept getting different values from the (unknown) formula used by the submission portal for the contest, so we used the numerous submissions we were 
allowed to instead test our model.  He tried linear regression, SVR, Lasso, and Kernal Ridge.  However, regression still gave the best answer, but unfortunately not much better than chance.  

In a final sprint before the deadline, we put together our final submission notebooks, imported the test data, and then started running models with different combinations of predictors.  I used my expertise in personality to my best ability 
to decide on sets of predictors, while my teammate used methods such as ridge regression and random forrest to see if we could find better outcomes there.  In the last moment of the competition, we put in our best result,
a model using all predictors, which only yielded a RMSE of .11.  However, the fourth place team had a .15, so we weren't too terribly far behind.  We high fived and exchanged memes, for the deed was done.

## Conclusion

If I had this all to do over, there are definitely a few more things I would have tried.  We were strapped on time, since both of us were doing this in our spare time outside of our day jobs, but if it were possible
I would have liked to have had more time to devote.  I would have liked to look for a free, open corpus of similar text responses that we could use to further our model's predictive ability.  The rules of the contest
said anything we used had to be free and open-source, which is why we did not buy and download the original LIWC tagging libraries that were used in past research.  However, in a different setting, I would have preferred
to go with those, or at least try them.  Also, based on theory I would have preferred to do something more complex where different models were used to predict different questions, since each question appeared to be clearly
tailored toward a different personality trait.  

From this experience, other than learning to use nltk, sklearn, and magic commands in Python, I learned some broader lessons:

  1. I learned how complicated collaborating with someone else on a coding project is, especially when working remotely, and I learned several tricks to make this collaboration easier and improve communication.  Judicious use of 
  screenshots, displaying code in Slack, and commenting/markdown cells in notebooks are fantastic tools for showing someone what you mean.  
  
  2. I learned the value of Git technology, as well as some pitfalls.  I was using a client called GitKraken that a member of our team had suggested, and at times it was more difficult to use than simply a command interface.
  However, I learned many tips such as branching, pull requests, merging completed branches into the master branch (but having them reviewed first), and forking.  I learned ettiquite for using git, such as the fact that I was creating
  new files when it was not necessary, because I could simply change my own files on my branch and merge them later.  
  
  3. I learned that having good debugging skills is as important if not more important than the code itself.  I learned or relearned useful debugging philosophies such as "fail fast" -- if you're going to try a thing, try it on a 
  subset of data or piece of test code before applying it to your entire datast or changing your entire code to incorporate it.  That way, if it doesn't work, you won't have spent much unnecessary time implementing it and won't have 
  to go back and undo all the changes you've made thus far.  I also got practice selectively commenting out lines of code so that you can isolate and determine where the problem starts.  Remembering these tricks instead of panicking 
  when something's not right can save a lot of time and anguish.  Also, google all error messages. 
  
Most importantly, I learned that I could hold my own in and enjoy a collaborative coding experience in a relatively new coding language.  I had a great time, even with all of the challenges I faced.  In fact, the challenges made the experience
better.  I now have so many new concepts with machine learning and NLP to explore!

The results of the competition can be found here: https://github.com/izk8/2019_SIOP_Machine_Learning_Winners
