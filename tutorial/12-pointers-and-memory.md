# 12 - Pointers and Memory

# Ponteiros e Memória Dinâmica em Raylib (C)

```c
#include "raylib.h"
#include <stdlib.h>

typedef struct Enemy
{
    int x;
    int y;
} Enemy;

int main()
{
    InitWindow(800, 600, "Pointers and Memory");

    int quantidade = 5;

    Enemy *enemies = malloc(sizeof(Enemy) * quantidade);

    for (int i = 0; i < quantidade; i++)
    {
        enemies[i].x = 100 * i + 50;
        enemies[i].y = 200;
    }

    while (!WindowShouldClose())
    {
        BeginDrawing();

        ClearBackground(RAYWHITE);

        for (int i = 0; i < quantidade; i++)
        {
            DrawRectangle(enemies[i].x,
                          enemies[i].y,
                          50,
                          50,
                          RED);
        }

        DrawText("Dynamic Memory Example", 10, 10, 20, BLACK);

        EndDrawing();
    }

    free(enemies);

    CloseWindow();

    return 0;
}
```

---

# O que foi adicionado nesta etapa

Aprendemos:
- ponteiros
- malloc
- memória heap
- memória dinâmica
- structs

---

# O que é ponteiro

Um ponteiro:
- guarda endereço de memória.

---

# O que é malloc

```c
malloc()
```

Aloca memória dinamicamente.

---

# O que é heap

Heap é:
- área de memória dinâmica.

---

# Estrutura Enemy

```c
typedef struct Enemy
```

Cria:
- tipo personalizado.

---

# Criando vetor dinâmico

```c
Enemy *enemies
```

Agora temos:
- vetor criado em tempo de execução.

---

# O que acontece internamente

O sistema operacional:
1. reserva memória
2. retorna endereço
3. programa usa memória

---

# Liberando memória

```c
free(enemies);
```

Muito importante.

Evita:
- memory leak
- desperdício de RAM

---

# Resultado esperado

Você verá:
- vários inimigos vermelhos
- criados dinamicamente

---

# Conceito novo aprendido

| Conceito | Explicação |
|---|---|
| Pointer | endereço de memória |
| malloc | alocação dinâmica |
| free | liberar memória |
| Heap | memória dinâmica |
| Struct | tipo personalizado |

---

# Curiosidade

Quase todos os jogos modernos usam:
- memória dinâmica
- ponteiros
- alocação em tempo real

---

# Desafio

## Desafio 1

Aumente quantidade de inimigos.

## Desafio 2

Movimente inimigos.

## Desafio 3

Use realloc.

---

# Próximo passo

Agora você já possui:
- renderização
- input
- colisão
- shooting
- inimigos
- memória dinâmica

Você já consegue criar:
- jogos arcade
- shooters
- mini engines
- sistemas ECS básicos
