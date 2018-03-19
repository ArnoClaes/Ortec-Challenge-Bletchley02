# Ortec Challenge Bletchley02
The present implementation of the Ortec-Challenge consists of 3 underlying documents excluding the README.md document: OrtecChallenge.ipynb, TEMPLATE_1, and TEMPLATE_2. 

When running the Ortec Challenge python notebook, the zipfile that contains the templates should be uploaded. Afterwards, the notebook can be runned seemlessly.

This solution can be divided into three sections: data preparation, model building, prediction & entity confirmation. 

In data preparation 11 targets are divided into ignore, simple and complex classes. The ignore target will be excluded from the final input of the present solution. The simple targets include: Sender Name, Sender KVK, Sender IBAN, Invoice Reference, Total, Conditions. The complex targets include the date, item, item quantities, and item totals. The reason for dividing into simple and complex targets is attributed to the need for two models; one that performs good in identifying easily identifiable elements, and another that performs good in identifying more noisy elements, e.g. item descriptions.

In model building the ultimate architecture is a 1-dimensional convolutional neural network for both models. The models are trained by the sparse categorical crossentropy loss metric, whilst being tuned by the adam-optimizer. Furthermore, the models consider 35 characters before and after the main character fed to the neural network (PADDING). Also, the best predictive performance in terms of validation accuracy is found by model 1 using 2 epochs for training the simple model, and 1 epoch for training the complex model.

In prediction & entity confirmation the output of the previous step is grouped and sorted by target categories. In order to provide one complete prediction, these outputs are stacked. Subsequently, target 'KVK' is used as the main input for performing a google-search, in an attempt to cross-reference the 'KVK' with 'Company Name'. The present program ultimately performs this cross-reference on multiple results returned from the google-search and finds the closest match. 

Please note: the closest match function only confirms an entity by KVK number if the predictive model outputs a name and the name output is not noisy.
