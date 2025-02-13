# PyMCDM - Re-identify

Python 3 library for re-identification of multi-criteria models.

Documentation is avaliable on [readthedocs](https://pymcdm-reidentify.readthedocs.io/en/latest/).

___

# Installation

You can download and install `pymcdm-reidentify` library using pip:

```Bash
pip install pymcdm-reidentify
```

You can run all tests with following command from the root of the project:

```Bash
python -m unittest -v
```

# Available methods

The library contains:

* Re-identification methods:

| Acronym            	     | Method Name                                                   | Reference  |
|:-------------------------|---------------------------------------------------------------|:----------:|
| SESP             	       | Stochastic Expected Solution Point                            | [[1]](#c1) |
| SITCOM              	    | Stochastic IdenTifiCation Of Models                           | [[2]](#c2) |
| SITW              	      | Stochastic IdenTification of Weights                          | [[3]](#c3) |
| SITWLocal              	 | Stochastic IdenTification of Weights - Local weights approach | [[4]](#c4) |
| STFN              	      | Stochastic Triangular Fuzzy Numbers                           | [[5]](#c5) |
| STRFN              	     | Stochastic Trapezoidal Fuzzy Number                           |     --     |

* Normalization methods:

| Acronym            	 | Method Name         | Reference  |
|:---------------------|---------------------|:----------:|
| FN             	     | Fuzzy Normalization | [[6]](#c6) |

* COMET Tools

| Acronym            	   | Method Name                                                                   | Reference  |
|:-----------------------|-------------------------------------------------------------------------------|:----------:|
| MLExpert             	 | Class which allows to evaluate CO in COMET using any Machine Learning method. | [[7]](#c7) |

___
# Usage example

Below is a simple example of the re-identification of a decision-making model.
For more examples with explanation see [examples]().

```python
import numpy as np
from mealpy.swarm_based.PSO import OriginalPSO
from pymcdm.methods import TOPSIS
from pymcdm_reidentify.methods import SITW

# Define exemplary data
# Decision matrix
matrix = np.random.random((1000, 2)) 
# Types of critieria
types = np.array([-1, 1]) # 
# Unknown expert criteria weights 
# For purpose of re-identifiaction method
weights = np.random.random((2))
weights = weights / np.sum(weights) 

# Define exemplary unknown expert model
preference = TOPSIS()(matrix, weights, types)
rank = TOPSIS().rank(preference)

# Create re-identifiaction object
stoch = OriginalPSO(epoch=1000, pop_size=100)
model = SITW(stoch.solve, TOPSIS(), types)

# Fit model
model.fit(matrix, rank, log_to=None)
```

# References

<a name="c1">[1]</a> Kizielewicz, B., Więckowski, J., & Sałabun, W. (2024, June). SESP-SPOTIS: Advancing Stochastic Approach for Re-identifying MCDA Models. In International Conference on Computational Science (pp. 281-295). Cham: Springer Nature Switzerland.

<a name="c2">[2]</a> Kizielewicz, B. (2022). Towards the identification of continuous decisional model: the accuracy testing in the SITCOM approach. Procedia Computer Science, 207, 4390-4400.

<a name="c3">[3]</a> Kizielewicz, B., Paradowski, B., Więckowski, J., & Sałabun, W. (2022). Identification of weights in multi-cteria decision problems based on stochastic optimization.

<a name="c4">[4]</a> Kizielewicz, B., Więckowski, J., Paradowski, B., Shekhovtsov, A., Wątróbski, J., & Sałabun, W. (2024, April). Stochastic Approaches for Criteria Weight Identification in Multi-criteria Decision Analysis. In Asian Conference on Intelligent Information and Database Systems (pp. 40-51). Singapore: Springer Nature Singapore.

<a name="c5">[5]</a> Kizielewicz, B., & Dobryakova, L. (2023). Stochastic Triangular Fuzzy Number (S-TFN) Normalization: A New Approach for Nonmonotonic Normalization. Procedia Computer Science, 225, 4901-4911.

<a name="c6">[6]</a> Kizielewicz, B., Więckowski, J., Paradowski, B., & Sałabun, W. (2022, July). Dealing with nonmonotonic criteria in decision-making problems using fuzzy normalization. In International conference on intelligent and fuzzy systems (pp. 27-35). Cham: Springer International Publishing.

<a name="c7">[7]</a> Kizielewicz, B., Więckowski, J., & Jankowski, J. (2023, September). Towards Re-identification of Expert Models: MLP-COMET in the Evaluation of Bitcoin Networks. In Special Sessions in the Information Technology for Business and Society Track of the Conference on Computer Science and Intelligence Systems (pp. 3-22). Cham: Springer Nature Switzerland.


 




