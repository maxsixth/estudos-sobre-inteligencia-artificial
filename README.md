# Redes Neurais



> **Qual é o computador mais FODIDO do mundo?**


![cérebrooooo](https://raw.githubusercontent.com/suissa/estudos-sobre-inteligencia-artificial/master/assets/images/brain1.jpg)


> **PERFEITO!** 
> 
> Agora imagine tentar emular ele em um computador!!!



![daaannnn](http://i.giphy.com/GAgI0RcNxTOmI.gif)


> **Pois é!**
> 
> Aproveitando-se desse poder de aprendizagem já foram descobertas diversas coisas/paradas/fitas que os cientistas ainda não conheciam, **se te falarem que isso é o futuro eles estão errados!**

> **Isso não é apenas nosso futuro como também o presente e **EU, Suissa,** tenho certeza que terá um impacto GIGANTESCO na nossa vida.**

Posso falar apenas nos trabalhos que tenho que posso implementar facilmente esse aprendizado de máquina, um exemplo claríssimo é em cima de BOTS que interagem com os usuários. Eu e meu aluno, [Rogério Munhoz](https://github.com/rjmunhoz), criamos um [BOT para Telegram](https://github.com/Webschool-io/Bot-Telegram-BeMEAN) focado em JS e para aprender, o qual já executa as mesmas funções para o Facebook também, a única coisa que realmente falta é um sistema de *Machine Learning* para fazermos com que esse [BOT](https://github.com/Webschool-io/Bot-Telegram-BeMEAN) interaja mais naturalmente e ainda aprenda com isso.


Eu poderia escrever 1 artigo apenas com as últimas descobertas feitas a partir de Redes Neurais, mas em vez disso deixarei alguns links abaixo:


- [The wonderful and terrifying implications of computers that can learn - 2014](https://www.ted.com/talks/jeremy_howard_the_wonderful_and_terrifying_implications_of_computers_that_can_learn)
- [The future of early cancer detection? - 2014](https://www.ted.com/talks/jorge_soto_the_future_of_early_cancer_detection)
- [How computers are learning to be creative - 2016](https://www.ted.com/talks/blaise_aguera_y_arcas_how_computers_are_learning_to_be_creative)

## O Cérebro

Creio que antes de entrar nesse assunto devo entender um pouco da estrutura do cérebro já que as Redes Neurais tendem a *"imita-lo"*, então vamos à Wikipedia:

> O cérebro é composto de duas grandes classes de células, neurônios e células das glia. Neurônios recebem mais atenção, mas, na verdade, as células gliais são mais frequentes, formando uma proporção de pelo menos 10 para 1. Existem diversos tipos de células gliais, que realizam um grande número de funções importantes como: suporte estrutural, suporte metabólico, isolamento, e guia para o desenvolvimento.

Bom sabemos que as Redes Neurais são baseadas nos neurônios, mas acredito que mais para frente ainda acharemos um lugar para as células da glia. :p

Olhe que interessante:

> As principais funções das células da glia são cercar os neurônios e mantê-los no seu lugar, fornecer nutrientes e oxigênio para os neurônios, isolar um neurônio do outro, destruir patógenos e remover neurônios mortos.

Veremos mais para frente se achamos um uso para ela.

## Metodologia de Estudo

Como vocês já devem saber que sou meio louco por isso gosto de testar formas diferentes de aprender, eu já conhecia todo o conceito sobre [Redes Neurais]() mas nunca tinha feito nada com ela muito menos programado uma. Entretanto hoje, no meu aniversário 20/11, um broder meu e que provavelmente fará um curso sobre [Machine Learning](https://en.wikipedia.org/wiki/Machine_learning) na [Webschool.io](http://webschool.io/) próximo ano, pediu-me que o ajudasse a refatorar um pouco seu código pois ele está mais acostumado com C/C++ e claro eu fui com a maior sede ao pote.

Porém ainda estava meio nebuloso algumas coisas pois a nomenclatura que ele usou para seus parâmetros não fazia muito sentido, para mim. Então pensei:

> **Bora modularizar/atomizar essa porra toda aí depois eu estudo e só monto o programa usando essas funções!**

![](http://i.giphy.com/JwwYTeuOHhEB2.gif) 


> Nesse estudo eu irei separar todas as funções para **entender CADA PARTE antes até de entender o todo**, pois a ideia é que depois de entender tod as partes eu refaça o código original sem precisar me basear nele.

Não irei abordar a parte matemática nesse primeiro momento, iremos estudar os conteúdos relacionados somente quando for necessário.

Nosso código para embasamento está cheio de `this`, vindo do C para JS no frontend e agora irá para módulos em Node.js, por exemplo essa função:

```js
this.Mutate = function(chromo)
{
    //traverse the chromosome and mutate each weight dependent
    //on the mutation rate
    for (i=0; i < chromo.length; ++i)
    {
        //do we perturb this weight?
        if (RandFloat() < this.m_dMutationRate)
        {
            //add or subtract a small value to the weight
            chromo[i] += (RandomClamped() * MAX_PERTUBATION);
        }
    }
    return chromo;
};
```

Na minha mão já virou:

```js
const RandFloat = () => Math.random() 
const RandomClamped = () => RandFloat() - RandFloat()
const Mutate = (chromo) => chromo.map((e, i) => (RandFloat() < 0.3)
                                                ? e += (RandomClamped() * 0.3)
                                                : e)

module.exports = Mutate
```

Logo mais veremos o que é essa função.

## Atomic Design

> Você deve se questionar se eu sou retardado mental para querer aplicar Atomic Design em Redes Neurais, neh?!




...





Pois então pense aqui comigo...

O elemento básico de uma rede neural são os neurônios, pois são eles que fazem a conexão entre os dados, assim como no nosso cérebro, correto?

Sabendo disso podemos deduzir que eles são nossos [átomos](https://pt.wikipedia.org/wiki/%C3%81tomo), beleza?!

Porém dentro das Redes Neurais cada neurônio possui pesos que serão usados para calcular sua saída, não vamos entrar nos detalhes técnicos agora, vamos nos ater ao conceito do Atomic Design.

Se o neurônio é nosso átomo e possui 1 ou mais pesos "dentro dele", esses pesos são o quê?


![quarks](https://raw.githubusercontent.com/suissa/estudos-sobre-inteligencia-artificial/master/assets/images/quarks.jpg)


Caso você não conheça a imagem acima, ela representa os [Quarks](https://pt.wikipedia.org/wiki/Quark) conhecidos pela Física Quântica atualmente...

> O quark, na física de partículas, é uma partícula elementar e um dos dois elementos básicos que constituem a matéria (o outro é o lépton). Quarks se combinam para formar partículas compostas chamadas hádrons; os mais estáveis desse tipo são os prótons e os nêutrons, que são os principais componentes dos núcleos atômicos[1]. Devido a um fenômeno conhecido como confinamento, quarks nunca são diretamente observados ou encontrados isoladamente; 

*fonte: [https://pt.wikipedia.org/wiki/Quark](https://pt.wikipedia.org/wiki/Quark)*

ps: caso você queira ver o uso de [Hadrons, confira meu Atomic Design no backend com Node.js](https://github.com/Webschool-io/Node-Atomic-Design-Modelo-Padrao#hádrons)

Ligando uma coisa na outra podemos afirmar que esses pesos são os quarks, pois seu agrupamento que "forma" o átomo/neurônio.

> Até aí nada de novo, né? 
> 
> Mas então porque comecei falando disso?

## Neurônio

Comecei por elas pois são os menores elementos que temos na Rede Neural e foi a primeira função que vi [aqui](https://github.com/suissa/estudos-sobre-inteligencia-artificial/blob/master/NN/CNeuralNet.js):

```js
function SNeuron(NumInputs){
    
    this.m_NumInputs = NumInputs + 1;
    this.m_vecWeight = [];
    
    //we need an additional weight for the bias hence the +1
    for (let i = 0; i < NumInputs + 1; ++i) {
        //set up the weights with an initial random value
        this.m_vecWeight[i] = 0.0;
    }
}
```

Como você deve ter visto no código original ele é cheiooooooo de `this` e como você sabe o `this` no JavaScript tem o valor de onde é chamado e não criado, mas beleza!

Então fui analisar ela antes de refatorar:

- entra NumInputs, número de inputs? 
- crio m_vecWeight como array vazio
- popula o array, do tamanho de NumInputs com 0.0

Porém antes de refatorar eu fui tirar algumas dúvidas com o nosso professor de IA da Webschool e perguntei se NumInputs era o número de entradas da Rede Neural e ele me disse que não, que na verdade **é a quantidade de pesos do neurônio!** Fora isso ainda me disse que os pesos **não podem ser 0!**

Pensei:

> POORRRA! Pq não faz o esquema do jeito então?

A primeira coisa que fiz foi modularizar essa função mudando `NumInputs` para `amountWeights` e colocar um valor padrão como randômico:

```js
module.exports = (amountWeights, defaultValue=Math.random()) => 
  Array.from({ length: amountWeights }, () => defaultValue)
```

OK! Agora temos como criar nossos neurônios, mas e aí eles vão para onde??

## Camadas

Quando me deparei com as camadas da Rede Neural logo precisei pesquisar se no nosso cérebro também existem essas camadas e por incrível que pareça existam, mas não como implementado na programação.

> As áreas neocorticais no decurso do seu período de desenvolvimento apresentam uma organização estrutural em seis camadas.
> 
> Córtex homogenético ou isocórtex – córtex inicial e áreas do córtex adulto que mantêm ainda as seis camadas
> Cortex heterogenético ou alocórtex – O paleocórtex e o arquicórtex nunca apresentam estas camadas também.
> 
> 
> ...
> 
> As células do neocórtex estão arranjadas numa série de seis camadas, mais evidentes em algumas áreas do que noutras. Estas camadas são de superficial para profunda:
> 
> Camada I – Camada molecular – pobre em células e com muitas fibras (células anácrinas – células horizontais de cajal);
> 
> Camada II – Camada granular externa – com poucas fibras e muitas células. Origem das fibras de associação curta;
> 
> Camada III – Camada piramidal externa – origem das fibras de associação longa, das fibras comissurais;
> 
> Camada IV – Camada granular interna – apresenta muitas fibras associadas a células. Contém a lâmina externa de Baillarger;
> 
> Camada V – Camada piramidal interna – estão presentes as células piramidais gigantes de Betz. As suas fibras projectam para estruturas subtalâmicas e corpo estriado. Contém a lâmina interna de Baillarger;
> 
> Camada VI – Camada multiforme ou plexiforme – origem das fibras que se projectam para o corpo estriado e suas receptoras. Grande variedade de células (como por exemplo as células de Martinotti que se estendem até à lâmina I).

*fonte: [](https://pt.wikipedia.org/wiki/C%C3%B3rtex_cerebral#Organiza.C3.A7.C3.A3o_cortical)*

Como existem **vários** tipos de Redes Neurais irei abordar o tipo [autoencoder](https://en.wikipedia.org/wiki/Autoencoder) que é composta de pelo menos 3 camadas:

- input/entrada
- hidden/intermediária (Fica melhor q escondida em português)
- output/saída

![](https://upload.wikimedia.org/wikipedia/commons/2/28/Autoencoder_structure.png)


Então antes de sabermos como essas camadas funcionam precisamos ver como criá-las, conseguimos ver isso nessa parte do código original:

```js
function SNeuronLayer(NumNeurons, NumInputsPerNeuron){
    
    this.m_NumNeurons = NumNeurons;
    this.m_vecNeurons = [];
    
    for(var i = 0; i < NumNeurons; i++){
        this.m_vecNeurons.push(new SNeuron(NumInputsPerNeuron));
    }
    
}
```

Analisando-a temos:

- entra `NumNeurons` e `NumInputsPerNeuron`
- define `this.m_NumNeurons` como `NumNeurons`
- define `this.m_vecNeurons` como um *array* vazio
- iteramos de 0 até `NumNeurons`
    + adicionando ao *array* `this.m_vecNeurons` a cada iteração
    + um novo neurônio. // new SNeuron(NumInputsPerNeuron)


> **Ainda não se perguntou onde estão a porra dos `return`s dessas funções?** Pois pergunte-se! :p


Agora vamos modularizar a função acima, renomeando seus parâmetros pois `NumInputsPerNeuron` na verdade significa a quantidade de pesos do neurônio a ser criado nessa camada.

```js
const Neuron = require('./neuron.js')

module.exports = (amountNeurons, amountWeight) => 
  Array.from({length: amountNeurons}, () => Neuron(amountWeight))
```

Podemos ainda deixar assim:

```js
const Neuron = require('./neuron.js')

module.exports = (length, amountWeight) => 
  Array.from({length}, () => Neuron(amountWeight))
```

> Flagrou a malandragem? ;)



### Hora do ADENDO

Você deve ter percebido que utilizei a função `Array.from` correto? Então só explicarei rapidinho como ela funciona, vamos pelo básico:

```js
> Array.from('Suissa')
[ 'S', 'u', 'i', 's', 's', 'a' ]
```

Logo essa função transforma uma *String* em *Array* igual à função `split`, porém ainda existe uma malandragem sapeca nela, podemos passar como objeto o tamanho desejado e de brinde ainda podemos passar uma função que gerará seus valores! Pois é...

```js
> Array.from({length: 8}, () => 0)
[ 0, 0, 0, 0, 0, 0, 0, 0 ]
```

Aliás há uns 5 meses atrás fiz um modulozinho (npm) simples para isso, o [atomic-array](https://www.npmjs.com/package/atomic-array)


### Fim do ADENDO

## Rede Neural

Bom depois que aprendemos a criar as camadas com os neurônios vamos continuar analisando o código, nisso já vemos que inicia a função principal:

```js
function CNeuralNet(I) {
    I = I || {};

    $.extend(I, {
        m_NumInputs: 0,
        m_NumOutputs: 0,
        m_NumHiddenLayers: 0,
        m_NeuronsPerHiddenLyr: 0,
        m_vecLayers: [],
    });

    $.extend(this, I);

    // ...
```

> Apenas com esse pequeno pedaço de código o que você refatoraria?

Vamos começar por aqui:


```js
function CNeuralNet(I) {
    I = I || {};
```

Podemos facilmente refatorar para:


```js
function CNeuralNet(I={}) {
```

Logo após notamos algo estranho:

```js
$.extend(I, {
    m_NumInputs: 0,
    m_NumOutputs: 0,
    m_NumHiddenLayers: 0,
    m_NeuronsPerHiddenLyr: 0,
    m_vecLayers: [],
});

$.extend(this, I);
```

**SIIIIMMMMMM!!!** Esse `$.extend` é do jQuery, não falei que esse código veio do Frontend?

No código acima ele está "colocando" os dados de 1 objeto para outro, porém podemos ou não obter o mesmo resultado usando [Object.assing](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign), deixando o código assim:


```js
Object.assign(I, {
    m_NumInputs: 0,
    m_NumOutputs: 0,
    m_NumHiddenLayers: 0,
    m_NeuronsPerHiddenLyr: 0,
    m_vecLayers: [],
});

Object.assign(this, I);
```

Porém eu modificaria mais uma coisa, o objeto:


```js
{
  m_NumInputs: 0,
  m_NumOutputs: 0,
  m_NumHiddenLayers: 0,
  m_NeuronsPerHiddenLyr: 0,
  m_vecLayers: [],
}
```

Para:

```js
const infos = {
  m_NumInputs: 0,
  m_NumOutputs: 0,
  m_NumHiddenLayers: 0,
  m_NeuronsPerHiddenLyr: 0,
  m_vecLayers: [],
}
Object.assign(I, infos);

Object.assign(this, I);
```

Agora basta unir os dois `Object.assign`s:


```js
const infos = {
  m_NumInputs: 0,
  m_NumOutputs: 0,
  m_NumHiddenLayers: 0,
  m_NeuronsPerHiddenLyr: 0,
  m_vecLayers: [],
}

Object.assign(this, Object.assign(I, infos))
```

Porém eu ainda não sei se é o resultado esperado pois não executei o código original para debuga-lo, estamos indo com a cara e a coragem heheheeh.


Na sequência temos a função que cria a rede, recebendo 4 parâmetros onde facilmente, se estivéssemos usando `class`, poderia ser o construtor:

```js
this.CreateNet = function(iNumInputs, iNeuronsPerHiddenLayer, iNumHiddenLayers, iNumOutputs) {

  this.m_NumInputs = iNumInputs;
  this.m_NumOutputs = iNumOutputs;
  this.m_NumHiddenLayers = iNumHiddenLayers;
  this.m_NeuronsPerHiddenLyr = iNeuronsPerHiddenLayer;
  
  //create the layers of the network
  if (this.m_NumHiddenLayers > 0) {
    //create first hidden layer
    this.m_vecLayers.push(new SNeuronLayer(this.m_NeuronsPerHiddenLyr, this.m_NumInputs));

    for (let i = 0; i < this.m_NumHiddenLayers - 1; ++i) 
      this.m_vecLayers.push(new SNeuronLayer(this.m_NeuronsPerHiddenLyr, this.m_NeuronsPerHiddenLyr));
    
    //create output layer
    this.m_vecLayers.push(new SNeuronLayer(this.m_NumOutputs, this.m_NeuronsPerHiddenLyr));
  }
  else 
    //create output layer
    this.m_vecLayers.push(new SNeuronLayer(this.m_NumOutputs, this.m_NumInputs));
}
```

Analisando a função acima percebemos que se ela tiver 1 ou mais camadas ocultas iremos criar essas camadas de neurônios, se não tiver camadas ocultas ela irá criar a camada de saída. 

Refatorando podemos modulariza-la dessa forma:

```js
const neuronLayer = require('./neuronLayer')

const createNet = (numInputs, neuronsPerHiddenLayer, numHiddenLayers, numOutputs) => {

  let arrLayers = []
  if (amountHiddenLayers) {
    arrLayers.push(neuronLayer(neuronsPerHiddenLayer, numInputs))

    for (let i = 0; i < iNumHiddenLayers - 1; ++i) 
      arrLayers.push(neuronLayer(neuronsPerHiddenLayer, neuronsPerHiddenLayer))

    arrLayers.push(neuronLayer(numOutputs, neuronsPerHiddenLayer))
  }
  else 
    arrLayers.push(neuronLayer(numOutputs, numInputs))
}

module.exports = createNet
```

Ainda não entendi o porquê criamos camadas onde o neurônio possui a mesma quantidade de pesos que a quantidade de neurônios dessa camada.

**PESQUISAR SOBRE**

Logo abaixo achamos uma função que fala por si só:

```js
this.GetWeights = function() {
  //this will hold the weights
  weights = [];

  //for each layer
  for (let i = 0; i < this.m_NumHiddenLayers + 1; ++i)
    //for each neuron
    for (let j = 0; j < this.m_vecLayers[i].m_NumNeurons; ++j)
      //for each weight
      for (let k = 0; k < this.m_vecLayers[i].m_vecNeurons[j].m_NumInputs;++k)
        weights.push(this.m_vecLayers[i].m_vecNeurons[j].m_vecWeight[k]);

  return weights;
}
```

Só pelo nome dela sabemos que ela deve retornar um *Array* com os pesos de cada neurônio de todas as camadas ocultas, sua refatoraçao é bem simples:

```js
const getWeights = (numHiddenLayers, vecLayers) => {
  weights = []

  //for each layer
  for (let i = 0; i < numHiddenLayers + 1; ++i)
    //for each neuron
    for (let j = 0; j < vecLayers[i].numNeurons; ++j)
      //for each weight
      for (let k = 0; k < vecLayers[i].vecNeurons[j].numInputs; ++k)
        weights.push(vecLayers[i].vecNeurons[j].m_vecWeight[k])

  return weights
}
module.exports = getWeights
```

E olha só que suave na nave a próxima função, só pelo nome já podemos inferir que ela irá definir o peso para cada neurônio:

```js
this.PutWeights = function(weights) {
  cWeight = 0;
  //for each layer
  for (let i = 0; i < this.m_NumHiddenLayers + 1; ++i) 
    //for each neuron
    for (let j = 0; j < this.m_vecLayers[i].m_NumNeurons; ++j) 
      //for each weight
      for (let k = 0; k < this.m_vecLayers[i].m_vecNeurons[j].m_NumInputs; ++k) 
        this.m_vecLayers[i].m_vecNeurons[j].m_vecWeight[k] = weights[cWeight++];
  
  return;
}
```



