# Google QUEST Q&A Labeling
## Improving automated understanding of complex question answer content

This is my github repo for the Kaggle Competition https://www.kaggle.com/c/google-quest-challenge

Follows my notes, most of the work is in the notebooks folder.

- **Exploratory Data Analysis**
    - Prediction Columns:
        - 'question_asker_intent_understanding',
        - 'question_body_critical', 
        - 'question_conversational',
        - 'question_expect_short_answer',
        - 'question_fact_seeking', 
        - 'question_has_commonly_accepted_answer',
        - 'question_interestingness_others', 
        - 'question_interestingness_self',      
        - 'question_multi_intent', 
        - 'question_not_really_a_question',       
        - 'question_opinion_seeking', 
        - 'question_type_choice',
        - 'question_type_compare', 
        - 'question_type_consequence',
        - 'question_type_definition', 
        - 'question_type_entity'
        - 'question_type_instructions', 
        - 'question_type_procedure',
        - 'question_type_reason_explanation', 
        - 'question_type_spelling',
        - 'question_well_written', 
        - 'answer_helpful',
        - 'answer_level_of_information', 
        - 'answer_plausible', 
        - 'answer_relevance',
        - 'answer_satisfaction', 
        - 'answer_type_instructions',
        - 'answer_type_procedure', 
        - 'answer_type_reason_explanation',
        - 'answer_well_written
    - Would be pretty interesting to have an instinctive understanding of the single prediction columns. Here might be some questions to answer for each label, e.g. for __question_not_really_a_question__
        - **What do data point with highest lowest value look like?** Some of them make sense some of them don't. The main observation is that some label looks really easy to predict, some labels look really hard. Especially how the "absence of" some features, is harder to predict than the presence of some feature. For instance, what is a "fact seeking" question is medium, what is not a fact seeking question is hard to tell.
        - **How is the distribution for the label?** distribution looks really skewed, especially a bunch of labels have a strong skew toward 0 labels. Makes me think I would need some sort of ad-hoc classifier for those with really unbalanced training data.**What labels correlate between each other?** Looks like I can use a [[correlation matrix]] for that, [dataframe.corr](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.corr.html
        - **What labels correlate between each other?** Looks like I can use a [[correlation matrix]] for that, [dataframe.corr](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.corr.html). Some interesting correlation happening, good answers label highly correlate with each other, and also question_type_X always correlate with answer_type_X, whereas question_type_X anticorrelates with question_type_Y. I am not too sure how to use this correlation data for modelling, one idea might be: let's train a classifier only if the answer is helpful or not.
        - **Is there some clustering happening between the data point in the labels space?** I could try to use PCA or TSN-E for that
    - We can also have a quick look at the input data
        - **What kind of categories/website do data come from?** I could use [[word cloud]] to visualise that. Here is the [code pointer](https://amueller.github.io/word_cloud/auto_examples/simple.html#sphx-glr-auto-examples-simple-py). Looks like there is 60 hosts and 5 categories. Everything is kind of equally distributed beside some outliers (e.g. stackoverflow)
        - **Do data from the same website cluster together?** Clustering by host shows some correlation, for instance tex, physics, and academia have sharp clustering in the PCA space. This might hint at training a classifier for each "class" of similar hosts? How to detect classes of hosts? I could get the centroids of my labeled clusters and then apply k-means on the centroids?
        - **Do data from same category cluster together?** Less obvious here, data from stackoverflow and from culture show some clustering, but there is too few categories and too much variance in the pca embeddings. Still might want to try out whatever I try for host clustering.
