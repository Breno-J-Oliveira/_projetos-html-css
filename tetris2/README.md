# 🎮 Jogo Tetris — Canvas API JavaScript

<p align="center">
  <img src="https://img.shields.io/badge/Status-Conclu%C3%ADdo-10B981?style=for-the-badge" alt="Status">
  <img src="https://img.shields.io/badge/Linhas-258-2563EB?style=for-the-badge" alt="Linhas de Código">
  <img src="https://img.shields.io/badge/Jogabilidade-Completa-111827?style=for-the-badge" alt="Jogabilidade">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white" alt="HTML5">
  <img src="https://img.shields.io/badge/Canvas_API-000000?style=for-the-badge&logo=html5&logoColor=white" alt="Canvas API">
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" alt="JavaScript">
  <img src="https://img.shields.io/badge/Jogo-Cl%C3%A1ssico-FF4500?style=for-the-badge" alt="Jogo Clássico">
</p>

---

## 📑 Índice
1. [Sobre](#-sobre)
2. [Mecânica do Jogo](#-mecânica-do-jogo)
3. [Peças (Tetrominós)](#-peças-tetrominós)
4. [Sistema de Pontuação](#-sistema-de-pontuação)
5. [Controles](#-controles)
6. [Código Técnico](#-código-técnico)
7. [Contatos](#-contatos)

---

## 🎯 Sobre

Implementação completa do clássico **jogo Tetris** em um único arquivo HTML de **258 linhas**, utilizando **Canvas API 2D** para toda a renderização. O jogo foi desenvolvido 100% em JavaScript vanilla, sem bibliotecas externas.

### Características
- 🧩 7 peças clássicas (tetrominós) com cores distintas
- 📊 Sistema de pontuação progressivo
- 📈 Níveis de dificuldade crescentes
- 🎚️ Slider de velocidade ajustável (100ms a 1000ms)
- 🎮 Controles intuitivos por teclado
- 💀 Tela de Game Over com pontuação final
- 🎨 Renderização via Canvas API 2D (sem imagens)

---

## 🎯 Mecânica do Jogo

### Grid de Jogo
- **Dimensões:** 10 colunas × 20 linhas
- **Tamanho da célula:** 30px × 30px
- **Área total do canvas:** 300px × 600px

### Loop Principal
```javascript
function gameLoop() {
  if (!gameOver) {
    moveDown();
    draw();
    setTimeout(gameLoop, speed);
  }
}
```

### Lógica de Colisão
- Verificação de limites laterais (esquerda/direita)
- Verificação de colisão com o fundo
- Verificação de colisão com peças já fixadas
- Rotação com kick (ajuste de posição se necessário)

---

## 🧩 Peças (Tetrominós)

| Peça | Forma | Cor | Hex |
|------|-------|-----|-----|
| **I** | ⬜⬜⬜⬜ (4×1) | Ciano | `#00FFFF` |
| **O** | ⬜⬜ / ⬜⬜ (2×2) | Amarelo | `#FFFF00` |
| **T** | ⬜⬜⬜ / _⬜_ (3×2) | Roxo | `#800080` |
| **S** | _⬜⬜ / ⬜⬜_ (3×2) | Verde | `#00FF00` |
| **Z** | ⬜⬜_ / _⬜⬜ (3×2) | Vermelho | `#FF0000` |
| **J** | ⬜__ / ⬜⬜⬜ (3×2) | Azul | `#0000FF` |
| **L** | __⬜ / ⬜⬜⬜ (3×2) | Laranja | `#FFA500` |

---

## 📊 Sistema de Pontuação

| Linhas Completadas | Pontos | Nome |
|-------------------|--------|------|
| 1 linha | 10 pontos | Single |
| 2 linhas | 20 pontos | Double |
| 3 linhas | 30 pontos | Triple |
| 4 linhas | 40 pontos | **Tetris!** |

### Progressão de Nível
- A cada 100 pontos, o nível aumenta
- Cada nível reduz o tempo de queda em 50ms
- Velocidade mínima: 100ms por tick

---

## 🎮 Controles

| Tecla | Ação |
|-------|------|
| **←** (Seta Esquerda) | Mover peça para a esquerda |
| **→** (Seta Direita) | Mover peça para a direita |
| **↓** (Seta Baixo) | Queda rápida (soft drop) |
| **↑** (Seta Cima) | Rotação horária |
| **Q** | Rotação anti-horária |
| **W** | Rotação horária (alternativa) |
| **Espaço** | Queda instantânea (hard drop) |

---

## 💻 Código Técnico

### Renderização Canvas
```javascript
const canvas = document.getElementById('tetris');
const ctx = canvas.getContext('2d');

function drawSquare(x, y, color) {
  ctx.fillStyle = color;
  ctx.fillRect(x * 30, y * 30, 30, 30);
  ctx.strokeStyle = '#333';
  ctx.strokeRect(x * 30, y * 30, 30, 30);
}

function draw() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  // Desenha grid
  for (let row = 0; row < 20; row++) {
    for (let col = 0; col < 10; col++) {
      if (board[row][col]) {
        drawSquare(col, row, board[row][col]);
      }
    }
  }
  // Desenha peça atual
  currentPiece.shape.forEach((row, y) => {
    row.forEach((value, x) => {
      if (value) {
        drawSquare(currentPiece.x + x, currentPiece.y + y, currentPiece.color);
      }
    });
  });
}
```

### Input Slider de Velocidade
```html
<input type="range" id="speedSlider" min="100" max="1000" value="500" step="50">
<label for="speedSlider">Velocidade: <span id="speedValue">500ms</span></label>
```


## 👤 Contatos e Redes Sociais

<p align="center">
  <a href="https://github.com/Breno-J-Oliveira" target="_blank">
    <img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub">
  </a>
  <a href="https://www.linkedin.com/in/breno-j-oliveira-672619352/" target="_blank">
    <img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn">
  </a>
  <a href="https://www.instagram.com/brenoov" target="_blank">
    <img src="https://img.shields.io/badge/Instagram-E4405F?style=for-the-badge&logo=instagram&logoColor=white" alt="Instagram">
  </a>
  <a href="https://x.com/BrenoJOliveira_" target="_blank">
    <img src="https://img.shields.io/badge/X-000000?style=for-the-badge&logo=x&logoColor=white" alt="X (Twitter)">
  </a>
</p>

---

<p align="center"><em>Desenvolvido com 💛 por Breno Oliveira — Técnico em Desenvolvimento de Sistemas | SENAI</em></p>