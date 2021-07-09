# Como usar o useCallback no React

## O que é o useCallback
O `useCallback` é um hook do React que permite a otimização de funções. </br>
Mas como ele faz isto ? Você intendera agora: </br>
Basicamente cada vez que um componente entra em redenização no React todas as </br> 
propiedades e alguns filhos desse componente são recriadas na Virtual DOM, para empedir </br> 
que o React gaste processamento recriando valores que não irao mudar existe </br>
alguns Hooks, para valores existe o `useMemo` e para funções existe o `useCallback`</br>
diferente do que algumas pessoas pensam o `useCallback` não torna a sua função mais </br>
rapida, mas sim evita que ela seja recriada desnesariamente.</br>

## Como usar o useCallback
Temos o uso do `useCalback` assim: </br>
`useCallback(fn,dp)`</br>
Onde `fn` é a funcao que você usaria naturalmente como: `() => {console.log(inputValue)}`</br>
Vemos que a funcao usa o valor de `inputValue` que é um estado criado com: </br>
`const [inputValue,setInputValue] = useState('')` </br>
Então devemos atualizar a nossa função toda vez que o valor de `inputValue` mudar,</br>
ai você se pergunta o React não faz isso automaticamente ?. E a resposta é não, porque </br>
ele não sabe as propiedades que nossa função usa então temos que informar para ele </br>
atravez do parametro `dp` que é um Array, e no nosso caso ele será: `[inputValue]`</br>
o retorno do `useCallback` será a sua funçao que você podera usar normalmente.</br>
Tenho que falar que a funçao é criada na criação do componente e cada vez que uma das </br>
propiedades do Array muda seu estado.</br>
Mas se o Array for vazio `[ ]`, a função só sera criada na criação do componente 

## Quando usar o useCallback
Você acabou de ver que o `useCallback` é um hook muito poderoso para a otimização de </br>
aplicações React, então você pensa que deve usar este hook em todas funções criadas </br>
na sua aplicação, mas não pense assim pois para ele funcionar desse jeito ele precisa </br>
validar se algum dos valores passados no Array `dp` mudou e para isso ele usa o </br>
algoritimo de [Shallow Compare](https://pt-br.reactjs.org/docs/shallow-compare.html) , 
e como você esta pensando isso gasta  processamento.</br>
Então basicamente tem vezes que o processamento gasto pelo algoritimo de Shallow Compare </br>
é maior que deixar com que o React recrie aquela função, mas ai fica a questão: </br>
> Quando usar o useCallback ?
###### Então aconcelhamos você usar ele em um desses casos:
* Quando a função é muito grande e você acha muito pessada recria-la.
* Quando essa função é passada para filhos desse componente principalmente </br>
se eles usam a função `memo()` ou são muito grandes.
* Quando seu componente tem muitas atualizações de estados, mas a função usa </br>
poucos ou nem um estado .