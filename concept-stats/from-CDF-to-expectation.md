[![purple-pi](https://img.shields.io/badge/Rendered%20with-Purple%20Pi-bd00ff?style=flat-square)](https://github.com/nschloe/purple-pi?activate)


# What 

- CDF에서 Expectation을 구할 수 있는 방법을 알아보자. 

# Why 

- 이를 통해 Markov inequality를 쉽게 도출할 수 있다. 

# How 

## Change of Integral 

https://mathinsight.org/double_integral_change_order_integration_examples

- 적분의 순서를 바꾸는 것이다. 
- 만일 $dx dy$ 순으로 적분이 이루진다고 하자. 이때, 먼저 적분되는 변수에 따라서 뒤에 적분되는 변수가 연동된다. 
- 순서를 바꾼다면 어떻게 될까? 적분의 순서가 바뀌는 경우가 발생한다. 


## From CDF to Expectation 

https://stats.stackexchange.com/questions/10159/find-expected-value-using-cdf

$$
1-F_X(x) = P(X \geq x) = \int_{x}^{\infty} f_X(t)dt, 
$$

$$
\int_{0}^{\infty} (1-F_X(x)) dx = \int_{0}^{\infty} P(X \geq x) dx = \int_{0}^{\infty} \int_{\infty}^{x} f_X(t) dt dx
$$

여기서 적분 순서를 바꿔보자. $dx$가 앞으로 오면, 앞의 내용을 응용해서 적분 구간을 설정할 수 있다. 

$$
\int_{0}^{\infty} (1-F_X(x)) dx = \int_{0}^{\infty} \int_{0}^{t} f_X(t) dx dt 
$$

$$
\left[\frac{x^3}{3}+x\right]_1^2
$$

$$
\int_{0}^{\infty} \left[ xf_X(t)\right]_0^t dx 
$$


- 이 식이 성립하려면 RV이 비음이어야 한다는 점에 주목하자. 

# Visual Proof of Markov Inequality 

![](https://github.com/anarinsk/til/blob/master/concept-stats/image.png?raw=true)

