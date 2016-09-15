# TP2# Trabalho Prático 2 - O Labirinto

![Keep Out!](images/Labirinto.png)


Neste trabalho, nosso objetivo é **criar um labirinto**. Nosso
objetivo é praticar os conceitos de projeção, iluminação, modelagem e
efeitos visuais vistos em sala de aula.
Um exemplo de labirinto pode ser visto no jogo [_"Keep Out"_][Keep Out].

Videos Keep Out:

[_"First Exploration!"_][First Exploration!]

[_"Demons Everywhere!"_][Demons Everywhere!]

[_"Death!"_][Death!]

[Keep Out]: http://www.playkeepout.com/
[Demons Everywhere!]: https://www.youtube.com/watch?v=0HXZA81ewN8
[Death!]: https://www.youtube.com/watch?v=F6s-lrX_Yk4
[First Exploration!]: https://www.youtube.com/watch?v=Efo14AGLWLg


Esse trabalho pode ser feito individualmente, ou em dupla, e
como funcionalidade básica, valendo 85% ou 75% (respectivamente) da
nota, deve ter os seguintes itens:

- **Mundo**:
  1. O mapa deve ser carregado apartir dos pixels de uma imagem, onde as cores:
    - Azul: Ponto inicial.
    - Vermelho: Ponto final.
    - Preto: Lugares inacessivéis.
    - Branco: Caminhos possíveis.
    Exemplo de Mapa:
    ![Mapa!](images/Mapa.png)
  Obs:  O caminho pode ser um plano;
        As paredes podem ser objetos da GLU e GLUT (Cubos)  ou planos cercando o caminho;
    
  2. O fim deve ser um teleport para o inicio.
- **Personagem**:
  - Ela deve possuir ao menos 3 "dedos" para pegar os objetos e
    deve ser capaz de executar o movimento de abertura e fechamento
    dos "dedos".
    - Caso não queira modelá-la com dedos, você pode criar algo semelhante,
      contanto que seja feita a modelagem de forma hierárquica (_i.e._, com
      `glPushMatrix()...glPopMatrix` aninhados)
  - Pode ser controlada pelo usuário com movimentos em todos os
    sentidos dos eixos X e Z utilizando as _"arrow keys"_
    (<kbd>&uarr;</kbd><kbd>&rarr;</kbd><kbd>&darr;</kbd><kbd>&larr;</kbd>).
  - A <kbd>barra de espaço</kbd> deve fazer o movimento para que
    a barra desça para tentar capturar um objeto.
    - Capturando ou não, a garra faz um movimento de descida, fecha os dedos,
      faz o movimento da subida e depois de retorno à sua "posição de repouso",
      só então abrindo os dedos e eventualmente liberando o objeto capturado.
    - Durante a movimentação "automática", ela não pode ser controlada.
  - Se a garra colide com um objeto, ela o captura, volta para sua altura
    original, volta para sua posição de repouso e solta o objeto.
    - Para fins de verificação de colisão entre a garra e os objetos,
      você pode considerar todos como sendo esferas.
- **Câmera**:
  1. Você deve usar projeção perspectiva via `glFrustum` ou `gluPerspective`.
  2. Devem existir 2 tipos de câmeras:
      1 - Câmera posicionada atrás do personagem; 
      ![Camera Atrás!](images/Camera_Atras.jpg)
      
      2 - Câmera em primeira pessoa. (Como no labirinto de exemplo Keep Out!).
      ![Camera 1P!](images/Camera_1P.png)

  3. A Câmera deve:
    - Rotacionar 90º para direita ao apertar a tecla "D" ou <kbd>&rarr;</kbd>;
    - Rotacionar 90º para esquerda ao apertar a tecla "A" ou <kbd>&larr;</kbd>;
    - Movimentar junto com o personagem apartir das teclas "W" ou <kbd>&uarr;</kbd> para frente;
    - Movimentar junto com o personagem apartir das teclas "S" ou <kbd>&darr;</kbd> para trás;
- **Gráficos**:
  1. Você deve usar o modelo de
    [iluminação do OpenGL, devidamente configurado][lighting].
    - Basta que sua cena tenha 1
    [fonte de luz direcional][lighting-directional].
  1. Todos os objetos da cena devem ter materiais configurados (não
    necessariamente com textura).

Para se obter o restante dos pontos do trabalho (ou até mesmo mais pontos
extras, até um limite de 133% da pontuação original) funcionalidades adicionais
podem/devem ser implementadas no jogo. Essas funcionalidades serão avaliadas
conforme a **dificuldade da implementação**, o **efeito obtido** com ela no
trabalho e a **qualidade da implementação**. Exemplos de funcionalidades
extras com suas respectivas pontuações **máximas**:

- Relativas aos **Objetos**:
  1. :star2: **Vários tipos (até 10%)**: em vez de apenas um tipo (_e.g._,
    brinquedo), pode ter vários outros: celular, livro, pelúcia etc.
  1. **Distribuídos de forma procedural (até 7%)**: em vez de determinar a
    posição de cada objeto você mesmo, crie uma função que o faça de forma
    aleatória ou pseudo-aleatória. Se optar por distribuição aleatória,
    deve tomar cuidado para não colocar objetos "um-den-du-ôto". Veja este
    [_post_ do fórum][obj-distribution] e os links nele sobre o assunto.
  1. **Cenário descrito em arquivo (até 5%)**: em vez de instanciar os
    objetos de forma _hard-coded_, crie um arquivo num formato proposto
    por você mesmo (_e.g._, `objetos-claw-machine.tp2`) que descreve quantos,
    que tipos, as posições e as orientações (rotação nos 3 eixos) dos objetos.
  1. :bomb: :boom: **Modelos no formato .obj (até 10%)**: em vez de usar os
    sólidos da GLU/GLUT, modele um objeto \*simples\* usando um _software_
    CAD, salve-o num formato \*simples\* (_e.g._, `.obj`) e carregue-o no
    seu programa. Há alguns tutoriais disponíveis nas _interwebs_ sobre
    como abrir um arquivo `.obj`, ler a informação sobre os vértices e
    desenhá-los... aqui estão alguns: [tutorial 1][obj-tut-1],
    [tutorial 2][obj-tut-2], [tutorial 3][obj-tut-3].
  1. **Objetos amontoados (até 7%)**: remova a restrição (da
    especificação básica) de que todos os objetos devem estar no chão e
    coloque-os amontados. Repare que a garra precisa, então, saber reconhecer
    direitinho com qual objeto houve colisão.
  1. :bomb: :boom: **Física (até 8%)**: faça com que
    os objetos obedeçam as leis da física para gravidade e atrito, de
    forma que eles se (re)acomodem quando um objeto for retirado.
- Relativas à **Garra**:
  1. **Animação de abertura/fechamento (8%)**: faça a garra abrir e fechar,
    quando for o caso, de forma animada.
- Relativas à **Câmera**:
  1. Visões **laterais (5%)**: ao se pressionar <kbd>c</kbd> ou <kbd>v</kbd>, a
    câmera deve trocar de posição como se o jogador tivesse andado para a
    direita ou esquerda, passando a olhar para a máquina por outro lado.
    Veja este [vídeo ilustrativo da câmera lateral][camera-lateral].
  1. :star2: Câmera **_top-down_ (6%)**: crie uma câmera com vista de cima da
    máquina. Essa câmera deve ser ativada quando a máquina estiver em
    "modo automático". Findo o movimento da garra, a câmera deve ser
    restabelecida.
    - :star2: **Modo _cheat_ (+3%)**: faça com que uma tecla ative essa câmera.
- Relativas a **Gráficos**:
  1. **Botões na tela (5%)**: em vez de teclas do teclado para tudo, use
    botões clicáveis via _mouse_.
  1. Fonte de **luz pontual (5%)**: além da fonte luminosa direcional, crie uma
    ou mais fontes de luz pontuais em pontos estratégicos.
  1. :star2: **Reshape (5%)**: permitir o redimensionamento da janela
    de visualização sem perda da razão de aspecto (sem que haja distorção
    de achatamento/alongamento).
  1. :collision: **_Skybox_ (até 5%)**: se considerarmos que nosso mundo
    está definido dentro de um cubo, podemos colocar uma imagem de textura
    em cada face interna (6) que represente o horizonte naquela direção. Veja
    [exemplos de texturas de _skyboxes_][skybox] e nossa aula sobre
    [efeitos visuais][visual-fx]. Repare que o cubo _skybox_ acompanha
    a posição, ou seja, não é possível se aproximar (e até sair) do cubo.
- Outros adicionais:
  1. **Outro tema (até 3%)**: por que se limitar a fazer uma simples
    máquina de garra, quando também podemos pensar em (_e.g._): (a) um OVNI
    abduzindo vacas transgênicas, ou (b) um navio pirata fantasma coletando
    baús do tesouro amaldiçoados ou até mesmo (c) um braço cyborg coletando
    petiscos em um prato, para comer. Liberte o ser criativo dentro de você!
  1. :star2: **Música (até 5%)**: você pode incluir ambientação sonora para
    sua máquina que pode incluir uma música ambiente e efeitos sonoros.
  1. **Qualquer outra idéia (??%)** que torne a máquina mais interessante ou
    agradável aos sentidos. Essas idéias precisam ser documentadas e
    explicadas no documento de entrega do trabalho (`README.txt`).


Legenda dos ícones:
  - :star2:: item sugerido por ser interessante ou super simplão.
  - :collision:: item com maior complexidade de implementação - não
    comece por estes!!

## Instruções gerais

O trabalho pode ser feito individualmente ou em duplas e deve ser produzido
integralmente pelos aluno ou dupla. Podem discutir idéias com outros colegas,
mas cada aluno/dupla deve ter a sua implementação independente dos demais.
**Trabalhos muito semelhantes receberão notas muito semelhantes (iguais a 0)**,
independente de quem copiou de quem. Trabalhos semelhantes aos de outras
pessoas (ex-alunos, pessoas na Internet) também receberão nota 0.


## O que faz perder nota

Alguns descuidos podem fazer com que sua nota fique abaixo do esperado:
- Seu trabalho não executa: nota 0
- Cópia de trabalho de outrem: nota 0
- Ausência de qualquer item obrigatório da entrega (descrito na próxima seção)
- Ausência de itens da especificação obrigatória
- Baixa legibilidade do código
- Baixa qualidade da implementação
- Atraso na entrega. Cada dia de atraso reduz o valor máximo de nota da
 maneira abaixo. Considere `x` como dias de atraso e `y` a penalidade
 percentual na nota:

 ![Fórmula de penalidade por atraso](../../images/penalidade-por-atraso.png)
 - Isso implica que 1 ou 2 dias de atraso são pouco penalizados
 - E após 5 dias de atraso, o trabalho vale 0
 - _Seeing is believing_: https://www.google.com.br/search?q=y%3D(2%5E(x-2)%2F0.16)%2Cy%3D100


## O que deve ser **entregue**

Deve ser entregue **um arquivo .tar.gz ou .zip** via **Moodle** contendo:
 1. 3+ _screenshots_ de diferentes cenas do seu jogo
 1. Todo o programa fonte, com os _Makefiles_ e bibliotecas necessárias
    para a compilação e execução do programa
 1. O arquivo executável
 1. Um arquivo **README** contendo:
    - Instruções para **compilação e execução**
    - **Lista de itens adicionais** que seu jogo está pleiteando
 1. [opcional, +3%] O link para um vídeo breve (_e.g._, youtube) do
    seu jogo mostrando as opções implementadas.

Qualquer dúvida, entre em contato comigo. Ou acrescente a sua interpretação no
arquivo README e mãos à obra.

[skybox]: https://www.google.com.br/search?q=skybox&safe=off&hl=pt-BR&source=lnms&tbm=isch&sa=X&ei=jMM_VenRNKuasQSCwYDABw&ved=0CAgQ_AUoAg&biw=1366&bih=599
[lighting]: http://fegemo.github.io/cefet-cg/classes/lighting/#26
[lighting-directional]: http://fegemo.github.io/cefet-cg/classes/lighting/#37
[obj-tut-1]: http://www.opengl-tutorial.org/beginners-tutorials/tutorial-7-model-loading/
[obj-tut-2]: http://netization.blogspot.in/2014/10/loading-obj-files-in-opengl.html
[obj-tut-3]: https://tutorialsplay.com/opengl/2014/09/17/lesson-9-loading-wavefront-obj-3d-models/
[obj-distribution]: http://moodle.cefetmg.br/mod/forum/discuss.php?d=3572
[visual-fx]: http://fegemo.github.io/cefet-cg/classes/visual-effects/#4
[camera-lateral]: https://youtu.be/T7zdZ4VJ3nw
