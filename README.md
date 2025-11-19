## Jogo - Experiência Criativa: Um jogo de plataforma 2D

Este é um jogo de plataforma 2D simples criado com o Construct 3, com foco em demonstrar funcionalidades básicas de jogabilidade, animação e interação.

### Visão Geral do Projeto

O jogo possui uma estrutura de layouts e folhas de eventos que controlam a lógica do jogo.

* **Layouts:**
    * **Menu:** Tela inicial do jogo.
    * **Subsolo 1, Subsolo 2, Subsolo 3:** Fases do jogo de plataforma.
    * **cutsecne:** Uma tela de *cutscene* que reproduz um vídeo.
    * **final:** Tela de encerramento, apresentando os créditos.
* **Folhas de Eventos:** Gerenciam a lógica de cada layout.

### Tecnologias Utilizadas

O jogo é executado usando o *runtime* do **Construct 3**, utilizando **WebGL** para renderização gráfica.

**Bibliotecas e APIs Centrais:**
* **gl-matrix:** Para operações de matrizes e vetores de alta performance, essenciais para a lógica de transformação 2D e 3D do jogo.
* **poly-decomp.js:** Utilizado para decomposição de polígonos.
* **Web Audio API:** Usada pelo plugin **Audio** para manipulação de som e música.

### Entidades e Comportamentos Principais

As classes de objetos no jogo interagem usando os plugins e comportamentos do Construct 3:

| Objeto | Plugins/Comportamentos | Finalidade |
| :--- | :--- | :--- |
| **Sprite4** (Personagem) | **Plataforma**, **Centrar Em**, **Destruir Fora do Layout** | Objeto principal controlável. Utiliza **Plataforma** para movimentação e **Centrar Em** para manter a câmera focada. |
| **Sprite3** (Projetil) | **Projétil**, **Destruir Fora do Layout** | Usado para ataques. O comportamento **Projétil** lida com o movimento constante e colisões. |
| **Sprite2, Sprite17** | **Sólido**, **Plataforma**, **Senóide** | Objetos de cenário com colisão (Sólido) ou que se movem usando **Plataforma** ou o movimento oscilatório de **Senóide**. |
| **FundoEmBlocos**, **FundoEmBlocos3/4/5** | | Elementos visuais de fundo criados com o plugin TiledBg (Fundo em Blocos). |
| **Texto**, **Texto2/3/4/5/6** | **Piscar** | Usados para *HUD*, *debug* ou interface, com o comportamento **Piscar** (Flash) aplicado para criar efeitos visuais. |

### Controles

* **Movimento:** Teclas de **Seta para a Esquerda** e **Seta para a Direita** controlam o movimento horizontal do personagem.
* **Pular:** Tecla **Seta para Cima** (ArrowUp) é usada para o salto.
* **Tiro:** A tecla **Z** é mencionada na fase como controle de tiro (via evento `OnKey`).
* **Menu:** Pressionar a tecla **Enter** na tela inicial inicia o jogo.

### Configurações de Compilação

O jogo está configurado com as seguintes propriedades:

* **Nome do Projeto:** JogoEXP.
* **Orientação:** Paisagem (`landscape`).
* **Tela Cheia:** Definido para `fullscreen` no `appmanifest.json`.
* **Dimensionamento:** O `fullscreenMode` padrão é `letterbox-scale`, ajustando o jogo para caber na tela mantendo a proporção de 854x480.
* **Mínimo de FPS:** 30.
* **Renderizador:** WebGL 2 é preferencial, com fallback para WebGL 1.

### Desenvolvimento

O código principal do *runtime* está em `c3runtime.js` e a inicialização é feita em `main.js`, que configura o ambiente DOM/Worker e inicia a interface de *runtime* do Construct 3.

O jogo utiliza um sistema de eventos para gatilhos como:
* `OnLayoutStart` / `OnLayoutEnd`.
* `OnCollision` (para Sprite/Plataforma).
* `OnKey` / `IsKeyDown` (para Teclado).
* **Áudio:** `Play` e `Stop` de músicas e sons como "bensound-epic" e "classic_hurt".

O desenvolvimento é feito para rodar em **modo DOM** ou **Worker** (dependendo do suporte e configuração).
