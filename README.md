# Consistency-Guided Temperature Scaling (CTS)
Official repository of our work on out-of-domain(OOD) calibration with **consistency-guided temperature scaling (CTS)**. Our paper, a collaborative effort between KAIST and Purdue University, will be published in **AAAI 2024** soon. \
This repository includes a quick summary of our method and a code implementation.

- **Title**: Consistency-Guided Temperature Scaling Using Style and Content Information for Out-of-Domain Calibration
- **Full paper link**: to be announced soon

> TL;DR: Our proposed CTS is a new method for **OOD calibration**, which is crucial for trustworthy AI systems but has been less explored so far. Motivated by our observation that over-confidence stemming from inconsistent predictions is the main obstacle to OOD calibration, our CTS takes consistencies into account in terms of two different aspects - **style and content** - which are the key components that can well-represent data samples in multi-domain settings.


## Quick Summary
### # Key Insights
The key intuition behind our method is that **keeping the consistency of predictions under style and content shifts can improve the reliability of the prediction on the unseen domain**, resulting in good OOD calibration.


| ![Image Alt text](/fig/intuitions.png) | 
|:--:| 
| *(a-b) Correlations between variance of predictions and OOD calibration performance for test samples from different target domains. Samples with high variance are more likely to show poor OOD calibration performance in both cases of style and content shifts.* 
*(c-d) Reliability diagrams for comparing calibration tendency depending on the variance of predictions under style/content variations. It shows that the poor calibration performance of high variance samples (pink line) arises from the over-confident predictions.* |



### # Proposed method: CTS
Inspired by the empirical observations above, we propose our CTS, which **optimizes the temperature such that the predictions are more consistent across variations in style/content**.
Finally, our CTS can improve OOD calibration on arbitrary target domains by optimizing domain-invariant temperature. 

| ![Image Alt text](/fig/method_fig_230815.jpg) | 
|:--:| 
| *Overview of our Consistency-guided Temperature Scaling (CTS)* |
> Step 1. Samples from the same class on the validation set (of source domains) are fed into the model in a pair-wise manner. \
> Step 2. Three different intermediate features (original, style shifted, content shifted) are generated. \
> Step 3. Style shifted logits $𝑓^{(𝑠_𝑗, 𝑐_𝑖)}$  and content shifted logits $𝑓^{(𝑠_𝑖, 𝑐_𝑗)}$ are created. \
> Step 4. Our temperature $𝑻_{𝑪𝑻𝑺}^∗$ is optimimized by combining style loss ($𝑳_{style}$), content loss ($𝑳_{content}$) and original NLL loss ($𝑳_{NLL}$).


