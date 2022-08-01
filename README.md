Brain Size and Personality

Using the size of brain structures to predict personality

Goals of the project

Of the various frontiers of knowledge and capabilities, it can be assumed that those related to deepening the understanding of the brain are poised to have the most revolutionary impact on humanity.
In recent years there have been many advances in technologies that allow us to see into the brain. One of these technologies is magnetic resonance imaging (MRI). MRIs use magnets and radio waves to construct a picture of the body to include muscles and organs. MRIs are typically used as a non-invasive diagnostic tool, helping doctors to identify internal conditions such as bleeding or tumors.

The National Institute of Health (NIH) has funded numerous studies related to the human connectome. A connectome is a map of the ‘wiring’ of an organism’s nervous system. There is an implicit recognition that the structure of an organism’s nervous system is related to its function. To help coordinate these studies the NIH established the Connectome Coordination Facility. Which among other things developed protocols to standardize the studies (Van Essen et. al., 2012).

One of the studies in the Human Connectome Project took MRIs of subjects in order to document the physical characteristics of a variety of brain structures along with self-reported behavioral and personality traits such as drug-use and feelings of anxiety.

While the minutiae of individual personalities are ultimately unique to each person, it has long been recognized that the broader outline of individuals can be grouped into categories. Over time different personality taxonomies have been developed. Astrology which divides personalities according to particular star constellations under which the person was born is one of the oldest of these systems. A far more modern taxonomy is the Myer-Briggs taxonomy which divides people into 16 personality types depending on their responses to a self-answered questionnaire (Cherry, 2021). This personality system is popular among the general population and business community. However, within an academic setting the Big Five taxonomy is the de-facto standard. The Big Five taxonomy also uses responses to a self-answered to assign subjects to a position along 5 personality continuums.  The continuums are openness to experience, conscientiousness, extraversion, agreeableness and neuroticism (Srivastava, 2022). It is the intention of this project to use machine learning models to predict the personality of an individual as determined by the Big Five Taxonomy by using measurements of brain structures taken by an MRI. 

One benefit of identifying which brain structures are responsible for personalities as described by the Big Five is that can be used to standardize the Big Five across time and cultures. For example, a question from the Big Five questionnaire is ‘I often feel blue’ however over time and across cultures there can different interpretations of the words ‘often’, ‘feel’ and ‘blue’ which will result in different personality assessments that are caused by differences in the interpretation of the question rather the underlying characteristic that the question is attempting to measure. Linking the taxonomy to physical brain structures eliminates the problem of cultural interpretation.  This increase in standardization and accuracy can also lead to better diagnostic capabilities. For instance, in identifying high risk individuals, heroin users for example tend to rank high in neuroticism, openness, agreeableness but low in conscientiousness, while ecstasy users tend to rank high in extraversion and openness but low in agreeableness and conscientiousness. It can also be used in career counseling as certain personality types tend to be better suited for certain careers.  

After a model is created, flask will be used to create an interactive app that suggests a career path to users based on their Big Five taxonomy profile.

Flask
A Big Five personality quiz was created using flask.

Data description

Link to data: https://wiki.humanconnectome.org/display/PublicData/S1200+3T+MRI+Session+Summary+CSVs Title: S1200 3T MRI Sessions Summary CSVs
The data includes 3T MRI imaging and behavioral data from 1206 healthy participants, collected from 2012 to 2015. The sex breakdown of the subjects are 656 females and 550 males. The ages range primarily from 22 to 35 with only 14 subjects being 36 or older.
Data is composed of 1206 rows across 582 columns. However only columns with brain structure measurements of which there are 199 columns will be used as features. The features are composed of the surface area, thickness and volume measurements of different brain structures. The 5 response variables will come from the 5 columns holding each of the Big Five continuum data.  

Software

Jupyter notebook(python) and flask will be used to build this project. 
Analyses & Model Specifications
The project began with extracting the relevant columns from the data set which were the 199 columns containing measurements of the brain’s physical structures plus 5 columns holding each of the Big Five continuum data for a total of 204 columns. The measurements of the brain were assigned to the variable ‘features’ and the remaining columns became the ‘response’.

Exploration of the data revealed that there were 93 and 7 rows with null values in the features and response respectively. Being a small percentage of 1206 the rows were dropped leaving 1106 rows for my analysis. 

Random variables were explored for outliers and normal distribution. Finding nothing out of the ordinary I proceed to substantiate a standard scaler and column transformer in anticipation of model building. 

Our problem being a multi-output numerical problem, I started with Linear Regression and Knearest Neighbors. Different parameters were used with GridSearch to find the best model. The resulting Rsquare was negative indicating no pattern was found.

A  tensor flow sequential model was built and  the scaling technique was changed to MinMax. Many variations of number of deep layers, neurons, learning rates etc were tried, but each led to a negative Rsquare.

A Dimensionality Reduction technique of multiplying the brain structures related to area and thickness and dropping those related to volume was done to create a new feature set. This too led to a negative Rsquare. Multiple variations of feature sets as well further modifications of the sequential model were tried but all resulted in negative in a Rsquare.

Dimensionality Reduction was then tried on the response variables, with numerical values above the mean(29) being assigned 1(high) and those below being assigned 0(Low). With the  idea a person would be rated as high or low in agreeableness, rather than say for example 33 out of 50. A new sequential model was built with the primary scoring metric being accuracy. Variations of this model were tried all yielding low accuracy scores.

Dimensionality Reduction was then tried by dropping one 1 of the 5 response variables. It was found that by dropping conscientiousness our model predicted with an accuracy of  82%. 

In conclusion with inclusion of caveats, namely predicting 4 rather than 5 traits and predicting them as high or low(categorical) versus continuous the project was a success. We were able to predict personality as measured by the Big Five using the size of brain structures.

An additional investigation was conducted by separating the data by gender. In doing so it was found that male accuracy rate was 77% and the female accuracy rate 90%. Indicating it was easier to predict female personality then male. At this point I theorized that this could be due  to what is known as the variability hypothesis , which is  the idea albeit a contestested one that in many areas of comparison women are on average more average than men. To give an example, in the measurements of hands, women show less variability in the size of their hands than men. My hypothesis then was that the standard deviation of females would be less than that of males, which is why the model was more accurate for females. My hypothesis proved correct, the standard deviation of both the size of brain structures and personality were smaller in females than males. 

Thus as a secondary conclusion it was found that the size of brain structures was a better predictor of female personality than male. This was due to reduced variability both in structure measurements and distribution of personality traits.


Deliverables
The project will be communicated via a video walkthrough of a jupyter notebook. In addition a pdf of the notebook will be submitted as well as cvs of the dataset.

References
1) Cherry, K., 2021. An Overview of the Myer-Briggs Type Indicator. [online] Verywell Mind.Available at: <https://www.verywellmind.com/the-myers-briggs-type-indicator-2795583>  [Accessed 27 June 2022].
2)Johnson, W., Carothers, A., & Deary, I. J., 2008. Sex Differences in Variability in General Intelligence: A New Look at the Old Question. Perspectives on psychological science : a journal of the Association for Psychological Science, 3(6), 518–531. Available at:  <https://citeseerx.ist.psu.edu/viewdoc/citations?doi=10.1.1.605.5483> [Accessed 29 June 2022].
3) Srivastava, S. 2022. Measuring the Big Five Personality Factors. [online] Uoregon. Available at: <https://pages.uoregon.edu/sanjay/bigfive.html> [Accessed 27 June 2022].
4) Van Essen, D. C., Ugurbil, K., Auerbach, E., Barch, D., Behrens, T. E., Bucholz, R., Chang, A., Chen, L., Corbetta, M., Curtiss, S. W., Della Penna, S., Feinberg, D., Glasser, M. F., Harel, N., Heath, A. C., Larson-Prior, L., Marcus, D., Michalareas, G., Moeller, S., Oostenveld, R., ...WU-Minn HCP Consortium. 2012. The Human Connectome Project: a data acquisition perspective. NeuroImage, 62(4), 2222–2231. Available at:<https://doi.org/10.1016/j.neuroimage.2012.02.018> [Accessed 27 June 2022]


