Programação Paralela  
Vinicius Aquino Rodrigues

Sumário

1. Parte 1 - Usando o gprof  
1.1 Ferramentas utilizadas  
1.2 Testando o profiler gprof  
1.3 Considerações sobre os perfis de execução  
2. Parte 2 - Usando outros profilers  
2.1 Profilers selecionados  
2.2 O programa testado  
2.3 Testando os profilers  
2.3.1 GlowCode  
2.3.2 CodeXL  
3. Referências  

<b>1. Parte 1 - Usando o gprof</b>

1.1 Ferramentas Utilizadas

Para esta seção do trabalho, realizada no sistema operacional Windows 10, foi utilizada a IDE Code::Blocks[1] cuja versão conta tanto com o GCC e o gprof. O gprof foi acessado através da linha de comando do Windows 10.

1.2 Testando o profiler gprof

Para realizar o teste do profiler gprof uma opção foi marcada nas configurações de compilação do Code::Blocks como mostra a imagem abaixo:

<img src="https://s31.postimg.org/kii1bash7/codeblocksprofilecode.png">

Após esta etapa foram realizados alguns testes de profiling, através do gprof, com diferentes configurações usando como base o programa dotprod_seq, variando-se nele o tamanho do vetor e o número de repetições.

A tabela abaixo mostra os resultados obtidos:

|Tamanho do vetor|Número de Repetições|Resultado|
|----------------|--------------------|---------|
|1000|10|<img src="https://s31.postimg.org/6otombs6z/gprof1000-10.png">|
|10000|10|<img src="https://s31.postimg.org/3uqj8vxqj/gprof10000-10.png">|
|100000|100|<img src="https://s31.postimg.org/xmnlo2s9n/gprof100000-100.png">|
|10000000|100|<img src="https://s31.postimg.org/ormrdkb6z/gprof10000000-100.png">|

1.3 Considerações sobre os perfis de execução

De acordo com os perfis de execução obtidos observa-se que as opções de configuração afetam apenas o tempo de execução das funções chamadas no respectivo programa. Além disso baseado nas informações dos perfis pode-se concluir que a função dot_product é uma candidata a paralelização, uma vez que ela é a função de maior custo computacional do programa.

2. Parte 2 - Usando outros profilers

2.1 Profilers selecionados

Os profilers foram selecionados a partir de uma lista de profilers obtida na Wikipedia[2], deu-se prioridade para profilers da plataforma Windows. A partir disso foi então escolhido o profiler GlowCode[3] e o profiler CodeXL[4].

2.2 O programa testado

O programa testado nos dois profilers citados anteriormente foi escrito na linguagem C e consiste em normalizar um vetor de tamanho variável repetidas vezes.

2.3 Testando os profilers

2.3.1 GlowCode

O profiler GlowCode necessita de uma chave de ativação obtida mediante cadastro que permite ao usuário avaliar o programa durante 21 dias. A instalação foi simples, não necessitando de instalações adicionais. Além de ser um profiler ele também apresenta alguns recursos tais como detecção de gargalos e vazamento de memória.

Para utilizar o profiler é necessário criar um projeto, escolher qual programa será avaliado e configurar alguns parâmetros. As imagens abaixo mostram cada uma dessas etapas:

<img src="https://s31.postimg.org/t0rhfntuz/glowcode1.png">
<img src="https://s31.postimg.org/4k9bl70u3/glowcode2.png">
<img src="https://s31.postimg.org/c08l6zw97/glowcode3.png">

Após vários testes realizados com o profiler este não retornou nenhum resultado satisfatório, de maneira que ele não foi capaz de identificar as funções executadas no programa nem apresentar quanto tempo ou recursos cada uma utilizou. A imagem abaixo mostra o resultado de um teste feito com os parâmetros 1000000 para o tamanho do vetor e 1000 para o número de repetições.

<img src="https://s31.postimg.org/6c2ag4mrv/glowcode7.png">

2.3.2 CodeXL

Este profiler é distribuído gratuitamente sob a licença MIT e teve instalação simples. Além de ser um profiler de CPU ele também é um profiler para GPU.

A utilização do profiler é simples, basta criar um projeto e selecionar qual programa será analisado e quais são seus parâmetros como mostra a figura abaixo.

<img src="https://s31.postimg.org/7ecgymfuz/codexl1.png">

As imagens abaixo apresentam o profiler com diferentes configurações:

Tamanho do vetor: 1000000, número de repetições: 1000
<img src="https://s31.postimg.org/hoevxw8bf/codexl2.png">

Tamanho do vetor: 10000000, número de repetições: 100
<img src="https://s31.postimg.org/wkdf5hz5n/codexl3.png">

Tamanho do vetor: 10000000, número de repetições: 1000
<img src="https://s31.postimg.org/idxoa9gkr/codexl4.png">

Com base nas informações fornecidas pelo profiler pode-se considerar que as funções normaliza_vetor e calcula_modulo são as mais custosas para o desempenho do programa podendo elas serem paralelizadas.

3. Referências

[1] Code::Blocks, Code::Blocks, http://www.codeblocks.org/  
[2] Wikipedia The Free Encyclopedia, List of performance analysis tools - Wikipedia, https://en.wikipedia.org/wiki/List_of_performance_analysis_tools  
[3] Electric Software Inc, GlowCode - Performance profiler, memory leak detector for C++ C# .NET programmers and QA. Fastest profiler toolset, resource analysis, leak detection for test, tune and optimization, http://www.glowcode.com/index.htm  
[4] Advanced Micro Devices, GitHub - GPUOpen-Tools/CodeXL: CodeXL is a comprehensive tool suite that enables developers to harness the benefits of CPUs, GPUs and APUs, https://github.com/GPUOpen-Tools/CodeXL
