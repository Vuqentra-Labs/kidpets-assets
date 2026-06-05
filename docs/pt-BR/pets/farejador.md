# Farejador

> [!IMPORTANT]
> **Versão documentada:** `KidPets 0.1.1`  
> **Última verificação do código:** `04/06/2026`  
> **Como verificar a versão instalada:** use `/kidpets version` dentro do servidor.  
>
> A versão oficial exata não pôde ser identificada somente pelos arquivos Java analisados, pois ela é carregada dos metadados do plugin.  
> Esta página descreve o comportamento e os **valores padrão** encontrados no snapshot informado acima. Um servidor pode apresentar valores diferentes caso o administrador tenha alterado o `config.yml`.

## Visão Geral

| Informação | Valor |
|---|---|
| Função Principal | Alimentação e coleta de alimentos |
| Função Secundária | Sobrevivência relacionada à fome |
| Nível Máximo | 10 |
| Faixas de habilidade | Níveis 1–4, níveis 5–9 e nível 10 |
| Habilidade Ativa | Buscar Comida |
| Passiva de Ação | Encontrar itens extras ao quebrar blocos elegíveis ou matar animais |
| Passiva de Necessidade | Recuperar automaticamente a fome do jogador |
| Super Poder | Encontrar uma comida especial após concluir um desafio matemático |
| Disponível na edição Free | Ativa, passivas, níveis e baú |
| Exclusivo da edição Premium | Super Poder |

O Farejador auxilia o jogador encontrando alimentos, gerando recompensas extras durante determinadas ações e recuperando automaticamente a fome quando necessário.

As habilidades não recebem melhorias individuais em todos os níveis. O comportamento muda somente ao entrar em uma nova faixa:

- **Níveis 1–4**
- **Níveis 5–9**
- **Nível 10**

---

## Resumo do que muda por faixa

| Recurso | Níveis 1–4 | Níveis 5–9 | Nível 10 |
|---|---|---|---|
| Baú próprio | 9 slots | 18 slots | 27 slots |
| Passiva em blocos comuns | Sim | Chance maior | Chance maior e pode entregar 1–2 itens |
| Passiva ao matar animais | Não | Carne crua adicional | Carne cozida adicional |
| Passiva em arbusto de frutas doces e cacau | Não | Não | Sim |
| Ajuda automática de fome | +4 fome | +6 fome, +2 saturação e efeito Saturação | +8 fome, +3 saturação, efeito Saturação e chance de item bônus |
| Ativa Buscar Comida | Alimentos simples | Carnes cruas e alimentos intermediários | Alimentos cozidos e chance de dourados |
| XP da ativa | +2 XP | +3 XP | +4 XP |
| Cooldown padrão da ativa | 120 segundos | 300 segundos | 420 segundos |

> [!NOTE]
> Na configuração padrão atual, o cooldown de **Buscar Comida aumenta** nas faixas superiores.

---

# Requisitos para as habilidades funcionarem

## Estado de conforto do Pet

A maioria das habilidades do Farejador exige que ele esteja confortável.

Por padrão, os três status abaixo começam em `100` e cada um perde `1` ponto a cada `60` segundos enquanto o Pet está ativo:

- Fome do Pet
- Sede do Pet
- Felicidade do Pet

Para o Farejador utilizar suas habilidades, todos os três status precisam estar em pelo menos `15`.

| Configuração padrão | Valor |
|---|---:|
| Fome mínima do Pet | 15 |
| Sede mínima do Pet | 15 |
| Felicidade mínima do Pet | 15 |
| Perda de cada status por ciclo | 1 |
| Intervalo do ciclo | 60 segundos |

Alimentar, dar água ou brincar com o Pet restaura status e concede `+1 XP`.

## Proximidade necessária

| Habilidade | Exigência de proximidade |
|---|---|
| Passiva ao quebrar blocos | Farejador ativo, no mesmo mundo e a até 12 blocos |
| Passiva ao matar animais | Farejador ativo, no mesmo mundo e a até 12 blocos |
| Passiva de fome baixa | Farejador ativo, no mesmo mundo e a até 12 blocos |
| Ativa Buscar Comida | Farejador confortável e no mesmo mundo |
| Super Poder | Farejador selecionado e ativo para acessar pelo menu |

A habilidade ativa não realiza uma verificação adicional de distância. Quando usada pelo menu, a comida é derrubada na localização do Farejador, desde que ele esteja no mesmo mundo do jogador.

---

# Passiva de Ação — Recompensas Extras

O Farejador pode encontrar um item adicional quando o jogador:

- quebra determinados blocos;
- ou, a partir do nível 5, mata determinados animais.

A recompensa adicional é guardada no baú próprio do Farejador.

Caso o baú esteja cheio:

- o item é derrubado próximo ao Farejador;
- a mensagem informa que o baú está cheio;
- a ativação **não concede o +1 XP** que seria recebido ao guardar o item com sucesso.

A passiva não possui cooldown ou limite de ativações por minuto na implementação atual.

## Fórmula da chance

A chance final padrão é calculada assim:

```text
chance final = chance base × multiplicador da faixa
```

A chance final é limitada ao máximo de `100%`.

## Chances padrão finais

| Categoria | Faixa | Chance Base | Multiplicador | Chance Final |
|---|---:|---:|---:|---:|
| Bloco comum | Níveis 1–4 | 12% | ×1,25 | **15%** |
| Bloco comum | Níveis 5–9 | 18% | ×1,45 | **26,1%** |
| Bloco comum | Nível 10 | 24% | ×1,75 | **42%** |
| Animal | Níveis 5–9 | 10% | ×1,45 | **14,5%** |
| Animal | Nível 10 | 16% | ×1,75 | **28%** |
| Bloco especial | Nível 10 | 4% | ×1,75 | **7%** |

## Quantidade recebida

| Categoria | Faixa | Quantidade padrão |
|---|---:|---:|
| Bloco comum | Níveis 1–4 | 1 |
| Bloco comum | Níveis 5–9 | 1 |
| Bloco comum | Nível 10 | 1–2 |
| Animal | Níveis 5–9 | 1 |
| Animal | Nível 10 | 1 |
| Bloco especial | Nível 10 | 1 |

## Blocos comuns elegíveis

Disponíveis desde o nível 1.

| Bloco quebrado | Recompensa adicional |
|---|---|
| Grama curta | Sementes de trigo |
| Grama alta | Sementes de trigo |
| Samambaia | Sementes de trigo |
| Trigo | Trigo |
| Cenouras | Cenoura |
| Batatas | Batata |
| Beterrabas | Beterraba |
| Melancia | Fatia de melancia |
| Abóbora | Abóbora |
| Folhas de carvalho | Maçã |
| Folhas de carvalho escuro | Maçã |
| Folhas de selva | Maçã |

## Blocos especiais elegíveis

Disponíveis somente no nível 10.

| Bloco quebrado | Recompensa adicional |
|---|---|
| Arbusto de frutas doces | Frutas doces |
| Cacau | Sementes de cacau |

## Animais elegíveis

Disponíveis a partir do nível 5. O animal precisa ter sido morto pelo jogador.

| Animal | Recompensa nos níveis 5–9 | Recompensa no nível 10 |
|---|---|---|
| Vaca | Carne bovina crua | Carne bovina cozida |
| Coguvaca | Carne bovina crua | Carne bovina cozida |
| Porco | Carne de porco crua | Carne de porco cozida |
| Galinha | Frango cru | Frango cozido |
| Ovelha | Carneiro cru | Carneiro cozido |
| Coelho | Coelho cru | Coelho cozido |

## XP da passiva

Uma recompensa guardada com sucesso no baú do Farejador concede:

```text
+1 XP
```

Se o baú estiver cheio e o item cair no chão, o código atual não concede esse XP.

## Notas da implementação atual

O código atual:

- não verifica se uma plantação está madura;
- não diferencia blocos naturais de blocos colocados pelo jogador;
- não possui rastreamento de blocos recolocados;
- não possui limite de ativações por minuto;
- não possui cooldown próprio para esta passiva;
- considera apenas folhas de carvalho, carvalho escuro e selva;
- não verifica explicitamente o modo de jogo do jogador nesta passiva.

Esses comportamentos são documentados porque fazem parte da implementação atual e podem mudar em versões futuras.

---

# Passiva de Necessidade — Ajuda Automática de Fome

Quando a fome do jogador fica baixa, o Farejador recupera automaticamente fome e saturação.

A habilidade:

- exige que o Farejador esteja confortável;
- exige que o Farejador esteja no mesmo mundo;
- exige distância máxima padrão de 12 blocos;
- concede `+2 XP` ao ativar;
- possui cooldown próprio por jogador.

## Intervalo de verificação

A condição de fome é verificada periodicamente, não imediatamente a cada alteração da barra.

No código atual, essa verificação utiliza o mesmo task da passiva do Axolote:

```yaml
axolotl.passive.interval-seconds: 20
```

Portanto, com a configuração padrão, o Farejador verifica a fome do jogador aproximadamente a cada `20 segundos`.

> [!WARNING]
> Na implementação atual, alterar `axolotl.passive.interval-seconds` também altera o intervalo de verificação desta passiva do Farejador.

## Efeito padrão por faixa

No Minecraft, a barra completa possui `20` pontos de fome.

| Faixa | Ativa quando a fome estiver em | Fome restaurada | Saturação adicionada | Efeito Saturação | Cooldown |
|---|---:|---:|---:|---:|---:|
| Níveis 1–4 | 4 ou menos | +4 | +1,0 | Não aplica | 180 segundos |
| Níveis 5–9 | 5 ou menos | +6 | +2,0 | 25 segundos, amplificador 0 | 120 segundos |
| Nível 10 | 6 ou menos | +8 | +3,0 | 55 segundos, amplificador 0 | 90 segundos |

A fome e a saturação são limitadas ao máximo de `20`.

## Item bônus do nível 10

No nível 10, cada ativação da ajuda automática possui `15%` de chance de também gerar um alimento bônus.

O item tenta ir para o baú do Farejador. Caso o baú esteja cheio, ele é derrubado próximo ao Pet.

### Pesos da recompensa bônus

| Item | Peso | Chance dentro da tabela bônus |
|---|---:|---:|
| Cenoura dourada | 35 | aproximadamente 38,46% |
| Carne bovina cozida | 30 | aproximadamente 32,97% |
| Carne de porco cozida | 25 | aproximadamente 27,47% |
| Maçã dourada | 1 | aproximadamente 1,10% |

O total dos pesos padrão é `91`. As chances da última coluna consideram somente os casos em que a chance inicial de 15% foi ativada.

### Chance total aproximada por ativação da passiva

| Item | Chance total aproximada |
|---|---:|
| Cenoura dourada | 5,77% |
| Carne bovina cozida | 4,95% |
| Carne de porco cozida | 4,12% |
| Maçã dourada | 0,16% |
| Nenhum item bônus | 85% |

## XP da passiva de necessidade

Cada ativação concede:

```text
+2 XP
```

---

# Habilidade Ativa — Buscar Comida

O jogador pode ativar **Buscar Comida** de duas formas:

1. Clicando em `Buscar Comida` no menu de ações do Pet;
2. Clicando com o botão direito no próprio Farejador, com a mão principal.

Ao clicar diretamente no Pet:

- agachar abre o menu em vez de usar a habilidade;
- segurar a Estrela dos Pets abre o menu;
- segurar um item válido de cuidado alimenta/brinca com o Pet em vez de usar a habilidade.

## Funcionamento

Quando ativada com sucesso:

1. o Farejador escolhe uma comida da tabela da faixa atual;
2. derruba exatamente `1` unidade próxima a ele;
3. inicia o cooldown;
4. concede XP;
5. na edição Premium, adiciona uma carga de recompensa normal ao Super Poder.

## Requisitos

- O Farejador precisa estar confortável;
- O Farejador e o jogador precisam estar no mesmo mundo;
- O cooldown da habilidade precisa ter terminado.

## Cooldown e XP

| Faixa | Cooldown Padrão | XP Recebida |
|---|---:|---:|
| Níveis 1–4 | 120 segundos | +2 XP |
| Níveis 5–9 | 300 segundos | +3 XP |
| Nível 10 | 420 segundos | +4 XP |

## Recompensas dos níveis 1–4

Cada utilização entrega exatamente `1` item.

| Item | Peso | Chance Padrão |
|---|---:|---:|
| Maçã | 45 | 45% |
| Fatia de melancia | 25 | 25% |
| Cenoura | 15 | 15% |
| Batata | 10 | 10% |
| Pão | 5 | 5% |

## Recompensas dos níveis 5–9

Cada utilização entrega exatamente `1` item.

| Item | Peso | Chance Padrão |
|---|---:|---:|
| Frango cru | 20 | 20% |
| Carne bovina crua | 20 | 20% |
| Carne de porco crua | 20 | 20% |
| Carneiro cru | 15 | 15% |
| Batata | 15 | 15% |
| Pão | 10 | 10% |

## Recompensas do nível 10

Cada utilização entrega exatamente `1` item.

| Item | Peso | Chance Padrão |
|---|---:|---:|
| Maçã dourada | 1 | 1% |
| Cenoura dourada | 5 | 5% |
| Carne bovina cozida | 20 | 20% |
| Carne de porco cozida | 20 | 20% |
| Frango cozido | 20 | 20% |
| Batata assada | 20 | 20% |
| Pão | 14 | 14% |

## Destino do item

A comida da habilidade ativa é sempre derrubada no mundo, próxima ao Farejador.

Ela não é enviada automaticamente ao baú do Pet ou ao inventário do jogador.

---

# Super Poder — Comida Especial

> [!IMPORTANT]
> O Super Poder existe somente na edição **Premium**.  
> Na edição Free, o botão aparece no menu, mas apenas informa que o recurso está bloqueado.

## Como carregar

O Super Poder exige, por padrão:

```text
2 recompensas normais
```

Para o Farejador, cada uso bem-sucedido de **Buscar Comida** registra uma recompensa normal.

O contador do Super Poder:

- é salvo no `pets.yml`;
- é armazenado por jogador;
- é compartilhado entre os tipos de Pet na implementação atual.

Isso significa que cargas obtidas com a habilidade ativa de outro Pet também podem permanecer disponíveis após trocar para o Farejador.

## Desafio matemático

Ao utilizar o Super Poder carregado:

1. o plugin cria uma soma com dois números aleatórios entre `2` e `9`;
2. o jogador recebe até `3` tentativas por padrão;
3. a resposta é solicitada por uma placa temporária;
4. caso a placa não possa ser usada, a pergunta é enviada pelo chat.

A tentativa em que o jogador acerta determina a tabela da recompensa.

Se todas as tentativas forem usadas sem acertar:

- a carga é consumida;
- nenhuma recompensa é entregue;
- nenhum XP do Super Poder é concedido.

## Recompensa ao acertar na primeira tentativa

Entrega exatamente `1` item.

| Item | Peso | Chance Padrão |
|---|---:|---:|
| Maçã dourada | 55 | 55% |
| Cenoura dourada | 35 | 35% |
| Carne bovina cozida | 10 | 10% |

## Recompensa ao acertar na segunda tentativa

Entrega exatamente `1` item.

| Item | Peso | Chance Padrão |
|---|---:|---:|
| Maçã dourada | 25 | 25% |
| Cenoura dourada | 55 | 55% |
| Carne bovina cozida | 20 | 20% |

## Recompensa ao acertar na terceira tentativa

Entrega exatamente `1` item.

| Item | Peso | Chance Padrão |
|---|---:|---:|
| Maçã dourada | 10 | 10% |
| Cenoura dourada | 60 | 60% |
| Frango cozido | 30 | 30% |

## Destino da recompensa

A recompensa tenta seguir esta ordem:

1. Baú do Farejador;
2. Inventário do jogador;
3. Chão próximo ao jogador, caso os dois estejam cheios.

## XP do Super Poder

Ao acertar o desafio e receber uma recompensa válida:

```text
+8 XP
```

O Super Poder não possui cooldown por tempo. A limitação é o carregamento por recompensas normais e o desafio matemático.

---

# Sistema de Níveis e Experiência

O Farejador possui nível e XP separados dos outros Pets.

A fórmula padrão para subir de nível é:

```text
XP necessária = nível atual × 20
```

## XP necessária por evolução

| Evolução | XP Necessária |
|---|---:|
| Nível 1 → 2 | 20 XP |
| Nível 2 → 3 | 40 XP |
| Nível 3 → 4 | 60 XP |
| Nível 4 → 5 | 80 XP |
| Nível 5 → 6 | 100 XP |
| Nível 6 → 7 | 120 XP |
| Nível 7 → 8 | 140 XP |
| Nível 8 → 9 | 160 XP |
| Nível 9 → 10 | 180 XP |

O código permite subir vários níveis de uma vez quando uma quantidade suficiente de XP é recebida.

Ao alcançar o nível 10:

- o XP restante é zerado;
- o Pet não acumula XP adicional enquanto estiver no nível máximo.

## Fontes de XP

| Ação | XP Padrão |
|---|---:|
| Permanecer com o Pet ativo durante um ciclo de status | +1 XP |
| Alimentar, dar água ou brincar com o Pet | +1 XP |
| Recompensa da passiva guardada com sucesso no baú | +1 XP |
| Passiva automática de fome baixa | +2 XP |
| Ativa Buscar Comida nos níveis 1–4 | +2 XP |
| Ativa Buscar Comida nos níveis 5–9 | +3 XP |
| Ativa Buscar Comida no nível 10 | +4 XP |
| Super Poder Premium concluído com sucesso | +8 XP |

## XP passiva por tempo

Por padrão, qualquer Pet ativo recebe:

```text
+1 XP a cada 60 segundos
```

Na implementação atual, o intervalo utilizado é o mesmo ciclo dos status:

```yaml
stats.decay.interval-seconds: 60
```

Embora exista a chave `xp.passive.interval-seconds`, o task atual utiliza `stats.decay.interval-seconds` para controlar o intervalo.

---

# Baú do Farejador

O Farejador possui um baú separado dos outros Pets.

| Faixa | Tamanho Padrão |
|---|---:|
| Níveis 1–4 | 9 slots |
| Níveis 5–9 | 18 slots |
| Nível 10 | 27 slots |

São enviados ao baú do Farejador:

- recompensas da passiva de ação;
- alimento bônus da passiva automática no nível 10;
- recompensa do Super Poder Premium.

A comida da habilidade ativa **Buscar Comida** não vai para o baú; ela é derrubada próxima ao Farejador.

---

# Chaves de Configuração

Os valores desta documentação representam os padrões gerados pelo plugin. Administradores podem alterá-los no `config.yml`.

## Ativa Buscar Comida

```yaml
sniffer.active.cooldown-seconds.level-1-4
sniffer.active.cooldown-seconds.level-5-9
sniffer.active.cooldown-seconds.level-10

sniffer.active.foods.level-1-4
sniffer.active.foods.level-5-9
sniffer.active.foods.level-10
```

## Passiva de recompensas extras

```yaml
sniffer.passive.max-distance

sniffer.passive.chance.simple.level-1-4
sniffer.passive.chance.simple.level-5-9
sniffer.passive.chance.simple.level-10

sniffer.passive.chance.medium.level-5-9
sniffer.passive.chance.medium.level-10

sniffer.passive.chance.rare.level-10

sniffer.passive.chance-multiplier.level-1-4
sniffer.passive.chance-multiplier.level-5-9
sniffer.passive.chance-multiplier.level-10

sniffer.passive.amount.simple-min
sniffer.passive.amount.simple-max
sniffer.passive.amount.medium-min
sniffer.passive.amount.medium-max
sniffer.passive.amount.rare-min
sniffer.passive.amount.rare-max
sniffer.passive.amount.level-10-common-max
```

## Passiva automática de fome

```yaml
sniffer.emergency.enabled

sniffer.emergency.trigger-food-level.level-1-4
sniffer.emergency.trigger-food-level.level-5-9
sniffer.emergency.trigger-food-level.level-10

sniffer.emergency.cooldown-seconds.level-1-4
sniffer.emergency.cooldown-seconds.level-5-9
sniffer.emergency.cooldown-seconds.level-10

sniffer.emergency.restore-food.level-1-4
sniffer.emergency.restore-food.level-5-9
sniffer.emergency.restore-food.level-10

sniffer.emergency.restore-saturation.level-1-4
sniffer.emergency.restore-saturation.level-5-9
sniffer.emergency.restore-saturation.level-10

sniffer.emergency.nutrition-seconds.level-1-4
sniffer.emergency.nutrition-seconds.level-5-9
sniffer.emergency.nutrition-seconds.level-10

sniffer.emergency.nutrition-amplifier.level-5-9
sniffer.emergency.nutrition-amplifier.level-10

sniffer.emergency.xp
sniffer.emergency.level-10-bonus-chance
sniffer.emergency.level-10-bonus-foods
```

## Super Poder Premium

```yaml
super.required-normal-rewards
super.challenge.max-attempts

super.sniffer.rewards.first
super.sniffer.rewards.second
super.sniffer.rewards.third
```

## Sistemas gerais que afetam o Farejador

```yaml
xp.required-multiplier
xp.passive.amount

stats.decay.interval-seconds
stats.decay.hunger
stats.decay.thirst
stats.decay.happiness
stats.comfort.minimum

pet-chest.slots.level-1-4
pet-chest.slots.level-5-9
pet-chest.slots.level-10

axolotl.passive.interval-seconds
```

---

# Notas da Implementação Atual

Esta seção registra detalhes do snapshot documentado para facilitar comparações com versões futuras.

1. **As habilidades utilizam três faixas de nível**, e não valores individuais em cada nível.
2. **O cooldown da ativa aumenta com o nível** nos valores padrão atuais.
3. **A passiva não verifica maturidade de plantações.**
4. **A passiva não diferencia blocos naturais de blocos colocados.**
5. **A passiva não possui rate limit ou cooldown próprio.**
6. **A passiva concede XP somente quando consegue guardar a recompensa no baú.**
7. **A verificação automática de fome usa atualmente `axolotl.passive.interval-seconds`.**
8. **A chave `xp.passive.interval-seconds` existe, mas o task atual usa `stats.decay.interval-seconds`.**
9. **As chaves antigas `sniffer.survival.*` existem na configuração padrão, mas a lógica executada utiliza `sniffer.emergency.*`.**
10. **Os cooldowns da ativa e da emergência ficam apenas em memória e são reiniciados ao reiniciar o plugin/servidor.**
11. **O contador de carga do Super Poder é salvo e compartilhado por jogador, não separado por Pet.**
12. **Existe código legado de uma habilidade de detecção do Farejador, mas a habilidade ativa ligada aos eventos e ao menu atual é Buscar Comida.**

---

# Como Conferir se Esta Página Ainda Está Atualizada

1. Dentro do servidor, execute:

```text
/kidpets version
```

2. Compare a versão exibida com o campo **Versão documentada** no início desta página.
3. Consulte o `CHANGELOG.md` da release.
4. Confira os valores atuais no menu **Config Visual** ou no `config.yml`.
5. Caso o comportamento tenha mudado, atualize esta página e a data da última verificação.

> [!WARNING]
> Quando a versão instalada for diferente da versão documentada, o comportamento do plugin e o `config.yml` da versão instalada devem ser considerados a fonte de verdade.
