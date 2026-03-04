# BERT-analysis
Topic analysis of the journal “Epistemology and Philosophy of Science” using BERT
## Research Context
The journal *Epistemology and Philosophy of Science* has been published since 2004, with 4 issues released per year.
## Research Goal
Identification of trends in the journal's thematic changes since 2004.
## Objectives
1.	Collect a text corpus.
2.	Extract topics of a reasonable size.
3.	Visualize changes in topic popularity over time.
4.	Analyze the resulting plots and identify trends.
## Methods Used
1.	Document AI (Google): Used for OCR to obtain high-quality text from article scans.
2.	BERT: Used to generate embeddings for each article.
3.	SpaCy: Used for text tokenization.
4.	BERTopic: Used for clustering the embeddings to identify meaningful topics.
5.	Matplotlib: Used for visualizing clusters and topic-over-time plots.
## Main Topic Extraction Method
The primary method for isolating topics was tuning the parameters of the HDBSCAN model (which is used by BERTopic). This model determines the approximate number of clusters, the clustering method, and how close the vectors must be to each other to be assigned to the same cluster. Thus, the task of extracting meaningful topics was solved specifically by finding the optimal parameters for HDBSCAN.
## Main Challenge
Initially, BERTopic did not produce adequate clustering regardless of the HDBSCAN parameters. As it turned out, the data contained two very distinct clusters:
1.	Articles directly related to the philosophy of science.
2.	"Meta-articles" about the journal itself (anniversaries, obituaries, etc.).

Instead of breaking down the large "research articles" cluster into sub-topics, the model tended to split the smaller cluster (e.g., separating anniversaries from obituaries).

**Topic maps at that stage:**

<img width="546" height="384" alt="image" src="https://github.com/user-attachments/assets/76174f9d-e17d-4c7d-bad6-36f5cedd1ff8" />

**Solution:**

After attempts to change the BERTopic parameters did not bring success, it was decided to apply BERTopic a second time. This time, only to those articles that were assigned to topic 0 (meaning directly to research articles).
As a result, topics were extracted, and changing the HDBSCAN parameters during the second use of BERTopic indeed allowed identifying different clusters.

## Examples of Extracted Topics
After BERTopic extracted the topics, 10 keywords associated with the topic were printed.
Settings for smaller clusters allowed extracting 94 topics, many of which were of interest (for example, articles on quantum mechanics). But such topics were too narrow for analysis.

<img width="558" height="406" alt="image" src="https://github.com/user-attachments/assets/5045ac47-4ffd-47f1-8b6c-b33047063eec" />

Therefore, improved HDBSCAN parameters were found, allowing for the distinction of 22 clusters.

<img width="585" height="442" alt="image" src="https://github.com/user-attachments/assets/d4400487-a1d0-417f-b013-00143ee5e4f4" />


**Translation of the first keywords for the topics below.**

**Topic 1** (Articles: 181):
  - 'proposition' (0.0193) 
  - 'reference' (0.0179)
  - 'predicate' (0.0157)
  - 'description' (0.0152) 
  - 'Kripke' (0.0149)

This topic is associated with the **philosophy of science**.

Topic frequency:

<img width="614" height="297" alt="image" src="https://github.com/user-attachments/assets/ec3e70f2-51e5-4f39-8414-53747e85047d" />



**Topic 2** (Articles: 78):
  - 'zone' (0.0269)
  - 'trade zone' (0.0254)
  - 'technological' (0.0222)
  - 'technosciences' (0.0185)
  - 'expertise' (0.0157)

This topic is associated with the **trading zones** (the concept of Peter Galison). Its frequency:

<img width="591" height="290" alt="image" src="https://github.com/user-attachments/assets/6696f548-3cd2-40c6-844a-b2c49fe497a1" />


**Topic 3** (Articles: 56):
  - 'phenomenal' (0.0434)
  - 'qualia' (0.0351)
  - 'gesture' (0.0203)
  - 'phenomenal quality' (0.0158)
  - 'color' (0.0154)

This topic is associated with the **philosophy of mind**. Its frequency:

<img width="606" height="300" alt="image" src="https://github.com/user-attachments/assets/4cd233be-17b4-49c5-9dcd-3edaa50b4116" />


**Topic 5** (Articles:  53):
  - 'circle' (0.0527)
  - 'Vienna' (0.0512)
  - 'Vienna circle' (0.0473) 
  - 'Heisenberg' (0.0368)
  - 'Humboldt' (0.0334) 
  - 'rule-following' (0.0242)
  - 'logical positivism' (0.0212)

This topic is associated with **logical positivism (and Wittgenstein)**. Its frequency:

<img width="619" height="178" alt="image" src="https://github.com/user-attachments/assets/e0516dc3-f64f-4de4-ac69-383f7641729a" />

(Keywords for the peak are translated)


## Main Findings
1. Topics that are weakly related to the journal's theme mostly receive attention only when thematic issues are written (as in the case of religion), or when there are peaks of interest in them (as in the case of economics and politics).
2. The popularity of some topics that are directly related to the journal may increase or decrease over time. For example, the philosophy of language and the closely related philosophy of logic are gradually losing popularity, although they are still an important topic for the journal, while "trading zones", on the contrary, are becoming more popular.
3. Topics close to the general theme of the journal are characterized by constant interest. Often at least one article per issue is published on the topic.
4. Some peaks of interest in a topic can be explained by dates. For example, an anniversary of Wittgenstein may be associated with an increase in interest in him during that period.
