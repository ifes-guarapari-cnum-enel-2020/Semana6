# Semana6
![](https://github.com/ifes-guarapari-cnum-enel-2020/Semana6/workflows/Julia%20CI/badge.svg)

Atividades Pedagógicas Não Presenciais

## Métodos de ponto fixo
Ponto fixo de uma função é quando o valor do domínio corresponde ao mesmo valor da imagem. Dessa forma, o método consiste em repetir sucessivamente uma função de interação até se encontrar o ponto fixo, que corresponderá ao zero da função original. O método de Newton-Raphson utiliza-se do método do ponto fixo por meio da equação da reta tangente (derivada) da função. O método da secante é uma variação de Newton-Raphson, em que a sequência de raízes de linhas secantes é usada para aproximar o valor do ponto fixo.

O método do ponto fixo se utiliza de uma função auxiliar em que o valor do domínio corresponde ao mesmo valor da imagem.

![formula](https://render.githubusercontent.com/render/math?math=e^x=x%2B2)

![formula](https://render.githubusercontent.com/render/math?math=f(x)=e^x-x-2)

![formula](https://render.githubusercontent.com/render/math?math=g(x)=e^x-2=x)

![formula](https://render.githubusercontent.com/render/math?math=g(x)=\ln(x%2B2)=x)
```julia
using .MathConstants:e

f(x) = e^x-x-2

error = 10^-3

function fixedpoint(a,g)
 x = g(a)
 while abs(x-a) > error
  a = x
  x = g(a)
 end
 return x
end

g(x) = log(x+2)
r = fixedpoint(1,g)
println(r)

g(x) = e^x-2
r = fixedpoint(-1,g)
println(r)
```

No método de Newton-Raphson, se um zero de dada função continuamente diferenciável, é possível usar a iteração do ponto fixo, como interseção entre o eixo das abscissas e a reta tangente ao gráfico da função.

![formula](https://render.githubusercontent.com/render/math?math=g(x)=x-\frac{f(x)}{{f}'(x)})

![formula](https://render.githubusercontent.com/render/math?math=g(x)=x-\frac{e^x-x-2}{e^x-1})
```julia
g(x) = x-((e^x-x-2)/(e^x-1))
r = fixedpoint(1,g)
println(r)
r = fixedpoint(-1,g)
println(r)
```

A ideia do método da secante é evitar a necessidade de conhecer a derivada analítica, ou seja, dada uma função, a ideia é aproximar a derivada pela razão fundamental da função secante.

![formula](https://render.githubusercontent.com/render/math?math=g(x)=x-h(x))

![formula](https://render.githubusercontent.com/render/math?math=h(x)=\frac{x_af_b-x_bf_a}{f_b-f_a})
```julia
function secant(a,b)
 g(a,b) = (a*f(b)-b*f(a))/(f(b)-f(a))
 x = g(a,b)
 while abs(x-b) > error
  a = b
  b = x
  x = g(a,b)
 end
 return x
end

r = secant(1,2)
println(r)

r = secant(-2,-1)
println(r)
```
