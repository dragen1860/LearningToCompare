
# Ominiglot
| Model                               	| Fine Tune 	| 5-way Acc.    	|               	| 20-way Acc   	|               	|
|-------------------------------------	|-----------	|---------------	|---------------	|--------------	|---------------	|
|                                     	|           	| 1-shot        	| 5-shot        	| 1-shot       	| 5-shot        	|
| MANN                                	| N         	| 82.8%         	| 94.9%         	| -            	| -             	|
| Matching Nets                       	| N         	| 98.1%         	| 98.9%         	| 93.8%        	| 98.5%         	|
| Matching Nets                       	| Y         	| 97.9%         	| 98.7%         	| 93.5%        	| 98.7%         	|
| MAML                                	| Y         	| 98.7+-0.4%    	| 99.9+-0.1%    	| 95.8+-0.3%   	| 98.9+-0.2%    	|
| Meta-SGD                            	|           	| 99.53+-0.26%  	| 99.93+-0.09%  	| 95.93+-0.38% 	| 98.97+-0.19%  	|
| TCML                                	|           	| 98.96+-0.20% 	| 99.75+-0.11% 	| 97.64+-0.30% 	| 99.36+-0.18% 	|
| Learning to Compare                 	| N         	| 99.6+-0.2%   	| 99.8+-0.1%    	| 97.6+-0.2%   	| 99.1+-0.1%    	|
| Ours(Res18, flatten features, 2 fc) 	| Y         	| 98.99% ,48120ep, 20b            	|       99.6%,48620ep, 5b         	|    96.99%,153920ep,20b            	|   97.2%, 63220ep,2b         	|
|naive, omni.py  | N | 99.6% | 99.8% |  98.88% |   |
|naive, omni.py, 2days  | N | 99.80% | 100% |  98.88% |   |




# mini-Imagenet

## Deeper version

| Model                               | Fine Tune | 5-way Acc. |        | 20-way Acc |        |
|-------------------------------------|-----------|------------|--------|------------|--------|
|                                     |           | 1-shot     | 5-shot | 1-shot     | 5-shot |
| Matching Nets                       | N         | 43.56%     | 55.31% | 17.31%     | 22.69% |
| Meta-LSTM                           |           | 43.44%     | 60.60% | 16.70%     | 26.06% |
| MAML                                | Y         | 48.7%      | 63.11% | 16.49%     | 19.29% |
| Meta-SGD                            |           | 50.49%     | 64.03% | 17.56%     | 28.92% |
| TCML                                |           | 55.71%     | 68.88% | -          | -      |
| Learning to Compare           	  | N         | 57.02%     | 71.07% | -          | -      |
| ***reproduction*				      | N         |  55.2%     |    68.8% |          |        | 
| ***Ours*				     		  | N         |  53.0%     |    64.6% |          |        | 

## Naive version

| Model                               | Fine Tune | 5-way Acc. |        | 20-way Acc |        |
|-------------------------------------|-----------|------------|--------|------------|--------|
|                                     |           | 1-shot     | 5-shot | 1-shot     | 5-shot |
| Matching Nets                       | N         | 43.56%     | 55.31% | 17.31%     | 22.69% |
| Meta-LSTM                           |           | 43.44%     | 60.60% | 16.70%     | 26.06% |
| MAML                                | Y         | 48.7%      | 63.11% | 16.49%     | 19.29% |
| Meta-SGD                            |           | 50.49%     | 64.03% | 17.56%     | 28.92% |
| Learing to compare                          |     N      | 51.38%     |67.07%| -    | - |
| naivern.py      (naive version)     |     N      | 53.8%     |	67.5%	| -    | - |
| naivern.py      (naive version, avg pool, 9e-4) |     N      | 56.0%->60.8%, 2days     |	68.1%	| -    | - |
| naive5.py      (naive version, avg pool, sum over features) |     N      |      |	72.7| -    | - |
| naivesum.py      (naive version, avg pool, sum over features, concat all setsz after f) |     N      |      |	70.8| -    | - |


## Simplified Deep version

| Model                               | Fine Tune | 5-way Acc. |        | 20-way Acc |        |
|-------------------------------------|-----------|------------|--------|------------|--------|
|                                     |           | 1-shot     | 5-shot | 1-shot     | 5-shot |
| Matching Nets                       | N         | 43.56%     | 55.31% | 17.31%     | 22.69% |
| Meta-LSTM                           |           | 43.44%     | 60.60% | 16.70%     | 26.06% |
| MAML                                | Y         | 48.7%      | 63.11% | 16.49%     | 19.29% |
| Meta-SGD                            |           | 50.49%     | 64.03% | 17.56%     | 28.92% |
| TCML                                |           | 55.71%     | 68.88% | -          | -      |
| Learning to Compare           	  | N         | 57.02%     | 71.07% | -          | -      |
| rn.py, 463bottleneck, 6x6, conv->maxpool   |     N      | 53.3%     |		| -    | - |
| simrn.py, 111basicneck                   |     N      | 55.4%     |	66.7%	| -    | - |
 


* 6x6 spational relation seems good, meaning larger spatial will lead to better
* naive version overcome all, meaning simplier nn 
* the conv after repnet will occupy very huge gpu memory, but only reduce it will not lead to good, 51% on 5-way-1shot
* avg pooling
* sum on feature can not converge
* g network can enlarge since it have more batch
* spatial d is very critical, small d lead to faster converge, however, when it read 50%, it read the roof. Large `d` will converge slow but 
have higher possibilityes.
* reduce Naive 4 conv to 3 conv will not improve performance(55.7%), and reduce d of spatial rn will not improve as well().
* add BatchNorm1d in self.g is extremely slow, will cost 3x time compared with none BN.



>naivesum 
0.712, 0.717, 0.736, 0.643, 0.672, 0.661, 0.653, 0.739, 0.677, 0.736, 0.741, 0.701, 0.603, 0.661, 0.693, 0.749, 0.709, 0.739, 0.659, 0.720, 0.688, 0.627, 0.717, 0.624, 0.715, 0.712, 0.741, 0.707, 0.704, 0.683, 0.683, 0.701, 0.728, 0.707, 0.715, 0.685, 0.720, 0.789, 0.680, 0.651, 0.664, 0.720, 0.784, 0.669, 0.744, 0.712, 0.600, 0.755, 0.717, 0.648, 0.595, 0.715, 0.731, 0.723, 0.680, 0.677, 0.699, 0.755, 0.688, 0.803, 0.707, 0.672, 0.651, 0.717, 0.747, 0.707, 0.744, 0.696, 0.712, 0.669, 0.717, 0.651, 0.704, 0.672, 0.696, 0.699, 0.645, 0.691, 0.768, 0.648, 0.685, 0.653, 0.616, 0.675, 0.629, 0.685, 0.736, 0.651, 0.691, 0.739, 0.635, 0.632, 0.707, 0.685, 0.693, 0.661, 0.643, 0.685, 0.699, 0.664, 0.773, 0.677, 0.709, 0.712, 0.659, 0.659, 0.733, 0.739, 0.787, 0.643, 0.747, 0.669, 0.643, 0.699, 0.733, 0.680, 0.680, 0.664, 0.704, 0.683, 
accuracy: 0.694533333333 sem: 0.00744224200062

>slave2: original version, train for 24hours
0.707, 0.754, 0.689, 0.677, 0.677, 0.701, 0.704, 0.733, 0.738, 0.674, 0.677, 0.723, 0.717, 0.724, 0.708, 0.686, 0.702, 0.684, 0.674, 0.696, 0.744, 0.727, 0.793, 
accuracy: 0.709146537842 sem: 0.0130249463636


>gpu: g+fc, f+fc
0.723, 0.750, 0.670, 0.693, 0.703, 0.707, 0.737, 0.727, 0.710, 0.673, 0.750, 0.673, 0.780, 0.650, 0.703, 0.623, 0.773, 0.823, 0.557, 0.693, 0.717, 0.720, 0.707, 0.667, 0.753, 
accuracy: 0.707333333333 sem: 0.0222004602888

>p100:
0.627, 0.690, 0.637, 0.703, 0.700, 0.700, 0.667, 0.617, 0.690, 0.673, 0.723, 0.680, 0.720, 0.750, 0.697, 0.740, 0.713, 0.777, 0.693, 0.670, 0.743, 0.770, 0.730, 0.730, 0.713, 
accuracy: 0.702133333333 sem: 0.0167383742684



