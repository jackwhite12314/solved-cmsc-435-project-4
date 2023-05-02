Download Link: https://assignmentchef.com/product/solved-cmsc-435-project-4
<br>
The project asks you to develop, evaluate and compare models for the prediction of proteins that interact with DNA and RNA using a provided dataset. Your model must classify a given protein sequence into one of four outcomes, i.e., interacts with DNA (DNA), interacts with RNA (RNA), interacts with both DNA and RNA (DRNA), and does not interact with DNA or RNA (nonDRNA). Although each group will solve the same task, the corresponding designs should be unique, i.e., collaboration between groups is not allowed.




<h1>Datasets</h1>

<strong>Two datasets</strong> are/will be provided:

<ul>

 <li><em>txt </em>(<em>training dataset</em>) that includes 391 DNA proteins, 523 RNA proteins, 22</li>

</ul>

DRNA proteins, and 7859 nonDRNA proteins, for the total of 8795 proteins.

<ul>

 <li><em>txt </em>(<em>blind test dataset</em>) that includes 8795 proteins, with similar proportions between the four classes of proteins. This is an independent test set, which means that entire design procedure (including feature generation, feature selection, parameterization and selection of classifiers, etc.) should be completed using only the training dataset. The test dataset should be used to evaluate your system only once. This dataset will be posted on the class web site 2 days before the project submission deadline and it will <strong>not </strong>include the annotation of the outcomes. You will have to predict the outcomes and the instructor will process and assess these predictions.</li>

</ul>

The training dataset is provided in the comma-separated format where each protein is represented by:

<ul>

 <li>the amino acid sequence</li>

 <li>the class encoded as DNA, RNA, DRNA, and nonDRNA</li>

</ul>

Test dataset will be the same format as the training dataset, except that the outcomes will not be provided.




<h1>Evaluation of Predictions</h1>

You are required to perform the 5-fold cross validation when using the <em>training dataset</em>. This cross validation divides the training dataset into 5 random, equal-size subsets, where one subset is used to test the prediction model and the remaining four to train/develop the prediction model; this is repeated 5 times, each time using a different subset as the test set. Consequently, this test results in predicting every sequence in the training dataset. This test procedure is supported by RapidMiner.




For each of the four outcomes you will convert the dataset into a binary problem, i.e., a given outcome (positive outcome) vs. all other outcomes (negative outcomes). For example, all proteins that are labeled as DNA will be considered as positive, and the remaining proteins (RNA, DRNA and nonDRNA) as negative. Next, for each of the four outcomes you will compute the following measures:

<em>            Sensitivity</em> = SENS = 100*TP / (TP + FN)

<em>            Specificity</em> = SPEC = 100*TN / (TN + FP)

<em>             PredictiveACC</em> = 100* (TP+TN) / (TP+FP+TN+FN)

<em>             MCC</em> = (TP*TN – FP*FN) / sqrt[(TP+FP)*(TP+FN)*(TN+FP)*(TN+FN)]

where TP is the number of true positives (correctly predicted positive outcomes), FP denotes false positives (negative outcomes that were predicted as positives), TN denotes true negatives (correctly predicted negative outcomes), FN stands for false negatives (positive outcomes that were predicted as negatives). You will also compute:

<em>averageMCC</em> = (MCCDNA + MCCRNA + MCCDRNA + MCCnonDRNA)/4 <em>accuracy</em> = 100*TP<sub>all</sub> / (number of all protein in the dataset)

where MCC<sub>DNA</sub>, MCC<sub>RNA</sub>, MCC<sub>DRNA</sub>, and MCC<sub>nonDRNA</sub> denote the MCC values when using the DNA, RNA, DRNA, and nonDRNA outcomes as the positives, and TP<sub>all</sub> is the number of correctly predicted outcomes (DNA proteins predicted as DNA proteins, RNA proteins predicted as RNA proteins, etc.). These measures can be computed based on the confusion matrix. You should <strong>round the values</strong> to one digit after the decimal point when reporting the accuracy, sensitivities, and specificity and to three digits after the decimal point when reporting MCC. <strong>You report must include the confusion matrix for your final/best solution</strong>.




You must also provide and <strong>summarize predictions on the <em>blind test dataset</em></strong>. To do that you will compute your model using the entire training dataset (using the same design, i.e., features, values of parameters, etc., as in your best 5 fold cross validation result) and you will use this model to predict sequences from the blind test dataset. In your report, you must discuss the corresponding results on both the training and blind test dataset; on the blind test dataset you can summarize your results by explaining and comparing how many proteins were predicted with a given outcome.




<h1>Design</h1>

You need to <strong>design</strong> your predictive model to maximize its predictive performance <strong>evaluated based on averageMCC using the 5 fold cross validation on the training dataset</strong>. The design may consider:

<ul>

 <li>Use of different features to encode the input protein sequence. The data mining algorithms require a rectangular dataset with a fixed size and structure of the feature vector for each object (protein). Thus, you will need to convert the input protein sequences (that have variable length) into a fixed set of (numerical) features. Lecture set 7 includes a few suggestions.</li>

 <li>Selection of a subset of the input features. This could potentially speed up computation of the model, remove weak/noisy features, and reduce overfitting. Feel free to combine results of multiple feature selection methods.</li>

 <li>Selection of the classification algorithm that you will use to compute your model from among many algorithms that are available in RapidMiner.</li>

 <li>Parametrization of the selected classification algorithm(s). This involves setting values of their key parameters.</li>

 <li>Building a system with multiple models that are used together. For instance, you could use multiple models that predict all 4 classes and combine their results together to generate one prediction. Check the methods in RapidMiner at Operators → Modeling → Predictive → Ensembles.</li>

 <li>Different ways to perform the prediction. There are at least two alternatives: use one model to predict all 4 classes vs. use 4 models to predict each of the four classes. In the latter case, you will have to combine the four results to select one “best” result for each protein. The advantage of the second approach is that you can choose different subsets of features and different classification algorithms and their parameters for each outcome/class.</li>

</ul>

<strong>NOTE 1</strong>: Ensure that you perform all design activities (e.g., feature selection, selection and parametrization of the classification algorithms, etc.) using the 5-fold cross validation on the training dataset. Otherwise you could overfit this dataset and your results on the test dataset could suffer.

<strong>NOTE 2:</strong> Your design should be done incrementally. Start with a simple initial solution (complete the entire design, prediction, and prediction assessment process) and gradually make your design more sophisticated with the objective to improve the predictive performance. In your report, you should clearly indicate <strong>one</strong> best set of results, which must be selected based on the cross validation results on the training dataset. Moreover, these results should be compared with your intermediate results (earlier/simpler designs, other alternatives, etc.) and with baseline results shown in Table 1, in order to justify your design choices. <strong>In your write up, report your results by adding them into Table 1. </strong>This will make it easy to compare the different alternatives. <strong>Clearly indicate which result is the best/final</strong>. You should explain how you made decisions that led you a certain direction of redesigning your model. You also should provide a convincing argument why and how your method is good/competitive in comparison to the baseline result in Table 1.




Table 1. Predictive results based on the 5-fold cross validation on the training dataset (this table is available in the Blackboard).




<table width="653">

 <tbody>

  <tr>

   <td width="107"><u>Outcome </u></td>

   <td width="126"><u>Quality measure </u></td>

   <td width="114"><u>Baseline result</u></td>

   <td width="80"><u>Design 1</u></td>

   <td width="80"><u>Design 2</u></td>

   <td width="72"><u>Design 3 </u></td>

   <td width="73"><u>Best Design</u></td>

  </tr>

  <tr>

   <td width="107">DNA</td>

   <td width="126"><em>Sensitivity</em></td>

   <td width="114">6.9</td>

   <td width="80"></td>

   <td width="80"></td>

   <td width="72"></td>

   <td width="73"></td>

  </tr>

  <tr>

   <td width="107"></td>

   <td width="126"><em>Specificity</em></td>

   <td width="114">99.3</td>

   <td width="80"></td>

   <td width="80"></td>

   <td width="72"></td>

   <td width="73"></td>

  </tr>

  <tr>

   <td width="107"></td>

   <td width="126"><em>PredictiveACC</em></td>

   <td width="114">95.2</td>

   <td width="80"></td>

   <td width="80"></td>

   <td width="72"></td>

   <td width="73"></td>

  </tr>

  <tr>

   <td width="107"></td>

   <td width="126"><strong><em>MCC</em></strong></td>

   <td width="114"><strong>0.132 </strong></td>

   <td width="80"><strong> </strong></td>

   <td width="80"><strong> </strong></td>

   <td width="72"><strong> </strong></td>

   <td width="73"><strong> </strong></td>

  </tr>

  <tr>

   <td width="107">RNA</td>

   <td width="126"><em>Sensitivity</em></td>

   <td width="114">39.6</td>

   <td width="80"></td>

   <td width="80"></td>

   <td width="72"></td>

   <td width="73"></td>

  </tr>

  <tr>

   <td width="107"></td>

   <td width="126"><em>Specificity</em></td>

   <td width="114">98.9</td>

   <td width="80"></td>

   <td width="80"></td>

   <td width="72"></td>

   <td width="73"></td>

  </tr>

  <tr>

   <td width="107"></td>

   <td width="126"><em>PredictiveACC</em></td>

   <td width="114">95.3</td>

   <td width="80"></td>

   <td width="80"></td>

   <td width="72"></td>

   <td width="73"></td>

  </tr>

  <tr>

   <td width="107"></td>

   <td width="126"><strong><em>MCC</em></strong></td>

   <td width="114"><strong>0.501 </strong></td>

   <td width="80"><strong> </strong></td>

   <td width="80"><strong> </strong></td>

   <td width="72"><strong> </strong></td>

   <td width="73"><strong> </strong></td>

  </tr>

  <tr>

   <td width="107">DRNA</td>

   <td width="126"><em>Sensitivity</em></td>

   <td width="114">4.5</td>

   <td width="80"></td>

   <td width="80"></td>

   <td width="72"></td>

   <td width="73"></td>

  </tr>

  <tr>

   <td width="107"></td>

   <td width="126"><em>Specificity</em></td>

   <td width="114">100.0</td>

   <td width="80"></td>

   <td width="80"></td>

   <td width="72"></td>

   <td width="73"></td>

  </tr>

  <tr>

   <td width="107"></td>

   <td width="126"><em>PredictiveACC</em></td>

   <td width="114">99.7</td>

   <td width="80"></td>

   <td width="80"></td>

   <td width="72"></td>

   <td width="73"></td>

  </tr>

  <tr>

   <td width="107"></td>

   <td width="126"><strong><em>MCC</em></strong></td>

   <td width="114"><strong>0.122 </strong></td>

   <td width="80"><strong> </strong></td>

   <td width="80"><strong> </strong></td>

   <td width="72"><strong> </strong></td>

   <td width="73"><strong> </strong></td>

  </tr>

  <tr>

   <td width="107">nonDRNA</td>

   <td width="126"><em>Sensitivity</em></td>

   <td width="114">98.6</td>

   <td width="80"></td>

   <td width="80"></td>

   <td width="72"></td>

   <td width="73"></td>

  </tr>

  <tr>

   <td width="107"></td>

   <td width="126"><em>Specificity</em></td>

   <td width="114">29.8</td>

   <td width="80"></td>

   <td width="80"></td>

   <td width="72"></td>

   <td width="73"></td>

  </tr>

  <tr>

   <td width="107"></td>

   <td width="126"><em>PredictiveACC</em></td>

   <td width="114">91.3</td>

   <td width="80"></td>

   <td width="80"></td>

   <td width="72"></td>

   <td width="73"></td>

  </tr>

  <tr>

   <td width="107"></td>

   <td width="126"><strong><em>MCC</em></strong></td>

   <td width="114"><strong>0.428 </strong></td>

   <td width="80"><strong> </strong></td>

   <td width="80"><strong> </strong></td>

   <td width="72"><strong> </strong></td>

   <td width="73"><strong> </strong></td>

  </tr>

  <tr>

   <td width="107"><strong><em>averageMCC</em></strong></td>

   <td width="126"></td>

   <td width="114"><strong>0.265 </strong></td>

   <td width="80"><strong> </strong></td>

   <td width="80"><strong> </strong></td>

   <td width="72"><strong> </strong></td>

   <td width="73"><strong> </strong></td>

  </tr>

  <tr>

   <td width="107"><em>accuracy</em></td>

   <td width="126"></td>

   <td width="114">90.8</td>

   <td width="80"></td>

   <td width="80"></td>

   <td width="72"></td>

   <td width="73"></td>

  </tr>

 </tbody>

</table>







<h2>3. Presentation</h2>

<ul>

 <li>8 minutes long plus 2 minutes for questions&amp;answer session  shall describe the design, results and conclusions             shall include the following parts:</li>

 <li>Motivation for your design. Briefly explain how you arrived at your final design.</li>

 <li>Description of your design. Explain (preferably with a diagram) how your method makes the predictions.</li>

 <li>Discussion and comparison of the quality of the achieved best results using the results on the training dataset and Table 1.</li>

 <li>This part is essential; see the conclusions part of your report.</li>

</ul>

<h2>4. Statement of contributions</h2>

<ul>

 <li>A short document with bullet-point style list of detailed contributions to the project for each team member. The contributions cover all aspects of the project including conceptualization and design of the methodology, implementation, testing, writing the report, preparing the presentation, making the presentation, coordination of the work, notes taking, etc.</li>

 <li>The contribution list for each team member should be accompanied with an estimated fraction of the total project effort, quantified in %. The effort estimates across the 5 team members must sum up to 100%. Each team should strive to balance the effort to be 20% for each team member.</li>

 <li>This statement will be used to distribute the project grade among the team members.</li>

</ul>




<h1>Marking</h1>

The evaluation of the project report and predictions constitutes 15% of the final mark from the course and it will consist of the following three parts:

<ol>

 <li>30% for the quality of the report</li>

 <li>20% for the quality of the design of the prediction method</li>

 <li>50% for the quality of the predictions measured using the 5 fold cross validation on the training dataset and on the blind test set.</li>

</ol>

<strong>NOTE 3</strong>: For item 3, the <em>averageMCC</em> is the main predictive quality measure that will be used to evaluate submitted solutions but the conclusions <strong>must discuss</strong> the other quality indices as well. <strong>Bonuses</strong> of 15%, 10%, and 5% will be given to the project submissions that secure the highest, the second highest and the third highest value of <em>averageMCC</em> on the blind test dataset. In case of a tie the winner will be decided based on the higher value of the <em>accuracy </em>on the blind test dataset.

<strong>NOTE 4</strong>: MCCs that are high(er) relative to other submissions or to the baseline result in Table 1 are not necessary to receive a full mark. The most important aspect is to show substantial progress from the initial solution – you should show and discuss how your best design is better when compared to your own alternative solutions and explain advantages compared to the baseline results in Table 1.




The presentation constitutes 10% of the final mark from the course and will be evaluated by the instructor, TA and your peers. The grade will consist of three parts:

<ol>

 <li>Grade assigned by the fellow students (<strong>30%</strong>). Each project group will complete a short evaluation form, see appendix A, to assess presentations of other groups. Instructor will gather and process these grades; they will be kept confidential. You should reassess and potentially revise your scores after all presentations on a given date are <em>completed</em> to assure <strong>consistency</strong>.</li>

 <li>TA’s grade (<strong>30%</strong>). TA will grade the quality of presentations using Appendix B.</li>

 <li>Instructor’s grade (<strong>40%</strong>). Instructor will grade the quality of presentations using Appendix C. The presentation mark, broken into the marks from peers, TA and instructor and including comments will be send by email to the group leader before the final exam.</li>

</ol>













<strong>Name of the presenting group</strong>         ………………………….……………………………………………




Remarks:

<ul>

 <li>For each question enter grade between 0 and <strong><u>20</u></strong> or between 0 and <strong><u>5</u></strong> (0 being the worst, 20 or 5 being the best)  Optionally please add comments (both positive and negative); they will be passed along to the presenting group.</li>

 <li>Average of these grades across all groups will be used to come up with the 30% of the peer-evaluation component.</li>

</ul>




<table width="681">

 <tbody>

  <tr>

   <td colspan="2" width="578"><strong><em>remarks </em></strong></td>

   <td width="103"><strong><em>grade </em></strong></td>

  </tr>

  <tr>

   <td colspan="2" width="578"><strong>Quality of Presentation</strong>Did you find the presentation interesting? Were the presenters prepared? Did you understand the topics covered in the presentation? How much did you learn? Was there anything significant missing? Were the conclusions and discussion of results covered sufficiently? How would you rate handling the discussion/questions?</td>

   <td width="103">min 0, max <strong><u>20</u></strong>  ……</td>

  </tr>

  <tr>

   <td colspan="2" width="578"><strong>Presentation Style</strong>Quality of presentation style – Was it finished on time? Too fast/slow? Well presented? Was the presenter just reading the slides or was (s)he presenting the material beyond the content of the slides? Was there an eye contact?</td>

   <td width="103">min 0, max <strong><u>5</u></strong>  ……</td>

  </tr>

  <tr>

   <td colspan="2" width="578"><strong>Quality of Slides</strong>Quality of slides – Did you find the slides too crowded? Too brief? Too many? Easy to read? Was the layout of individual slides appropriate and consistent? How was the overall quality of the organization, in terms of the order and flow of the slides?</td>

   <td width="103">min 0, max <strong><u>5</u></strong>   ……</td>

  </tr>

  <tr>

   <td width="141"><strong>Additional </strong><strong>Comments </strong></td>

   <td width="438"><strong> </strong></td>

   <td width="103"></td>

  </tr>

  <tr>

   <td width="141"></td>

   <td width="438"></td>

   <td width="103"></td>

  </tr>

 </tbody>

</table>

<strong> </strong>

<strong>                                                 </strong>

TA’s Evaluation Form for Project Presentations




<strong>Date</strong> (circle the correct date)              December 3, 2019    or    December 5, 2019







<h1><strong>Name of the presenting group</strong>         ………………………….………………………………………</h1>







<table width="623">

 <tbody>

  <tr>

   <td width="387"><strong><em>TASK </em></strong></td>

   <td width="104"></td>

   <td width="84"><strong><em>grade </em></strong></td>

   <td width="48"><em>max grade </em></td>

  </tr>

  <tr>

   <td width="387"> Quality of <em>Motivation for the proposed design</em> </td>

   <td width="104"></td>

   <td width="84"><strong> </strong></td>

   <td width="48">4</td>

  </tr>

  <tr>

   <td width="387">Quality of the <em>Description of the proposed design</em></td>

   <td width="104"></td>

   <td width="84"><strong> </strong></td>

   <td width="48">4</td>

  </tr>

  <tr>

   <td width="387"> Quality of the <em> Discussion and comparison of the quality </em><em> </em></td>

   <td width="104"></td>

   <td width="84"><strong> </strong></td>

   <td width="48">4</td>

  </tr>

  <tr>

   <td width="387"> Quality of <em>Conclusions</em> </td>

   <td width="104"></td>

   <td width="84"><strong> </strong></td>

   <td width="48">8</td>

  </tr>

  <tr>

   <td width="387"> Quality of the Presentation and Presentation Style </td>

   <td width="104"></td>

   <td width="84"><strong> </strong></td>

   <td width="48">10</td>

  </tr>

  <tr>

   <td width="387"></td>

   <td width="104">TA’s total mark</td>

   <td width="84">             <strong> </strong></td>

   <td width="48"><strong>30 </strong></td>

  </tr>

 </tbody>

</table>




<strong>             </strong>

Instructor’s Evaluation Form for Project Presentations




<strong>Date</strong> (circle the correct date)              December 3, 2019    or    December 5, 2019







<h1><strong>Name of the presenting group</strong>         ………………………….………………………………………</h1>







<table width="623">

 <tbody>

  <tr>

   <td width="256"><strong><em>TASK </em></strong></td>

   <td width="234"><strong><em>comments </em></strong></td>

   <td width="84"><strong><em>grade </em></strong></td>

   <td width="48"><em>max grade </em></td>

  </tr>

  <tr>

   <td width="256">Submission of presentation on time</td>

   <td width="234">(up to -4 points penalty)</td>

   <td width="84"><strong> </strong></td>

   <td width="48">Y / 0</td>

  </tr>

  <tr>

   <td width="256">Presentation finished on time</td>

   <td width="234">(up to -4 points penalty)</td>

   <td width="84"><strong> </strong></td>

   <td width="48">Y / 0</td>

  </tr>

  <tr>

   <td colspan="2" width="491"> Quality of <em>Motivation for the proposed design</em> </td>

   <td width="84"><strong> </strong></td>

   <td width="48">5</td>

  </tr>

  <tr>

   <td colspan="2" width="491">Quality of the <em>Description of the proposed design</em></td>

   <td width="84"><strong> </strong></td>

   <td width="48">5</td>

  </tr>

  <tr>

   <td colspan="2" width="491"> Quality of the <em> Discussion and comparison of the quality </em><em> </em></td>

   <td width="84"><strong> </strong></td>

   <td width="48">5</td>

  </tr>

  <tr>

   <td colspan="2" width="491"> Quality of <em>Conclusions</em> </td>

   <td width="84"><strong> </strong></td>

   <td width="48">10</td>

  </tr>

  <tr>

   <td colspan="2" width="491"> Quality of the Presentation and Presentation Style </td>

   <td width="84"><strong> </strong></td>

   <td width="48">15</td>

  </tr>

  <tr>

   <td colspan="2" width="491">Instructor’s total mark</td>

   <td width="84">             <strong> </strong></td>

   <td width="48"><strong>40 </strong></td>

  </tr>

 </tbody>

</table>





