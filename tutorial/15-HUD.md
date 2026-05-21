# 15 - HUD

# Criando HUD (Interface do Jogador) em Raylib (C)

# Objetivo da Aula

Nesta aula iremos aprender a criar uma:

```text
HUD
```

HUD significa:

```text
Heads-Up Display
```

Ou seja:

```text
interface visual do jogador
```

A HUD mostra informações importantes durante o jogo:

- vida
- score
- munição
- tempo
- energia
- minimapa
- itens
- status

---

# O que iremos aprender

Nesta aula vamos criar:

- score
- vida
- barra de vida
- munição
- tempo
- mensagens na tela
- interface fixa

Tudo isso será desenhado sobre o jogo.

---

# O que é HUD nos jogos

Exemplos famosos:

| Jogo | HUD |
|---|---|
| Mario | moedas e vidas |
| Doom | vida e munição |
| GTA | mapa e dinheiro |
| Fortnite | vida e inventário |
| Minecraft | coração e fome |

---

# Código Completo
#include "raylib.h"

int main(void)
{
    InitWindow(1000, 600, "HUD em Raylib");

    SetTargetFPS(60);

    Vector2 jogador = { 480, 300 };
    float velocidade = 4.0f;

    int score = 0;
    int vida = 100;
    int municao = 30;
    float tempo = 0;

    while (!WindowShouldClose())
    {
        tempo += GetFrameTime();

        if (IsKeyDown(KEY_RIGHT)) jogador.x += velocidade;
        if (IsKeyDown(KEY_LEFT))  jogador.x -= velocidade;
        if (IsKeyDown(KEY_UP))    jogador.y -= velocidade;
        if (IsKeyDown(KEY_DOWN))  jogador.y += velocidade;

        if (IsKeyPressed(KEY_P))
        {
            score += 10;
        }

        if (IsKeyPressed(KEY_H))
        {
            vida -= 10;
            if (vida < 0) vida = 0;
        }

        if (IsKeyPressed(KEY_SPACE))
        {
            municao--;
            if (municao < 0) municao = 0;
        }

        BeginDrawing();

        ClearBackground(RAYWHITE);

        // Mundo do jogo
        DrawRectangleV(jogador, (Vector2){ 40, 40 }, BLUE);

        // Fundo da HUD
        DrawRectangle(0, 0, 1000, 115, LIGHTGRAY);
        DrawLine(0, 115, 1000, 115, DARKGRAY);

        // Título
        DrawText("HUD DO JOGO", 20, 15, 28, DARKBLUE);

        // Score
        DrawText(TextFormat("Score: %d", score), 20, 65, 20, BLACK);

        // Vida
        DrawText(TextFormat("Vida: %d", vida), 220, 65, 20, BLACK);

        // Barra de vida
        DrawRectangle(220, 40, 200, 20, RED);
        DrawRectangle(220, 40, vida * 2, 20, GREEN);
        DrawRectangleLines(220, 40, 200, 20, BLACK);

        // Munição
        DrawText(TextFormat("Municao: %d", municao), 470, 65, 20, BLACK);

        // Tempo
        DrawText(TextFormat("Tempo: %.1f", tempo), 700, 65, 20, BLACK);

        // Instruções
        DrawText("P = Pontos | H = Dano | ESPACO = Gasta Municao",
                 20, 560, 18, MAROON);

        EndDrawing();
    }

    CloseWindow();

    return 0;
}
```

---

# Explicação COMPLETA da Arquitetura

# 1. O que é HUD

HUD significa:

```text
informações desenhadas sobre o jogo
```

A HUD normalmente:
- não faz parte do mundo
- fica fixa na tela
- acompanha jogador

---

# Exemplo visual

```text
┌─────────────────────────────┐
│ SCORE  VIDA  MUNIÇÃO TEMPO │ ← HUD
├─────────────────────────────┤
│                             │
│                             │
│         MUNDO DO JOGO       │
│                             │
│                             │
└─────────────────────────────┘
```

---

# 2. Variáveis da HUD

```c
int score = 0;
int vida = 100;
int municao = 30;
float tempo = 0;
```

Essas variáveis representam:

| Variável | Função |
|---|---|
| score | pontuação |
| vida | HP do jogador |
| municao | tiros restantes |
| tempo | tempo de jogo |

---

# 3. Atualizando tempo

```c
tempo += GetFrameTime();
```

---

# O que GetFrameTime faz

```c
GetFrameTime()
```

retorna:

```text
tempo entre um frame e outro
```

Exemplo:

```text
0.016 segundos
```

em 60 FPS.

---

# Resultado

O tempo cresce suavemente:

```text
0.1
0.2
0.3
0.4
```

---

# 4. Sistema de Score

```c
if (IsKeyPressed(KEY_P))
{
    score += 10;
}
```

Cada vez que o jogador aperta `P`:

```text
ganha 10 pontos
```

---

# 5. Sistema de Vida

```c
if (IsKeyPressed(KEY_H))
{
    vida -= 10;
}
```

Cada vez que o jogador aperta `H`:

```text
perde vida
```

---

# Proteção contra vida negativa

```c
if (vida < 0)
    vida = 0;
```

Evita:

```text
vida negativa
```

---

# 6. Sistema de Munição

```c
if (IsKeyPressed(KEY_SPACE))
{
    municao--;
}
```

Simula:
- uso de munição

---

# Proteção contra munição negativa

```c
if (municao < 0)
    municao = 0;
```

---

# 7. Fundo da HUD

```c
DrawRectangle(
    0,
    0,
    1000,
    90,
    LIGHTGRAY
);
```

Cria:
- painel superior

---

# 8. Linha separadora

```c
DrawLine()
```

Desenha:
- linha divisória

Separando:
- HUD
- mundo do jogo

---

# 9. TextFormat()

```c
TextFormat("Score: %d", score)
```

Permite inserir:
- variáveis dentro do texto

---

# O que significa %d

```text
%d = inteiro
```

---

# O que significa %.1f

```text
%.1f = float com 1 casa decimal
```

---

# 10. Barra de vida

Primeiro desenhamos:

```c
DrawRectangle(... RED)
```

que é:
- fundo da barra

---

Depois:

```c
DrawRectangle(... GREEN)
```

que representa:
- vida restante

---

# O mais importante

Observe:

```c
vida * 2
```

Isso transforma:

```text
100 de vida
```

em:

```text
200 pixels
```

---

# Visualização da barra

```text
████████████████████
```

Quando perde vida:

```text
██████████
```

---

# 11. HUD fixa

A HUD:
- NÃO se move
- NÃO depende da câmera
- fica fixa

Isso é MUITO importante em jogos.

---

# Fluxo do programa

```text
INPUT
   ↓
Atualiza score/vida
   ↓
Atualiza HUD
   ↓
Renderiza mundo
   ↓
Renderiza interface
```

---

# Conceitos profissionais aprendidos

| Conceito | Foi usado |
|---|---|
| HUD | ✔ |
| Barra de Vida | ✔ |
| Score | ✔ |
| Tempo | ✔ |
| Interface | ✔ |
| TextFormat | ✔ |
| UI Básica | ✔ |
| Overlay | ✔ |

---

# O que o aluno aprende de verdade

O aluno começa a entender:

```text
jogo ≠ apenas mundo gráfico
```

Jogos também possuem:
- interface
- feedback visual
- informações em tempo real

---

# Curiosidade MUITO importante

Mesmo jogos AAA usam:
- HUDs
- overlays
- barras
- indicadores
- feedback visual

A HUD é uma das partes mais importantes:
- UX
- gameplay
- experiência do jogador

---

# Resultado esperado

Você verá:

✅ jogador azul  
✅ score  
✅ barra de vida  
✅ munição  
✅ tempo de jogo  
✅ HUD fixa no topo  

---

# Atividade da Aula

## Exercício 1

Adicione:

- moedas
- energia
- XP

---

## Exercício 2

Crie:
- minimapa simples

---

## Exercício 3

Faça:
- barra de mana

---

# Desafio Extra

Adicione:

- ícones
- imagens
- sprites na HUD

---

# Super Desafio

Crie uma HUD completa com:

```text
vida
mana
xp
nível
mini mapa
arma atual
inventário
```

---

# Próximo passo

Na próxima aula podemos evoluir para:

```text
16 - Particles.md
```

onde iremos aprender:
- partículas
- explosões
- efeitos visuais
- fumaça
- brilho
- feedback visual avançado
