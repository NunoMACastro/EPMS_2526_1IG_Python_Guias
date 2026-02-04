[Voltar ao README principal](../README.md)

# Memória · 10.º Ano (Informática de Gestão)

Materiais de apoio em formato **Markdown** sobre memória de computador e gestão de memória em Python.

Estes ficheiros foram escritos para alunos em fase inicial, com explicações muito guiadas, linguagem simples e foco em compreensão real dos conceitos.

---

## Índice

- [Como usar estes materiais](#como-usar-estes-materiais)
- [`00_fundamentos_hardware_bits_cpu_memoria.md`](#00_fundamentos_hardware_bits_cpu_memoriamd)
- [`01_memoria_do_computador_cache_primaria_secundaria.md`](#01_memoria_do_computador_cache_primaria_secundariamd)
- [`02_ram_rom_binario_bytes_enderecos.md`](#02_ram_rom_binario_bytes_enderecosmd)
- [`03_gestao_de_memoria_em_python_referencias_mutabilidade_gc.md`](#03_gestao_de_memoria_em_python_referencias_mutabilidade_gcmd)
- [`04_heap_stack_frames_e_execucao_python.md`](#04_heap_stack_frames_e_execucao_pythonmd)
- [`05_estruturas_dinamicas_e_complexidade.md`](#05_estruturas_dinamicas_e_complexidademd)
- [`06_do_codigo_a_execucao_real_so_cpu_isa.md`](#06_do_codigo_a_execucao_real_so_cpu_isamd)
- [Rota de estudo recomendada](#rota-de-estudo-recomendada)

---

## Como usar estes materiais

1. Lê um ficheiro de cada vez, com calma.
2. Não saltes secções: os conceitos foram organizados de forma progressiva.
3. Quando aparecer um termo novo, para e confirma se o entendeste antes de continuar.
4. No ficheiro de binário (`02_...`), resolve os exercícios.
5. Revisa os resumos no fim de cada ficheiro.

---

### `00_fundamentos_hardware_bits_cpu_memoria.md`

**Objetivo:** criar base sólida antes da memória em Python: bits, transístor, RAM (condensador/transístor), CPU, ciclo de execução, endereços e barramentos.

---

### `01_memoria_do_computador_cache_primaria_secundaria.md`

**Objetivo:** perceber, de forma clara, o que é memória num computador e porque existem vários tipos (cache, primária, secundária).

---

### `02_ram_rom_binario_bytes_enderecos.md`

**Objetivo:** dominar RAM vs ROM, sistema binário, bytes e noções de endereçamento de memória.

> Este é o único ficheiro desta pasta com exercícios.

---

### `03_gestao_de_memoria_em_python_referencias_mutabilidade_gc.md`

**Objetivo:** perceber como Python gere memória automaticamente (referências, objetos mutáveis/imutáveis, garbage collection).

---

### `04_heap_stack_frames_e_execucao_python.md`

**Objetivo:** compreender Heap vs Stack, stack frames, recursão e o caminho de execução de código Python (`.py` -> bytecode -> PVM).

---

### `05_estruturas_dinamicas_e_complexidade.md`

**Objetivo:** introdução teórica a estruturas dinâmicas (pilha, fila, lista ligada, árvore, dicionário) e complexidade (Big-O).

---

### `06_do_codigo_a_execucao_real_so_cpu_isa.md`

**Objetivo:** ligar tudo numa visão de sistema: do código-fonte até à execução real no CPU, com papel do sistema operativo, loader, processo/thread, ISA e ciclo de vida de ficheiros.

---

## Rota de estudo recomendada

1. `00_fundamentos_hardware_bits_cpu_memoria.md`
2. `01_memoria_do_computador_cache_primaria_secundaria.md`
3. `02_ram_rom_binario_bytes_enderecos.md`
4. `03_gestao_de_memoria_em_python_referencias_mutabilidade_gc.md`
5. `04_heap_stack_frames_e_execucao_python.md`
6. `05_estruturas_dinamicas_e_complexidade.md`
7. `06_do_codigo_a_execucao_real_so_cpu_isa.md`

---

## Changelog

- **2026-02-04**: Criação inicial da pasta `Memoria` com guia de estudo e 5 módulos.
- **2026-02-04**: Adicionado módulo `00` de fundamentos (hardware, CPU, RAM, endereços).
- **2026-02-04**: Adicionado módulo `06` com a visão completa de execução real (SO, CPU, ISA e ficheiros).
