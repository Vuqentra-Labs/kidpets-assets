# Configuração

Os exemplos abaixo descrevem uma possível estrutura de configuração. Ajuste conforme a implementação real do plugin.

## Configurações Gerais

```yaml
language: pt-BR
debug: false
save-interval-seconds: 300
```

## Exemplo de Configuração de Pet

```yaml
pets:
  axolotl:
    enabled: true
    display-name: "Axolote"
    role: "Cura e Sobrevivência"

    action-passive:
      enabled: true

    need-passive:
      enabled: true
      cooldown-seconds: 60

    active:
      cooldown-seconds: 45

    ultimate:
      cooldown-seconds: 600
```

## Regras Recomendadas

- Mantenha os tempos de recarga configuráveis.
- Mantenha as mensagens configuráveis.
- Permita desativar Pets individualmente.
- Armazene valores de balanceamento fora do código-fonte.
- Valide as configurações durante a inicialização.
